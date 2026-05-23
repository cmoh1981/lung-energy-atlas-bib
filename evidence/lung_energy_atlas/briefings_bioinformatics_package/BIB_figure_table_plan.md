# BIB Figure and Table Plan

This display package is designed for *Briefings in Bioinformatics* as a practitioner resource. The visual hierarchy should be:

1. generalizable validation framework;
2. LEMPA as the worked example;
3. failure handling and decision logic;
4. H4b only as a subordinate caveated remainder.

The package must help future atlas-guided radiogenomics studies decide whether to proceed, collapse targets, defer validation, or archive a line without overclaiming success.

## Figure 1. Atlas-guided radiogenomics validation framework

- Message: Atlas-guided radiogenomics should be treated as a staged validation workflow, not as a single prediction task. Biologic plausibility, linkage integrity, target stability, predictive performance, and replication readiness are separate gates.
- Input files:
  - `finalization/jcr5_package/journal_strategy/jcr5_target_strategy.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `handoffs/phase_c_trigger_criteria.md`
- Caption: `Figure 1. Atlas-guided radiogenomics validation framework. A practitioner-facing framework is proposed in which organ-matched atlas construction, paired cohort linkage, deconvolution agreement, target freezing, predictive evaluation, held-out robustness, and secondary-association audit are treated as explicit gates. The framework emphasizes that biologically informative atlas outputs do not by themselves validate imaging-based recovery of transcriptomic targets.`
- BIB fit rationale: Works as a reusable bioinformatics roadmap that readers can apply outside NSCLC and outside LEMPA.
- Overclaim risk: Do not draw the framework as if successful prediction is the expected default outcome; the figure should show archive/defer branches as legitimate endpoints.

## Figure 2. LEMPA lung energy atlas case study

- Message: LEMPA provides a biologically informative organ-specific atlas layer that is reusable even though the paired radiogenomic validation line remained negative.
- Input files:
  - `figures/fig1_pathway_capacity_heatmap.png`
  - `figures/fig1_pathway_capacity_heatmap.pdf`
  - `finalization/jcr5_package/manuscript_jcr5_draft.md`
  - `sources/conceptual_framework.md`
- Caption: `Figure 2. LEMPA lung energy atlas case study. The Lung Energy Metabolism Pathway Atlas maps glycolysis, oxidative phosphorylation, pentose phosphate pathway, tricarboxylic acid cycle, and lactate-related pathway structure across 584,944 Human Cell Atlas lung cells spanning 50 annotated cell types. In the BIB framing, the atlas is presented as the reusable resource layer, while the paired radiogenomic line is treated separately as a stress test of whether such atlas-derived targets can be recovered from imaging.`
- BIB fit rationale: Keeps the paper anchored in a concrete, reusable bioinformatics resource while preserving the case-study identity.
- Overclaim risk: Do not let atlas strength visually imply successful downstream radiogenomic validation.

## Figure 3. Failure-mode cascade

- Message: The main translational lesson is a failure cascade: target instability appeared before robust prediction, forcing module collapse and leaving only a caveated residual association.
- Input files:
  - `results/v2/multi_method_attempt_v3.md`
  - `results/v2/b3_v2_intra_v1_cross_source.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/post_v2_audit/h4b_audit.md`
- Caption: `Figure 3. Failure-mode cascade in the LEMPA worked example. Multi-method deconvolution disagreement at the intended cell-type level triggered collapse to four broad modules, after which the primary module-level predictive gate still failed and only a narrow H4b association-level remainder remained under major caveats. The cascade highlights where atlas-guided radiogenomics can break before clinical or biological claims become transportable.`
- BIB fit rationale: Converts one negative case into a general failure taxonomy for benchmarking and study design.
- Overclaim risk: H4b must appear as the last, smallest branch; significant values must not read as project rescue.

## Figure 4. Practitioner decision tree

- Message: Readers need explicit rules for deciding whether to proceed, collapse targets, defer validation, or archive a radiogenomic line.
- Input files:
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `handoffs/phase_c_trigger_criteria.md`
  - `finalization/jcr5_package/checklists/TRIPOD_transparency_mapping.md`
  - `finalization/jcr5_package/checklists/STROBE_mapping.md`
- Caption: `Figure 4. Practitioner decision tree for atlas-guided radiogenomics. Decision nodes define whether a study should continue to predictive evaluation, collapse targets under predeclared rules, defer because a robustness surface is absent, or archive the line until independent paired resources or reproducibility-grade method stacks become available.`
- BIB fit rationale: Strongly practice-oriented and directly aligned with BIB's resource-and-tools readership.
- Overclaim risk: Do not let target collapse look like routine optimization; it should be presented as a constrained fallback after upstream failure.

## Table 1. Data layers for atlas-guided radiogenomics

- Draft outputs:
  - `finalization/briefings_bioinformatics_package/tables/table1_data_layers.md`
  - `finalization/briefings_bioinformatics_package/tables/table1_data_layers.csv`
- Message: Successful atlas-guided radiogenomics depends on multiple linked data layers, each of which can independently limit interpretability.
- Input files:
  - `sources/conceptual_framework.md`
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/paired/attrition.md`
  - `results/post_v2_audit/h4b_audit.md`
  - `handoffs/phase_c_trigger_criteria.md`
- Caption: `Table 1. Data layers required for atlas-guided radiogenomics. The table summarizes the minimum data layers, their role in the workflow, what the LEMPA case executed successfully, and what failure mode appears when any layer is weak or absent.`
- BIB fit rationale: Generalizes the manuscript beyond LEMPA by turning one case into a reusable study-design checklist.
- Overclaim risk: Do not imply that presence of all layers guarantees validation success; the table should support feasibility assessment, not optimism.

## Table 2. Validation gates and failure handling

- Draft outputs:
  - `finalization/briefings_bioinformatics_package/tables/table2_validation_gates.md`
  - `finalization/briefings_bioinformatics_package/tables/table2_validation_gates.csv`
- Message: Radiogenomics studies need explicit pass/fail gates and predeclared actions when a gate fails.
- Input files:
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `results/post_v2_audit/h4b_audit.md`
  - `handoffs/phase_c_trigger_criteria.md`
- Caption: `Table 2. Validation gates and failure handling for atlas-guided radiogenomics. Each gate is linked to the required evidence, a minimum pass criterion, and the recommended failure interpretation or next action.`
- BIB fit rationale: Provides a methods-aware operator table suitable for future benchmarking papers and study protocols.
- Overclaim risk: Do not soften failed gates into optional warnings; failure handling must preserve negative outcomes when thresholds are missed.

## Table 3. LEMPA case-study gate outcomes

- Draft outputs:
  - `finalization/briefings_bioinformatics_package/tables/table3_lempa_gate_outcomes.md`
  - `finalization/briefings_bioinformatics_package/tables/table3_lempa_gate_outcomes.csv`
- Message: The LEMPA worked example should show exactly which gates passed, failed, or remained unavailable, and what each state allowed the manuscript to claim.
- Input files:
  - `results/v1/V1_FINAL_SUMMARY.md`
  - `results/v2/V2_FINAL_SUMMARY.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/post_v2_audit/h4b_audit.md`
  - `docs/04-report/nsclc_radiogenomics_post_v2_closure.report.md`
  - `handoffs/phase_c_trigger_criteria.md`
- Caption: `Table 3. LEMPA case-study gate outcomes. V1, V2, and the post-V2 audit are summarized as an executed benchmark history showing where the line remained usable, where it failed, and why the final classification stayed METHOD-FRAGILE NEGATIVE.`
- BIB fit rationale: Keeps the case study concrete while preserving its value as a benchmarking example rather than a success claim.
- Overclaim risk: Do not compress SKIPPED or caveated states into PASS/FAIL shorthand that hides transportability limits.

## Table 4. Reporting checklist for future studies

- Draft outputs:
  - `finalization/briefings_bioinformatics_package/tables/table4_reporting_checklist.md`
  - `finalization/briefings_bioinformatics_package/tables/table4_reporting_checklist.csv`
- Message: Future studies should report enough design, target-definition, provenance, and robustness detail to prevent the same interpretive failures.
- Input files:
  - `finalization/jcr5_package/checklists/STROBE_mapping.md`
  - `finalization/jcr5_package/checklists/TRIPOD_transparency_mapping.md`
  - `finalization/jcr5_package/checklists/reproducibility_package.md`
  - `results/post_v2_audit/evidence_freeze.md`
  - `results/post_v2_audit/h4b_audit.md`
- Caption: `Table 4. Reporting checklist for future atlas-guided radiogenomics studies. The checklist emphasizes cohort linkage, target stability, fallback transparency, reproducibility assets, and explicit reporting of negative outcomes.`
- BIB fit rationale: Strongest practitioner-facing item in the package; it turns the paper into a resource for future study design and reporting.
- Overclaim risk: Do not mark unresolved reproducibility or model-specification items as complete merely because they are mentioned narratively.
