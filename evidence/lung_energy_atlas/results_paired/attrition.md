# B2 Attrition Report

Generated for `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\paired\nsclc_paired_radiomics_deconvolution.csv`.

## Inputs

- Radiomics: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\radiomics\nsclc211_features_qc.csv`
- Deconvolution consensus: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\deconvolution\nsclc130_consensus.csv`

## Counts

- Radiomics rows loaded: 162
- Deconvolution rows loaded: 130
- Radiomics duplicate-patient exclusions: 0
- Deconvolution duplicate-patient exclusions: 0
- Radiomics unique patients after exclusions: 162
- Deconvolution unique patients after exclusions: 130
- Paired patients after inner join: 130
- Radiomics-only patients excluded from pair set: 32
- Deconvolution-only patients excluded from pair set: 0

## Exclusion Rules

- Patient IDs were normalized by trimming whitespace only.
- Duplicate patient IDs in either source were excluded entirely to preserve patient-level uniqueness.
- Final pairing used an inner join on `PatientID`.

## Duplicate Patient IDs

- Radiomics duplicates: None
- Deconvolution duplicates: None

## Unpaired Patients

- Radiomics-only: R01-001, R01-002, R01-008, R01-009, R01-010, R01-011, R01-019, R01-020, R01-025, R01-030, R01-036, R01-044, R01-045, R01-047, R01-050, R01-053, R01-058, R01-070, R01-074, R01-075, R01-082, R01-085, R01-086, R01-087, R01-088, R01-090, R01-092, R01-095, R01-143, R01-161, R01-162, R01-163
- Deconvolution-only: None
