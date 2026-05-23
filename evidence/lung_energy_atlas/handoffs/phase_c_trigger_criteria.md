# Phase C Trigger Criteria

Phase C is deferred by default. Reopen it only if at least one trigger below is met with the required evidence in hand.

## Trigger 1 - Independent paired cohort at scale

**Condition:** A validated independent lung cancer cohort with paired imaging and RNA-seq is available at `N >= 100`.

- Evidence required before execution: cohort source documented; case count verified after QC; one-to-one patient linkage between imaging and RNA-seq confirmed; histology and basic clinical covariates present.
- Minimum artifacts needed: cohort manifest, patient ID linkage table, RNA-seq matrix/counts, CT/PET image manifest, metadata dictionary.
- What opencode should do next: create a Phase C preflight, verify joins and attrition, rerun the V2 endpoint stack on the independent cohort without changing frozen V1/V2 outputs.

## Trigger 2 - Public TCGA/CPTAC-style linkage becomes usable

**Condition:** Public metadata cleanly links TCGA/CPTAC RNA-seq with CT or PET images and patient IDs.

- Evidence required before execution: duplicate-free ID map; reproducible retrieval path for both omics and imaging; proof that the usable linked sample count is large enough for held-out testing.
- Minimum artifacts needed: patient linkage table, imaging accession list, RNA-seq file list, histology/site metadata, retrieval notes.
- What opencode should do next: build a linkage QC report first, then decide whether the public cohort qualifies as the independent Phase C cohort or should remain a candidate only.

## Trigger 3 - IRB-cleared hospital paired cohort

**Condition:** A hospital cohort with paired imaging and molecular assay is available under approved IRB.

- Evidence required before execution: IRB or data-use approval reference; confirmed paired sample count after exclusions; imaging modality list; assay type and processing notes.
- Minimum artifacts needed: approved cohort roster, de-identified linkage key, imaging manifest, assay matrix or vendor output, collection/protocol metadata.
- What opencode should do next: lock the cohort definition, write a Phase C data-readiness memo, and execute the same analysis gates prospectively on the hospital cohort.

## Trigger 4 - Method stack restored for a reproducibility-grade rerun

**Condition:** The R environment is restored enough to run MuSiC/BayesPrism and canonical GSVA, and the restored stack reproduces the frozen pathway-scoring inputs on a test slice.

- Evidence required before execution: package versions recorded; successful dry run on frozen V1/V2-compatible inputs; output sanity checks showing non-degenerate fractions and callable pathway scores.
- Minimum artifacts needed: environment lockfile, runnable scripts, test-run log, small frozen input slice, output QC table.
- What opencode should do next: run a method-readiness audit first; only promote this to Phase C execution if Trigger 1, 2, or 3 is also met.

## Trigger 5 - Replication-ready external linkage with technical covariates

**Condition:** A paired cohort becomes available with one-to-one image-to-omics linkage plus scanner/site or batch covariates needed for cross-source robustness checks.

- Evidence required before execution: no duplicate expansion in joins; site/scanner or batch fields populated; enough samples per stratum to support held-out testing.
- Minimum artifacts needed: linked cohort table, technical covariate table, QC summary, sample attrition summary.
- What opencode should do next: verify that robustness splits are feasible before any modeling, then open Phase C as a replication-focused run rather than another method-fragile rescue attempt.
