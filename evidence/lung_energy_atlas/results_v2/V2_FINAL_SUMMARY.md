# V2 Final Summary

## Gate Status

| Gate | Status | Basis | Evidence |
| --- | --- | --- | --- |
| V2-G1 | PASS | Scaden scale-up smoke test completed with all four non-degeneracy checks passing. | `results/v2/scaden_scale_up_smoke.md` |
| V2-G2 | FAIL | Top-10 NNLS-abundant agreement median was `-0.087`, with `1/10` cell types at `r >= 0.4`; C1 module-level collapse was triggered. | `results/v2/multi_method_attempt_v3.md`, `results/v2/nsclc130_consensus_v2.csv` |
| V2-G3 | PASS | Timestamped abundance freeze file was written and used for downstream B3-v2 reporting. | `results/v2/cell_type_abundance.csv`, `results/v2/multi_method_attempt_v3.md` |
| V2-G4 | FAIL | Only `1/4` primary module targets reached pooled Pearson `r >= 0.30`. | `results/v2/b3_v2_intra_v1_cross_source.md`, `results/v2/b3_v2_cv_metrics.csv` |
| V2-G5 | SKIPPED | Intra-V1 held-out cross-source design was infeasible locally; B3-v2 ran pooled 5-fold CV only. | `results/v2/intra_v1_stratification_feasibility.md`, `results/v2/b3_v2_intra_v1_cross_source.md` |
| V2-G6 | PASS | All five inherited H4-family rows were populated with effect, raw p, BH FDR, and partial-correlation fields. | `results/v2/b4_v2_hypothesis_tests.csv` |

## Outcome Classification

`METHOD-FRAGILE NEGATIVE`

Reasoning: V2 executed successfully and remained analyzable, but the multi-method agreement gate failed, forcing module-level collapse before B3-v2. The pooled CV primary endpoint then failed (`1/4` primary modules passing), while V2-G5 cross-source robustness was not estimable from local frozen artifacts. This is therefore a negative result whose interpretation remains method-fragile rather than method-robust.

## What V2 Showed

- The scaden HCA Sikkema 2023 path was executable and non-degenerate at N=130 (`V2-G1 PASS`).
- NNLS and scaden did not agree at the intended cell-type level (`V2-G2 FAIL`), so the run fell back to four broad modules.
- Under that fallback, only the endothelial module cleared the pooled-CV threshold (`V2-G4 FAIL`).
- The inherited H4-family test table was fully populated (`V2-G6 PASS`), with significant H4b radiomic heterogeneity associations retained and H4a/H4c remaining null.

## Honest Limitations

- Pathway scoring still relies on `gseapy.ssgsea`, and B4-v2 reused the existing V1 pathway-score layer rather than replacing it with canonical GSVA R.
- The V2 robustness surface is intra-V1 cross-source only; it is not an independent external cohort replication.
- A2-v2 triggered the pre-specified C1 module-level collapse, so downstream interpretation is at `epithelial / immune / endothelial / stromal` module level rather than original cell-type resolution.
- SS/A1 used an explicitly reduced training configuration: top 50 HCA `ann_finest_level` labels, donor-balanced cap of 200 cells per label, 2000 overlapping genes, 600 simulated bulks, and 100 optimizer steps per ensemble member.
- A1-v2 did not rerun a full-HCA retrain; `results/v2/nsclc130_scaden_fractions.csv` is the promoted SS PASS production matrix documented in `results/v2/scaden_celltype_axis.md`.
- SF found no feasible leave-one-site-out, leave-one-RNA-batch-out, or histology-split design in the local frozen artifacts, so `V2-G5` remained untestable.

## Frozen-Artifact Confirmation

V1 and preflight artifacts were not modified during this finalization step. Current mtime spot-checks remained on pre-existing files outside the two allowed targets:

- `results/v1/` latest sampled file: `results/v1/b3_sensitivity_abundance_restricted.md` at `2026-05-21T22:31:14.7781971+09:00`
- `results/deconvolution/` latest sampled file: `results/deconvolution/multi_method_attempt_v2.md` at `2026-05-21T22:53:32.6314725+09:00`
- `results/paired/` latest sampled file: `results/paired/nsclc_paired_radiomics_deconvolution.csv` at `2026-05-21T20:49:34.4167971+09:00`
- `results/v2_preflight/` latest sampled file: `results/v2_preflight/v2_executability_decision.md` at `2026-05-22T07:42:20.3579471+09:00`

Only `results/v2/V2_FINAL_SUMMARY.md` and `progress.md` were edited in this finalization step.

## Protected-File Confirmation

- `drafts/osf_preregistration_v4_hypotheses.md` was not modified (sampled mtime `2026-05-16T19:37:18.5989879+09:00`).
- `V2_REDESIGN_CRITERIA.md` was not modified (sampled mtime `2026-05-22T09:52:04.5710221+09:00`).
- Prior prompts were not modified: `OPENCODE_NEXT_PROMPT.md`, `OPENCODE_NEXT_PROMPT_v2.md`, `OPENCODE_NEXT_PROMPT_v3.md`, `OPENCODE_NEXT_PROMPT_v4.md`, and `OPENCODE_NEXT_PROMPT_v5.md` all retained pre-existing mtimes.
- No local `manuscript_draft.md` file was present in this workspace during finalization, so none was modified.
- No local `REVIEW*.md` files were present in this workspace during finalization, so none were modified.

## Hand-Back

Opencode is finished. Claude should run `/pdca analyze nsclc_radiogenomics_v2`.
