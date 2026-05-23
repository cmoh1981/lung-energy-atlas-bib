# H4b Audit

## Verdict

`H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`

## Scope

Task B only. Frozen inputs were inspected read-only and new outputs were written only under `results/post_v2_audit/`.

## Key Findings

1. Target construction: heterogeneity_variance is reproduced as the sample variance across the four collapsed consensus module fractions (epithelial, immune, endothelial, stromal) and does not use radiomic columns in its construction.
2. Predictor independence: `CT_firstorder_Entropy`, `CT_glcm_Contrast`, and `CT_glcm_Idm` are joined predictors only; they are not components of the target calculation.
3. Join integrity: each frozen source table is one row per patient, the inner join remains `130` unique patients with no duplicate expansion, and the H4b analysis subset is `123` after ordinary missing-feature filtering.
4. Sign coherence: entropy is negative, contrast is negative, and homogeneity is positive against `heterogeneity_variance` in both the frozen and recomputed outputs.
5. Fallback dependence: The target definition is fully dependent on the V2 module-collapse fallback because it is computed from the four collapsed modules in `results/v2/nsclc130_consensus_v2.csv`, not from the original higher-resolution V1 cell-type weighted-capacity target.
6. Technical-covariate context: `CT_shape_MeshVolume` remains the strongest obvious available technical correlate descriptively, but the frozen partial-correlation adjustment leaves the H4b directions and significance intact; site and vendor fields are too low-variability to add a stronger descriptive concern here.

## Recomputation

Recomputed H4 family statistics used the frozen V2 consensus, frozen QC radiomics, frozen V1 pathway-score file, the inherited Pearson/Spearman definitions, linear-residual partial correlations against `CT_shape_MeshVolume`, and BH FDR over the 5-test H4 family.

| hypothesis_id | n_recomputed | effect_recomputed | p_raw_recomputed | bh_fdr_recomputed | partial_effect_recomputed | partial_p_recomputed | partial_bh_fdr_recomputed | all_fields_match |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| H4b_entropy | 123 | -0.390791773551042 | 7.86334270589371e-06 | 3.93167135294686e-05 | -0.397486166823593 | 5.3053870837622e-06 | 2.6526935418811e-05 | YES |
| H4b_contrast | 123 | -0.340623125866356 | 0.000115701492742331 | 0.000192835821237218 | -0.349905199210638 | 7.27297685245879e-05 | 0.000121216280874313 | YES |
| H4b_homogeneity | 123 | 0.37084427036442 | 2.41671713202386e-05 | 6.04179283005966e-05 | 0.372857308689427 | 2.16497009942412e-05 | 5.4124252485603e-05 | YES |

## V1 vs V2 Target Context

The frozen V1 H4b table used `metabolic_heterogeneity_variance` from the original cell-type weighted-capacity construction. V2 instead matches a variance over the collapsed four-module consensus fractions. This target redefinition materially strengthens the observed H4b associations and should be called out explicitly anywhere H4b is propagated.

| hypothesis_id | V1_effect | V1_p_raw | V1_partial_effect | V1_partial_p | V2_frozen_effect | V2_frozen_p_raw | V2_frozen_partial_effect | V2_frozen_partial_p |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| H4b_entropy | -0.175625737723277 | 0.0520129974614737 | -0.206111103945518 | 0.0221865831082494 | -0.390791773551042 | 7.86334270589371e-06 | -0.397486166823593 | 5.3053870837622e-06 |
| H4b_contrast | -0.0672139923087541 | 0.460111131388652 | -0.0832054275064168 | 0.360213391995218 | -0.340623125866356 | 0.0001157014927423 | -0.349905199210638 | 7.27297685245879e-05 |
| H4b_homogeneity | 0.0887738058079064 | 0.328853447726146 | 0.121544930414931 | 0.180503708659012 | 0.37084427036442 | 2.41671713202386e-05 | 0.372857308689427 | 2.16497009942412e-05 |

## Descriptive Technical-Covariate Context

| covariate | type | n | association_with_target | p_two_sided | unique_levels | note |
| --- | --- | ---: | ---: | ---: | ---: | --- |
| CT_shape_MeshVolume | numeric | 123 | -0.0667861887503063 | 0.462978081288369 | 123 | descriptive only |
| CT_PatientAge_num | numeric | 129 | -0.081530480075401 | 0.358343884363573 | 36 | descriptive only |
| CT_ImageCount | numeric | 130 | 0.078830382732879 | 0.3726544454228 | 94 | descriptive only |
| CT_Site | categorical | 130 |  |  | 1 | Stanford=130 |
| CT_Manufacturer | categorical | 125 |  |  | 4 | GE MEDICAL SYSTEMS=107; SIEMENS=14; Philips=3; TOSHIBA=1 |
| CT_ManufacturerModelName | categorical | 73 |  |  | 5 | Discovery CT750 HD=62; LightSpeed VCT=5; LightSpeed16=2; Discovery STE=2; Discovery 690=2 |
| CT_mask_source | categorical | 129 |  |  | 2 | SEG=117; fallback_body_outline=12 |

## Strongest Reason For Verdict

The signal is exactly reproducible, but it is tied to a module-collapse-derived target definition rather than an independent, unchanged heterogeneity endpoint.

## Acceptance Check

- Recomputation matched frozen V2 H4b values: yes.
- Required frozen-table join/QC checks completed.
- No protected or frozen V1/V2 artifacts were modified.
