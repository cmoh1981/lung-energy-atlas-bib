# Scaden Scale-Up Smoke Test

- Status: PASS
- Gate: V2-G1
- Runtime seconds: 190.96
- Python: `C:\Users\ohbry\lempa_env\Scripts\python.exe`
- Atlas: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\data\atlases\hca_lung_atlas_core.h5ad`
- Bulk RNA: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\data\tcia\nsclc_radiogenomics\nsclc_radiogenomics_rnaseq.txt.gz`

## Training Settings

- top_labels: 50
- max_cells_per_label: 200
- max_genes: 2000
- n_samples: 600
- cells_per_sample: 250
- batch_size: 128
- steps_per_model: 100
- ensemble_models: m256,m512,m1024
- label_column: ann_finest_level
- donor_column: donor_id
- gene_column: feature_name

## Reference Reduction

- Retained the top 50 HCA `ann_finest_level` labels by cell count out of 61 total labels.
- Capped each retained label at 200 donor-balanced cells, reducing the reference to 10000 cells total.
- Restricted genes to the top 2000 overlapping `feature_name` symbols ranked by V1 bulk variance from 15557 total overlaps.
- Training uses 600 simulated bulks, 250 cells per simulated bulk, and 100 optimizer steps per ensemble member.

## Reference Summary

- atlas_total_cells: 584944
- atlas_total_genes: 27402
- atlas_total_labels: 61
- selected_labels: 50
- selected_label_names: ['Alveolar macrophages', 'AT2', 'Suprabasal', 'Basal resting', 'Goblet (nasal)', 'Multiciliated (non-nasal)', 'CD8 T cells', 'Monocyte-derived Mph', 'Club (nasal)', 'CD4 T cells', 'Classical monocytes', 'NK cells', 'EC general capillary', 'Adventitial fibroblasts', 'Club (non-nasal)', 'DC2', 'Non-classical monocytes', 'Alveolar Mph CCL3+', 'AT1', 'EC arterial', 'EC aerocyte capillary', 'Mast cells', 'EC venous systemic', 'EC venous pulmonary', 'Alveolar fibroblasts', 'Multiciliated (nasal)', 'Interstitial Mph perivascular', 'Hillock-like', 'B cells', 'pre-TB secretory', 'Lymphatic EC mature', 'Pericytes', 'Smooth muscle', 'Plasma cells', 'Goblet (bronchial)', 'Peribronchial fibroblasts', 'SMG serous (nasal)', 'AT0', 'SMG serous (bronchial)', 'SMG duct', 'Alveolar Mph MT-positive', 'Alveolar Mph proliferating', 'Deuterosomal', 'AT2 proliferating', 'Goblet (subsegmental)', 'Myofibroblasts', 'Lymphatic EC differentiating', 'Ionocyte', 'SM activated stress response', 'Plasmacytoid DCs']
- selected_cells: 10000
- selected_genes: 2000
- overlap_genes_total: 15557
- cells_per_label: {'Alveolar macrophages': 200, 'AT2': 200, 'Suprabasal': 200, 'Basal resting': 200, 'Goblet (nasal)': 200, 'Multiciliated (non-nasal)': 200, 'CD8 T cells': 200, 'Monocyte-derived Mph': 200, 'Club (nasal)': 200, 'CD4 T cells': 200, 'Classical monocytes': 200, 'NK cells': 200, 'EC general capillary': 200, 'Adventitial fibroblasts': 200, 'Club (non-nasal)': 200, 'DC2': 200, 'Non-classical monocytes': 200, 'Alveolar Mph CCL3+': 200, 'AT1': 200, 'EC arterial': 200, 'EC aerocyte capillary': 200, 'Mast cells': 200, 'EC venous systemic': 200, 'EC venous pulmonary': 200, 'Alveolar fibroblasts': 200, 'Multiciliated (nasal)': 200, 'Interstitial Mph perivascular': 200, 'Hillock-like': 200, 'B cells': 200, 'pre-TB secretory': 200, 'Lymphatic EC mature': 200, 'Pericytes': 200, 'Smooth muscle': 200, 'Plasma cells': 200, 'Goblet (bronchial)': 200, 'Peribronchial fibroblasts': 200, 'SMG serous (nasal)': 200, 'AT0': 200, 'SMG serous (bronchial)': 200, 'SMG duct': 200, 'Alveolar Mph MT-positive': 200, 'Alveolar Mph proliferating': 200, 'Deuterosomal': 200, 'AT2 proliferating': 200, 'Goblet (subsegmental)': 200, 'Myofibroblasts': 200, 'Lymphatic EC differentiating': 200, 'Ionocyte': 200, 'SM activated stress response': 200, 'Plasmacytoid DCs': 200}
- donors_per_label: {'Alveolar macrophages': 84, 'AT2': 73, 'Suprabasal': 77, 'Basal resting': 77, 'Goblet (nasal)': 75, 'Multiciliated (non-nasal)': 102, 'CD8 T cells': 86, 'Monocyte-derived Mph': 88, 'Club (nasal)': 54, 'CD4 T cells': 88, 'Classical monocytes': 87, 'NK cells': 74, 'EC general capillary': 69, 'Adventitial fibroblasts': 73, 'Club (non-nasal)': 73, 'DC2': 91, 'Non-classical monocytes': 83, 'Alveolar Mph CCL3+': 60, 'AT1': 65, 'EC arterial': 77, 'EC aerocyte capillary': 47, 'Mast cells': 81, 'EC venous systemic': 75, 'EC venous pulmonary': 71, 'Alveolar fibroblasts': 64, 'Multiciliated (nasal)': 37, 'Interstitial Mph perivascular': 78, 'Hillock-like': 38, 'B cells': 77, 'pre-TB secretory': 88, 'Lymphatic EC mature': 69, 'Pericytes': 38, 'Smooth muscle': 74, 'Plasma cells': 70, 'Goblet (bronchial)': 54, 'Peribronchial fibroblasts': 59, 'SMG serous (nasal)': 9, 'AT0': 57, 'SMG serous (bronchial)': 21, 'SMG duct': 43, 'Alveolar Mph MT-positive': 36, 'Alveolar Mph proliferating': 48, 'Deuterosomal': 70, 'AT2 proliferating': 49, 'Goblet (subsegmental)': 32, 'Myofibroblasts': 41, 'Lymphatic EC differentiating': 36, 'Ionocyte': 50, 'SM activated stress response': 21, 'Plasmacytoid DCs': 44}
- label_count_threshold_at_top_n: 552

## Output

- Predictions written: True
- Prediction matrix shape: [130, 50]
- Prediction file: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_predictions.csv`
- Report file: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke.md`

## Gate Checks

- no_nan: PASS
- no_all_zero_rows: PASS
- per_cell_type_variance_gt_zero: PASS
- sample_to_sample_variation_present: PASS
- row_sum_min: 0.9999997019767761
- row_sum_max: 1.0000003576278687
- variance_min: 4.6583551238654763e-08
- variance_max: 1.0817416296049487e-05
- stddev_min: 0.00021583223133347929
- stddev_max: 0.003288984065875411

## Work Files

- counts: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\training\hca_scaleup_counts.txt`
- celltypes: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\training\hca_scaleup_celltypes.txt`
- cell_types_list: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\training\cell_types.txt`
- bulk_predict: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\training\bulk_data.txt`
- simulated_h5ad: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\simulated\hca_scaleup.h5ad`
- simulated_bulk_data: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\simulated\bulk_data.txt`
- simulated_cell_fractions: `C:\Users\ohbry\OneDrive\Apps\lung-energy-atlas\writing_outputs\20260516_lung-energy-pathway-mapping\results\v2\scaden_scale_up_smoke_work\simulated\cell_fractions.txt`
