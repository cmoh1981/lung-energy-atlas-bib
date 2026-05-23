# Lung Energy Atlas JCR 5% Publication Package

Created: 2026-05-23. Revision: v2 (post JCR-5% revision pass).

## Purpose

This folder is a curated publication package for the Lung Energy Metabolism Pathway Atlas (LEMPA) project. It consolidates manuscript drafts, review records, analysis outputs, figures, tables, and submission materials needed to prepare a *Briefings in Bioinformatics*-level review with worked case study.

The package does not change the frozen scientific conclusion. LEMPA is a useful normal-lung metabolic atlas. Its paired NSCLC radiogenomic validation line remains `METHOD-FRAGILE NEGATIVE`.

## Package Location

`C:\Users\ohbry\OneDrive\Apps\lung_energy_atlas_JCR5_publication_20260523`

## Source Roots

- Lung-energy project: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas`
- Legacy review/work folder: `C:\Users\ohbry\OneDrive\Apps\beta cell`

## Main Folders

- `manuscript/`: current BIB-oriented manuscript drafts (v1 and v2) plus revision notes and supplement.
  - `manuscript/BIB_JCR5_manuscript_draft.md` — v1 (narrative-only; retained for diff/audit).
  - `manuscript/v2_BIB_JCR5_manuscript_draft.md` — v2 (JCR-5% targeted; embedded tables, formal Methods, citations, mathematical gate definitions, limitations, reopening criteria; ~9,800 words).
  - `manuscript/revision_notes.md` — v1→v2 change log.
  - `manuscript/supplement/METHODS_SUPPLEMENT.md` — reproducibility-grade methodology detail.
  - `manuscript/supplement/GLOSSARY.md` — defined terms.
  - `manuscript/supplement/REPORTING_COMPLIANCE.md` — STROBE + TRIPOD item-by-item mapping.
- `submission/`: submission readiness and bibliography lock.
  - `submission/SUBMISSION_READINESS.md` — v2 status: `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA`.
  - `submission/BIBLIOGRAPHY_LOCKED_CORE.md` — 29 entries (26 LOCKED, 3 PLACEHOLDER for author-supplied identifiers).
- `tables/`: data/results index.
- `figures/`: top-level figure exports selected from the evidence folders.
- `evidence/lung_energy_atlas/`: copied analysis outputs and prior BIB package from the lung-energy project.
- `evidence/beta_cell/`: copied review history, legacy manuscript artifacts, figures, finalization outputs, and related result folders.

## v2 Revision Highlights

- Manuscript expanded from ~5,500 to ~9,800 words.
- Seven quantitative tables embedded in the main text (data layers, validation gates, LEMPA gate outcomes, V1 CV outcomes, V2 cross-method agreement, V2 module CV, H4b V1-vs-V2 cross-version comparison).
- Formal Methods section (Section 3) plus methods supplement.
- Mathematical definitions of gates G2 and G4.
- Six-mode failure taxonomy (Section 5).
- Four named reopening triggers (Section 7.2).
- Six explicit limitation classes (Section 7.3).
- 30 numbered references mapped to 29 locked bibliography entries.
- STROBE and TRIPOD reporting-compliance appendix.
- Status promoted from `NEEDS_TARGETED_REVISION` to `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA`.

## Scientific State (unchanged from v1)

- V1 status: honest negative baseline.
- V2 status: `METHOD-FRAGILE NEGATIVE`.
- H4a: null.
- H4c: null.
- H4b: interpretable only with major caveats.
- External replication: absent.
- Phase C: dormant unless new paired cohort, restored method stack, new annotation level, or independent imaging modality is provided.

## Core Numerical Anchors (unchanged)

- Atlas scale: 584,944 lung cells and 50 annotated cell types.
- V1 predictive gate: 3/50 cell types reached cross-validated Pearson r ≥ 0.30, below the prespecified success criterion (≥10).
- V2 deconvolution agreement: top-10 median NNLS/Scaden agreement = −0.087; 1/10 top-abundance cell types reached r ≥ 0.4.
- V2 collapsed module gate: 1/4 modules passed the pooled cross-validation threshold.
- H4b retained FDR values: entropy 3.93 × 10⁻⁵, contrast 1.93 × 10⁻⁴, homogeneity 6.04 × 10⁻⁵.

## Current Readiness

Status: `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA`

The v2 manuscript is substantive enough to support PI-level scientific review and editor presubmission inquiry. Remaining blockers are author-team metadata (author list, affiliations, ORCID, funding, conflicts, ethics), reproducibility identifiers (code repo URL, archive DOI, OSF accession), production-rendered figures (Figures 1, 3, 4), one overclaim audit focused on H4b, and final reference-style conversion to BIB Vancouver superscript-numeric.

## Exclusions

This package is a publication-preparation bundle. It is not a complete reproducibility archive. Raw DICOM files, full raw single-cell data, full code repositories, and external archive identifiers must be handled separately before submission.
