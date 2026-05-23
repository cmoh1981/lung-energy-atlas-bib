# Practitioner Checklist for Atlas-Guided Radiogenomics

This checklist is designed for use as a boxed item or supplementary checklist in a practitioner-focused *Briefings in Bioinformatics* article. It is intended for studies that translate cell-atlas-derived programs or cell states into patient-level imaging, radiomics, or radiogenomic endpoints.

## 1. Pre-analysis data readiness

- [ ] Confirm that the atlas, bulk transcriptomic, imaging, segmentation, and metadata layers all exist before model building starts.
- [ ] Record analytic sample counts separately for source cohort, QC-passing imaging cohort, and final paired cohort.
- [ ] Freeze the analysis-ready cohort and feature inventory before testing downstream associations.
- [ ] Define in advance which failures should halt interpretation rather than trigger unplanned rescue analyses.

## 2. Cell atlas and gene-set compatibility

- [ ] Verify that atlas cell identities, tissue context, and donor composition are appropriate for the disease setting being modeled.
- [ ] Check that gene sets or pathway programs are biologically interpretable at the atlas resolution actually available.
- [ ] Flag when developmental, rare, or low-abundance states are being projected into adult or sparsely represented patient cohorts.
- [ ] Separate atlas-resource claims from patient-level validation claims.

## 3. Deconvolution method agreement

- [ ] Run more than one deconvolution strategy when cell-type-level inference is central to the study claim.
- [ ] Predefine an agreement threshold for treating a cell state as interpretable across methods.
- [ ] Report disagreement as a primary result, not as a technical footnote.
- [ ] Do not treat downstream correlations as robust if upstream cell-fraction estimates disagree materially.

## 4. Target abundance and endpoint selection

- [ ] Check whether the proposed cell-state or pathway target is abundant enough to support patient-level inference.
- [ ] Avoid rare targets as primary imaging endpoints unless there is a prespecified justification and adequate support surface.
- [ ] State clearly when endpoint collapse from cell type to broader module is triggered.
- [ ] Interpret any post-collapse association as answering a different biological question than the original cell-type target.

## 5. Imaging feature QC

- [ ] Document image inclusion rules, segmentation provenance, and radiomics QC filters.
- [ ] Record how many cases were lost to unreadable images, missing masks, feature extraction failure, or harmonization problems.
- [ ] Avoid presenting weak transcriptomic targets as validated if imaging reproducibility is not established first.
- [ ] Keep feature preprocessing, filtering, and transformation rules fixed and auditable.

## 6. Cohort attrition and linkage

- [ ] Show source N, QC-passing N, paired N, and analysis-specific N for every major endpoint.
- [ ] Describe the exact linkage rules used to join imaging, transcriptomic, and clinical records.
- [ ] Audit duplicate patients, unmatched samples, and subset drift after each filtering step.
- [ ] Treat severe attrition or unstable linkage as an interpretation limit, not just a methods note.

## 7. Cross-source or external validation

- [ ] Decide before analysis what would count as acceptable internal stratified validation, cross-source validation, or external replication.
- [ ] Report when site, batch, histology, or external cohort structure is too sparse to support the intended validation gate.
- [ ] Do not replace absent external validation with rhetorical claims of translational promise.
- [ ] Archive the line as incomplete or method-fragile when no credible robustness surface exists.

## 8. Reporting negative and method-fragile results

- [ ] Report negative primary outcomes directly and early.
- [ ] Distinguish null results, underpowered negatives, and method-fragile negatives.
- [ ] Keep residual positive-looking findings subordinate when they depend on fallback targets, subset shifts, or post hoc reinterpretation.
- [ ] Explain what failed, why it matters, and what future studies should avoid repeating.

## 9. Reproducibility artifacts

- [ ] Provide a claim-to-artifact map linking conclusions to frozen outputs.
- [ ] List data sources, code locations, environment details, and run-order assumptions.
- [ ] State which artifacts are frozen and should be inspected rather than regenerated.
- [ ] Include enough provenance that a reviewer can audit the negative result as easily as a positive one.

## Minimum interpretation rule

- [ ] If atlas compatibility is weak, deconvolution agreement fails, the target is too rare, attrition is severe, or no robustness surface exists, report the study as negative, unstable, or method-fragile rather than validated.
