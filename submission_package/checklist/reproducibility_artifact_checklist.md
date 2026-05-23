# Reproducibility Artifact Checklist
## LEMPA Radiogenomics Validation Study

*Target: Briefings in Bioinformatics — emphasizes reproducibility and open science*

This checklist tracks all reproducibility artifacts required for submission to Briefings in Bioinformatics. Items are categorized as **COMPLETE**, **IN_PROGRESS**, **NOT_STARTED**, or **N/A**.

Briefings in Bioinformatics has strong reproducibility expectations including code sharing, pre-registration, and environment lock. The checklist below is aligned with the journal's reproducibility guidelines.

---

## Code Archive

| Artifact | Status | Notes |
|----------|--------|-------|
| Code archive URL (GitHub) | **NOT_STARTED** | URL placeholder: `https://github.com/[institution]/lung-energy-atlas` |
| GitHub repository public | **NOT_STARTED** | Must be public or under embargo for review |
| Zenodo DOI for code release | **NOT_STARTED** | BIB expects persistent DOI for code — obtain before submission |
| Version tag (e.g., v1.0.0) | **NOT_STARTED** | Tag at submitted manuscript commit |
| README with installation and quick-start | **NOT_STARTED** | BIB reviewers will test reproducibility |
| License (MIT/Apache 2.0) | **NOT_STARTED** | Required for open science |

---

## Environment Lock

| Artifact | Status | Notes |
|----------|--------|-------|
| Conda `environment.yml` | **NOT_STARTED** | `conda env export > environment.yml` |
| `requirements.txt` (pip) | **NOT_STARTED** | Secondary lock file |
| Docker image | **NOT_STARTED** | Build and push to Docker Hub or GHCR |
| Docker image Zenodo | **NOT_STARTED** | Persistent archive for Docker image |
| Hardware specs documented | **NOT_STARTED** | GPU model, RAM, CPU — BIB may ask about computational feasibility |

---

## Analysis Pipeline

| Artifact | Status | Notes |
|----------|--------|-------|
| End-to-end run script | **NOT_STARTED** | `run_validation.py` or equivalent |
| Parameter sweep logs | **NOT_STARTED** | Archive all sweeps — BIB values transparency here |
| Random seed documentation | **NOT_STARTED** | Required for computational reproducibility claims |
| Software versions | **NOT_STARTED** | Capture all package versions |

---

## Pre-registration

| Artifact | Status | Notes |
|----------|--------|-------|
| OSF pre-registration | **NOT_STARTED** | BIB strongly encourages pre-registration — URL placeholder: `https://osf.io/XXXXX` |
| Pre-registration public | **NOT_STARTED** | Set visibility to public or embargo |
| Deviations documented | **NOT_STARTED** | List any deviations in Methods |

---

## Data Provenance

| Artifact | Status | Notes |
|----------|--------|-------|
| TCIA dataset version/date | **NOT_STARTED** | Document specific TCIA collection DOI accessed |
| ACRIN data access agreement | **NOT_STARTED** | Note DUA protocol |
| HCA Sikkema reference version | **NOT_STARTED** | Document atlas version and date accessed |
| Imaging metadata provenance | **NOT_STARTED** | Document de-identification procedure |
| GEO accession for new expression data | **NOT_STARTED** | Deposit if new transcriptomic data generated |

---

## Software Versions

| Package | Version | Status |
|---------|---------|--------|
| Python | ≥3.9 | **NOT_STARTED** |
| scanpy | TBD_PLACEHOLDER | |
| scaden | TBD_PLACEHOLDER | |
| PyRadiomics | TBD_PLACEHOLDER | |
| gseapy | TBD_PLACEHOLDER | |
| scipy | TBD_PLACEHOLDER | |
| scikit-learn | TBD_PLACEHOLDER | |
| pandas | TBD_PLACEHOLDER | |
| numpy | TBD_PLACEHOLDER | |
| matplotlib | TBD_PLACEHOLDER | |
| seaborn | TBD_PLACEHOLDER | |
| Jupyter | TBD_PLACEHOLDER | For notebooks/ |

---

## Computing Hardware

| Spec | Detail | Status |
|------|--------|--------|
| GPU model | **TBD_PLACEHOLDER** | e.g., NVIDIA A100 40GB |
| GPU driver / CUDA version | **TBD_PLACEHOLDER** | e.g., CUDA 11.8 |
| RAM | **TBD_PLACEHOLDER** | e.g., 128 GB |
| CPU | **TBD_PLACEHOLDER** | e.g., AMD EPYC 7763 |
| Storage | **TBD_PLACEHOLDER** | ~500 GB |

---

## Submission Package

| Artifact | Status | Notes |
|----------|--------|-------|
| Code Zenodo DOI | **NOT_STARTED** | Required before submission |
| Docker image Zenodo DOI | **NOT_STARTED** | Persistent reference |
| GEO accession (if applicable) | **NOT_STARTED** | |
| Supplementary tables finalized | **IN_PROGRESS** | S1–S6 drafted; formatting to be verified |
| Pre-registration link in manuscript | **NOT_STARTED** | Add OSF link to Methods |

---

## BIB-Specific Reproducibility Expectations

Briefings in Bioinformatics typically evaluates:

1. **Can the reviewer install the environment and run the code?**  
   → Provide `environment.yml`, `requirements.txt`, and Docker image.

2. **Is the analysis pipeline documented end-to-end?**  
   → Provide a single run script that reproduces all main figures.

3. **Are random seeds fixed?**  
   → Document all seeds; computational results must be reproducible within tolerance.

4. **Is there a pre-registration record?**  
   → BIB reviewers may check OSF pre-registration against the analysis.

5. **Are processed data provided?**  
   → Supplementary tables should contain all processed data needed to verify claims without re-running full pipeline.

6. **Is the code permanently archived?**  
   → Zenodo DOI is expected for any novel computational method papers.

---

## Progress Summary

| Category | COMPLETE | IN_PROGRESS | NOT_STARTED | N/A |
|----------|:--------:|:-----------:|:-----------:|:---:|
| Code Archive | 0 | 0 | 6 | 0 |
| Environment Lock | 0 | 0 | 5 | 0 |
| Analysis Pipeline | 0 | 0 | 4 | 0 |
| Pre-registration | 0 | 0 | 3 | 0 |
| Data Provenance | 0 | 0 | 5 | 0 |
| Software Versions | 0 | 0 | 12 | 0 |
| Computing Hardware | 0 | 0 | 5 | 0 |
| Submission Package | 0 | 1 | 3 | 0 |
| **Total** | **0** | **1** | **43** | **0** |

---

## Priority Actions

1. **Create GitHub repository** — upload all code, add README, license, and Zenodo integration
2. **Obtain Zenodo DOI** for code release — enable auto-archiving in GitHub settings
3. **Export environment lock** — `conda env export > environment.yml` and `pip freeze > requirements.txt`
4. **Pre-register on OSF** — before any new analysis runs
5. **Document random seeds** — `docs/random_seeds.md` with all seeds used

---

*If a BIB reviewer cannot reproduce the main results within reasonable effort, this is grounds for rejection. Prioritize the reproducibility package before submission.*