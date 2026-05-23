# B3 Abundance-Restricted Sensitivity (Post-Hoc)

> **Status:** Exploratory post-hoc analysis. The OSF pre-registered B3 success
> criterion (≥10 of all 50 cell types reaching CV r ≥ 0.30) remains the primary
> result and remains FAILED. This sensitivity check explores whether the failure
> is concentrated in rare cell types where deconvolution noise dominates.

## Abundance distribution
- Canonical cell-type set: 50 cell types derived from `results/deconvolution/nsclc130_consensus.csv` and intersected with the paired and CV artifacts.
- Mean median fraction across the 50 cell types: 1.6%; cell types with median fraction > 0: 10/50.
- Cell types above the exploratory abundance thresholds: >0.5% median = 10, >1% median = 10, >5% median = 7.
- Top 5 cell types by median fraction: pulmonary alveolar type 1 cell (15.7% median; 14.2% mean), alveolar macrophage (13.9% median; 13.0% mean), alveolar type 1 fibroblast cell (12.0% median; 12.4% mean), lung pericyte (9.2% median; 9.9% mean), alveolar adventitial fibroblast (8.8% median; 8.6% mean).

## Success counts by abundance threshold

| Threshold (median fraction) | N abundant | N reaching r ≥ 0.30 | Success ratio | Note |
|------------------------------|------------|---------------------|---------------|------|
| All (pre-spec, no filter)   | 50         | 3                   | 6%            | Pre-spec gate; FAIL |
| > 0.5%                       | 10         | 3                   | 30.0%         | Exploratory |
| > 1%                         | 10         | 3                   | 30.0%         | Exploratory |
| > 5%                         | 7         | 1                   | 14.3%         | Exploratory |

## Top-3 abundant cell types hitting r ≥ 0.30
- alveolar macrophage: best-model Pearson r=0.341; median fraction=13.9%; mean fraction=13.0%; % patients >1%=95.4%
- pulmonary alveolar type 2 cell: best-model Pearson r=0.424; median fraction=3.4%; mean fraction=6.2%; % patients >1%=55.4%
- capillary endothelial cell: best-model Pearson r=0.339; median fraction=3.0%; mean fraction=4.0%; % patients >1%=62.3%

## Interpretation guidance for Claude (neutral)
- If success ratio rises substantially when rare cell types are excluded, this is consistent with the "underpowered + dilution" hypothesis.
- If success ratio is unchanged, the failure is NOT explained by rare-cell-type noise alone, and the dominant cause is elsewhere (feature set, target operationalization, or true lack of signal).
- The pre-spec gate failure is binding regardless of this sensitivity outcome.
