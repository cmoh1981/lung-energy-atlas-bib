# BIB Figure Legends — Draft

*Briefings in Bioinformatics — Atlas-Guided Radiogenomics Validation: A Lung Energy Metabolism Worked Example*

---

## Figure 1. Atlas-guided radiogenomics validation framework.

Atlas-guided radiogenomics should be treated as a staged validation workflow rather than a single prediction task. The workflow proceeds from a reference cell atlas (Human Cell Atlas Lung, 584,944 cells, 50 annotated cell types, 1,627 gene markers) through two parallel deconvolution arms — NNLS (non-negative least squares) and scaden (deep learning deconvolution, 600 simulated bulks, 5-fold cross-validation) — to three stratification designs: by H4 subgroups, by radiomic cluster, and by pathway module. All three stratification attempts encountered failure or partial failure, triggering the cascade G2 partial → G5 fail → B3 module collapse → V2 METHOD-FRAGILE NEGATIVE. Endpoints marked with borders are legitimate scientific conclusions, not execution failures. HCA = Human Cell Atlas. LEMPA = Lung Energy Metabolism Pathway Atlas. NNLS = non-negative least squares.

*(~150 words)*

---

## Figure 2. LEMPA lung energy atlas case study — cohort and data layers.

LEMPA comprised 130 patients with paired CT imaging and bulk RNA-seq (123 after routine missing-feature filtering for the H4b entropy analysis). RNA-seq processing retained 148 genes overlapping the HCA reference panel and MSigDB v7.5 Hallmark collection (50 pathways). Deconvolution was performed using NNLS and scaden (600 simulated bulks, 100 steps per model, 5-fold cross-validation). Cross-method agreement at the intended cell-type surface failed (top-10 median = −0.087), triggering target collapse from 50 cell types to four broad modules (endothelial, epithelial, immune, stromal), of which only the endothelial module passed the pooled cross-validation threshold (r = 0.343). The atlas layer remains reusable as a normal-lung reference; the paired branch is documented as a transparent negative benchmark. HCA = Human Cell Atlas. LEMPA = Lung Energy Metabolism Pathway Atlas.

*(~130 words)*

---

## Figure 3. Failure-mode cascade in the LEMPA worked example.

G2 PARTIAL indicates that only NNLS reached consensus, preventing cross-method comparison at the intended cell-type surface. G5 FAIL shows that the pre-specified correlation gate (r ≥ 0.30) was met by only 3 of 50 cell types. B3 collapse marks the forced reduction from 50 cell types to four broad modules, after which pooled cross-validation passed only the endothelial module (r = 0.343). H4b survived as a caveated remainder (Benjamini-Hochberg FDR = 3.93 × 10⁻⁵ for entropy, 1.93 × 10⁻⁴ for contrast, 6.04 × 10⁻⁵ for homogeneity) but required a fallback target definition; the target redefinition is the critical caveat and the association remains subordinate to the negative line-level conclusion. V2 = second validation redesign. FDR = Benjamini-Hochberg false discovery rate.

*(~130 words)*

---

## Figure 4. Practitioner decision tree for atlas-guided radiogenomics.

Five decision nodes define whether a study should continue to predictive evaluation, collapse to module-level targets, defer pending a larger paired cohort, or archive the line entirely. Node 1 tests for paired RNA-seq + imaging availability. Node 2 checks atlas applicability to disease tissue. Node 3 requires cross-method agreement (NNLS + scaden median r ≥ 0.0) before proceeding. Node 4 requires N ≥ 100 for module-level cross-validated testing. Node 5 applies the pre-specified CV threshold (e.g., r ≥ 0.30), with a pre-declared fallback hypothesis when the primary gate fails. LEMPA encountered failure at Nodes 3 and 5, resulting in a METHOD-FRAGILE NEGATIVE line classification. The practitioner checklist summarizes five pre-analysis actions: freeze gates, test agreement first, prefer stable targets, pre-specify fallback, and report negatives as first-class results. CV = cross-validation. H4b = hypothesis 4b.

*(~140 words)*

---

*Notes on BIB figure legend style:*
- Factual, method-specific language throughout
- No rhetorical inflation ("groundbreaking," "robust," "comprehensive")
- All abbreviations defined at first use
- Statistical thresholds and outcomes reported verbatim from study
- Results framed as executed benchmark, not implied success
- Legends should stand alone without reference to the main text