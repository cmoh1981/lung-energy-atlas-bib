# Methods Supplement

Companion document to `manuscript/v2_BIB_JCR5_manuscript_draft.md`. Provides the procedural and parameter-level detail needed to reproduce the LEMPA case study and to apply the staged validation framework to a new organ-and-imaging-modality combination. Section numbers mirror the manuscript Methods (Section 3).

All file paths are relative to the main analysis project root `writing_outputs/20260516_lung-energy-pathway-mapping/` as preserved in `evidence/lung_energy_atlas/` of this publication package.

---

## S3.1 Atlas construction (detail)

**Source.** Integrated Human Lung Cell Atlas (HLCA) v1.0, as published by Sikkema et al. (2023) [3] and distributed through the Human Cell Atlas data portal. The atlas was downloaded as a `.h5ad` AnnData object (`lung_atlas.h5ad`, ~5.87 GB on disk).

**Annotation level used.** `ann_finest_level` (50 cell types after exclusion of doublets and clinically inconsistent labels).

**Cell count.** 584,944 cells across 49 donors.

**Pre-processing.** No re-clustering or label reassignment. Cells with `is_doublet` flags or with cell-type labels marked deprecated in the HLCA release notes were excluded prior to use.

**Pathway gene sets.**

| Pathway | Source | Notes |
| --- | --- | --- |
| Glycolysis | MSigDB Hallmark `HALLMARK_GLYCOLYSIS` [22] | Used unchanged. |
| Oxidative phosphorylation | MSigDB Hallmark `HALLMARK_OXIDATIVE_PHOSPHORYLATION` [22] | Used unchanged. |
| Pentose phosphate pathway | Curated set; documented in `data/pathway_gene_sets/` | KEGG-derived gene list. |
| TCA cycle | Curated set; documented in `data/pathway_gene_sets/` | KEGG-derived gene list. |
| Lactate-related metabolism | Curated set; documented in `data/pathway_gene_sets/` | Combined LDHA/LDHB/MCT family. |

**Atlas-only pathway scoring.** Cell-level scores were computed with `gseapy.gsva` (Python adaptation of GSVA-style enrichment) for each pathway and cell. Cell-type-level summaries are the per-cell-type mean and standard deviation across donors. Outputs are archived in `results/02_pathway_capacity/`.

---

## S3.2 Deconvolution (detail)

### S3.2.1 NNLS branch (primary)

**Signature matrix.** Derived from the HLCA `ann_finest_level` labels via a per-cell-type marker-gene aggregation. Genes were ranked by per-cell-type log-fold-change against the rest of the atlas; the top-50 markers per cell type were retained and the per-cell-type mean expression of these markers across atlas cells was used as the signature column. The signature matrix dimensions are 2,000 genes × 50 cell types.

**Algorithm.** Non-negative least squares regression: for each patient $i$, the fraction vector $\mathbf{F}_i$ is the solution of $\min_{\mathbf{F} \ge 0} \| \mathbf{S} \mathbf{F} - \mathbf{x}^{\mathrm{bulk}}_i \|_2^2$, where $\mathbf{S}$ is the signature matrix and $\mathbf{x}^{\mathrm{bulk}}_i$ is the per-patient bulk expression vector. Implementation via `scipy.optimize.nnls`.

**Normalization.** Per-patient fraction vectors are normalized to sum to 1 by dividing by the row sum.

### S3.2.2 Scaden branch (secondary)

**Training data.** Simulated bulk mixtures drawn from the HLCA with the following configuration:

| Parameter | Value | Rationale |
| --- | --- | --- |
| Cell types | Top 50 by `ann_finest_level` | Matches NNLS branch resolution. |
| Donor balancing cap | 200 cells per (cell-type, donor) | Prevents single-donor dominance. |
| Overlapping genes | 2,000 | Maximizes overlap with NSCLC-RG bulk RNA-seq. |
| Simulated mixtures | 600 | Reduced from the canonical 32,000 for local compute. |
| Optimizer steps per ensemble member | 100 | Reduced from the canonical 5,000 for local compute. |
| Ensemble size | 3 networks | Smallest stable ensemble. |
| Output normalization | Softmax over cell-type heads | Standard Scaden default. |

**Algorithm.** Scaden [9] is a multi-layer feedforward neural network trained on the simulated bulk mixtures with cell-type fractions as targets. At inference, the trained networks are applied to the NSCLC-RG bulk expression vectors and the ensemble prediction (mean of softmax outputs) is taken as the predicted fraction vector.

**Acknowledged limitation.** The reduced configuration (600 mixtures, 100 optimizer steps) is below the canonical Scaden recommendation and was forced by local compute. The configuration is documented so that a future re-run with the canonical configuration can be assessed against the frozen LEMPA outputs. We do not claim that the reduced configuration is sufficient for general use; we report it because it is what was executed.

### S3.2.3 Cross-method agreement scoring (gate G2)

For each cell type $k$ in the top-10 NNLS-abundant subset $\mathcal{K}^{\star}$ (top-10 by NNLS-mean fraction across the 130 paired patients):

1. Compute Pearson correlation $\rho_k$ between $\mathbf{F}^{(\mathrm{NNLS})}_{\cdot k}$ and $\mathbf{F}^{(\mathrm{Scaden})}_{\cdot k}$ across the 130 patients.
2. Aggregate over $\mathcal{K}^{\star}$: $\tilde{\rho} = \mathrm{median}_{k \in \mathcal{K}^{\star}} \rho_k$, and $L^{\mathrm{pass}} = |\{k \in \mathcal{K}^{\star} : \rho_k \ge 0.40\}|$.
3. Gate verdict: PASS if $\tilde{\rho} \ge 0.30$ **and** $L^{\mathrm{pass}} \ge 6$; FAIL otherwise.

Observed: $\tilde{\rho} = -0.087$, $L^{\mathrm{pass}} = 1$. Verdict: FAIL.

### S3.2.4 Predeclared fallback on G2 failure

If G2 fails at the cell-type resolution, the fallback rule collapses cell types into four broad consensus modules using a fixed mapping table (`data/processed/module_mapping.csv`):

| Module | Cell types contributing |
| --- | --- |
| Epithelial | AT1, AT2, ciliated, secretory, basal, club, goblet, ionocyte, neuroendocrine, brush, hillock |
| Immune | alveolar macrophage, interstitial macrophage, monocyte, DC, T (CD4/CD8/regulatory/γδ/Tcm/Tem), NK, B, plasma, mast |
| Endothelial | capillary, arterial, venous, lymphatic, aerocyte |
| Stromal | fibroblast, smooth muscle (airway/vascular), pericyte, mesothelial |

The collapsed-module fractions are the sum of the constituent cell-type fractions per patient.

---

## S3.3 Radiomics extraction (detail)

**Software.** PyRadiomics [13] under IBSI-aware settings [18].

**Modality.** Pre-treatment CT (and PET where available, used only for SUV~max~ in H4a/H4c). The H4b texture features used CT only.

**Configuration.**

| Parameter | Value |
| --- | --- |
| Bin width | 25 HU |
| Voxel resampling | 1.0 × 1.0 × 1.0 mm³ |
| Interpolation | sitkBSpline |
| Resegmentation | (−1000, 400) HU window for lung tissue |
| Discretization | fixed-bin-width |
| Wavelet decomposition | disabled (kept feature space interpretable) |
| Feature classes enabled | firstorder, shape, GLCM, GLRLM, GLSZM, NGTDM, GLDM |

**Output.** Per-patient feature table with ~196 columns. Stored as `results/radiomics/nsclc211_features.csv` (pre-QC) and `results/radiomics/nsclc211_features_qc.csv` (QC-filtered, 162 rows).

**QC rules.** Patients with missing CT volumes, failed mask extraction, or PyRadiomics runtime errors were removed. The full failure log is in `results/radiomics/nsclc211_failures.csv`.

**Mask provenance.** Per-patient mask source is recorded in the `CT_mask_source` column. The H4b analysis subset of 129 patients with a populated mask source field distributed as: SEG = 117, fallback_body_outline = 12.

---

## S3.4 Pathway scoring (detail)

**Algorithm.** Single-sample gene set enrichment analysis (ssGSEA) [26] as implemented in `gseapy.ssgsea`. The algorithm is a rank-based enrichment statistic on per-sample gene rankings.

**Reason for substitution.** Canonical GSVA-R [23] requires an R bridge that was unavailable in the local executing environment. `gseapy.ssgsea` produces sample-level scores compatible with downstream Pearson and partial-correlation tests, which is the requirement for H4a, H4b, and H4c.

**Score interpretation.** Positive scores reflect higher relative pathway expression in the sample. Score magnitudes are not directly comparable across pathways with different gene-set sizes; only within-pathway across-sample comparisons are used in this manuscript.

**Reproducibility note.** ssGSEA and GSVA scores are typically highly correlated on Hallmark gene sets but are not identical. A future re-run with canonical GSVA-R would yield closely correlated but not exactly matching scores. We do not claim that the V1/V2 frozen pathway scores would be exactly reproduced by GSVA-R; we claim that the within-pathway ranks would be highly preserved.

---

## S3.5 Hypothesis testing and FDR (detail)

### S3.5.1 H4 family construction

| Hypothesis | Test | Sample size | Predictor | Target |
| --- | --- | ---: | --- | --- |
| H4a (glycolysis) | Pearson | 117 | CT first-order / PET SUV~max~ | Glycolysis ssGSEA score |
| H4b (entropy) | Spearman | 123 | CT first-order Entropy | Heterogeneity variance |
| H4b (contrast) | Spearman | 123 | CT GLCM Contrast | Heterogeneity variance |
| H4b (homogeneity) | Spearman | 123 | CT GLCM Homogeneity (Idm) | Heterogeneity variance |
| H4c (OXPHOS) | Pearson | 117 | CT first-order / PET SUV~max~ | OXPHOS ssGSEA score |

**Heterogeneity variance construction.**

- V1: variance across the 50 per-cell-type weighted capacity scores (per-patient).
- V2: variance across the four collapsed consensus module fractions (per-patient).

This V1→V2 redefinition is the binding caveat on H4b (Section 4.4 and Table 7 of the main manuscript).

### S3.5.2 Partial correlation procedure

For each H4 row, the partial correlation adjusting for `CT_shape_MeshVolume` is computed by linear residualization: regress predictor and target on `CT_shape_MeshVolume`, take residuals, and compute the correlation of the residuals.

### S3.5.3 FDR control

Benjamini–Hochberg [27] FDR is applied within the 5-test H4 family using the raw two-sided p-values from each correlation. Reported BH-FDR values in the manuscript correspond to this family.

### S3.5.4 Frozen V2 H4b values (machine precision)

| Hypothesis | n | Effect | p~raw~ | BH-FDR | Partial effect | Partial p | Partial BH-FDR |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| H4b — Entropy | 123 | −0.390791773551042 | 7.86334270589371 × 10⁻⁶ | 3.93167135294686 × 10⁻⁵ | −0.397486166823593 | 5.3053870837622 × 10⁻⁶ | 2.6526935418811 × 10⁻⁵ |
| H4b — Contrast | 123 | −0.340623125866356 | 1.15701492742331 × 10⁻⁴ | 1.92835821237218 × 10⁻⁴ | −0.349905199210638 | 7.27297685245879 × 10⁻⁵ | 1.21216280874313 × 10⁻⁴ |
| H4b — Homogeneity | 123 | 0.37084427036442 | 2.41671713202386 × 10⁻⁵ | 6.04179283005966 × 10⁻⁵ | 0.372857308689427 | 2.16497009942412 × 10⁻⁵ | 5.4124252485603 × 10⁻⁵ |

These values are exactly reproduced by `results/post_v2_audit/h4b_recompute.csv` (audit confirmation in `results/post_v2_audit/h4b_audit.md`).

---

## S3.6 Cross-validation and predictive scoring (detail)

**Outer-CV scheme.** 5-fold cross-validation with patient-level splits. Folds are deterministic given a random seed (`docs/random_seeds.md`).

**Per-fold pipeline (V1 cell-type prediction).**

1. Within the training fold: standardize radiomic features (z-score); fit one of ElasticNet, RandomForest, or LightGBM with default hyperparameters (model choice predeclared per target).
2. On the held-out fold: predict the per-cell-type fraction; record the prediction.
3. After all folds: concatenate predictions across folds and compute Pearson r against the frozen NNLS fraction column.

**Per-fold pipeline (V2 module-level prediction).** Identical to V1 except that the target is one of the four collapsed consensus modules and the model class is ElasticNet (the predeclared default for module-level targets).

**Why r and not R²?** Pearson r is symmetric in errors of scale and is the predeclared metric in the gate specification (Section 2.2). R² would penalize prediction-target scale mismatches that are not the question of interest at the gate level.

**Gate G4 verdict logic (V1).** Count cell types with cross-validated r ≥ 0.30. Verdict: PASS if count ≥ 10; FAIL otherwise.

**Gate G4 verdict logic (V2 modules).** Count modules with cross-validated r ≥ 0.30 (out of 4). Verdict: PASS if count ≥ 2; FAIL otherwise. Observed: count = 1 (endothelial only).

---

## S3.7 Computing environment

**Language.** Python ≥ 3.9.

**Key libraries.**

| Library | Role | Reference |
| --- | --- | --- |
| Scanpy | AnnData / atlas inspection | [24] |
| gseapy | ssGSEA pathway scoring | [26] (ssGSEA), [30] (GSEA framework) |
| PyRadiomics | Radiomic feature extraction | [13] |
| scaden | Deep-learning deconvolution | [9] |
| SciPy | NNLS, correlation tests | [28] |
| scikit-learn | ElasticNet, RandomForest, CV folds | [29] |

**Pinned versions.** Listed in `environment.yml` in the public code repository (URL PLACEHOLDER) and exposed in the archived Docker image (Zenodo DOI PLACEHOLDER).

**Hardware.** Single workstation, x86_64. GPU not required for the reported runs (Scaden ran on CPU for the reduced configuration).

**Random seeds.** Documented in `docs/random_seeds.md` and embedded in the relevant scripts (`scripts/v1_cv_pipeline.py`, `scripts/v2/run_b3_v2.py`).

**Acknowledged constraint.** R-based GSVA path not available. ssGSEA was substituted as documented in S3.4. R-based deconvolution methods (e.g., BayesPrism, MuSiC) were also not exercised. Reopening trigger 2 in the main manuscript (Section 7.2) is the criterion under which these would be re-introduced.

---

## Reproduction recipe

To reproduce the LEMPA frozen evidence from a clean checkout of the public code repository:

```bash
# 1. Clone the repository (URL PLACEHOLDER).
git clone https://github.com/PLACEHOLDER/lung-energy-atlas.git
cd lung-energy-atlas

# 2. Build the environment (Conda).
conda env create -f environment.yml
conda activate lempa

# 3. Download data.
#    - HLCA: via the Human Cell Atlas portal.
#    - NSCLC-Radiogenomics: via TCIA (data-use agreement required).
#    See docs/data_access.md for step-by-step instructions.

# 4. Run the atlas-only pathway capacity analysis.
snakemake --cores 4 results/02_pathway_capacity/cell_type_pathway_scores.csv

# 5. Run V1 paired validation.
snakemake --cores 4 results/v1/V1_FINAL_SUMMARY.md

# 6. Run V2 redesign.
snakemake --cores 4 results/v2/V2_FINAL_SUMMARY.md

# 7. Run post-V2 H4b audit.
snakemake --cores 1 results/post_v2_audit/h4b_audit.md
```

Each Snakemake target writes the corresponding result file. The full DAG is in `Snakefile`. Frozen reference outputs are archived alongside the repository for diff comparison.

---

## Provenance

This supplement is the v2 methods document. It supersedes any inline methods detail in the v1 manuscript draft. Numerical values cited here are taken from the frozen analysis outputs in `evidence/lung_energy_atlas/` of this publication package and were not regenerated for this supplement.
