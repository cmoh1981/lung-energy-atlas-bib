# BIB Submission Checklist

Use this checklist to decide whether the *Briefings in Bioinformatics* package is ready to leave internal revision and move to editor-facing review. This checklist is submission-facing rather than analysis-facing: it assumes the LEMPA scientific state is frozen and asks whether the package now reads as a practitioner resource, case study, and validation-framework paper rather than as an under-supported original-research submission.

## 1. BIB article-type fit

- [ ] The manuscript is framed as a bioinformatics review, practical guide, or worked case study rather than a standard IMRAD original-research paper.
- [ ] The practitioner-resource value is explicit in the title, abstract, introduction, and conclusions.
- [ ] The general framework is primary and the LEMPA case study is presented as the evidence anchor rather than the sole novelty claim.
- [ ] No section rhetorically depends on successful radiogenomic validation.

## 2. Frozen-result integrity

- [ ] Frozen results under `results/v1/`, `results/v2/`, `results/deconvolution/`, `results/paired/`, and `results/post_v2_audit/` were treated as read-only.
- [ ] Source manuscript and OSF hypothesis files were not edited.
- [ ] V1 is consistently described as an honest negative baseline.
- [ ] V2 is consistently described as `METHOD-FRAGILE NEGATIVE`.
- [ ] H4a and H4c are reported as null.
- [ ] H4b, if mentioned, is always subordinate to the project-level negative outcome and labeled `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`.

## 3. Claim discipline and overclaim control

- [ ] The abstract does not imply successful validation, clinical readiness, or robust imaging-to-cell-state prediction.
- [ ] The manuscript does not imply external replication.
- [ ] The manuscript does not visually or rhetorically center H4b.
- [ ] Negative benchmark value is explicitly treated as a contribution.
- [ ] Phase C is described as dormant unless trigger criteria are met.

## 4. BIB-useful figures and tables

- [ ] Main figures teach a general validation framework or failure-mode logic that remains useful beyond LEMPA.
- [ ] Main tables include data-layer requirements, validation gates, case-study outcomes, and reporting guidance.
- [ ] Each figure and table has a caption that states the practitioner lesson, not only the local result.
- [ ] Figure/table inputs are traceable to frozen artifacts.
- [ ] H4b, if shown, is displayed with caveat-forward captioning and without rescue framing.

## 5. Methods transparency for submission

- [ ] Eligibility, participant flow, and cohort attrition are summarized in a submission-ready form.
- [ ] Variables, targets, predictors, and fallback target-collapse rules are defined in one place.
- [ ] Deconvolution methods, pathway scoring choices, and method-dependence risks are reported explicitly.
- [ ] Missing-data handling, preprocessing, and model workflow are described clearly enough for editor review.
- [ ] The manuscript distinguishes preregistered analyses, fallback analyses, and post-V2 audit work.

## 6. Reporting-framework coverage

- [ ] Observational-study reporting is aligned with the STROBE mapping.
- [ ] Predictive-model transparency limitations are aligned with the TRIPOD mapping.
- [ ] The paper does not overstate TRIPOD completeness where the predictive line remains a negative stress test.
- [ ] Submission metadata sections required by the target journal are complete or explicitly blocked.

## 7. Bibliography and metadata lock

- [ ] Core references for atlases, radiogenomics, deconvolution, pathway scoring, radiomics, and reporting standards are identified.
- [ ] References used in the manuscript have been verified and formatted for submission.
- [ ] No placeholder or unverified citation is presented as final.
- [ ] Author contributions, funding, conflicts, ethics wording, and data/code availability statements are ready.

## 8. Reproducibility package readiness

- [ ] A submission-facing reproducibility manifest maps claims to artifacts.
- [ ] Figure/table provenance is explicit.
- [ ] Data-accession and code-archive identifiers are available or clearly listed as blockers.
- [ ] Software environment details and rerun assumptions are documented.
- [ ] The package tells a reader what can be rerun directly and what is intentionally frozen.

## 9. Final release gate

- [ ] The package reads as BIB-fit rather than as a mispositioned original-research manuscript.
- [ ] The strongest scientific value is the validation framework plus honest negative case study.
- [ ] All remaining blockers are editorial, metadata, or reproducibility gaps rather than unresolved scientific ambiguity.
- [ ] If any box above remains unchecked, the package should stay `NEEDS_TARGETED_REVISION` rather than move forward as submission-ready.
