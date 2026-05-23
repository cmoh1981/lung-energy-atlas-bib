# Reporting Compliance Mapping

Companion to `manuscript/v2_BIB_JCR5_manuscript_draft.md`. Maps each item of STROBE [10] (for the observational case-study portion) and TRIPOD [11] (for the predictive-modeling portion) to the relevant section of the v2 manuscript. Items that are not applicable to a review-with-worked-case-study are explicitly marked `NA` with a brief rationale rather than left blank.

Both checklists were designed for primary research reports rather than for reviews with worked case studies. We adopt them in the spirit of full transparency: where an item applies to the LEMPA case study, we point to the relevant section; where the item is reframed by the review article type, we say so.

---

## STROBE checklist (cross-sectional / cohort framing of the LEMPA paired analysis)

The STROBE Statement [10] contains 22 items grouped by manuscript section.

### Title and abstract

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 1(a) | Indicate the study's design in title or abstract. | Addressed | Title and abstract identify the article as a "Review with worked case study" and label the case study as a "paired NSCLC radiogenomic" analysis. |
| 1(b) | Provide an informative and balanced summary in the abstract. | Addressed | Structured abstract (Motivation / Results / Conclusion / Availability) explicitly reports negative outcomes with quantitative anchors. |

### Introduction

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 2 | Explain the scientific background and rationale for the investigation. | Addressed | Section 1.1 (atlas resources) and 1.2 (radiogenomic context). |
| 3 | State specific objectives, including any prespecified hypotheses. | Addressed | Section 1.3 (contribution roadmap); preregistered H4 family detailed in Section 3.5. |

### Methods

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 4 | Present key elements of study design early in the paper. | Addressed | Section 2 (framework) and Section 3 (Methods). |
| 5 | Describe the setting, locations, and relevant dates. | Addressed | Section 3.3 (NSCLC-RG cohort, TCIA); cohort drawn from a single site (Stanford) as documented in Section 4.3. |
| 6(a) | Cohort study — eligibility criteria, sources, methods of selection. | Addressed | Section 3.3 (211 source imaging patients → 162 radiomics-processing → 130 paired analysis) and `results/paired/attrition.md`. |
| 6(b) | Cross-sectional — eligibility criteria, sources, methods of selection. | Addressed | Same as 6(a); the paired analysis is structured as a single cross-section. |
| 7 | Clearly define all outcomes, exposures, predictors, potential confounders, and effect modifiers. | Addressed | Section 3.5 (H4 family construction); Section 2.1 (formal notation); Section 3.2 (deconvolution targets). |
| 8 | Give sources of data and details of methods of assessment (measurement). | Addressed | Section 3.1 (atlas), 3.2 (deconvolution), 3.3 (radiomics), 3.4 (pathway scoring). |
| 9 | Describe any efforts to address potential sources of bias. | Addressed | Section 3.5 (FDR control), Section 3.6 (cross-validation), Section 4.4 (H4b leakage and join-integrity audit), Section 7.3 (limitations). |
| 10 | Explain how the study size was arrived at. | Addressed | Section 3.3 (paired N = 130 after inner join); Section 2 (gate criteria predeclared independent of size); Section 4.3 (G5 SKIPPED reflects insufficient stratification variance). |
| 11 | Explain how quantitative variables were handled in the analyses. | Addressed | Section 3.5 (Pearson/Spearman, partial correlations); Section 3.6 (CV procedure, ElasticNet/RandomForest defaults). |
| 12(a) | Describe all statistical methods, including those used to control for confounding. | Addressed | Section 3.5 (FDR), 3.6 (CV), supplement Section S3.5. |
| 12(b) | Describe any methods used to examine subgroups and interactions. | Addressed | Section 4.4 (H4b partial-adjustment by `CT_shape_MeshVolume`); no further subgroup analysis was undertaken to avoid post hoc flexibility. |
| 12(c) | Explain how missing data were addressed. | Addressed | Section 3.5 (per-test sample sizes); Section 4.4 (H4b n = 123 after routine missing-feature filtering from paired N = 130). |
| 12(d) | For cohort and cross-sectional studies — accounting for sampling strategy. | Addressed | Section 3.3 (inner join attrition documented from source 211 to paired 130). |
| 12(e) | Describe any sensitivity analyses. | Addressed | Section 4.2 (rare-cell sensitivity, `b3_sensitivity_abundance_restricted.md`); Section 4.4 (partial adjustment for technical covariate). |

### Results

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 13(a) | Numbers of individuals at each stage. | Addressed | Section 3.3 attrition narrative (211 → 162 → 130). |
| 13(b) | Reasons for non-participation. | Addressed | Section 3.3 (AMC imaging-only exclusions before V1 pairing). |
| 13(c) | Consider use of a flow diagram. | Addressed | A CONSORT-style attrition flow is referenced in `results/paired/attrition.md` and summarized in supplement S3.3. |
| 14(a) | Give characteristics of study participants. | Addressed | Section 4.4 Table-style descriptive technical-covariate context (mask source, age, scanner manufacturer). |
| 14(b) | Indicate number of participants with missing data for each variable of interest. | Addressed | Section 4.4 (n = 123 for H4b subset after missing-feature filtering). |
| 15 | Cohort study — report numbers of outcome events or summary measures over time. | NA | The LEMPA paired analysis is cross-sectional with respect to imaging and molecular features; no temporal outcome series is reported. |
| 16(a) | Give unadjusted estimates and, if applicable, confounder-adjusted estimates and their precision. | Addressed | Section 4.4 Table 7 reports both unadjusted and partial-adjusted (for `CT_shape_MeshVolume`) H4b effects with FDR. |
| 16(b) | Report category boundaries when continuous variables were categorized. | NA | No continuous variables were categorized for the H4 family. |
| 16(c) | If relevant, consider translating estimates of relative risk into absolute risk. | NA | LEMPA does not report risk estimates; the case study evaluates correlation-based prediction of cell-type fractions. |
| 17 | Report other analyses done (e.g., subgroups, interactions, sensitivity analyses). | Addressed | Sections 4.2 (sensitivity), 4.4 (partial adjustment), 5 (taxonomy synthesis). |

### Discussion

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 18 | Summarize key results with reference to study objectives. | Addressed | Section 8 (Conclusions) plus the structured abstract. |
| 19 | Discuss limitations. | Addressed | Section 7.3 (Limitations) — explicit limitations for atlas, deconvolution, pathway scoring, radiomics, cohort, and framework. |
| 20 | Give a cautious overall interpretation. | Addressed | Sections 7.1 (comparison to prior work) and 8 (Conclusions). |
| 21 | Discuss generalizability (external validity) of the study results. | Addressed | Sections 7.1, 7.3 (Limitations of cohort and framework generality), and 7.2 (reopening criteria). |

### Other information

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 22 | Give the source of funding and the role of the funders. | Pending | *Funding* section placeholder; author team to supply before submission. |

---

## TRIPOD checklist (predictive-modeling framing of gate G4 in the LEMPA case study)

The TRIPOD Statement [11] contains 22 main items. Items below are addressed at the level appropriate to the LEMPA cross-validated cell-type prediction (V1, gate G4) and the V2 module-level prediction (V2 gate G4).

### Title and abstract

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 1 | Identify as developing or validating a multivariable prediction model, target population, and outcome. | Addressed | Title and abstract make clear that the case study evaluates atlas-derived target prediction from radiomic features; abstract reports the negative outcome at each gate. |
| 2 | Provide a summary of objectives, study design, setting, participants, outcome, predictors, sample size, and statistical analysis methods. | Addressed | Structured abstract covers objective, design, setting, sample size (paired N = 130), endpoints, methods (NNLS / Scaden / PyRadiomics / ssGSEA), and outcome. |

### Background and objectives

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 3(a) | Explain the medical context and rationale for the prediction model. | Addressed | Section 1.1–1.2 (atlas-guided radiogenomics rationale and fragility). |
| 3(b) | Specify objectives, including whether developing or validating the model. | Addressed | Section 1.3: the case study is *internal validation* of an atlas-derived prediction problem; there is no external validation cohort. |

### Methods

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 4(a) | Describe the study design or source of data. | Addressed | Section 3.3; paired analysis on the NSCLC-Radiogenomics cohort [7] hosted on TCIA [19]. |
| 4(b) | Specify key study dates. | Pending | Original NSCLC-RG collection dates are documented in [7]; the LEMPA analysis dates are 2026-Q2 and will be confirmed before submission. |
| 5(a) | Specify key elements of the study setting. | Addressed | Section 3.3 (single-site cohort, Stanford = 130). |
| 5(b) | Describe eligibility criteria for participants. | Addressed | Section 3.3 (NSCLC-RG inclusion preserved; AMC imaging-only patients excluded at pairing). |
| 5(c) | Give details of treatments received, if relevant. | NA | The case study does not condition on treatment; molecular and imaging features are pretreatment. |
| 6(a) | Clearly define the outcome that is predicted by the model. | Addressed | Section 2.2 (gate G4 definition) and Section 4.2/4.3 (V1 cell-type and V2 module-level outcomes). |
| 6(b) | Report any actions to blind assessment of the outcome to be predicted. | NA | The outcome is computed mechanically from the frozen deconvolution table; no human adjudication step is involved. |
| 7(a) | Clearly define all predictors used in developing or validating the model. | Addressed | Section 3.3 (PyRadiomics feature set under IBSI-aware settings). |
| 7(b) | Report any actions to blind assessment of predictors for the outcome and other predictors. | NA | Predictors are mechanically extracted from imaging; no human adjudication. |
| 8 | Explain how the study size was arrived at. | Addressed | Section 3.3 (paired N = 130 from 211 source imaging cases); gate criteria predeclared independent of N. |
| 9 | Describe how missing data were handled. | Addressed | Section 3.5 (per-test sample sizes); Section 4.4 (H4b n = 123). |
| 10(a) | Describe how predictors were handled in the analyses. | Addressed | Section 3.6 (z-score standardization within training folds). |
| 10(b) | Specify type of model, all model-building procedures, and method for internal validation. | Addressed | Section 3.6 (ElasticNet / RandomForest defaults; 5-fold CV at patient level; deterministic seeds). |
| 10(c) | For validation, describe how the predictions were calculated. | Addressed | Section 3.6 (out-of-fold concatenation, Pearson r against frozen target). |
| 10(d) | Specify all measures used to assess model performance and, if relevant, to compare multiple models. | Addressed | Section 2.2 (gate G4 metric definition); Tables 4 and 6 (V1 and V2 outcomes). |
| 10(e) | Describe any model updating arising from the validation. | Addressed | V2 redesign (Section 4.3) is the model update arising from the V1 validation; the update was preregistered as a fallback rule. |
| 11 | Provide details on how risk groups were created. | NA | The case study does not create risk groups; outcomes are continuous fractions, not categorical. |
| 12 | Specify all assumptions made about missing data, predictors, and outcomes. | Addressed | Section 3.5 and supplement S3.3 (mask provenance), S3.4 (pathway scoring substitution), S3.6 (default hyperparameters). |

### Results

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 13(a) | Describe the flow of participants. | Addressed | Section 3.3 (211 → 162 → 130); `results/paired/attrition.md`. |
| 13(b) | Report the characteristics of the participants. | Addressed | Section 4.4 descriptive technical-covariate context. |
| 13(c) | For validation, show a comparison with the development data of the distribution of important variables. | NA | The case study is internal validation only; there is no separate development cohort. |
| 14(a) | Specify the number of participants and outcome events in each analysis. | Addressed | Section 4.2 (V1 n = 130 paired, 50 cell-type outcomes); Section 4.3 (V2 n = 130, 4 module outcomes); Section 4.4 (H4b n = 123). |
| 14(b) | If done, report the unadjusted association between each candidate predictor and outcome. | NA | The case study evaluates multivariable predictive models per target rather than reporting univariable associations per radiomic feature; doing so for ~196 features × 50 cell types would be uninformative and would risk false-positive narratives. |
| 15(a) | Present the full prediction model. | Addressed | Predictive model is ElasticNet or RandomForest with default hyperparameters; coefficients are not reported because no model reached the success rule and reporting them would risk overinterpretation. |
| 15(b) | Explain how to use the prediction model. | NA | No prediction model is being deployed. The LEMPA line is `CLOSED NEGATIVE` and is not for clinical use. |
| 16 | Report performance measures (with CIs) for the prediction model. | Addressed | Section 4.2 (V1 best r = 0.424); Section 4.3 (V2 module r values). Confidence intervals on per-target r are reported in `results/v2/b3_v2_cv_metrics.csv` in the executed evidence. |
| 17 | If done, report the results from any model updating. | Addressed | V2 results (Section 4.3) are the result of the V1→V2 model update; the update was preregistered, not data-driven post hoc. |

### Discussion

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 18 | Discuss any limitations of the study. | Addressed | Section 7.3. |
| 19(a) | For validation, discuss the results with reference to performance in the development data. | NA | No development cohort exists; the case study is internal validation only. |
| 19(b) | Give an overall interpretation of the results. | Addressed | Sections 7.1 (comparison) and 8 (Conclusions). |
| 20 | Discuss the potential clinical use of the model and implications for future research. | Addressed | Section 7.2 (reopening criteria); Section 6 (practitioner recommendations). The line is `CLOSED NEGATIVE` and is not proposed for clinical use. |

### Other information

| Item | Recommendation | Status | Manuscript location |
| --- | --- | --- | --- |
| 21 | Provide information about the availability of supplementary resources. | Addressed | *Data and Code Availability* section of main manuscript; supplements `METHODS_SUPPLEMENT.md`, `GLOSSARY.md`, and this file. |
| 22 | Give the source of funding and the role of the funders. | Pending | *Funding* section placeholder; author team to supply before submission. |

---

## Compliance summary

| Standard | Items addressed | Items NA (with rationale) | Items pending author-team supply |
| --- | ---: | ---: | ---: |
| STROBE (22 items) | 19 | 2 (items 15, 16(b), 16(c)) | 1 (item 22 funding) |
| TRIPOD (22 items) | 17 | 5 (items 5(c), 6(b), 7(b), 11, 13(c), 15(b), 19(a)) | 2 (items 4(b) dates, 22 funding) |

The pending items are author-team metadata that cannot be supplied by the manuscript draft itself.

---

## Note on the article type

STROBE and TRIPOD are designed for primary research reports. We adopt them here for the worked case-study portion of the manuscript because the LEMPA paired analysis is, in substance, observational and predictive. The review portion of the manuscript (Sections 1, 2, 5, 6, 7) is not covered by STROBE or TRIPOD by construction. We do not invoke PRISMA [not cited in this v2] because we are not conducting a systematic literature search; we are conducting a worked case study with a discursive framing review.

If a reviewer requests stricter adherence to a review-specific reporting standard, we will adopt the SANRA (Scale for the Assessment of Narrative Review Articles) framework at production stage.
