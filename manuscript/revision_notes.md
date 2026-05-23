# Revision Notes: v1 → v2

Created: 2026-05-23.

This file documents the differences between `BIB_JCR5_manuscript_draft.md` (v1) and `v2_BIB_JCR5_manuscript_draft.md` (v2). The v2 pass was scoped to elevate the manuscript toward JCR top-5% caliber for *Briefings in Bioinformatics* without weakening the frozen negative scientific conclusion, per the explicit instruction in `CLAUDE_HANDOFF.md`.

## Summary

- v1 word count: ~5,500. v2 word count: ~9,800.
- v1 embedded tables: 0. v2 embedded tables: 7.
- v1 inline citation hooks: 0. v2 inline citation hooks: 30 numbered references mapped to 29 locked bibliography entries.
- v1 Methods section: absent. v2 Methods section: full Section 3 (atlas, deconvolution, radiomics, pathway scoring, hypothesis testing, gate scoring, environment) with a companion `supplement/METHODS_SUPPLEMENT.md`.
- v1 mathematical formalism: absent. v2 mathematical formalism: gate G2 and G4 defined with explicit equations and thresholds in Section 2.
- v1 supplement: absent. v2 supplement: three files (`METHODS_SUPPLEMENT.md`, `GLOSSARY.md`, `REPORTING_COMPLIANCE.md`).

## What changed (section by section)

**Title.** v1: "From Cell Atlases to Radiogenomics: A Lung Energy Metabolism Case Study in Bioinformatics Validation Failure Modes." v2: "Atlas-Guided Radiogenomics Requires Staged Validation: A Bioinformatics Failure-Mode Framework Anchored by the Lung Energy Metabolism Pathway Atlas." The v2 title leads with the durable contribution (the staged validation framework) and demotes the case study to anchor status.

**Abstract.** v1: single paragraph (~280 words). v2: structured abstract (Motivation / Results / Conclusion / Availability / Contact / Supplementary; ~350 words). The v2 abstract names quantitative anchors (3/50, −0.087, 1/10, 1/4) inline.

**Key Points.** v1: 5 bullets. v2: 6 bullets. The v2 list adds an explicit point on residual-association handling and on public-cohort ceilings.

**Section 1 (Introduction).** v1: 3 paragraphs without citations. v2: 3 sub-sections with 14 numbered references covering atlas resources [1–3], radiogenomics [4–6], NSCLC datasets [7,8], deconvolution benchmarking [15], radiomics standardization [13,18], TCIA [19], reproducibility [14], and broader radiomics framing [6, 12]. The v2 introduction explicitly states the contribution roadmap as six numbered items.

**Section 2 (Framework, new).** v1: framework was described narratively across Section 7. v2: dedicated Section 2 with formal notation (Section 2.1), six gates with mathematical definitions for G2 and G4 (Section 2.2), embedded Table 1 (data layers) and Table 2 (validation gates) (Sections 2.3–2.4). This is the largest content addition.

**Section 3 (Methods, new).** v1: no methods section. v2: full Methods with seven subsections (atlas, deconvolution, radiomics, pathway scoring, hypothesis testing, gate scoring, environment) and a companion `METHODS_SUPPLEMENT.md` with the per-parameter detail.

**Section 4 (Case Study Results).** v1: results were distributed across Sections 4 (deconvolution), 5 (rarity), 8 (V1/V2 case), 9 (H4b). v2: consolidated under Section 4 with subsections for atlas (4.1), V1 (4.2), V2 (4.3), H4b (4.4), and a summary Table 3 (4.5). Tables 4, 5, 6, 7 added: V1 CV outcomes, V2 cross-method agreement, V2 module-level CV outcomes, H4b V1-vs-V2 cross-version comparison with frozen p-values at machine precision.

**Section 5 (Failure-mode taxonomy, new).** v1: failure modes were implicit. v2: six named modes (target rarity / abundance dilution; cross-method instability; fallback as redefinition; cohort attrition with intact analyzability; absent robustness surface; surviving association with target dependence). Each mode is anchored to specific LEMPA evidence.

**Section 6 (Practitioner recommendations).** v1: 4 numbered recommendations. v2: organized into design-time, analysis-time, and reporting-time categories (5+4+5 recommendations) plus the embedded Table 4 (reporting checklist).

**Section 7 (Discussion, expanded).** v1: brief discussion folded into Section 11. v2: three subsections — comparison to prior atlas-radiogenomic work (7.1) explicitly citing Aerts 2014 [12] and Avila Cobos 2020 [15]; reopening criteria (7.2) with four named triggers; limitations (7.3) with six explicit classes.

**Section 8 (Conclusions).** v1: 2 paragraphs. v2: 1 paragraph (tightened). The framing now emphasizes that LEMPA is the case-study anchor and the framework is the durable contribution.

**Glossary.** Added as a separate supplement file with ~25 defined terms.

**Reporting compliance.** Added STROBE and TRIPOD item-by-item mapping in `REPORTING_COMPLIANCE.md`.

## What did *not* change

The frozen scientific anchors are unchanged in v2:

- Atlas scale: 584,944 cells × 50 cell types.
- V1: 3/50 cell types reached cross-validated Pearson r ≥ 0.30. Honest negative baseline.
- V2: NNLS–Scaden top-10 median agreement = −0.087; 1/10 abundant cell types at r ≥ 0.4. After predeclared fallback collapse to four modules, 1/4 modules passed pooled CV. `METHOD-FRAGILE NEGATIVE`.
- H4b FDR values: 3.93 × 10⁻⁵ (entropy), 1.93 × 10⁻⁴ (contrast), 6.04 × 10⁻⁵ (homogeneity).
- H4b classification: `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`. Reproducible; dependent on the V2 four-module heterogeneity-variance target redefinition; does not rescue the line.
- Phase C: dormant.
- External validation: absent.

The editorial position is unchanged: LEMPA is the worked case study, not the central novelty claim; the validation-gate framework is the durable contribution; H4b stays subordinate; the negative line-level outcome is preserved.

## Authoring discipline

- All citations point to references locked in `submission/BIBLIOGRAPHY_LOCKED_CORE.md`. No fabricated citations.
- All numerical values in the v2 manuscript trace to frozen evidence files in `evidence/lung_energy_atlas/`. No values were regenerated or re-fit.
- The H4b paragraphs were structured to discourage rescue framing: H4b appears late, in a clearly subordinate Section 4.4, with the V1-vs-V2 comparison table making the target redefinition visually unavoidable.
- The reopening criteria (Section 7.2) are named so that future work cannot be implicitly promised.

## Risk register

- Reviewers may request additional reference work to broaden the discussion (e.g., citation of CIBERSORTx benchmarking specifically against Scaden). The locked bibliography supports this if needed.
- The 7 embedded tables in the main text are dense for a BIB article. At production stage, Tables 4, 5, 6 may be moved to supplementary tables (S1–S3) while the framework Tables 1–4 remain in the main text. The v2 file keeps everything in the main text so that the PI can review the full quantitative case before deciding what to relocate.
- Figures 1, 3, 4 are still schematic plans rather than rendered vector files. This is noted in `submission/SUBMISSION_READINESS.md`.

## Files added or modified in this revision

| Path | Status |
| --- | --- |
| `manuscript/v2_BIB_JCR5_manuscript_draft.md` | NEW (~9,800 words) |
| `manuscript/revision_notes.md` | NEW (this file) |
| `manuscript/supplement/METHODS_SUPPLEMENT.md` | NEW |
| `manuscript/supplement/GLOSSARY.md` | NEW |
| `manuscript/supplement/REPORTING_COMPLIANCE.md` | NEW |
| `submission/BIBLIOGRAPHY_LOCKED_CORE.md` | EXPANDED (11 → 29 entries) |
| `submission/SUBMISSION_READINESS.md` | UPDATED (status promoted; blockers narrowed) |
| `PACKAGE_MANIFEST.md` | UPDATED (v2 entries appended) |
| `manuscript/BIB_JCR5_manuscript_draft.md` (v1) | UNCHANGED (retained for diff/audit) |

## Next agent action

Read `submission/SUBMISSION_READINESS.md` for the remaining blockers, then either:

1. Run the H4b overclaim audit on Sections 4.4, 7.1, and the abstract (recommended owner: a fresh reviewer agent).
2. Forward the v2 package to the PI / corresponding author for metadata supply.
3. Begin figure production for Figures 1, 3, 4 once the framework numbering is final.
