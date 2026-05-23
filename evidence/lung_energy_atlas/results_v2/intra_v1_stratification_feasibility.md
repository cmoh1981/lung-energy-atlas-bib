# Task SF: Intra-V1 Stratification Feasibility

## Scope

This note executes only Task SF from `OPENCODE_NEXT_PROMPT_v5.md` using frozen V1 artifacts and local metadata only. No V1 artifacts were modified.

## Inputs Used

- Paired N=130 table: `results/paired/nsclc_paired_radiomics_deconvolution.csv`
- Pairing attrition log: `results/paired/attrition.md`
- QC radiomics table: `results/radiomics/nsclc211_features_qc.csv`
- TCIA series metadata: `data/tcia/nsclc_radiogenomics/series.csv`
- TCIA patient table: `data/tcia/nsclc_radiogenomics/patients.csv`
- Local RNA matrix: `data/tcia/nsclc_radiogenomics/nsclc_radiogenomics_rnaseq.txt.gz`

## Cohort Anchor

- `results/paired/attrition.md` reports `Paired patients after inner join: 130`.
- All counts below are for that paired N=130 cohort.

## 1. Imaging-site / scanner-model inventory

### Imaging site counts

Site labels were read from the frozen paired table (`CT_Site`, `PT_Site`) and verified against `series.csv` for the referenced `CT_SeriesInstanceUID` and `PT_SeriesInstanceUID` in the paired cohort.

| Stratum | Count |
|---|---:|
| CT site = Stanford | 130 |
| PT site = Stanford | 130 |
| CT/PT site combination = Stanford / Stanford | 130 |

Evidence for site collapse:
- `series.csv` verification found `missing_ct_series = 0` and `missing_pt_series = 0` for the paired cohort.
- After verification, CT site labels remained a single value: `Stanford`.
- After verification, PT site labels remained a single value: `Stanford`.

### Scanner model counts

Counts below use the paired cohort columns `CT_ManufacturerModelName` and `PT_ManufacturerModelName`. Blank strings are retained as missing metadata, not imputed.

#### CT scanner model

| CT manufacturer model | Count |
|---|---:|
| Discovery CT750 HD | 62 |
| <missing> | 57 |
| LightSpeed VCT | 5 |
| Discovery 690 | 2 |
| Discovery STE | 2 |
| LightSpeed16 | 2 |

#### PT scanner model

| PT manufacturer model | Count |
|---|---:|
| Discovery STE | 62 |
| <missing> | 57 |
| Discovery 690 | 11 |

#### Paired CT/PT scanner combination

| CT/PT scanner combination | Count |
|---|---:|
| CT=<missing>; PT=<missing> | 57 |
| CT=Discovery CT750 HD; PT=Discovery STE | 56 |
| CT=Discovery CT750 HD; PT=Discovery 690 | 6 |
| CT=LightSpeed VCT; PT=Discovery 690 | 3 |
| CT=Discovery STE; PT=Discovery STE | 2 |
| CT=Discovery 690; PT=Discovery 690 | 2 |
| CT=LightSpeed16; PT=Discovery STE | 2 |
| CT=LightSpeed VCT; PT=Discovery STE | 2 |

## 2. RNA-seq batch label inventory

### Local search result

No separate local GSE103584 sample-metadata or batch-metadata file was found in this workspace.

Evidence:
- Workspace search for `*GSE103584*` returned no metadata file.
- Workspace content search for `batch`, `submitter`, and `processing date` found planning/spec text only, not a local machine-readable sample metadata table for the paired cohort.
- `data/tcia/nsclc_radiogenomics/` contains `nsclc_radiogenomics_rnaseq.txt.gz`, but directory inspection showed no accompanying batch/sample-annotation file.
- Inspection of the gzip contents showed a patient-ID header and gene-expression rows, consistent with an expression matrix rather than a metadata table.

### Available local batch labels

None found locally.

### Batch counts

Not computable from local frozen artifacts.

## 3. Histology subtype label inventory

### Local search result

No machine-readable structured histology label file was found locally for the paired N=130 cohort.

Evidence:
- `patients.csv` contains only `PatientId`, `PatientName`, `PatientSex`, `Collection`, `Phantom`, `SpeciesCode`, `SpeciesDescription`, and `Authorized`.
- `series.csv` contains imaging-series metadata only; no histology field is present.
- The frozen paired table and QC radiomics table do not contain histology columns.
- Workspace grep found histology terms only in planning/proposal prose, not in a structured cohort metadata table usable for stratification.

### Available histology labels

None found locally in machine-readable structured form.

### Histology counts

Not computable from local frozen artifacts.

## 4. Feasibility evaluation

### Pre-specified rules

- Leave-one-imaging-site-out is feasible iff at least 3 sites have at least 20 patients each.
- Leave-one-RNA-batch-out is feasible iff at least 3 batches have at least 20 patients each.
- Histology-split is feasible iff LUAD >= 30 and non-LUAD >= 30.

### Verdicts

| Design | Required rule | Observed local evidence | Verdict |
|---|---|---|---|
| Leave-one-imaging-site-out | >= 3 sites with >= 20 patients each | Only 1 site (`Stanford`) across all 130 paired patients | Not feasible |
| Leave-one-RNA-batch-out | >= 3 batches with >= 20 patients each | No local batch labels found; batch counts not computable | Not feasible |
| Histology-split | LUAD >= 30 and non-LUAD >= 30 | No local structured histology labels found; LUAD/non-LUAD counts not computable | Not feasible |

## 5. Recommended B3-v2 design choice

All three stratified intra-V1 designs are unavailable from the local frozen artifacts used for Task SF.

Recommended fallback for B3-v2:
- Omit V2-G5 stratified intra-V1 cross-source design.
- Proceed with pooled patient-level 5-fold CV only.
- Document the omission as a Constraint 4 fallback caused by local label unavailability / single-site collapse, not as a silent substitution.

## Bottom line

- Imaging-site stratification fails because the paired N=130 cohort collapses to a single verified site (`Stanford`).
- RNA-batch stratification fails because no local batch metadata file or usable batch labels were found.
- Histology stratification fails because no local machine-readable histology labels were found.
- Therefore, pooled 5-fold CV only is the honest SF recommendation.
