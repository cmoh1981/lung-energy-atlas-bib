# BIB Manuscript Outline

Article type anchor: **Review with worked case study**.

Frozen evidence anchor: V1 honest negative baseline; V2 `METHOD-FRAGILE NEGATIVE`; H4a and H4c null; H4b retained only as `H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS`; no external replication; Phase C deferred pending trigger criteria.

## 1. Abstract

- purpose: State the practitioner-facing problem, define the review-with-case-study format, summarize the frozen LEMPA evidence state, and foreground the validation-gate contribution rather than any success claim.
- evidence inputs:
  - `finalization/briefings_bioinformatics_package/BIB_fit_memo.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/post_v2_audit/h4b_audit.md`
- key messages:
  - Cell atlases are biologically informative starting resources but do not by themselves validate patient-level radiogenomic prediction.
  - Atlas-guided radiogenomics requires explicit upstream and downstream validation gates before any translational claim is defensible.
  - LEMPA is best presented as a worked example of a plausible bridge that remained negative under frozen public-data constraints.
  - Deconvolution disagreement, target collapse, and limited paired-cohort surfaces can convert a biologically credible question into a method-fragile negative result.
  - Negative benchmark outcomes are still useful when they are transparently archived and converted into reusable reporting discipline.
- overclaim risks:
  - Implying successful radiogenomic validation in the opening sentence.
  - Presenting H4b as the abstract's dominant empirical takeaway.
  - Framing the article as an original NSCLC biomarker paper instead of a bioinformatics resource.
- figure/table links:
  - Planned main text: Figure 1 validation framework; Figure 2 LEMPA atlas case; Table 2 validation gates.

## 2. Key points

- purpose: Provide a BIB-style scan-friendly set of takeaways that generalize beyond the LEMPA case.
- evidence inputs:
  - `finalization/briefings_bioinformatics_package/BIB_fit_memo.md`
  - `finalization/jcr5_package/final_quality_gate.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
- key messages:
  - Atlas-guided radiogenomics should be treated as a multi-gate validation problem, not a one-step discovery workflow.
  - Deconvolution agreement is a prerequisite, not a cosmetic sensitivity analysis.
  - Rare or diluted targets are weak imaging endpoints even when their biology is compelling.
  - Public paired cohorts often fail at reproducibility, attrition, or cross-source robustness before biology can be fairly tested.
  - Honest negative closure can be more useful than rhetorical rescue.
- overclaim risks:
  - Overloading the key points with study-specific numbers instead of portable principles.
  - Including any bullet that sounds clinically actionable.
- figure/table links:
  - Planned main text: Figure 1; Table 1 data layers; Table 2 validation gates.

## 3. Introduction: why atlas-guided radiogenomics needs validation discipline

- purpose: Define the field-level problem and explain why biologically plausible atlas-to-imaging bridges often fail without structured validation discipline.
- evidence inputs:
  - `finalization/briefings_bioinformatics_package/BIB_fit_memo.md`
  - `finalization/jcr5_package/final_quality_gate.md`
  - `finalization/briefings_bioinformatics_package/BIB_bibliography_lock_plan.md`
- key messages:
  - Single-cell and spatial atlas resources have expanded the biological resolution available for organ-specific hypothesis generation.
  - Translating atlas-derived cell-state hypotheses into patient-linked imaging models introduces new failure surfaces absent from atlas-only studies.
  - BIB fit depends on explaining those failure surfaces as a practitioner problem rather than narrating a single study's disappointment.
  - A gate-based framework is needed to distinguish plausible biological bridges from validated predictive bridges.
- overclaim risks:
  - Treating atlas availability as evidence of downstream predictability.
  - Sounding like the paper will solve radiogenomics broadly rather than discipline its claims.
- figure/table links:
  - Planned main text: Figure 1.
  - Planned support: Table 1 data layers.

## 4. Lung energy metabolism as a motivating case

- purpose: Introduce why lung energy metabolism is a suitable motivating substrate for a worked example without overselling the atlas layer as a clinical endpoint.
- evidence inputs:
  - `figures/fig1_pathway_capacity_heatmap.png`
  - `figures/fig2b_lifespan_correlation_heatmap.png`
  - `finalization/jcr5_package/figure_plan.md`
  - `finalization/briefings_bioinformatics_package/BIB_bibliography_lock_plan.md`
- key messages:
  - Lung energy metabolism is distributed across epithelial, immune, endothelial, and stromal populations rather than concentrated in one lineage.
  - This heterogeneity makes the lung a strong atlas-building use case and a hard radiogenomic translation use case.
  - The atlas branch remains scientifically informative even when the paired validation branch fails.
  - The motivating case works because it separates biological plausibility from predictive success.
- overclaim risks:
  - Overstating developmental or lifespan conclusions from adult-skewed atlas data.
  - Collapsing atlas informativeness into an implied imaging biomarker claim.
- figure/table links:
  - Existing asset: `figures/fig1_pathway_capacity_heatmap.png`.
  - Existing secondary asset: `figures/fig2b_lifespan_correlation_heatmap.png`.
  - Planned main text: Figure 2 LEMPA atlas case.

## 5. Data layers required for atlas-guided radiogenomics

- purpose: Map the data stack practitioners actually need before attempting atlas-guided radiogenomic validation.
- evidence inputs:
  - `results/paired/attrition.md`
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `finalization/jcr5_package/checklists/TRIPOD_transparency_mapping.md`
  - `finalization/jcr5_package/checklists/reproducibility_package.md`
- key messages:
  - The minimum stack includes atlas annotations, bulk RNA-seq or matched omics, deconvolution outputs, imaging features, masks, patient linkage metadata, and technical covariates.
  - Attrition and join integrity are first-order scientific concerns because they define the actual validation surface.
  - Reporting should distinguish source cohort size, processed imaging size, paired size, and analysis-subset size.
  - Missing or low-variability technical covariates can block robustness checks even when the main data layers exist.
- overclaim risks:
  - Reporting nominal cohort sizes instead of executed paired and analyzable counts.
  - Treating partially linked public data as equivalent to a replication-ready cohort.
- figure/table links:
  - Planned main text: Table 1 data layers for atlas-guided radiogenomics.
  - Planned support: Table 2 validation gates.

## 6. Deconvolution as the first failure point

- purpose: Establish that target definition stability begins with deconvolution agreement, making it the first gate rather than a downstream footnote.
- evidence inputs:
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `finalization/jcr5_package/figure_plan.md`
  - `finalization/briefings_bioinformatics_package/BIB_bibliography_lock_plan.md`
- key messages:
  - V2 executed successfully but failed at the intended cell-type agreement surface before predictive modeling could be fairly interpreted.
  - The critical empirical signature was top-10 agreement median `-0.087` with only `1/10` abundant cell types at `r >= 0.4`.
  - When independent methods disagree at target level, any downstream modeling claim inherits that instability.
  - A failed agreement gate should force either collapse, deferral, or archive, not optimistic interpretation.
- overclaim risks:
  - Treating executability as biological validation.
  - Describing module collapse as a refinement instead of a failure-triggered fallback.
- figure/table links:
  - Planned main text: Figure 3 V1/V2 gate results; Figure 4 method fragility and module collapse.
  - Planned support: Table 2 validation gates.

## 7. Target rarity and abundance dilution

- purpose: Explain why low-abundance or diluted atlas targets can fail as imaging endpoints even when they are biologically interesting.
- evidence inputs:
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `finalization/jcr5_package/final_quality_gate.md`
- key messages:
  - V1's pre-registered cell-type endpoint failed, with only `3/50` cell types reaching `r >= 0.30` against a required count of 10.
  - Rare targets are vulnerable to abundance dilution, deconvolution uncertainty, and weak observable imaging signal.
  - The failure to recover most cell-type targets is not merely a tuning issue; it challenges target suitability.
  - Target consolidation may improve analyzability but can also change the scientific meaning of the endpoint.
- overclaim risks:
  - Presenting the three passing V1 cell types as partial validation success.
  - Ignoring how target redefinition changes comparability across versions.
- figure/table links:
  - Planned main text: Figure 3 V1/V2 gate results.
  - Planned support: Table 3 LEMPA case-study gate outcomes.

## 8. Imaging feature reproducibility and cohort attrition

- purpose: Show that even before modeling, imaging QC, patient linkage, and technical covariates constrain what validation claims are possible.
- evidence inputs:
  - `results/paired/attrition.md`
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/post_v2_audit/h4b_audit.md`
  - `handoffs/phase_c_trigger_criteria.md`
- key messages:
  - The executed paired set was `130` patients after inner join, not the larger nominal imaging cohort.
  - Attrition from imaging source to paired analysis set should be displayed as part of the result, not buried in methods.
  - Site and scanner metadata determine whether cross-source robustness is even testable.
  - A cohort can be analyzable for association tests yet still be inadequate for robust validation.
- overclaim risks:
  - Confusing paired analyzability with external reproducibility.
  - Underreporting the impact of limited site/vendor heterogeneity on robustness claims.
- figure/table links:
  - Planned main text: Table 1 data layers; Table 3 LEMPA case-study gate outcomes.
  - Planned support: participant-flow or attrition table in future figure/table package.

## 9. Validation gates: from plausible bridge to falsifiable benchmark

- purpose: Formalize the proposed validation-gate framework as the manuscript's main portable bioinformatics contribution.
- evidence inputs:
  - `results/post_v2_audit/evidence_freeze.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `handoffs/phase_c_trigger_criteria.md`
  - `finalization/jcr5_package/figure_plan.md`
- key messages:
  - Validation gates should span executability, deconvolution agreement, target freeze, predictive performance, cross-source robustness, and residual-association interpretation.
  - Failed gates are informative because they define what cannot be claimed.
  - A benchmark can be scientifically valuable even when it closes negative, if the gate logic is explicit and reproducible.
  - Trigger criteria for reopening should be external-resource based, not optimism based.
- overclaim risks:
  - Describing the framework as universally complete rather than a pragmatic minimum.
  - Omitting skipped gates, especially cross-source robustness infeasibility.
- figure/table links:
  - Planned main text: Figure 1 atlas-guided validation framework.
  - Planned main text: Table 2 validation gates and failure handling.

## 10. LEMPA case study: V1 honest negative and V2 method-fragile negative

- purpose: Present the frozen empirical line as a worked example within the broader framework, preserving the negative outcome as the central result.
- evidence inputs:
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `results/post_v2_audit/evidence_freeze.md`
- key messages:
  - V1 closed as an honest negative baseline with `3/50` cell types meeting the preregistered B3 threshold.
  - V2 remained executable but failed multi-method agreement, triggered four-module collapse, and then failed pooled module-level validation with `1/4` modules passing.
  - The line-level conclusion is therefore `METHOD-FRAGILE NEGATIVE`, not partial success.
  - The worked example is valuable because it documents where a reasonable pipeline failed under real public-data constraints.
- overclaim risks:
  - Framing V2 as a stronger attempt that nearly succeeded.
  - Letting a single passing module stand in for overall validation.
- figure/table links:
  - Planned main text: Figure 3 V1/V2 gate results.
  - Planned main text: Figure 4 method fragility and module collapse.
  - Planned support: Table 3 LEMPA case-study gate outcomes.

## 11. Interpreting caveated residual associations such as H4b

- purpose: Show how to report a reproducible residual association without allowing it to rescue a failed validation line.
- evidence inputs:
  - `results/post_v2_audit/h4b_audit.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `results/post_v2_audit/evidence_freeze.md`
- key messages:
  - H4b was exactly reproducible within the frozen V2 artifacts and preserved sign coherence after partial adjustment.
  - The retained signal is association-only and depends on a target defined from four collapsed consensus modules.
  - The V1-to-V2 target change materially strengthened H4b, so continuity with the original hypothesis surface is broken.
  - Residual associations can be reported honestly only when their dependence structure is made unavoidable to the reader.
- overclaim risks:
  - Making H4b visually dominant because its p-values are small.
  - Calling H4b a validation signal, biological rescue, or confirmation of deconvolution accuracy.
- figure/table links:
  - Planned main text: Figure 5 H4b caveated heterogeneity remainder.
  - Planned support: Table 3 LEMPA case-study gate outcomes.

## 12. Reporting checklist for future atlas-guided radiogenomics

- purpose: Convert the LEMPA experience into a reusable reporting checklist for analysts, reviewers, and editors.
- evidence inputs:
  - `finalization/jcr5_package/checklists/STROBE_mapping.md`
  - `finalization/jcr5_package/checklists/TRIPOD_transparency_mapping.md`
  - `finalization/jcr5_package/checklists/reproducibility_package.md`
  - `finalization/jcr5_package/final_quality_gate.md`
- key messages:
  - Reporting should disclose data-layer provenance, target definitions, gate criteria, attrition, missing-data handling, and robustness feasibility.
  - Observational and predictive reporting scaffolds both matter in atlas-guided radiogenomics.
  - Claim-to-artifact traceability should be treated as part of the scientific result.
  - Negative or skipped gates must be reported explicitly, not normalized away.
- overclaim risks:
  - Marking incomplete transparency elements as resolved.
  - Framing the checklist as journal compliance rather than minimum reporting discipline.
- figure/table links:
  - Planned main text: Table 4 reporting checklist for future studies.
  - Planned support: Supplementary claim-to-evidence and reporting tables.

## 13. Practical recommendations for practitioners

- purpose: Distill the framework and case-study lessons into actionable design and review recommendations.
- evidence inputs:
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `handoffs/phase_c_trigger_criteria.md`
  - `finalization/jcr5_package/final_quality_gate.md`
  - `finalization/briefings_bioinformatics_package/BIB_fit_memo.md`
- key messages:
  - Do not proceed to patient-level modeling until deconvolution agreement has been quantified and judged acceptable.
  - Prefer targets with sufficient abundance, stability, and biological continuity across methods and versions.
  - Treat cohort linkage, technical covariates, and held-out robustness surfaces as prerequisites for strong validation language.
  - Archive negative lines cleanly and reopen only when new paired resources or restored method stacks satisfy explicit trigger criteria.
  - Use residual positive signals as hypothesis generators, not rescue narratives.
- overclaim risks:
  - Giving recommendations that imply clinical deployment readiness.
  - Presenting the recommendations as if they had already been externally validated.
- figure/table links:
  - Planned main text: Figure 1 framework; Table 2 gates; Table 4 checklist.

## 14. Conclusions

- purpose: Close with the generalizable contribution, keep the frozen negative state visible, and position LEMPA as a falsifiable benchmark rather than a translational success story.
- evidence inputs:
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `finalization/briefings_bioinformatics_package/BIB_fit_memo.md`
- key messages:
  - LEMPA demonstrates that a biologically strong atlas can coexist with a failed or fragile radiogenomic validation line.
  - The durable contribution is the validation discipline, failure-mode map, and reporting framework extracted from that experience.
  - Atlas-guided radiogenomics should advance through falsifiable benchmarks and explicit gates, not optimistic bridge rhetoric.
  - Future progress depends more on better paired cohorts and robustness surfaces than on rhetorical reinterpretation of the current line.
- overclaim risks:
  - Ending with aspirational success language not supported by the frozen evidence.
  - Letting H4b appear as the concluding emotional payoff.
- figure/table links:
  - Planned main text: Figure 1 framework; Table 2 validation gates; Table 4 reporting checklist.
