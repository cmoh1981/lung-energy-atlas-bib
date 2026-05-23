# Atlas-Guided Radiogenomics Requires Staged Validation: A Bioinformatics Failure-Mode Framework Anchored by the Lung Energy Metabolism Pathway Atlas

**Authors.** [Author 1, Author 2, ?? Corresponding Author]. *Affiliations and ORCID identifiers to be supplied by the author team before submission.* See `checklist/submission_readiness.md` for the metadata block.

**Article type.** Review with worked case study.

**Target journal.** *Briefings in Bioinformatics*.

**Manuscript version.** v2 (2026-05-23).

---

## Abstract

Single-cell atlases increasingly define biologically plausible targets for imaging-linked molecular inference, but plausibility at atlas resolution does not guarantee patient-level validation. We argue that atlas-guided radiogenomics should be treated as a staged bioinformatics validation problem with explicit gates for executability, cross-method target agreement, target freezing, predictive performance, held-out robustness, and residual-association interpretation. We formalize this framework and apply it to the Lung Energy Metabolism Pathway Atlas (LEMPA), an organ-matched normal-lung resource covering 584,944 cells across 50 annotated cell types anchored in the integrated Human Lung Cell Atlas [1-3]. Under frozen public-data conditions using the NSCLC-Radiogenomics collection [7] paired with LEMPA-derived targets, the validation line closed negative under its own prespecified criteria. In version 1, only 3 of 50 cell types reached cross-validated Pearson r >= 0.30 against a required count of 10. In version 2, a redesigned branch using deep-learning deconvolution alongside non-negative least squares remained executable but failed the cross-method agreement gate, with a top-10 median agreement of -0.087 and only 1 of 10 abundant cell types reaching r >= 0.40. After predeclared collapse to four broad consensus modules, only 1 of 4 modules passed pooled cross-validation. A narrow texture-versus-heterogeneity association (H4b) remained reproducible within the frozen V2 artifacts, but it depended on fallback-derived target redefinition and therefore could not rescue the line-level conclusion. LEMPA functions here as a transparent benchmark whose value lies in identifying where the atlas-to-imaging bridge failed rather than in amplifying a surviving remainder. The practical contribution of the manuscript is therefore a validation framework, an evidence-linked failure-mode taxonomy, and a reporting template for future atlas-guided radiogenomic studies. Pipeline code, environment locks, and processed result tables are archived as described in *Data and Code Availability*; final repository and archive identifiers must be supplied by the author team before submission.
---

## Key Points

- Atlas-guided radiogenomics fails most often *upstream* of the predictive model; deconvolution disagreement, target rarity, and limited paired cohorts can invalidate a study before any model is fit.
- Validation should be staged into six explicit gates (executability, cross-method target agreement, target freeze, predictive performance, held-out robustness, secondary-association audit), each with prespecified pass criteria and predeclared actions on failure.
- A failed gate is informative: it tells the field what cannot yet be claimed and disciplines downstream interpretation.
- Atlas usefulness and translational validation sit on different evidentiary tiers; the LEMPA atlas remains reusable as a normal-lung reference even though its paired NSCLC radiogenomic branch closed as a method-fragile negative.
- Residual positive-looking associations from fallback-derived targets must remain visually and rhetorically subordinate to the line-level outcome; reproducibility of a remainder is necessary but not sufficient for interpretive prominence.
- Public paired cohorts are valuable benchmarks but typically lack the cross-source heterogeneity needed for externalizable validation; reopening criteria should be specified in advance rather than implied.

---

## 1. Introduction

### 1.1 Atlas resources have outpaced their validation tooling

The last decade has produced organ-matched and pan-organ single-cell references at a scale that has materially changed what counts as a biologically anchored hypothesis. The Human Cell Atlas initiative [1] accelerated this shift, first through early organ-specific maps such as the molecular atlas of the human lung [2] and later through integrated resources such as the Human Lung Cell Atlas (HLCA) [3]. These atlases allow investigators to define cell-type-resolved states, pathway programs, and lineage structure before any downstream patient-level modeling begins. In imaging, the natural translational extension is radiogenomics: the attempt to relate quantitative image features to molecular and cellular organization [4-6,12]. Atlas-guided radiogenomics combines these two trajectories by asking whether atlas-derived cell-state fractions or pathway scores can be recovered from lesion-scale imaging.

The idea is attractive because it offers a bridge between high-resolution biology and non-invasive phenotyping. If a lung atlas captures heterogeneity across alveolar epithelium, endothelium, immune populations, and stromal compartments, then one might expect imaging features that summarize tissue texture and morphology to recover at least part of that structure. However, that bridge is more fragile than the atlas layer alone suggests. It depends on accurate projection of atlas signals into bulk samples, sufficient agreement between plausible deconvolution methods, reproducible radiomic features across segmentation and scanner settings, and a paired cohort rich enough to support falsifiable validation rather than optimistic correlation hunting [13-16]. Once any one of these layers weakens, the entire line narrows.

This is the point at which much of the current literature remains under-tooled. Reviews of cell-type deconvolution and radiogenomic biomarker development have made clear that target instability, feature reproducibility, and cohort structure can all cap downstream performance [6,15,16]. Yet atlas-guided radiogenomic studies still tend to foreground the biological appeal of the target while under-reporting the validation surface required to test it. When imaging is asked to predict a quantity that is itself unstable across deconvolution methods, the model is being evaluated against an under-defined endpoint. That problem is not a secondary caveat. It defines the ceiling on what the study can claim.
### 1.2 Why atlas-guided radiogenomics is a worthwhile but fragile target

Despite these constraints, the field is worth pursuing. CT and PET are already embedded in routine non-small-cell lung cancer (NSCLC) care [17], radiomic feature extraction is now supported by harmonized software and reference definitions through PyRadiomics and IBSI [13,18], and public paired resources such as the NSCLC-Radiogenomics collection [7] hosted on TCIA [19] allow method execution without de novo cohort assembly. These resources create a genuine opportunity to ask whether atlas-derived biological structure leaves a recoverable imaging signature at patient scale.

What remains missing is not motivation but validation discipline. Most atlas-guided radiogenomic studies still do not prespecify the target-definition gate, do not quantify agreement across deconvolution methods before predictive modeling, do not freeze the target table before downstream evaluation, and do not define in advance what combination of failures should force a line to close as a negative benchmark rather than drift into exploratory reinterpretation. The resulting literature risks overproducing attractive bridges and underproducing reliable ones. In that setting, a transparent negative benchmark is often more informative than a rhetorically rescued positive-looking remainder.
### 1.3 Our contribution and roadmap

This manuscript is written as a practitioner-facing review with a worked case study. First, we formalize atlas-guided radiogenomics as a staged validation problem with explicit gates that can be reused across studies. Second, we document the executed LEMPA workflow in enough detail to make the gate decisions reproducible. Third, we use the LEMPA line to show how a biologically strong atlas contribution can coexist with a negative and method-fragile translational outcome. Finally, we translate that experience into a failure-mode taxonomy, a reporting checklist, and explicit reopening criteria for future work.

LEMPA is therefore not presented as a success narrative with a caveat appended in discussion. It is presented as an evidence-linked benchmark whose main value lies in showing where the atlas-to-imaging bridge broke and how that break should be reported. We preserve that negative classification deliberately. In a literature vulnerable to selective emphasis on optimistic radiogenomic associations, the more durable contribution is often the framework that prevents overclaiming [20].
---

## 2. A staged validation framework for atlas-guided radiogenomics

### 2.1 Definitions and notation

We define the atlas-guided radiogenomic problem formally. Let:

- $\mathcal{A}$ denote an organ-matched single-cell reference with annotated cell types $\{c_1, \ldots, c_K\}$ and pathway gene sets $\{p_1, \ldots, p_J\}$;
- $\mathbf{X}^{\mathrm{bulk}} \in \mathbb{R}^{N \times G}$ denote a bulk transcriptomic matrix over $N$ patients and $G$ genes;
- $\mathbf{F} \in \mathbb{R}^{N \times K}$ denote the patient-level cell-type fraction matrix produced by a deconvolution method $D$ that maps $\mathbf{X}^{\mathrm{bulk}}$ to $\mathbf{F}$ using $\mathcal{A}$ as the reference;
- $\mathbf{S} \in \mathbb{R}^{N \times J}$ denote the patient-level pathway score matrix produced by a single-sample pathway-scoring algorithm $P$ applied to $\mathbf{X}^{\mathrm{bulk}}$;
- $\mathbf{R} \in \mathbb{R}^{N \times M}$ denote the patient-level radiomic feature matrix with $M$ features extracted from paired CT (and optionally PET) volumes using a standardized pipeline;
- $\mathbf{y}$ denote the validation target ??typically a column of $\mathbf{F}$, $\mathbf{S}$, or a function thereof.

The atlas-guided radiogenomic question is: does there exist a function $f: \mathbb{R}^M \to \mathbb{R}$ such that $f(\mathbf{R})$ recovers $\mathbf{y}$ with cross-validated performance exceeding a prespecified threshold, on a paired analysis cohort of size $n \le N$ after one-to-one linkage and quality control? The gate framework below decomposes this question into stages at which the line can fail.

### 2.2 The six validation gates

We formalize six gates that we propose as a minimum standard for any atlas-guided radiogenomic study. The exposition mirrors prior staged validation rationales for clinical prediction modeling [21,11].

**Gate 1 ??Executability.** The chosen pipeline must run without degeneracy on the intended cohort. Concretely, the deconvolution method must return non-degenerate fractions (no all-zero columns for cell types specified in $\mathcal{A}$, no rows summing to zero, no NaN propagation) on a smoke-test subset of size $n_{\mathrm{smoke}}$. Pass criterion: every predeclared non-degeneracy check returns true.

**Gate 2 ??Cross-method target agreement.** Given two deconvolution methods $D_1$ and $D_2$ applied to the same $\mathbf{X}^{\mathrm{bulk}}$ and the same reference $\mathcal{A}$, the per-cell-type agreement is computed as the Pearson correlation across patients of the matched fraction columns:

$$
\rho_k = \mathrm{Pearson}\bigl(\mathbf{F}^{(D_1)}_{\cdot k}, \mathbf{F}^{(D_2)}_{\cdot k}\bigr), \quad k = 1, \ldots, K.
$$

The gate evaluates a summary statistic over the abundant subset $\mathcal{K}^{\star}$ (the top-$L$ cell types by NNLS-mean abundance):

$$
\tilde{\rho} = \mathrm{median}_{k \in \mathcal{K}^{\star}} \rho_k.
$$

The pass criterion has two components: $\tilde{\rho} \ge \tilde{\rho}^{\star}$ (an absolute agreement threshold) and $\bigl|\{k \in \mathcal{K}^{\star} : \rho_k \ge \rho^{\star}\}\bigr| \ge L^{\star}$ (a minimum count of cell types meeting an individual-agreement threshold). For LEMPA we used $L=10$, $\tilde{\rho}^{\star} = 0.30$, $\rho^{\star} = 0.40$, $L^{\star} = 6$.

**Gate 3 ??Target freeze.** Before any downstream evaluation, the target table $\mathbf{F}$ (or the consensus thereof when two methods are used) must be written to a timestamped artifact and frozen. The pass criterion is the existence of that artifact and the demonstrable use of it by downstream code paths; modification thereafter requires a new gate-3 run.

**Gate 4 ??Predictive performance.** Cross-validated prediction of each frozen target $\mathbf{y}_k$ from $\mathbf{R}$ proceeds under a prespecified outer-CV scheme. We define per-target cross-validated Pearson correlation $r_k = \mathrm{Pearson}(\hat{\mathbf{y}}_k, \mathbf{y}_k)$ and a predeclared success rule: a minimum count $L^{\dagger}$ of targets must reach $r_k \ge r^{\star}$. For LEMPA V1 we used $L^{\dagger} = 10$ targets at $r^{\star} = 0.30$; for V2 the rule was applied to four collapsed consensus modules with $L^{\dagger} = 2$ and $r^{\star} = 0.30$ (with the threshold reflecting the smaller module count).

**Gate 5 ??Held-out robustness.** Performance must be challenged across at least one technical or cohort split (site, scanner manufacturer, batch, or histology). The gate is **estimable** if the cohort contains adequate variation in the chosen stratification variable to support a leave-one-stratum-out evaluation. If estimable, the pass criterion is a predeclared minimum cross-source $r$ or AUC. If not estimable, the gate is recorded as `SKIPPED` and downstream language must reflect the absent robustness surface.

**Gate 6 ??Secondary-association audit.** Any retained positive-looking association that is not the primary endpoint must be (i) reproducible from the frozen artifacts, (ii) demonstrably independent of leakage between predictor and target construction (i.e., the predictor variables must not enter the target definition), (iii) join-integrity confirmed (no duplicate patient expansion), and (iv) interpretable under partial adjustment for at least one descriptive technical covariate. A passing residual association is reported only as a caveated remainder when the line-level result is negative.

### 2.3 Required data layers

A reader who wishes to design or review an atlas-guided radiogenomic study can use Table 1 as a checklist for the minimum input stack. The LEMPA-anchored entries in the table illustrate how each layer fared in the case study.

**Table 1. Data layers required for atlas-guided radiogenomics.**

| Data layer | Workflow role | LEMPA executed source/status | Minimum requirement for future studies | Common failure if weak or absent | LEMPA lesson |
| --- | --- | --- | --- | --- | --- |
| Organ-matched cell atlas | Defines biologically plausible cell states and pathway targets before any imaging linkage is attempted. | Human Lung Cell Atlas [3]; 584,944 cells across 50 annotated cell types; strong atlas layer retained. | Organ-matched reference with stable cell annotation and clearly defined pathway programs. | Targets may be biologically implausible or too noisy to justify downstream validation. | A strong atlas can be publishable and reusable even when patient-level radiogenomic validation fails. |
| Paired bulk RNA-seq or transcriptomic target layer | Supplies patient-level molecular targets for deconvolution, module construction, and pathway scoring. | NSCLC-Radiogenomics transcriptomic layer [7] available for 130 linked patients after inner join. | One-to-one patient-linked molecular matrix with QC and sample manifest. | Imaging cannot be benchmarked against patient-level molecular truth. | Public paired RNA is the core bridge layer; without it, radiogenomics remains speculative. |
| Imaging feature layer | Provides the non-invasive predictor space to be tested against transcriptomic targets. | 162 radiomics-processing patients; 130 retained in paired analysis; QC feature table generated with PyRadiomics [13] under IBSI-aware definitions [18]. | Harmonized feature extraction, modality provenance, and explicit QC thresholds. | Feature instability or untracked preprocessing can overwhelm any biologic signal. | Imaging availability alone did not guarantee recoverable atlas-derived targets. |
| ROI mask / segmentation layer | Defines what tissue is measured and whether radiomic predictors are reproducible. | Mask provenance available in frozen outputs; H4b audit confirmed `SEG=117`, `fallback_body_outline=12`. | Auditable mask source for each patient and clear fallback rules. | Feature values may drift because the sampled region is inconsistent or weakly documented. | Mask provenance should be surfaced explicitly because it affects trust in feature-based associations. |
| Technical and cohort metadata | Enables attrition accounting, held-out robustness checks, and descriptive confounding review. | Pairing attrition documented; site/vendor metadata available but too limited for robust V2 held-out splits. | Site, scanner, batch, histology, and linkage metadata with enough spread to support robustness testing. | Transportability cannot be assessed; apparent internal findings may be non-generalizable. | V2-G5 could not be estimated because frozen local strata were not rich enough for held-out robustness. |
| Independent external paired cohort | Converts an internal stress test into a real replication surface. | Not available; Phase C remains dormant pending explicit trigger criteria. | Independent paired imaging-plus-RNA cohort with `N >= 100`, one-to-one linkage, and technical covariates. | The study can report only an internal benchmark or negative stress test, not external validation. | No external paired cohort means archive the broad line rather than narrate a near-success. |

### 2.4 The gate framework as a single table

Table 2 collates the six gates with predeclared pass criteria, the recommended action on failure, and the LEMPA anchor for each. The table is intended to be reused by other studies; the LEMPA column should be replaced with the new study's evidence.

**Table 2. Validation gates and failure handling for atlas-guided radiogenomics.**

| Gate | What it tests | Required evidence | Minimum pass criterion | If the gate fails | Practitioner action | LEMPA anchor |
| --- | --- | --- | --- | --- | --- | --- |
| G0 Pairing integrity | Whether imaging and molecular data are linked one patient to one patient. | Attrition report, linkage manifest, duplicate check. | Explicit inner-join count with no duplicate expansion. | Any downstream performance result is uninterpretable. | Stop and repair linkage before modeling. | V1 paired set reached 130 unique patients with no duplicate expansion. |
| G1 Executability / non-degeneracy | Whether the chosen deconvolution or prediction branch can run without collapse or pathological output. | Smoke test, QC summary, non-degeneracy checks. | All predeclared non-degeneracy checks pass. | The method branch is not usable for evidence generation. | Archive or replace that branch; do not claim method failure was only biological. | V2-G1 passed for the Scaden [9] branch. |
| G2 Cross-method target agreement | Whether the target surface is stable across at least two plausible deconvolution methods. | Agreement summary on abundant targets. | Predeclared agreement threshold met at the intended resolution. | Target instability appears before prediction and invalidates strong downstream claims. | Collapse targets only under predeclared rules or stop the line. | V2-G2 failed with top-10 median `??.087` and `1/10` at `r ??0.4`. |
| G3 Target freeze | Whether downstream modeling uses a fixed target table rather than a moving target definition. | Timestamped abundance or target freeze file used downstream. | Frozen target table exists before B3/B4 evaluation. | Downstream estimates are vulnerable to silent analytic drift. | Re-freeze the target set and rerun downstream steps transparently. | V2-G3 passed. |
| G4 Predictive validation | Whether imaging recovers the target surface at the declared endpoint. | Cross-validated metric table and threshold rule. | Predeclared performance threshold met. | The line remains a negative benchmark, not a validated predictor. | Report the negative result directly; do not soften failure into trend language. | V1 failed the `??0` cell-type rule; V2-G4 failed with `1/4` modules passing. |
| G5 Held-out robustness / replication | Whether performance survives site, batch, histology, or external-cohort separation. | Feasibility memo or held-out/external performance table. | Robustness surface is estimable and passes declared criteria. | Internal findings cannot be generalized or transported confidently. | Defer validation claims and seek trigger-grade external resources. | V2-G5 was skipped because frozen strata were insufficient. |
| G6 Secondary-association audit | Whether any residual positive-looking association is reproducible and independent of leakage. | Hypothesis table, recomputation, target-construction audit, join-integrity audit. | Recomputed values match frozen results and target independence is demonstrated. | Residual associations should be suppressed or heavily caveated. | Keep only subordinate audited remainders; do not let them rescue a failed line. | H4b remained only `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`. |

A graphical version of the framework, including archive/defer branches as legitimate endpoints, is provided as Figure 1; the LEMPA atlas case study layer is shown as Figure 2; a failure-mode cascade for the LEMPA worked example is shown as Figure 3; and a practitioner decision tree is shown as Figure 4 (see *Figures* and `checklist/submission_readiness.md` for production status of each figure).

---

## 3. Methods (Case Study Reproducibility)

This section documents the executed methodology that produced the frozen LEMPA evidence. It is written so that the gate framework in Section 2 can be reproduced by another group on a different organ-and-imaging-modality combination. Code and environment identifiers are provided in *Data and Code Availability*; identifiers marked PLACEHOLDER must be supplied by the author team before submission.

### 3.1 Atlas construction

The atlas layer was constructed from the integrated Human Lung Cell Atlas (HLCA) version published by Sikkema and colleagues [3] and accessed via the Human Cell Atlas data portal [1]. The HLCA harmonizes 49 donors across multiple studies, yielding 584,944 cells annotated at the `ann_finest_level` granularity into 50 cell types (after exclusion of doublet labels and clinically inconsistent annotations). Cell-type labels were preserved as published; no re-clustering was performed. Pathway gene sets were drawn from the Molecular Signatures Database Hallmark collection [22] for glycolysis (`HALLMARK_GLYCOLYSIS`) and oxidative phosphorylation (`HALLMARK_OXIDATIVE_PHOSPHORYLATION`), and from custom curated sets for pentose phosphate pathway activity, tricarboxylic acid cycle behavior, and lactate-related metabolism. Atlas-level pathway scoring used the GSVA enrichment framework [23] adapted to single-cell data via `gseapy` (see Section 3.4). Data handling and atlas inspection used Scanpy [24].

### 3.2 Deconvolution

Two deconvolution branches were used. The primary V1 branch used a non-negative least squares (NNLS) regression on a marker-gene signature matrix derived from the HLCA `ann_finest_level` labels, in the lineage of the NNLS / regression-on-signature methods reviewed alongside CIBERSORTx and related tools [25]. The secondary V2 branch used Scaden [9], a multi-layer feedforward neural network trained on simulated bulk mixtures drawn from the same HLCA reference. The Scaden training configuration was: top 50 HLCA `ann_finest_level` labels; donor-balanced cap of 200 cells per label; 2,000 overlapping genes; 600 simulated bulk mixtures; 100 optimizer steps per ensemble member. This was an explicitly reduced configuration reflecting the local compute environment; the configuration is documented in the supplement (`supplement/METHODS_SUPPLEMENT.md`) so that re-running with a larger configuration would not require re-deriving these settings. Both branches produced patient-by-cell-type fraction matrices over the 130-patient paired analysis set.

The deconvolution-agreement gate (G2) was scored as defined in Section 2.2: the per-cell-type Pearson correlation between NNLS and Scaden fractions was computed across the 130 paired patients, restricted to the top-10 NNLS-abundant cell types, and summarized as the median ($\tilde{\rho}$) together with the count meeting $\rho_k \ge 0.40$. The choice of NNLS abundance as the restriction variable was prespecified.

### 3.3 Radiomics extraction

Radiomic features were extracted from pre-treatment CT volumes in the NSCLC-Radiogenomics collection [7] hosted on TCIA [19]. Feature definitions followed PyRadiomics [13] and were configured under IBSI-aware settings [18] for bin width, voxel resampling, and interpolation. The full extraction set included first-order, shape, and matrix-based texture features (GLCM, GLRLM, GLSZM, NGTDM, GLDM). Segmentation masks were taken from the published SEG resource where available; for patients without a SEG mask, a fallback whole-body outline was used and flagged in the per-patient mask provenance column. The mask provenance distribution on the H4b analysis subset was `SEG = 117` and `fallback_body_outline = 12` (out of 129 cases with a populated mask field).

Of 211 source imaging patients documented at intake, 49 were excluded before pairing (AMC imaging-only cases without matching transcriptomic data), 162 entered radiomics processing, and 130 remained in the paired analysis after inner join with the molecular and deconvolution artifacts. Of these, 7 cases failed PyRadiomics processing or paired QC, leaving the V1 paired set at 130 unique patients. Attrition details are documented in `results/paired/attrition.md` and summarized as a CONSORT-style flow in the supplement.

### 3.4 Pathway scoring

Patient-level pathway scoring used `gseapy.ssgsea` in the local Python environment, in lieu of canonical GSVA-R. We adopted ssGSEA [26] for two reasons: it produces sample-level scores compatible with downstream Pearson and partial-correlation tests, and it does not require an R bridge that was unavailable in the executed environment. The substitution is a known limitation; we discuss its implications in Section 7.3. Reference gene sets were the MSigDB Hallmark Glycolysis and Oxidative Phosphorylation sets [22], with score directionality preserved (positive scores reflect higher relative pathway expression in the sample).

### 3.5 Hypothesis testing and FDR control

The H4 family of hypotheses (H4a glycolysis vs. CT first-order/PET maximum standardized uptake value; H4b texture features vs. cell-type heterogeneity variance; H4c oxidative phosphorylation vs. CT first-order/PET maximum SUV) was preregistered in `drafts/osf_preregistration_v4_hypotheses.md` (the OSF accession identifier is a placeholder pending author-team supply). For each hypothesis, the primary effect estimate was Pearson or Spearman correlation as appropriate to the predictor type, with two-sided $p$-values from the standard correlation null. Partial correlations adjusted for `CT_shape_MeshVolume` were computed via linear residualization. Multiple testing correction within the H4 family was Benjamini?밐ochberg FDR [27] across the 5-test family. All values are reported at machine precision in `results/v2/b4_v2_hypothesis_tests.csv` and re-audited in `results/post_v2_audit/h4b_recompute.csv` (Section 4.4).

### 3.6 Validation gate scoring

Each gate in Section 2 was scored against frozen evidence files. Gate decisions were recorded in `results/v2/V2_FINAL_SUMMARY.md` and the post-V2 evidence freeze in `results/post_v2_audit/evidence_freeze.md`. We additionally provide a recomputation of H4b that confirms exact reproduction of frozen V2 values (Section 4.4 and Table 5).

### 3.7 Computing environment

Analyses ran on a single workstation with Python ??.9, SciPy [28], scikit-learn [29], Scanpy [24], and `gseapy`. Software versions are listed in `environment.yml` in the public code repository (URL PLACEHOLDER). A Docker container with the exact pinned versions is archived at `Zenodo DOI PLACEHOLDER`. Random seeds for cross-validation folds and for the Scaden ensemble are listed in `docs/random_seeds.md`. The R-based GSVA path was not available in this environment; ssGSEA was substituted as described in Section 3.4.

---

## 4. Case Study Results

This section reports the LEMPA evidence under the gate framework defined in Section 2. The case study has three observational tiers: the atlas layer (Section 4.1), the V1 paired validation (Section 4.2), and the V2 redesigned validation with its H4b residual (Sections 4.3??.4). A summary gate table appears as Table 3 (Section 4.5).

### 4.1 The atlas layer (LEMPA description)

LEMPA quantifies pathway-level energy metabolism across 584,944 lung cells from the HLCA [3] spanning 50 annotated cell types. The cell-type composition is dominated by alveolar epithelial cells (AT1 and AT2), capillary and arterial endothelial cells, alveolar and interstitial macrophages, lymphocyte subsets (T, B, NK), and stromal populations (fibroblasts, smooth muscle, pericytes), with smaller specialized populations including airway secretory cells, basal cells, ciliated cells, and rare lineages. Pathway scoring showed broad heterogeneity across the normal lung, with glycolytic enrichment concentrated in specialized airway epithelial and immune populations rather than collapsing onto a single canonical metabolic state. Detailed atlas-only outputs are archived in `results/02_pathway_capacity/` and visualized in `figures/lung_fig1_pathway_capacity_heatmap.{png,pdf}` (Figure 2 of this manuscript).

The atlas layer passes all atlas-only gates: cell annotation is stable as published in [3]; the pathway program library is unambiguous; and the lifespan trajectory analyses (`results/03_lifespan/`) are framed as adult-skewed in keeping with the donor composition of the HLCA. We deliberately do not extend the atlas into developmental claims because the HLCA donor pool is adult-dominated.

### 4.2 V1 paired validation: honest negative baseline

After QC and inner join, the V1 paired analysis cohort comprised 130 patients linked one-to-one between radiomics and molecular deconvolution outputs. Gate G0 (pairing integrity) was satisfied: the inner join produced 130 unique patients with no duplicate expansion (`results/paired/attrition.md`). Gate G1 (executability) was satisfied for the NNLS branch.

The V1 primary endpoint was gate G4 over the 50 cell types in the HLCA `ann_finest_level` labeling. The preregistered success rule was that at least 10 cell types reach cross-validated Pearson $r \ge 0.30$ between radiomic-predicted and deconvolution-derived fractions. The observed result was 3 of 50 cell types: pulmonary alveolar type 2 cell (ElasticNet, $r = 0.424$); alveolar macrophage (RandomForest, $r = 0.341$); capillary endothelial cell (RandomForest, $r = 0.339$). All other cell types fell below $r = 0.30$. Gate G4 therefore failed at V1 (Table 4).

**Table 4. V1 cross-validated cell-type prediction outcomes (gate G4).**

| Metric | Required (preregistered) | Observed (V1) | Verdict |
| --- | ---: | ---: | --- |
| Number of cell types with cross-validated Pearson r ??0.30 (out of 50) | ??10 | 3 | FAIL |
| Top cell type: pulmonary alveolar type 2, ElasticNet | ??| r = 0.424 | informational |
| Second cell type: alveolar macrophage, RandomForest | ??| r = 0.341 | informational |
| Third cell type: capillary endothelial cell, RandomForest | ??| r = 0.339 | informational |
| All other cell types | ??| r < 0.30 | informational |

The V1 H4 family (gate G6 layer) was analyzable but null after FDR correction in the V1 frozen tables. H4a (SUV~max~ vs. glycolysis GSVA, n = 117) returned Pearson r = ??.002 with BH-FDR = 0.510; H4c (SUV~max~ vs. OXPHOS GSVA, n = 117) returned r = ??.054, BH-FDR = 0.510; H4b (entropy, contrast, homogeneity vs. heterogeneity variance, n = 123) returned Spearman ? in [??.176, 0.089] with BH-FDR ??0.260 across all three texture terms. V1 therefore closed as an honest negative baseline: the preregistered cell-type endpoint did not pass, and no H4 hypothesis cleared FDR.

A rare-cell sensitivity analysis (`results/v1/b3_sensitivity_abundance_restricted.md`) did not overturn the V1 G4 failure: restricting to higher-abundance cell types did not increase the count meeting the preregistered threshold above the pass criterion.

### 4.3 V2 redesign: method-fragile negative

V2 was intended to test whether the V1 outcome reflected recoverable method constraints rather than an intrinsically weak translation surface. The redesign substituted the deep-learning deconvolution method Scaden [9] alongside the NNLS branch, with cross-method agreement (gate G2) elevated to a primary prerequisite for downstream interpretation. Gates G1 (executability) and G3 (target freeze) passed: the Scaden scale-up smoke test cleared all four non-degeneracy checks (`results/v2/scaden_scale_up_smoke.md`), and the abundance freeze file (`results/v2/cell_type_abundance.csv`) was written and used downstream.

Gate G2 failed. The top-10 NNLS-abundant cell types yielded a median NNLS-vs-Scaden agreement of $\tilde{\rho} = -0.087$ across the 130 paired patients, with only 1 of 10 cell types reaching $\rho_k \ge 0.40$. Detailed per-cell-type agreements are reported in `results/v2/multi_method_attempt_v3.md` and summarized in Table 5.

**Table 5. V2 cross-method agreement on the top-10 NNLS-abundant cell types (gate G2).**

| Metric | Required (preregistered) | Observed (V2) | Verdict |
| --- | ---: | ---: | --- |
| Median Pearson agreement across top-10 cell types ($\tilde{\rho}$) | ??0.30 | ??.087 | FAIL |
| Count of cell types with $\rho_k \ge 0.40$ (out of 10) | ??6 | 1 | FAIL |
| Method 1 | NNLS on HLCA signature [25] | as preregistered | informational |
| Method 2 | Scaden deep-learning ensemble [9] | as preregistered | informational |
| Cohort size for agreement test | 130 | 130 | informational |

Under the predeclared fallback rule, target collapse from the 50 cell types to four broad consensus modules (epithelial, immune, endothelial, stromal) was triggered. The collapsed-module gate G4 used a smaller required count ($L^{\dagger} = 2$ modules out of 4) at the same $r^{\star} = 0.30$ threshold. The observed outcome was 1 of 4 modules passing (the endothelial module only, $r = 0.31$). The other three modules ??epithelial, immune, stromal ??did not reach the threshold (`results/v2/b3_v2_cv_metrics.csv`).

**Table 6. V2 module-level cross-validated prediction outcomes after predeclared collapse (gate G4).**

| Consensus module | Cross-validated Pearson r | Threshold | Verdict |
| --- | ---: | ---: | --- |
| Endothelial | 0.31 | ??0.30 | PASS |
| Epithelial | < 0.30 | ??0.30 | FAIL |
| Immune | < 0.30 | ??0.30 | FAIL |
| Stromal | < 0.30 | ??0.30 | FAIL |
| **Aggregate (passing modules)** | **1 of 4** | **??2 of 4** | **FAIL** |

Gate G5 (held-out robustness) was recorded as `SKIPPED`. The frozen NSCLC-Radiogenomics paired cohort had effectively non-variable site (Stanford = 130) and limited vendor variation (GE = 107, Siemens = 14, Philips = 3, Toshiba = 1), which together did not support a credible leave-one-site-out, leave-one-vendor-out, or leave-one-batch-out evaluation (`results/v2/intra_v1_stratification_feasibility.md`). We did not attempt to manufacture stratification from the available metadata because doing so would have produced near-empty strata with uninterpretable correlations.

The V2 line-level classification is therefore `METHOD-FRAGILE NEGATIVE`: the redesigned pipeline ran without degeneration, but the multi-method agreement gate failed, target collapse was triggered under the predeclared rule, and the collapsed-target predictive gate still failed.

### 4.4 H4b: caveated residual association

Within the V2 H4 family, hypothesis H4b survived as a positive-looking remainder. The H4b construction relates three CT texture features (`CT_firstorder_Entropy`, `CT_glcm_Contrast`, `CT_glcm_Idm`) to the variance across the four collapsed consensus module fractions (heterogeneity variance). We re-audited H4b under the gate-G6 secondary-association audit (`results/post_v2_audit/h4b_audit.md`); the audit confirmed exact reproducibility of frozen V2 values, predictor-target independence (the radiomic predictors do not enter the target construction), join integrity (130 unique patients with no duplicate expansion; 123 in the H4b analysis subset after ordinary missing-feature filtering), and sign coherence under partial adjustment.

The most important caveat is that the V1 and V2 H4b targets are not the same construct. V1 used `metabolic_heterogeneity_variance` from the original cell-type weighted-capacity construction across all 50 cell types; V2 uses the variance across the four collapsed consensus module fractions. This target redefinition materially strengthens the V2 H4b association relative to V1.

**Table 7. H4b cross-version comparison (gate G6).**

| Hypothesis | V1 effect (frozen) | V1 p~raw~ | V1 partial effect (adj. MeshVolume) | V1 partial p | V2 effect (frozen) | V2 p~raw~ | V2 partial effect | V2 partial p | V2 BH-FDR | V2 partial BH-FDR |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| H4b ??Entropy vs. heterogeneity variance | ??.176 | 0.0520 | ??.206 | 0.0222 | ??.391 | 7.86 횞 10?삘겤 | ??.397 | 5.31 횞 10?삘겤 | 3.93 횞 10?삘겣 | 2.65 횞 10?삘겣 |
| H4b ??Contrast vs. heterogeneity variance | ??.067 | 0.460 | ??.083 | 0.360 | ??.341 | 1.16 횞 10?삘겢 | ??.350 | 7.27 횞 10?삘겣 | 1.93 횞 10?삘겢 | 1.21 횞 10?삘겢 |
| H4b ??Homogeneity vs. heterogeneity variance | 0.089 | 0.329 | 0.122 | 0.181 | 0.371 | 2.42 횞 10?삘겣 | 0.373 | 2.16 횞 10?삘겣 | 6.04 횞 10?삘겣 | 5.41 횞 10?삘겣 |
| Cohort size (V1 ??V2) | n = 123 | | | | n = 123 | | | | | |
| Target construction | Cell-type weighted-capacity variance (50 cell types) | | | | Variance across 4 collapsed consensus modules | | | | | |

The V2 H4b effects are stronger than V1 because the four-module variance is a different quantity. Within the gate framework, H4b is therefore reportable as a `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS` residual association inside an otherwise negative line ??not as a rescue, validation, or confirmation. We deliberately keep H4b late in the manuscript, visually subordinate, and bound to its fallback-derived target so that no reader can mistake it for the primary endpoint.

We confirmed that H4b does not arise from leakage: the radiomic predictors do not enter the heterogeneity-variance target construction. We confirmed that H4b does not arise from duplicate joining: the inner join is 130 unique patients with one row per patient. We confirmed sign coherence under partial adjustment for `CT_shape_MeshVolume`, the strongest available technical correlate. Site and vendor variation were too limited to add a stronger descriptive partial-adjustment surface. The remainder is therefore audited but does not change the line-level outcome.

### 4.5 LEMPA gate outcomes at a glance

Table 3 consolidates the V1?밮2 outcomes under the gate framework. Each row maps a gate or stage to its frozen evidence, what happened in LEMPA, what practitioners may claim, and what they should do next.

**Table 3. LEMPA case-study gate outcomes.**

| Stage or gate | Status | Frozen evidence | What happened in LEMPA | What practitioners may claim | What practitioners should do next |
| --- | --- | --- | --- | --- | --- |
| V1 cohort linkage and pairing (G0) | PASS | `results/v1/V1_FINAL_SUMMARY.md`; `results/paired/attrition.md` | 211 source imaging patients narrowed to 162 radiomics-processing patients and 130 paired patients after inner join. | The paired dataset was real and analyzable. | Preserve attrition accounting as part of the main evidence trail. |
| V1 B3 cell-type prediction gate (G4) | FAIL | `results/v1/V1_FINAL_SUMMARY.md`; `results/v1/cv_metrics_per_celltype.csv` | Only 3/50 cell types met the preregistered r ??0.30 threshold; the required pass count was ??10. | V1 is an honest negative or underpowered baseline. | Do not narrate V1 as partial validation. |
| V1 H4-family hypothesis layer (G6 setup) | PASS for analyzability, null for support | `results/v1/V1_FINAL_SUMMARY.md`; `results/v1/hypothesis_tests.csv` | H4a, H4b, and H4c were analyzable but none remained BH-FDR significant. | The preregistered hypotheses were testable, but V1 provided no positive support. | Keep null results visible. |
| V2-G1 executability | PASS | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/scaden_scale_up_smoke.md` | The Scaden branch ran successfully and was non-degenerate at N = 130. | The redesign was executed rather than merely proposed. | Distinguish executability from validation success. |
| V2-G2 cross-method agreement | FAIL | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/multi_method_attempt_v3.md` | Top-10 NNLS-abundant agreement median was ??.087; only 1/10 abundant cell types reached r ??0.4; module collapse was triggered. | The target surface was unstable at the intended cell-type resolution. | Treat target instability as a primary result, not a nuisance. |
| V2-G3 abundance freeze | PASS | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/cell_type_abundance.csv` | A frozen abundance table was written before downstream B3-v2 reporting. | Downstream V2 summaries used a fixed target table. | Keep frozen target artifacts explicit in the manuscript and supplement. |
| V2-G4 module-level predictive gate | FAIL | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/b3_v2_intra_v1_cross_source.md` | Only 1/4 primary modules passed pooled r ??0.30; endothelial was the only passing module. | The redesigned line remained negative at the primary predictive gate. | Report failure directly; do not frame module collapse as rescue. |
| V2-G5 held-out robustness surface | SKIPPED | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/intra_v1_stratification_feasibility.md` | Frozen local strata did not support feasible held-out site, batch, or histology splits. | No transportability or cross-source robustness claim is available. | Defer stronger claims until trigger-grade external resources exist. |
| V2-G6 inherited H4 table population | PASS | `results/v2/V2_FINAL_SUMMARY.md`; `results/v2/b4_v2_hypothesis_tests.csv` | All inherited H4-family rows were populated; H4a and H4c remained null; H4b was the only positive-looking remainder. | The association layer is reportable only within the negative main outcome. | Keep H4-family interpretation subordinate to the failed main line. |
| Post-V2 H4b audit (G6 audit) | CAVEATED PASS | `results/post_v2_audit/h4b_audit.md` | Recomputed H4b values matched frozen outputs exactly, but the target depended on four-module collapse rather than the original V1 heterogeneity target. | H4b is `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`, not project rescue. | Mention only late and with explicit fallback dependence. |
| Final closure state | CLOSED NEGATIVE | `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`; `handoffs/phase_c_trigger_criteria.md` | V1 remained negative, V2 remained analyzable but method-fragile negative, and Phase C was deferred pending explicit triggers. | The broad radiomics-to-cell-fraction line should be archived for routine planning. | Reopen only if an independent paired cohort or equivalent trigger-grade resource becomes available. |

---

## 5. Failure-mode taxonomy

The LEMPA case study suggests that atlas-guided radiogenomic failure is rarely a single-event problem. More often, the line degrades through a sequence of linked weaknesses that appear at different data layers but converge on the same interpretive outcome: the target surface becomes too unstable, too diluted, or too weakly stress-tested to sustain a strong translational claim. We therefore frame the main recurrent patterns as a compact failure-mode taxonomy rather than as an after-the-fact list of caveats.

The first pattern is target rarity and abundance dilution. When the biologically interesting atlas states are rare in mixed tissue samples, the variance available for recovery at patient scale contracts before imaging enters the analysis. In LEMPA V1, the broad cell-type endpoint failed largely at low-abundance targets, and abundance restriction did not reverse the negative result. The practical point is not that rare states should never be studied, but that biological specificity and imaging recoverability are different design criteria.

The second pattern is cross-method target instability. If two plausible deconvolution methods disagree materially on the quantity that imaging is meant to predict, downstream performance estimates become difficult to interpret because the endpoint itself is no longer stable. LEMPA's V2 agreement failure, with a top-10 median of -0.087, is an extreme example, but the underlying problem is general: imaging cannot validate a target that the upstream transcriptomic layer has not defined consistently enough to serve as ground truth [15,16].

The third pattern is fallback-driven target redefinition. Predeclared fallback rules are useful because they preserve analyzability and prevent silent analytical drift. However, they also change the scientific question. In LEMPA, collapse from 50 cell types to four broad consensus modules was methodologically defensible under the preregistered rule, but the resulting module-level endpoint was not a rescued version of the original cell-type endpoint. It was a different target with broader biological semantics and a different evidentiary burden.

The fourth pattern is cohort attrition with intact analyzability. Public paired datasets often remain workable after attrition, but the inferential surface is defined by the final joined cohort rather than by the largest source count. LEMPA moved from 211 source imaging cases to 162 radiomics-processing cases and then to 130 paired patients. That pathway matters because execution on a real paired cohort is not the same thing as validation on a cohort with enough depth, heterogeneity, and metadata to support durable claims.

The fifth pattern is an absent robustness surface. Even when the analysis runs cleanly, site, vendor, batch, or histology variation may be too limited to support a meaningful held-out evaluation. LEMPA reached that state in V2: the study was analyzable, but the available strata were too thin to justify transportability language. Reporting such a gate as SKIPPED is not a technical embarrassment. It is the correct statement of what the data can and cannot support.

The final pattern is the rhetorically dangerous surviving association. A narrow positive-looking remainder can persist inside an otherwise negative line, particularly after target collapse or endpoint reformulation. LEMPA's H4b remainder falls into this category. It was reproducible and auditable, but it depended on fallback-derived target construction and therefore could not reverse the broader line-level classification. This is precisely the kind of result that benefits from explicit taxonomy: the manuscript can report the association without allowing it to dominate the interpretation.
---

## 6. Practitioner recommendations and reporting discipline

### 6.1 Design-time recommendations

Before any paired analysis begins, investigators should prespecify the endpoint, the success threshold, the agreement gate, the fallback rule, and the intended robustness surface in one place. The practical purpose of this discipline is to keep later analytical flexibility from being mistaken for planned validation logic. In atlas-guided radiogenomics, the target-definition step is too important to remain implicit.

A second design principle is to select endpoints for recoverability as well as biological appeal. Cell states that are rare, composition-sensitive, or weakly stable across methods may still be worth studying, but they should not automatically become primary imaging endpoints. If the likely recoverable unit is a broader compartment or module, that possibility should be admitted at design time rather than only after the primary endpoint fails.

Investigators should also define reopening criteria in advance. If the line fails, what new resource would justify another run: a new paired cohort, a restored method stack, a revised atlas annotation, or an additional imaging modality? Explicit trigger criteria protect the literature from open-ended narratives of deferred success.

### 6.2 Analysis-time recommendations

During execution, the key operational rule is to freeze the target table before downstream modeling and to verify that the predictive code reads from that frozen artifact. Executability should then be reported separately from validation. A branch that ran successfully has cleared a necessary condition for evidence generation, but it has not yet shown that the endpoint is stable or recoverable.

Agreement should be measured before predictive performance is interpreted. If the agreement gate fails, the fallback rule should be invoked transparently and the manuscript should state that the scientific question has narrowed. Residual associations should then be recomputed from frozen artifacts to confirm reproducibility, join integrity, and predictor-target independence rather than inferred from narrative confidence.

### 6.3 Reporting-time recommendations

At write-up, source, processed, paired, and analyzable counts belong in the main text because they define the actual validation surface. Each gate should be labeled explicitly as PASS, FAIL, or SKIPPED, and fallback-derived endpoints should remain visually and rhetorically subordinate to the primary endpoint. This is especially important when a narrow positive-looking remainder survives inside an otherwise failed line.

The abstract should also state the line-level classification directly. Terms such as NEGATIVE, METHOD-FRAGILE NEGATIVE, or INCONCLUSIVE are more informative than diffuse language about mixed signals or partial support. In a fragile multimodal workflow, precision about what failed is part of the scientific contribution.

### 6.4 Table 8: Reporting checklist for future studies
Table 8 collects the items above into a single reporting checklist that can be reused by other studies. The right column gives the LEMPA-specific lesson for each item.

**Table 8. Reporting checklist for future atlas-guided radiogenomics studies.**

| Item | Minimum report | Common failure if omitted | LEMPA lesson |
| --- | --- | --- | --- |
| Atlas provenance | Name the organ-matched atlas [1,3], annotation version, pathway definitions, and any population skew that affects interpretation. | Atlas claims appear stronger or more general than the underlying reference supports. | The lung atlas layer was strongest when framed as an adult-skewed normal-lung resource, not as a universal lifespan map. |
| Paired cohort lineage | Report source cohort counts, exclusions, final paired `N`, and one-to-one linkage rules. | Readers cannot tell whether the predictive benchmark used a real paired cohort or a drifting subset. | LEMPA needed exact counts from 211 source imaging cases to 130 paired patients to keep the benchmark interpretable. |
| Predictor and target definitions | List imaging predictors, transcriptomic targets, covariates, and whether each endpoint was preregistered or fallback-derived. | Residual associations may be mistaken for original primary endpoints. | H4b became high-risk because its V2 target depended on module collapse rather than the original V1 heterogeneity construct. |
| Deconvolution agreement audit | Show at least one cross-method agreement summary before downstream prediction [15]. | Weak targets are treated as ground truth and downstream failures are misattributed. | V2-G2 failure showed that target instability can invalidate the intended cell-type validation surface before modeling. |
| Fallback rules | Declare in advance when targets will be collapsed, analyses skipped, or a line archived. | Post hoc salvage steps can be misread as planned optimization. | Module collapse to epithelial, immune, endothelial, and stromal was only interpretable because the fallback was explicit. |
| Primary predictive gate | State the exact performance metric, threshold, and success rule before showing results. | Negative outcomes are softened into trends or selective examples. | V1 remained negative because the binding rule was ??0 cell types at r ??0.30, not a best-cell-type narrative. |
| Held-out robustness surface | Report whether site, batch, histology, or external-cohort splits were feasible and what happened if they were not [21]. | Internal performance is overgeneralized as transportable validation. | V2-G5 had to stay `SKIPPED` because frozen local strata could not support a real held-out test. |
| Null and secondary hypothesis handling | Report nulls alongside positive-looking remainders and state whether multiple-testing correction was used [27]. | Significant leftovers can overshadow the actual negative main result. | H4a and H4c stayed null, which prevented H4b from being presented as broad biologic confirmation. |
| Figure and table provenance | Map each display item to exact frozen inputs and generation logic. | Visual summaries become harder to audit than the text. | The BIB package needed an explicit figure/table plan so the practitioner story stayed evidence-linked. |
| Environment and method-stack caveats | Report software constraints, scoring substitutions, and whether the executed stack differs from the ideal stack. | Readers assume a reproducibility grade that the run did not actually meet. | LEMPA had to state that pathway scoring used `gseapy.ssgsea` [26] rather than canonical GSVA-R [23] in the local environment. |
| External replication status | Say explicitly whether an independent paired cohort existed and whether replication was achieved. | Stress-test results are mistaken for validated transportable models. | No external paired cohort meant the broad line had to be archived rather than promoted. |
| Reopening criteria | If a line is deferred, state what future evidence would justify reopening it. | Failed programs linger as implicit future promises. | Phase C remained dormant until trigger-grade paired resources or reproducibility-grade method restoration become available. |

---

## 7. Discussion

### 7.1 Comparison to prior atlas-radiogenomic efforts

A growing radiogenomic literature has shown that imaging can recover clinically relevant endpoints when the target is stable and the validation surface is strong enough. The classic example is the radiomic survival work of Aerts and colleagues [12], which established both the feasibility of quantitative image-based prediction and the importance of independent validation cohorts. Subsequent reviews have reinforced two connected lessons: radiomic reproducibility depends on harmonized feature extraction [6,13,18], and the field must distinguish clearly between exploratory feature associations and endpoints with translational durability.

Atlas-guided radiogenomics is more demanding than those earlier settings because it adds an upstream target-construction problem. The endpoint is no longer a relatively stable clinical outcome such as survival. It is a deconvolution-derived fraction, a pathway score, or a function of those quantities, all of which depend on the reference atlas, the signature definition, and the computational method used to project single-cell structure into bulk samples. In that setting, target instability is not a nuisance parameter. It is part of the biological and statistical object under study.

LEMPA therefore sits in a different niche from the classic radiomic prediction literature. The atlas layer is not the primary novelty claim; HLCA already provides the core reference [3]. The contribution is the validation logic extracted from a line that remained biologically interesting but translationally negative under frozen public-data conditions. The point is not that radiomics failed, nor that atlases are uninformative. The point is that their combination imposes a stricter burden of target definition than the field has often acknowledged.

### 7.2 Reopening criteria

We therefore treat reopening criteria as part of the scientific result rather than as an administrative note. The LEMPA paired line should be reopened only if at least one trigger-grade change occurs: an independent paired imaging-plus-RNA cohort with meaningful technical heterogeneity, restoration of a broader method stack that permits stronger agreement testing, a revised atlas annotation that supports a more recoverable target resolution without ad hoc collapse, or an additional imaging modality that changes the biological observability surface.

In the absence of those triggers, the correct status is archival rather than latent optimism. The atlas layer remains reusable as a normal-lung reference, but the broad paired radiogenomic line should not continue to circulate as an implied near-success. Explicit reopening criteria prevent that drift and make later positive claims more defensible if they are eventually achieved.

### 7.3 Limitations of this work

Several limitations remain intrinsic to the present study. The atlas layer inherits the adult-skewed provenance and harmonization choices of HLCA [3], so developmental interpretation should remain narrow. The deconvolution comparison is limited to NNLS and Scaden [9,25], and other pairs could behave differently. The pathway-scoring layer uses gseapy.ssgsea [26] rather than canonical GSVA-R [23], reflecting the executed environment rather than the ideal stack. The radiomics branch, although IBSI-aware [18], still inherits configuration dependence and limited mask-provenance uniformity. Finally, the paired NSCLC-Radiogenomics cohort [7] remains sufficient for an internal benchmark but insufficient for a meaningful held-out robustness surface.

These limitations do not nullify the case study, but they do define its scope. The six-gate framework is intended to generalize conceptually across organs and modalities, whereas the concrete thresholds and observed failures are specific to this organ, cohort, atlas, and method stack. The appropriate inference is therefore not that atlas-guided radiogenomics is doomed, but that stronger claims require a validation surface stronger than the one available here.
---

## 8. Conclusions

LEMPA shows that a biologically useful cell atlas and a successful patient-level radiogenomic bridge are not the same achievement. The atlas layer remains informative as a normal-lung metabolic reference, whereas the paired NSCLC branch closed as a transparent negative benchmark under frozen public-data conditions. That distinction is the main scientific point of the manuscript.

The durable contribution is therefore not a rescued positive claim. It is a practical validation discipline for atlas-guided radiogenomics: the target must remain stable across plausible methods, the endpoint must be frozen before modeling, predictive performance must pass its prespecified rule, robustness must be estimable before it is claimed, and any residual association must stay subordinate when the broader line fails. By treating LEMPA as a worked example rather than a near-success, the manuscript converts one negative case into reusable guidance for how future atlas-guided radiogenomic studies should be designed, challenged, and reported.
---

## Glossary

A standalone glossary of all technical terms used in this manuscript is provided in `supplement/GLOSSARY.md`. Key terms include *atlas-guided radiogenomics*, *validation gate*, *executability*, *cross-method target agreement*, *target freeze*, *predictive validation*, *held-out robustness*, *secondary-association audit*, *METHOD-FRAGILE NEGATIVE*, *line-level classification*, *predeclared fallback*, *target redefinition*, and *reopening criteria*.

## Reporting compliance

STROBE [10] and TRIPOD [11] mapping for this manuscript is provided in `supplement/REPORTING_COMPLIANCE.md`. Items that are not applicable to a review-with-worked-case-study are explicitly marked NA rather than left blank.

---

## Data and Code Availability

This manuscript reports a paired analysis on the NSCLC-Radiogenomics collection [7] hosted on TCIA [19]. Imaging and clinical metadata are available through the TCIA portal under the original collection's data-use agreement. The Human Lung Cell Atlas [3] is accessed through the Human Cell Atlas portal [1].

The LEMPA analysis pipeline (code) and the executed environment (Docker/Conda lock) are intended to be archived as follows; the identifiers below are PLACEHOLDERS that must be supplied by the corresponding author before submission and are listed here so reviewers can verify their presence at production time:

- **Code repository:** `[github.com/PLACEHOLDER/lung-energy-atlas]` (URL PLACEHOLDER).
- **Archived release:** Zenodo DOI `10.5281/zenodo.PLACEHOLDER`.
- **Preregistration:** OSF accession `[osf.io/PLACEHOLDER]`.
- **Processed result tables:** included as Supplementary Data S1?밪5 at the journal portal (V1 cell-type CV metrics; V2 NNLS?밪caden agreement; V2 module-level CV metrics; H4b cross-version comparison; reporting-compliance mapping).
- **Software environment:** `environment.yml` and `Dockerfile` in the repository; random seeds documented in `docs/random_seeds.md`.

Raw imaging data are subject to the NSCLC-Radiogenomics and TCIA data-use agreements and are not redistributed in this manuscript or its supplement.

## Ethics

This study analyzed only de-identified public data accessed under the NSCLC-Radiogenomics [7] and TCIA [19] data-use agreements. No primary human-subject data were collected. The corresponding author's institutional ethics statement and any local data-use language will be added before submission (see `checklist/submission_readiness.md`).

## Conflicts of Interest

To be completed by the author team before submission.

## Funding

To be completed by the author team before submission.

## Acknowledgments

To be completed by the author team before submission.

## Author Contributions

To be completed by the author team before submission. The recommended template (consistent with CRediT taxonomy) is provided in `checklist/submission_readiness.md`.

---

## References

Numbered references are listed below. Final manuscript conversion to BIB Vancouver superscript-numeric style will occur at the production stage. The full locked bibliography with DOIs and URLs is in `bibliography/references_locked.md`.

1. Regev A, Teichmann SA, Lander ES, *et al.* The Human Cell Atlas. *eLife* 2017;6:e27041.
2. Travaglini KJ, Nabhan AN, Penland L, *et al.* A molecular cell atlas of the human lung from single-cell RNA sequencing. *Nature* 2020;587:619??25.
3. Sikkema L, Ram챠rez-Su찼stegui C, Strobl DC, *et al.* An integrated cell atlas of the lung in health and disease. *Nature Medicine* 2023;29:1563??577.
4. Gillies RJ, Kinahan PE, Hricak H. Radiomics: Images Are More than Pictures, They Are Data. *Radiology* 2016;278(2):563??77.
5. Lambin P, Leijenaar RTH, Deist TM, *et al.* Radiomics: the bridge between medical imaging and personalized medicine. *Nature Reviews Clinical Oncology* 2017;14(12):749??62.
6. Bera K, Braman N, Gupta A, Velcheti V, Madabhushi A. Predicting cancer outcomes with radiomics and artificial intelligence in radiology. *Nature Reviews Clinical Oncology* 2022;19(2):132??46.
7. Bakr S, Gevaert O, Echegaray S, *et al.* A radiogenomic dataset of non-small cell lung cancer. *Scientific Data* 2018;5:180202.
8. Aerts HJWL. The Potential of Radiomic-Based Phenotyping in Precision Medicine: A Review. *JAMA Oncology* 2016;2(12):1636??642.
9. Menden K, Marouf M, Oller S, *et al.* Deep learning-based cell composition analysis from tissue expression profiles. *Science Advances* 2020;6(30):eaba2619.
10. von Elm E, Altman DG, Egger M, *et al.* The Strengthening the Reporting of Observational Studies in Epidemiology (STROBE) Statement. *PLoS Medicine* 2007;4(10):e296.
11. Collins GS, Reitsma JB, Altman DG, Moons KGM. Transparent Reporting of a multivariable prediction model for Individual Prognosis or Diagnosis (TRIPOD): the TRIPOD statement. *Annals of Internal Medicine* 2015;162(1):55??3.
12. Aerts HJWL, Velazquez ER, Leijenaar RTH, *et al.* Decoding tumour phenotype by noninvasive imaging using a quantitative radiomics approach. *Nature Communications* 2014;5:4006.
13. van Griethuysen JJM, Fedorov A, Parmar C, *et al.* Computational Radiomics System to Decode the Radiographic Phenotype. *Cancer Research* 2017;77(21):e104?밻107.
14. Munaf챵 MR, Nosek BA, Bishop DVM, *et al.* A manifesto for reproducible science. *Nature Human Behaviour* 2017;1:0021.
15. Avila Cobos F, Alquicira-Hernandez J, Powell JE, Mestdagh P, De Preter K. Benchmarking of cell type deconvolution pipelines for transcriptomics data. *Nature Communications* 2020;11:5650.
16. Sturm G, Finotello F, Petitprez F, *et al.* Comprehensive evaluation of transcriptome-based cell-type quantification methods for immuno-oncology. *Bioinformatics* 2019;35(14):i436?밿445.
17. Ettinger DS, Wood DE, Aisner DL, *et al.* Non-Small Cell Lung Cancer, Version 3.2022, NCCN Clinical Practice Guidelines in Oncology. *Journal of the National Comprehensive Cancer Network* 2022;20(5):497??30.
18. Zwanenburg A, Valli챔res M, Abdalah MA, *et al.* The Image Biomarker Standardization Initiative: Standardized Quantitative Radiomics for High-Throughput Image-based Phenotyping. *Radiology* 2020;295(2):328??38.
19. Clark K, Vendt B, Smith K, *et al.* The Cancer Imaging Archive (TCIA): Maintaining and Operating a Public Information Repository. *Journal of Digital Imaging* 2013;26(6):1045??057.
20. Ioannidis JPA. Why most published research findings are false. *PLoS Medicine* 2005;2(8):e124.
21. Steyerberg EW, Harrell FE Jr. Prediction models need appropriate internal, internal?밻xternal, and external validation. *Journal of Clinical Epidemiology* 2016;69:245??47.
22. Liberzon A, Birger C, Thorvaldsd처ttir H, Ghandi M, Mesirov JP, Tamayo P. The Molecular Signatures Database hallmark gene set collection. *Cell Systems* 2015;1(6):417??25.
23. H채nzelmann S, Castelo R, Guinney J. GSVA: gene set variation analysis for microarray and RNA-Seq data. *BMC Bioinformatics* 2013;14:7.
24. Wolf FA, Angerer P, Theis FJ. SCANPY: large-scale single-cell gene expression data analysis. *Genome Biology* 2018;19:15.
25. Newman AM, Steen CB, Liu CL, *et al.* Determining cell type abundance and expression from bulk tissues with digital cytometry. *Nature Biotechnology* 2019;37:773??82.
26. Barbie DA, Tamayo P, Boehm JS, *et al.* Systematic RNA interference reveals that oncogenic KRAS-driven cancers require TBK1. *Nature* 2009;462:108??12.
27. Benjamini Y, Hochberg Y. Controlling the false discovery rate: a practical and powerful approach to multiple testing. *Journal of the Royal Statistical Society Series B* 1995;57(1):289??00.
28. Virtanen P, Gommers R, Oliphant TE, *et al.* SciPy 1.0: fundamental algorithms for scientific computing in Python. *Nature Methods* 2020;17:261??72.
29. Pedregosa F, Varoquaux G, Gramfort A, *et al.* Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research* 2011;12:2825??830.
30. Subramanian A, Tamayo P, Mootha VK, *et al.* Gene set enrichment analysis: A knowledge-based approach for interpreting genome-wide expression profiles. *Proceedings of the National Academy of Sciences USA* 2005;102(43):15545??5550.

---

*End of v2 manuscript draft. Word count: ~9,800. Status: targeted JCR top-5% revision pass complete; submission still requires author metadata, identifier supply, final BIB-native figure rendering, and one editorial overclaim audit focused on H4b.*



