# Evidence Freeze

Date: 2026-05-22
Scope: Task A only from `OPENCODE_NEXT_PROMPT_v6.md`.

## Frozen Input Set

The audit inventory covers exactly 11 Task A inputs listed in `OPENCODE_NEXT_PROMPT_v6.md:58-70`.

## V1 Classification

V1 is an honest negative baseline / underpowered negative validation result, not a successful cross-validation pass.

Primary supporting files:
- `results/v1/V1_FINAL_SUMMARY.md`: states only 3 cell types met the pre-registered B3 threshold and explicitly labels V1 a negative or underpowered validation result.
- `results/v1/cv_metrics_per_celltype.csv`: contains the per-cell-type B3 CV evidence underlying the 3-of-50 pass count.
- `results/v1/hypothesis_tests.csv`: shows H4a, H4b, and H4c were analyzable but not BH-FDR significant in V1.
- `results/v1/b3_sensitivity_abundance_restricted.md`: records the exploratory abundance-restricted sensitivity and confirms the pre-specified failure remains binding.
- `results/deconvolution/multi_method_attempt_v2.md`: records that the second method ran but failed agreement, supporting the method-dependence caveat around late V1 interpretation.

## V2 Classification

V2 classification is `METHOD-FRAGILE NEGATIVE`.

Primary supporting files:
- `results/v2/V2_FINAL_SUMMARY.md`: states the final classification and summarizes why the run is negative but method-fragile.
- `results/v2/multi_method_attempt_v3.md`: records V2-G2 failure, top-10 agreement median `-0.087`, `1/10` cell types at `r >= 0.4`, and triggered module-level collapse.
- `results/v2/b3_v2_intra_v1_cross_source.md`: records V2-G4 failure (`1/4` primary modules passing pooled CV) and that V2-G5 could not be estimated as a held-out cross-source test.
- `results/v2/intra_v1_stratification_feasibility.md`: documents why site/batch/histology stratification was infeasible from frozen local artifacts.
- `results/v2/b4_v2_hypothesis_tests.csv`: confirms the H4-family table was fully populated and that H4b remained the only positive-looking remainder while H4a/H4c were null.

## V2 Gate Table

| Gate | Status | Claim | Carrying files |
| --- | --- | --- | --- |
| V2-G1 | PASS | Scaden scale-up smoke test was executable and non-degenerate. | `results/v2/V2_FINAL_SUMMARY.md` |
| V2-G2 | FAIL | Cell-type-level NNLS vs scaden agreement failed; module-level collapse was triggered. | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/multi_method_attempt_v3.md` |
| V2-G3 | PASS | A timestamped abundance freeze existed and was used downstream. | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/multi_method_attempt_v3.md` |
| V2-G4 | FAIL | Only `1/4` primary modules reached pooled Pearson `r >= 0.30`. | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/b3_v2_intra_v1_cross_source.md` |
| V2-G5 | SKIPPED | No feasible leave-one-site-out, leave-one-batch-out, or histology split was available in frozen artifacts. | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/intra_v1_stratification_feasibility.md`, `results/v2/b3_v2_intra_v1_cross_source.md` |
| V2-G6 | PASS | H4-family rows were fully populated; H4b remained significant while H4a/H4c were null. | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/b4_v2_hypothesis_tests.csv` |

## Claim-to-Artifact Map

| Claim | Files carrying the claim |
| --- | --- |
| V1 B3 gate failed (3 cell types met threshold, not >=10) | `results/v1/V1_FINAL_SUMMARY.md`, `results/v1/cv_metrics_per_celltype.csv` |
| V1 B4 panel analyzable but null after FDR | `results/v1/V1_FINAL_SUMMARY.md`, `results/v1/hypothesis_tests.csv` |
| V1 rare-cell sensitivity does not overturn the primary failure | `results/v1/b3_sensitivity_abundance_restricted.md` |
| V1/V1-era second-method restoration was not robust | `results/deconvolution/multi_method_attempt_v2.md` |
| V2 preflight was executable but not fully green (`YELLOW-B`) | `results/v2_preflight/v2_executability_decision.md` |
| V2 method fragility was driven by multi-method disagreement | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/multi_method_attempt_v3.md` |
| V2 pooled module-level CV still failed the primary endpoint | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/b3_v2_intra_v1_cross_source.md` |
| V2 cross-source robustness could not be estimated from frozen local strata | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/intra_v1_stratification_feasibility.md`, `results/v2/b3_v2_intra_v1_cross_source.md` |
| V2 retained only an H4b positive-looking remainder; H4a/H4c stayed null | `results/v2/V2_FINAL_SUMMARY.md`, `results/v2/b4_v2_hypothesis_tests.csv` |

## Missing Expected Artifacts

None of the 11 Task A inputs were missing.

Consequence:
- No classification claim in this freeze is blocked by an absent Task A input artifact.

## Noted Inconsistency Surface

- V1 `results/v1/hypothesis_tests.csv` shows H4b as non-significant after BH FDR, while V2 `results/v2/b4_v2_hypothesis_tests.csv` shows all three H4b rows as strongly significant. This is not a missing artifact problem, but it is the most important continuity break to keep visible when interpreting the retained H4b remainder inside an otherwise `METHOD-FRAGILE NEGATIVE` run.
