# LEMPA Submission Package

Created: 2026-05-23.

**Target journal:** *Briefings in Bioinformatics*.
**Article type:** Review with worked case study.
**Manuscript title:** Atlas-Guided Radiogenomics Requires Staged Validation: A Bioinformatics Failure-Mode Framework Anchored by the Lung Energy Metabolism Pathway Atlas.
**Manuscript version:** v2 (post JCR-5% revision pass).
**Submission status:** `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA`.

This folder is the consolidated submission package. It contains everything a corresponding author needs to (1) review the manuscript scientifically, (2) supply the missing author/identifier metadata, and (3) submit to the journal. Bulky internal evidence (frozen analysis outputs, intermediate drafts, audit history) lives one level up in `../evidence/` and is *not* duplicated here.

## Folder layout

```
submission_package/
├── README.md                  ← you are here
├── manuscript/                ← main text and submission letters
│   ├── main_manuscript.md     ← v2 manuscript (~10,000 words) — THE submission file
│   ├── v1_manuscript_for_reference.md  ← v1 (narrative-only fallback, retained for diff)
│   ├── revision_notes.md      ← v1→v2 change log
│   ├── cover_letter.md
│   └── presubmission_inquiry.md
├── supplement/                ← three supplementary files referenced by the main manuscript
│   ├── METHODS_SUPPLEMENT.md  ← reproducibility-grade computational methods
│   ├── GLOSSARY.md            ← defined terms (~25)
│   └── REPORTING_COMPLIANCE.md ← STROBE + TRIPOD item-by-item mapping
├── bibliography/
│   └── references_locked.md   ← 35 LOCKED entries + 3 PLACEHOLDER (code repo, archive DOI, OSF)
├── figures/                   ← 14 figure files (PNG + PDF pairs)
├── tables/
│   └── data_results_index.md  ← evidence-to-claim mapping
├── metadata/                  ← TEMPLATES — author team must fill these
│   ├── author_contributions.md
│   ├── conflicts_of_interest.md
│   ├── ethics_statement.md
│   ├── funding_acknowledgments.md
│   └── data_code_availability.md
└── checklist/
    ├── submission_readiness.md         ← current status + remaining blockers
    └── reproducibility_artifact_checklist.md
```

## What is locked vs. what needs author-team supply

**Locked and ready (no further work needed for scientific content):**

- Main manuscript (~10,000 words, 7 embedded tables, formal Methods, mathematical gate definitions, 30 numbered references, limitations, reopening criteria).
- Three supplementary files.
- Bibliography (35 LOCKED entries with DOIs).
- Cover letter and presubmission inquiry drafts.
- Tables / data-results index.
- 14 selected figure files.
- Revision notes (v1→v2 change log).
- Submission-readiness checklist.

**Author-team must supply before submission:**

1. **Author metadata** in `metadata/author_contributions.md`:
   - Full author list with affiliations
   - ORCID identifiers
   - Corresponding author identification and contact email
   - Author contribution statement (CRediT taxonomy preferred)
2. **Compliance metadata** in `metadata/` files:
   - `funding_acknowledgments.md` — funding sources and grant numbers
   - `conflicts_of_interest.md` — declared conflicts (or "none declared")
   - `ethics_statement.md` — institutional ethics / data-use language
3. **Reproducibility identifiers** in `metadata/data_code_availability.md`:
   - Public code repository URL (replacing `[github.com/PLACEHOLDER/lung-energy-atlas]`)
   - Archived release DOI (replacing `10.5281/zenodo.PLACEHOLDER`)
   - OSF preregistration accession (replacing `[osf.io/PLACEHOLDER]`)
4. **Figure production:** vector renderings for Figures 1, 3, 4 (currently schematic plans in the manuscript text). Figures 2 and 5 are already exported in `figures/`.
5. **One overclaim audit** focused on H4b paragraphs (Sections 4.4, 7.1, and the abstract sentence on H4b) by a fresh reviewer who is not the lead writer.

## Frozen scientific anchors (preserved verbatim from the handoff)

The following statements remain fixed unless new analyses directly overturn them:

- LEMPA is useful as a normal-lung energy-metabolism atlas.
- Atlas scale: 584,944 lung cells, 50 annotated cell types.
- V1: honest negative baseline; only 3/50 cell types reached cross-validated Pearson r ≥ 0.30.
- V2: `METHOD-FRAGILE NEGATIVE`; top-10 NNLS/Scaden agreement = −0.087; 1/10 cell types at r ≥ 0.4; 1/4 collapsed modules passed pooled CV.
- H4a: null. H4c: null. H4b: interpretable only with major caveats, dependent on the four-module target redefinition.
- H4b BH-FDR: entropy 3.93 × 10⁻⁵, contrast 1.93 × 10⁻⁴, homogeneity 6.04 × 10⁻⁵.
- External replication: absent. Phase C: dormant pending explicit reopening triggers.

## Submission workflow (recommended order)

1. **PI / corresponding author review.** Read `manuscript/main_manuscript.md`. If the framing or any specific claim needs adjustment, do that first. Note: the manuscript is structured so that scientific content can be edited without breaking citations or table numbers.
2. **Run the H4b overclaim audit.** Have a fresh reviewer (not the lead writer) read Sections 4.4 and 7.1 and the abstract sentence on H4b. Verify no language frames H4b as rescue, validation, or confirmation.
3. **Fill the metadata.** Complete the 5 files in `metadata/`. Replace all `PLACEHOLDER` and `TBD_PLACEHOLDER` markers.
4. **Finalize the figures.** Render Figures 1, 3, 4 as vector files. Confirm Figures 2 and 5 in `figures/` are publication-resolution.
5. **Convert references to BIB Vancouver style** (superscript-numeric) at production stage.
6. **Submit the presubmission inquiry first** if the editor prefers that route; otherwise submit the full manuscript with cover letter directly.

## Editorial position (load-bearing)

The strongest submission path is **not** to sell LEMPA as a successful radiogenomic discovery paper. The strongest path is to frame LEMPA as a practitioner-facing bioinformatics validation case study: a large and useful lung metabolic atlas whose paired public NSCLC radiogenomic branch transparently failed key validation gates. This position is preserved verbatim in the v2 manuscript and should not be weakened during finalization.

## Files external to this package

The following supporting material lives outside `submission_package/` and is *not* duplicated here:

- **Frozen analysis outputs** for V1, V2, post-V2 audit, deconvolution, radiomics, paired tables: `../evidence/lung_energy_atlas/results_*` and `../evidence/lung_energy_atlas/results_post_v2_audit/`.
- **Prior BIB review/quality-gate records** (for audit trail): `../evidence/lung_energy_atlas/briefings_bioinformatics_package/`.
- **Legacy artifacts** from the earlier project: `../evidence/beta_cell/`.
- **Handoff and provenance**: `../CLAUDE_HANDOFF.md`, `../PACKAGE_MANIFEST.md`.

These are referenced by the manuscript and supplements via relative paths but are not part of the journal submission itself.

## Contact and ownership

This package was assembled by an automated revision pass on 2026-05-23 acting on the directives in `../CLAUDE_HANDOFF.md`. All scientific anchors, the editorial position, and the H4b caveat structure were preserved per the handoff's hard warning that the negative conclusion must not be weakened for narrative effect. The corresponding author is the final authority on every claim in this package.
