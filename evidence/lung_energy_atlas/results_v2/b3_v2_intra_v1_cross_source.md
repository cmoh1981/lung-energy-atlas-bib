# B3-v2 Intra-V1 Cross-Source CV

## Scope

- Task executed: `B3-v2` only.
- Consensus source: `results/v2/nsclc130_consensus_v2.csv`.
- Abundance source: `results/v2/cell_type_abundance.csv` (frozen; all four modules are `tier == primary`).
- Radiomics source: `results/radiomics/nsclc211_features_qc.csv` (frozen QC features).
- SF source: `results/v2/intra_v1_stratification_feasibility.md`.
- Because A2 triggered module-level collapse, B3-v2 was restricted to the four module targets: epithelial, immune, endothelial, stromal.
- Because SF found leave-one-site-out, leave-one-batch-out, and histology-split infeasible, this run executes pooled patient-level 5-fold CV only.

## Modeling

- Patients evaluated after inner join: 130.
- Numerical CT/PT radiomic features used: 152.
- Folds: 5 (KFold with shuffle=True, random_state=42).
- Models: ElasticNet and RandomForest using the same defaults as the frozen V1 CV pipeline.
- Primary endpoint: pooled Pearson r >= 0.30 for each primary module, counted at the best-performing model per module.

## Pooled 5-Fold Results

| Module | Best model | Best pooled r | Best pooled p | G4 pass | ElasticNet r | RandomForest r |
| --- | --- | ---: | ---: | --- | ---: | ---: |
| epithelial | RandomForest | 0.268 | 0.002 | FAIL | 0.082 | 0.268 |
| immune | RandomForest | 0.154 | 0.081 | FAIL | 0.009 | 0.154 |
| stromal | RandomForest | 0.173 | 0.049 | FAIL | 0.071 | 0.173 |
| endothelial | RandomForest | 0.343 | 0.000 | PASS | 0.312 | 0.343 |

## Gate Verdicts

- **V2-G4:** FAIL (1/4 primary modules reached pooled Pearson r >= 0.30 at their best-performing model).
- **V2-G5:** OMITTED / N/A. SF found no feasible leave-one-site-out, leave-one-batch-out, or histology-split design, so intra-V1 robustness was not estimable in this run.
- SF fallback confirmation from source note: yes.

## Honest Interpretation

- This output does not claim intra-V1 cross-source robustness because no feasible held-out design existed in the local frozen artifacts.
- V2-G5 is therefore reported as omitted / N/A rather than passed.
- B3-v2 remains a pooled-CV-only check on the four module-level targets created by the A2 module-collapse fallback.
