# V1 Final Summary

## Final cohort sizes / attrition

- Source imaging cohort documented for pairing review: 211 patients.
- AMC imaging-only patients excluded before V1 radiomics pairing: 49.
- R01 manifest patients carried into V1 radiomics processing: 162.
- Stream 1 radiomics outcome: 162 attempted, 155 CT OK, 155 PT OK, 148 paired imaging OK.
- Stream 1 failures are logged in `results/radiomics/nsclc211_failures.csv`.
- B2 paired analysis set: 130 patients after inner join of QC radiomics input and deconvolution consensus.
- Pairing attrition is documented in `results/paired/attrition.md`.

## What completed successfully

- `results/radiomics/nsclc211_features_qc.csv` exists and is the QC radiomics input used for B2/B3/B4.
- `results/paired/nsclc_paired_radiomics_deconvolution.csv` exists with paired N = 130.
- `results/v1/cv_predictions.csv`, `results/v1/cv_metrics_per_celltype.csv`, and `results/v1/v1_report.md` were generated for V1 cross-validation.
- `results/v1/hypothesis_tests.csv` and `results/v1/h4_panel_figure.pdf` were generated for the B4 run.
- Operational documentation exists for the failed second-method restoration attempt and the NNLS-only fallback in `results/deconvolution/multi_method_attempt.md` and `results/deconvolution/single_method_justification.md`.

## B3 V1 cross-validation outcome

- The pre-registered success criterion was at least 10 cell types with cross-validated Pearson r >= 0.30.
- The observed result was 3 cell types meeting that threshold, so the criterion was not met.
- The 3 cell types reaching r >= 0.30 were pulmonary alveolar type 2 cell (ElasticNet, r = 0.424), alveolar macrophage (RandomForest, r = 0.341), and capillary endothelial cell (RandomForest, r = 0.339).
- This is a negative or underpowered validation result for V1 rather than a successful cross-validation pass.

## B4 hypothesis-testing outcome

- B4 was rerun after explicit pathway scoring was materialized from the 130-patient RNA-seq cohort and joined into the paired table.
- H4a SUVmax vs glycolysis GSVA: n = 117, Pearson r = -0.002, BH FDR = 0.510, partial BH FDR = 0.512.
- H4c SUVmax vs OXPHOS GSVA: n = 117, Pearson r = -0.054, BH FDR = 0.510, partial BH FDR = 0.450.
- H4b entropy vs heterogeneity variance: n = 123, Spearman rho = -0.176, BH FDR = 0.260, partial BH FDR = 0.111.
- H4b contrast vs heterogeneity variance: n = 123, Spearman rho = -0.067, BH FDR = 0.510, partial BH FDR = 0.450.
- H4b homogeneity vs heterogeneity variance: n = 123, Spearman rho = 0.089, BH FDR = 0.510, partial BH FDR = 0.450.
- On this rerun, all preregistered B4 hypotheses are analyzable, but the observed effects remain small and not FDR-significant.

## Method restrictions / environment caveats

- The second deconvolution method could not be restored in this environment, so the current consensus output remains NNLS-only rather than a restored 2-method consensus.
- The explicit B4 pathway scores were generated in Python with `gseapy.ssgsea` using MSigDB Hallmark Glycolysis and Oxidative Phosphorylation gene sets; the canonical GSVA R package was not used in this environment.
- The radiomics full cohort for V1 uses the 162 R01 manifest patients, not the broader 211 imaging-patient list.
- Rscript was unavailable during the second-method restoration attempt, which limited options for non-Python deconvolution recovery.

## Quality gates status (G1-G6)

- G1: PASS. `results/radiomics/nsclc211_features_qc.csv` exists with 162 rows and 196 columns, exceeding the >=130 rows and >=120 features gate.
- G2: PARTIAL. A consensus table exists at 130 x 50 cell-type fractions, but no valid 2-method consensus was restored; NNLS-only justification exists.
- G3: PASS. `results/paired/attrition.md` exists and is populated.
- G4: PASS. The final paired table exists with N = 130.
- G5: FAIL. Only 3 cell types reached cross-validated Pearson r >= 0.30, below the pre-registered >=10 threshold.
- G6: PASS. The hypothesis-testing file exists, and H4a, H4b, and H4c now all have analyzable rows with populated effect-size and FDR fields.

## Recommended next step for Claude review

- Review V1 as an honest negative/partial run, confirm whether NNLS-only deconvolution is acceptable for the write-up baseline, and decide whether the next iteration should focus on restoring an independent second deconvolution method or revising the B3/B4 feature and target definitions before rerun.
