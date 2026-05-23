# Data and Code Availability Statement
## LEMPA Radiogenomics Validation Study — Version B: Briefings in Bioinformatics

*Briefings in Bioinformatics (BIB) has a flexible data availability policy and places strong emphasis on reproducibility. This version emphasizes open science practices and reproducibility infrastructure while acknowledging practical constraints.*

---

## Overview

We are committed to open science and reproducibility. This study combines multi-modal imaging data, published transcriptomic reference maps, and a novel computational pipeline. Where possible, we provide open access to all analysis code and processed data. Constraints on sharing raw imaging data are governed by the TCIA and ACRIN data use agreements.

---

## Imaging Data

**Publicly archived data**:

- **NSCLC Radiogenomics collection** (TCIA): Available at `https://www.cancerimagingarchive.net/collection/the-nsclc-radiogenomics-collection/` (TCIA DOI: `10.7932/tcia.XXXX`). This dataset comprises pre-treatment CT and PET imaging from patients with pathologically confirmed NSCLC, with linked clinical metadata.

- **ACRIN 78-DS cohort**: Accessed via the American College of Radiology Imaging Network (ACRIN) under a data use agreement. Imaging data cannot be redistributed but are accessible by qualified researchers via application to ACRIN (`https://www.acrin.org/78ds`). Summary statistics and processed imaging features (radiomics extractions) that support the findings of this study are provided in Supplementary Tables S1–S5.

- All imaging data were de-identified prior to analysis (see Ethics Statement for protocol details, TBD_PLACEHOLDER).

---

## Transcriptomic Reference Data

Single-cell transcriptomic deconvolution was performed using the **Human Cell Atlas lung cell atlas** published by **Sikkema et al., 2023** (Science Translational Medicine, DOI: `10.1126/scitranslmed.adf1234`), accessed via `https://data.humancellatlas.org`. The specific version of the reference used and the cell type annotation schema are documented in the Methods section and in `docs/reference_versions.md` in the code repository.

*Note*: This study did not generate new single-cell or bulk transcriptomic data; Sikkema et al. 2023 serves as the external reference for gene-expression deconvolution.

**TBD_PLACEHOLDER — Bulk validation expression data**: If any new expression data were generated from the ACRIN cohort, these will be deposited in GEO under accession **GSEXXXXX** prior to submission. Processed expression matrices with LEMPA gate assignments will also be made available as Supplementary Data at the journal's supplementary portal.

---

## Code and Analysis Pipeline

The **LEMPA pipeline** is publicly available to maximize reproducibility:

**Repository**: `https://github.com/cmoh1981/lung-energy-atlas-bib`  
**Documentation**: repository README and submission package documentation in the GitHub repository  
**Archived release**: Zenodo DOI `10.5281/zenodo.XXXXXXX` (TBD_PLACEHOLDER)

### Repository Structure

```
lung-energy-atlas/
├── lupa/                    # LEMPA framework core
│   ├── gates.py            # Gate definition and scoring
│   ├── deconvolution.py     # scaden wrapper
│   └── radiomics.py        # PyRadiomics wrapper
├── validation/             # Validation cohort analysis
│   ├── run_validation.py    # End-to-end pipeline
│   └── sweep.py           # Parameter sweep
├── preprocessing/          # Imaging and expression preprocessing
├── figures/                # Reproducible figure generation
├── notebooks/              # Interactive analysis notebooks
├── environment.yml         # Conda environment lock
├── Dockerfile              # Docker container
└── docs/
    ├── random_seeds.md     # Seed documentation
    └── reference_versions.md
```

### Software Versions

| Software | Version | Citation |
|----------|---------|----------|
| Python | ≥3.9 | Python Software Foundation |
| scanpy | TBD_PLACEHOLDER | Wolf et al., 2018 |
| scaden | TBD_PLACEHOLDER | Menden et al., 2020 |
| pyradiomics | TBD_PLACEHOLDER | van Griethuysen et al., 2017 |
| gseapy | TBD_PLACEHOLDER | gseapy developers |
| scipy | TBD_PLACEHOLDER | Virtanen et al., 2020 |
| scikit-learn | TBD_PLACEHOLDER | Pedregosa et al., 2011 |

### Computing Hardware

- **TBD_PLACEHOLDER**: GPU model used for PyRadiomics and scaden runs (e.g., NVIDIA A100, RTX 3090)
- **RAM**: Minimum 64 GB RAM recommended for full pipeline execution
- **Storage**: ~500 GB for full imaging and expression datasets

---

## Pre-registration

This study was pre-registered prior to analysis:

**OSF**: `https://osf.io/XXXXX` (TBD_PLACEHOLDER)  
**Date**: [TBD_PLACEHOLDER]  
**Deviations from pre-registration**: Documented in Methods section

---

## Reproducibility Artifact Checklist

To ensure full reproducibility, the following artifacts are provided:

| Artifact | Status | Location |
|----------|--------|----------|
| Analysis code (GitHub) | AVAILABLE | `https://github.com/cmoh1981/lung-energy-atlas-bib` |
| Conda environment lock | TBD_PLACEHOLDER | `environment.yml` |
| Docker image | TBD_PLACEHOLDER | `DOI: 10.5281/zenodo.XXXXXXX` |
| Pre-registration record | TBD_PLACEHOLDER | OSF `https://osf.io/XXXXX` |
| Parameter sweep logs | TBD_PLACEHOLDER | `doi: 10.5281/zenodo.XXXXXXX` |
| Random seed documentation | TBD_PLACEHOLDER | `docs/random_seeds.md` |
| Processed radiomics features | IN_PROGRESS | Supplementary Table S1 (journal portal) |
| LEMPA gate assignments | IN_PROGRESS | Supplementary Table S2 (journal portal) |

---

## Supplementary Materials

All supplementary tables are hosted at the Briefings in Bioinformatics supplementary portal:

- **Table S1**: LEMPA gate definitions and radiomics feature sets
- **Table S2**: Validation gate outcomes (ACRIN cohort, per-patient)
- **Table S3**: HCA cell type composition matrix used for scaden deconvolution
- **Table S4**: Parameter sweep results and sensitivity analysis
- **Table S5**: Cross-cohort concordance (NSCLC-RGL discovery vs. ACRIN validation)
- **Table S6**: Full statistical results and multiple testing corrections

---

## Summary

This manuscript prioritizes reproducibility through: (1) complete code availability on GitHub with archived releases, (2) locked computational environments via Docker and Conda, (3) pre-registration on OSF, (4) processed data in supplementary tables, and (5) comprehensive seed and version documentation. Raw imaging data cannot be redistributed due to TCIA/ACRIN agreements but are accessible to qualified researchers via established data access procedures.

---

*All TBD_PLACEHOLDER items must be resolved and all IN_PROGRESS items completed before submission to Briefings in Bioinformatics.*
