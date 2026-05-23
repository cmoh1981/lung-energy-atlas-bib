# Atlas-Guided Radiogenomics Requires Staged Validation

Submission-oriented repository for the *Briefings in Bioinformatics* manuscript:

`Atlas-Guided Radiogenomics Requires Staged Validation: A Bioinformatics Failure-Mode Framework Anchored by the Lung Energy Metabolism Pathway Atlas`

## What this repository contains

- `submission_package/`
  - current manuscript, supplement, figures, bibliography, metadata, and checklists prepared for submission
- `evidence/lung_energy_atlas/briefings_bioinformatics_package/`
  - BIB-oriented drafting assets, figure/table plans, and package notes
- selected executed evidence files under `evidence/lung_energy_atlas/`
  - summary reports and audit artifacts that support the manuscript's gate classifications
- top-level `figures/`, `tables/`, `manuscript/`, and `submission/`
  - working copies of submission-facing assets

## What this repository does not contain

- raw TCIA / NSCLC-Radiogenomics imaging data
- raw third-party Human Cell Atlas data
- large local training artifacts, scratch work, and runtime state
- bulky generated files that are not needed for manuscript review

These materials are excluded because they are either governed by third-party access terms or are local execution artifacts rather than submission assets.

## Reproducibility scope

This repository is organized around the executed submission package and the evidence required to interpret the manuscript's staged validation results. The paper should be read as a reproducibility-aware negative benchmark:

- the atlas layer is reusable as a normal-lung reference resource
- the paired radiogenomic validation line closed negative under prespecified gates
- residual associations are retained only as caveated subordinate findings

## Key locations

- Main manuscript:
  - `submission_package/manuscript/main_manuscript.md`
- Submission tables:
  - `submission_package/tables/`
- Submission figures:
  - `submission_package/figures/`
- Locked references:
  - `submission_package/bibliography/references_locked.md`
- Readiness checklist:
  - `submission_package/checklist/submission_readiness.md`

## External data sources

- NSCLC-Radiogenomics collection / TCIA
- Human Cell Atlas / Human Lung Cell Atlas

Access to those resources should follow their original licenses, terms, and data-use agreements.

## Status

This repository is prepared as a submission-facing code and materials package for *Briefings in Bioinformatics*. Final archive DOI, preregistration identifier, and author metadata remain to be populated in the manuscript before journal submission.

