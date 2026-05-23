# A2-v2 Multi-Method Attempt v3

- Task: `A2-v2`
- Generated UTC: `2026-05-22T02:23:22Z`
- Frozen NNLS baseline: `results/deconvolution/nsclc130_cell_fractions_nnls.csv`
- Frozen consensus input: `results/deconvolution/nsclc130_consensus.csv`
- Scaden input: `results/v2/nsclc130_scaden_fractions.csv`
- Frozen consensus effectively NNLS-only: **yes**
- Interpretation: the frozen `nsclc130_consensus.csv` is numerically identical to the frozen NNLS matrix after column reordering, so the honest baseline for A2-v2 is NNLS rather than a true pre-existing multi-method consensus.

## Axis Alignment

- Common samples: `130`
- Scaden source labels: `50`
- Mapped scaden target labels: `39`
- NNLS labels: `50`
- Retained comparison intersection: `39` target labels
- Unmapped scaden labels dropped: `none`
- NNLS-only labels dropped from per-cell-type agreement: `CD1c-positive myeloid dendritic cell, T cell, acinar cell, brush cell of tracheobronchial tree, dendritic cell, fibroblast, hematopoietic stem cell, mesothelial cell, mucus secreting cell, pulmonary neuroendocrine cell, stromal cell`
- Mapped scaden targets absent from NNLS and dropped: `none`

### Collapsed scaden labels

- `capillary endothelial cell` <= EC aerocyte capillary, EC general capillary
- `club cell` <= Club (non-nasal), Club (nasal)
- `endothelial cell of lymphatic vessel` <= Lymphatic EC differentiating, Lymphatic EC mature
- `epithelial cell of lower respiratory tract` <= Suprabasal, SMG duct, pre-TB secretory
- `lung macrophage` <= Interstitial Mph perivascular, Alveolar Mph CCL3+, Alveolar Mph MT-positive, Alveolar Mph proliferating
- `multiciliated epithelial cell` <= Deuterosomal, Multiciliated (nasal)
- `pulmonary alveolar type 2 cell` <= AT2, AT2 proliferating
- `vein endothelial cell` <= EC venous systemic, EC venous pulmonary

## Agreement Summary

- Top-10 NNLS-abundant median r: `-0.087`
- Top-10 with r >= 0.4: `1/10`
- V2-G2 verdict: **FAIL**
- C1 outcome: **module-level collapse**
- Module-level collapse triggered: **yes**
- Compromised status: **yes**
- Restriction flag: **no**
- Note: Agreement was computed on per-cell-type z-scores across patients; consensus values are reported in raw fraction space to preserve abundance tiering for downstream B3.

## Top-10 NNLS-Abundant Cell Types

| Rank | Cell type | NNLS median fraction | Pearson r |
| --- | --- | ---: | ---: |
| 1 | pulmonary alveolar type 1 cell | 0.1568 | -0.178 |
| 2 | alveolar macrophage | 0.1387 | 0.110 |
| 3 | alveolar type 1 fibroblast cell | 0.1197 | -0.313 |
| 4 | lung pericyte | 0.0923 | -0.212 |
| 5 | alveolar adventitial fibroblast | 0.0876 | 0.005 |
| 6 | tracheobronchial goblet cell | 0.0810 | -0.591 |
| 7 | multiciliated epithelial cell | 0.0536 | -0.195 |
| 8 | pulmonary alveolar type 2 cell | 0.0337 | 0.039 |
| 9 | capillary endothelial cell | 0.0305 | 0.505 |
| 10 | lung macrophage | 0.0118 | 0.100 |

## Output Panel

- `nsclc130_consensus_v2.csv` shape: `130 x 5` including `sample_id`
- `cell_type_abundance.csv` rows: `4`

### Module composition used for collapse

- `epithelial`: NNLS[club cell, serous secreting cell, mucus secreting cell, pulmonary alveolar epithelial cell, acinar cell, pulmonary alveolar type 1 cell, pulmonary alveolar type 2 cell, brush cell of tracheobronchial tree, multiciliated columnar cell of tracheobronchial tree, nasal mucosa goblet cell, epithelial cell of lower respiratory tract, respiratory basal cell, ionocyte, multiciliated epithelial cell, tracheobronchial serous cell, tracheobronchial goblet cell, pulmonary neuroendocrine cell, bronchial goblet cell, respiratory tract hillock cell]; scaden[serous secreting cell, tracheobronchial goblet cell, respiratory tract hillock cell, club cell, epithelial cell of lower respiratory tract, pulmonary alveolar type 2 cell, multiciliated epithelial cell, bronchial goblet cell, multiciliated columnar cell of tracheobronchial tree, pulmonary alveolar epithelial cell, pulmonary alveolar type 1 cell, respiratory basal cell, tracheobronchial serous cell, nasal mucosa goblet cell, ionocyte]
- `immune`: NNLS[hematopoietic stem cell, T cell, mast cell, B cell, dendritic cell, alveolar macrophage, natural killer cell, CD4-positive, alpha-beta T cell, CD8-positive, alpha-beta T cell, plasmacytoid dendritic cell, plasma cell, classical monocyte, elicited macrophage, non-classical monocyte, conventional dendritic cell, CD1c-positive myeloid dendritic cell, lung macrophage]; scaden[lung macrophage, conventional dendritic cell, plasmacytoid dendritic cell, alveolar macrophage, non-classical monocyte, CD8-positive, alpha-beta T cell, natural killer cell, classical monocyte, B cell, elicited macrophage, CD4-positive, alpha-beta T cell, mast cell, plasma cell]
- `endothelial`: NNLS[endothelial cell of lymphatic vessel, capillary endothelial cell, vein endothelial cell, pulmonary artery endothelial cell]; scaden[capillary endothelial cell, endothelial cell of lymphatic vessel, vein endothelial cell, pulmonary artery endothelial cell]
- `stromal`: NNLS[fibroblast, mesothelial cell, myofibroblast cell, smooth muscle cell, stromal cell, lung pericyte, tracheobronchial smooth muscle cell, bronchus fibroblast of lung, alveolar type 1 fibroblast cell, alveolar adventitial fibroblast]; scaden[lung pericyte, tracheobronchial smooth muscle cell, bronchus fibroblast of lung, myofibroblast cell, alveolar type 1 fibroblast cell, alveolar adventitial fibroblast, smooth muscle cell]
