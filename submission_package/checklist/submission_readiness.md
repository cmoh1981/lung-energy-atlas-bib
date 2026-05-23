# Submission Readiness (v2)

Created: 2026-05-23. Revision: v2 (post JCR-5% revision pass).

Target journal: *Briefings in Bioinformatics*.

Target article type: Review with worked case study.

Current status: `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA`.

## Status delta from v1

| Dimension | v1 status (2026-05-23 AM) | v2 status (2026-05-23 PM) |
| --- | --- | --- |
| Editorial position | Defined | Unchanged (locked) |
| Manuscript depth | ~5,500 words; narrative-only; no embedded tables; no Methods | ~9,800 words; 7 embedded tables; formal Methods (Section 3); mathematical gate definitions; comparative discussion; limitations; reopening criteria |
| Citation hooks | None in prose | Numerical citations integrated throughout; references list embedded |
| Bibliography lock | 11 entries; `TO VERIFY` items for PyRadiomics, Scaden, TRIPOD, STROBE, deconvolution comparators | 29 entries; 26 `LOCKED`, 3 `PLACEHOLDER` (code repo, archive DOI, OSF) |
| Tables 1–4 | Existed in evidence folder only | Embedded in manuscript main text (Sections 2 and 6) |
| Quantitative case-study tables | Absent in main text | Tables 4, 5, 6, 7 embedded (V1 CV outcomes; V2 agreement; V2 module CV; H4b V1-vs-V2 cross-version comparison) |
| Methods supplement | Absent | `manuscript/supplement/METHODS_SUPPLEMENT.md` complete |
| Glossary | Absent | `manuscript/supplement/GLOSSARY.md` complete |
| STROBE/TRIPOD compliance | Absent | `manuscript/supplement/REPORTING_COMPLIANCE.md` complete (19/22 STROBE items addressed; 17/22 TRIPOD items addressed; remainder marked NA with rationale) |
| Limitations section | Absent | Section 7.3 (6 explicit limitation classes) |
| Reopening criteria | Implicit | Section 7.2 (4 named triggers) |
| Failure-mode taxonomy | Implicit | Section 5 (6 named modes) |
| Author / funding / CoI / ethics metadata | Placeholder | Still placeholder (cannot be invented; supplied by author team) |
| Code / data / OSF identifiers | Placeholder | Still placeholder (cannot be invented; supplied by author team) |

## Editorial position (unchanged from v1)

The strongest submission path is **not** to sell LEMPA as a successful radiogenomic discovery paper. The strongest path is to frame LEMPA as a practitioner-facing bioinformatics validation case study: a large and useful lung metabolic atlas whose paired public NSCLC radiogenomic branch transparently failed key validation gates. This editorial position is preserved verbatim in the v2 manuscript and supplement and is reinforced by the new failure-mode taxonomy (Section 5) and limitations (Section 7.3).

## Ready components (after v2 pass)

- v2 BIB-oriented manuscript at `manuscript/v2_BIB_JCR5_manuscript_draft.md` (~9,800 words).
- v1 manuscript at `manuscript/BIB_JCR5_manuscript_draft.md` retained for diff/audit.
- Prior BIB package preserved in `evidence/lung_energy_atlas/briefings_bioinformatics_package`.
- Core result state is frozen and internally consistent. All scientific anchors from the handoff are preserved verbatim in v2.
- Bibliography v2 lock at `submission/BIBLIOGRAPHY_LOCKED_CORE.md` (29 entries; 26 `LOCKED` with full DOI/URL, 3 `PLACEHOLDER` for author-supplied identifiers).
- Data/results index at `tables/DATA_RESULTS_INDEX.md`.
- Methods supplement at `manuscript/supplement/METHODS_SUPPLEMENT.md`.
- Glossary at `manuscript/supplement/GLOSSARY.md`.
- Reporting compliance mapping at `manuscript/supplement/REPORTING_COMPLIANCE.md` (STROBE + TRIPOD).
- Revision notes at `manuscript/revision_notes.md`.

## Blocking items before submission

The following items are unchanged from v1 in the sense that they remain blocked, but the locus of the block is narrower than before: every blocker now sits at *author-team metadata* or *production rendering* rather than at manuscript content.

1. **Author metadata.**
   - Author list (full names, ORCID identifiers)
   - Institutional affiliations (numbered)
   - Corresponding author identification and contact email
   - Author contribution statement (CRediT taxonomy preferred)

2. **Compliance metadata.**
   - Funding statement
   - Conflict of interest statement
   - Ethics / data-use statement (institutional language)
   - Acknowledgments

3. **Reproducibility identifiers.**
   - Public code repository URL (replacing `[github.com/PLACEHOLDER/lung-energy-atlas]`)
   - Archived release DOI (replacing `10.5281/zenodo.PLACEHOLDER`)
   - OSF preregistration accession (replacing `[osf.io/PLACEHOLDER]`)
   - Environment lock checksum (after final pin of `environment.yml`)

4. **Figure production.**
   - Figure 1: atlas-guided radiogenomics validation framework — BIB-native vector rendering needed.
   - Figure 2: LEMPA lung energy atlas case study — assembled from `lung_fig1_pathway_capacity_heatmap.*` and `lung_fig2_lifespan_correlation_heatmap.*`; ready for vector export.
   - Figure 3: failure-mode cascade — schematic to be rendered.
   - Figure 4: practitioner decision tree — schematic to be rendered.
   - Figure 5 (optional): H4b caveated heterogeneity remainder — keep visually subordinate; consider folding into the supplement only.

5. **Reference list conversion.**
   - Convert the 30-entry numbered list in the v2 manuscript to BIB Vancouver superscript-numeric style at production stage.
   - Reconcile final reference numbering with the locked bibliography after any final-pass additions/removals.

6. **One overclaim audit.**
   - Conduct a single editorial overclaim audit focused on the H4b paragraphs (Sections 4.4, 7.1, and the abstract sentence on H4b). Verify that no language has crept in that frames H4b as rescue, validation, or confirmation. Recommended owner: a reviewer who is not the lead writer.

## Recommended finalization order

1. Run the overclaim audit (item 6 above). Resolve any flagged sentences.
2. Author team supplies metadata (items 1–3).
3. Production team finalizes figure renderings (item 4) and reference style (item 5).
4. PI / corresponding author signs off on the data/code availability statement.
5. Prepare cover letter from `evidence/lung_energy_atlas/briefings_bioinformatics_package/BIB_cover_letter.md` (already drafted; needs author-team finalization).
6. Optionally prepare a presubmission inquiry from `BIB_presubmission_inquiry.md` if the editor prefers that path.
7. Submit.

## Decision

Status promoted from `NEEDS_TARGETED_REVISION` (v1) to `READY_FOR_PI_REVIEW_BLOCKED_ON_METADATA` (v2). The manuscript is now substantive enough to support PI-level scientific review and editor presubmission inquiry. It is not yet ready for journal submission because author-team metadata and production-rendered figures have not been supplied. No further content rewriting is required to clear the manuscript itself; the remaining work is metadata, identifier supply, and figure production.

The frozen scientific state remains unchanged from the handoff:

- LEMPA atlas: 584,944 cells × 50 cell types; useful normal-lung reference.
- V1: 3/50 cell types reached cross-validated Pearson r ≥ 0.30 against a required count of 10. Honest negative baseline.
- V2: NNLS–Scaden top-10 median agreement = −0.087; 1/10 abundant cell types at r ≥ 0.4. After predeclared fallback collapse to four modules, 1/4 modules passed pooled CV. `METHOD-FRAGILE NEGATIVE`.
- H4b: `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`. Reproducible; dependent on the V2 four-module heterogeneity-variance target redefinition; does not rescue the line.
- Phase C: dormant; reopening triggers explicit in Section 7.2.

If the corresponding author objects to any framing in the v2 manuscript, the v1 manuscript remains available at `manuscript/BIB_JCR5_manuscript_draft.md` as the conservative narrative-only fallback.
