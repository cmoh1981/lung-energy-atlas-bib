# From Cell Atlases to Radiogenomics: A Lung Energy Metabolism Case Study in Bioinformatics Validation Failure Modes

## Abstract

Cell atlases are increasingly used to define biologically plausible targets for imaging-linked molecular inference, but plausibility at atlas resolution does not guarantee patient-level validation. For practitioners, the main lesson is not that atlas-guided radiogenomics is impossible, but that it should be treated as a staged bioinformatics validation problem with explicit gates for target definition, deconvolution agreement, abundance stability, cohort linkage, and robustness. This review with worked case study uses the Lung Energy Metabolism Pathway Atlas (LEMPA) to show how a strong normal-lung atlas contribution can coexist with a negative translational validation line. LEMPA maps pathway-level energy metabolism across 584,944 lung cells spanning 50 annotated cell types and remains useful as a normal-lung reference resource. Its paired NSCLC radiogenomic branch, however, closed negatively under frozen public-data conditions. In V1, only 3/50 cell types reached the prespecified cross-validated threshold of r >= 0.30. In V2, the redesign remained analyzable but failed the intended agreement and predictive gates: the top-10 median agreement between deconvolution methods was -0.087, only 1/10 top-abundance cell types reached r >= 0.4, and only 1/4 collapsed modules passed the pooled cross-validation threshold. H4a and H4c were null, while H4b survived only as a narrow association-level remainder tied to a fallback-dependent target definition. The practical contribution of this manuscript is therefore a validation discipline for atlas-guided radiogenomics, together with a failure-mode map showing why negative benchmark outcomes are informative when they are reported transparently rather than rhetorically rescued.

## Key Points

- Atlas-guided radiogenomics requires validation gates rather than bridge rhetoric.
- Deconvolution agreement should be treated as a prerequisite, not a supplementary sensitivity analysis.
- Rare or diluted cell-type targets can be biologically compelling yet weak as imaging endpoints.
- Public paired cohorts can be sufficient for execution while remaining insufficient for external validation.
- Negative benchmark outcomes are useful when they identify where the translation path failed.

## 1. Introduction

The central bioinformatics lesson of atlas-guided radiogenomics is that biological resolution and predictive resolution are different achievements. A single-cell atlas can identify compelling cell states, pathway structure, and organ-specific heterogeneity, but the moment those atlas-derived states are projected onto patient-linked imaging data, the problem changes. The analyst is no longer evaluating cell biology alone. The analyst is evaluating whether multiple data layers, each with their own uncertainty structure, remain coherent enough to support a falsifiable patient-level claim.

That distinction matters because the field is vulnerable to optimistic bridge narratives. Atlas-derived targets can appear biologically persuasive, radiomics can appear richly quantitative, and public paired datasets can appear to provide a ready validation surface. In practice, however, decisive failure points often sit upstream of the final predictive model. Target rarity can dilute recoverable signal. Deconvolution methods can disagree on the quantities that imaging is supposed to predict. Cohort linkage can reduce nominal sample size to a much smaller analyzable set. Technical covariates and source heterogeneity can be too limited to support meaningful robustness checks.

This article is written as a practitioner resource on those failure modes, using the Lung Energy Metabolism Pathway Atlas as a worked example. The goal is not to present a successful lung cancer radiogenomic validation story. The goal is to show how a biologically informative atlas project encountered negative and method-fragile outcomes once its targets were tested against frozen public paired NSCLC data, and how those outcomes can be converted into reusable validation guidance.

## 2. Lung Energy Metabolism as a Motivating Case

Lung energy metabolism is distributed across structurally and functionally distinct cellular compartments rather than concentrated in one dominant lineage. Airway epithelial maintenance, immune surveillance, endothelial homeostasis, stromal support, and alveolar function all impose different bioenergetic demands. A normal-lung atlas should therefore reveal organized pathway heterogeneity rather than a single canonical metabolic profile.

LEMPA was built around this atlas question. Using an integrated human lung cell atlas resource, the project quantified glycolysis, pentose phosphate pathway activity, tricarboxylic acid cycle behavior, oxidative phosphorylation, and lactate-related metabolism across 50 annotated lung cell types. The resulting atlas showed broad pathway heterogeneity across the normal lung, with glycolytic enrichment concentrated in specialized airway epithelial and immune populations rather than collapsing onto one universal lung metabolic state.

The same biological richness, however, makes radiogenomic translation harder. Imaging features operate at patient and lesion scale, whereas atlas-defined targets can be rare, composition-sensitive, and method-dependent. A target that is biologically coherent in a single-cell framework may still be poorly suited as an imaging endpoint if it is weakly abundant, unstable across deconvolution methods, or only indirectly represented in a mixed tumor sample.

## 3. Atlas-Guided Radiogenomics as a Multi-Layer Join Problem

Atlas-guided radiogenomics should be treated as a multi-layer join problem before it is treated as a modeling problem. At minimum, the analyst needs a well-characterized atlas resource, a strategy for deriving target signatures or fractions, bulk transcriptomic data that can be aligned to those targets, imaging features and masks derived under known quality procedures, patient linkage that preserves one-to-one correspondence, and enough metadata to evaluate robustness across meaningful technical strata.

The LEMPA case makes this point concrete. The atlas layer was large and biologically informative. The paired validation branch, however, did not operate on the nominal imaging cohort size alone. After quality control and inner joining radiomics with molecular and deconvolution artifacts, the executed paired analysis surface was 130 patients. That count was sufficient for analyzability, but it was not equivalent to a replication-ready cohort and did not provide a credible held-out robustness surface for site, batch, or histology testing.

A practitioner-focused paper should therefore present integration quality as part of the scientific result. If the joint dataset is thin, technically imbalanced, or missing key metadata, downstream claims about validation should narrow accordingly, even when the modeling code runs cleanly.

## 4. Deconvolution Agreement as the First Validation Gate

Deconvolution agreement determines whether the imaging target remains stable enough to interpret. If independent deconvolution strategies do not agree on the cell-type or module-level quantities that imaging is supposed to recover, any subsequent predictive performance estimate inherits an unresolved target-definition problem. Agreement should therefore be treated as an early validation gate, not as an after-the-fact sensitivity analysis.

LEMPA illustrates this point through the V2 redesign. V2 was not a technical non-run. The second deconvolution branch executed, produced non-degenerate outputs, and preserved an analyzable workflow. The failure emerged when agreement was measured. At the intended cell-type surface, the top-10 median agreement between methods was -0.087, and only 1/10 top-abundance cell types reached r >= 0.4. Those values describe a target definition that failed to hold together across methods strongly enough to support confident downstream interpretation.

Once agreement fails at the cell-type surface, downstream modeling cannot be presented as if it were still testing the original target. The analyst may proceed to a fallback representation for diagnostic or exploratory purposes, but the status of the claim has changed. In LEMPA, that change triggered collapse from higher-resolution cell-type targets to four broad modules. The fallback preserved analyzability but marked a loss of target fidelity that must remain visible in later interpretation.

## 5. Target Rarity and Abundance Dilution

Rare or weakly represented targets are intrinsically difficult imaging endpoints. Even when they are biologically interesting, they may contribute too little stable signal to be recovered from mixed tissue expression and lesion-scale radiomics. This is one of the most important lessons for practitioners because the temptation to select the most biologically specific atlas target is often strongest precisely when that target is least likely to remain recoverable in paired patient data.

The V1 LEMPA result is an honest example. The preregistered success criterion required at least 10 cell types to reach cross-validated Pearson r >= 0.30. Only 3/50 cell types reached that threshold. This is not best read as near success or partial validation. It is best read as evidence that most intended cell-type endpoints were not recoverable under the available paired-data conditions.

Target collapse must also be interpreted carefully. Collapsing from many cell types to broad modules can improve analyzability because larger compartments are often more abundant and more stable across methods. But collapse changes the scientific question. A module-level signal is not a rescued cell-type-level signal. It is a different target with different biological meaning.

## 6. Imaging Feature Reproducibility and Cohort Attrition

The imaging side of atlas-guided radiogenomics can narrow interpretation through ordinary but consequential forms of attrition. Radiomic feature extraction depends on segmentation quality, feature completeness, and patient linkage. Robustness claims additionally depend on whether the cohort contains enough technical heterogeneity to support meaningful stratified tests. A pipeline can therefore be analyzable at face value while still lacking the structure needed for a strong validation claim.

In LEMPA, the paired public NSCLC branch reached an executed analysis set of 130 patients, with the H4b analysis subset at 123 after routine missing-feature filtering. The relevant point is not that this count was unusable. It is that the frozen local artifacts did not support a credible held-out robustness surface for the kinds of cross-source checks needed to offset deconvolution fragility. Site information was effectively non-variable, and vendor information was limited.

For practitioners, imaging quality control and cohort structure should be reported as part of the validation logic. A study may generate radiomics, deconvolution outputs, and paired tables while still remaining too constrained for strong predictive language.

## 7. Validation Gates

The most generalizable contribution of the LEMPA experience is a gate-based framework for atlas-guided radiogenomics.

Gate 1 is executability: can the full paired pipeline run without degeneration?

Gate 2 is agreement: do independent deconvolution strategies support a stable target surface?

Gate 3 is target freeze: has the endpoint been fixed cleanly enough to prevent silent drift during evaluation?

Gate 4 is predictive performance: does cross-validated association reach its prespecified threshold at the target surface the study set out to test?

Gate 5 is robustness: can the signal be challenged across meaningful technical or cohort splits?

Gate 6 is residual interpretation: if a narrow association remains after broader failure, can it be described honestly without reversing the line-level outcome?

This framing converts negative outcomes into structured information. A failed gate tells the field what was not achieved and where the translational bridge broke. That is more informative than a vague conclusion that the data were underpowered or that the biology was complex.

## 8. LEMPA Worked Case: V1 and V2

The worked example can be summarized directly. V1 was an honest negative baseline. The prespecified B3 criterion required at least 10 cell types with cross-validated Pearson r >= 0.30, but only 3/50 cell types reached that mark. H4a and H4c did not produce supportive evidence in the frozen V1 outputs, and V1 H4b was not significant after false-discovery-rate correction. The original patient-level validation line did not pass under its own preregistered criterion.

V2 tested whether the V1 outcome reflected recoverable method constraints rather than an intrinsically weak translation surface. V2 remained technically analyzable, but the intended cell-type agreement path failed. The top-10 median agreement was -0.087, and only 1/10 top-abundance cell types reached r >= 0.4, forcing collapse to four broad modules. At that fallback surface, only 1/4 modules passed the pooled cross-validation threshold.

The line-level classification is therefore `METHOD-FRAGILE NEGATIVE`. The project was not invalidated by technical non-execution, but the resulting evidence did not support a method-robust positive claim.

## 9. Interpreting H4b

Residual positive-looking associations are often the most rhetorically dangerous part of a negative line because they invite rescue narratives. LEMPA's H4b remainder is useful precisely because it shows how such a signal should be handled. The result was reproducible within the frozen V2 tables, its sign pattern remained coherent after partial adjustment, and it did not appear to arise from duplicate joins or direct radiomic leakage. Those strengths justify reporting the association rather than discarding it.

At the same time, H4b cannot reverse the broader conclusion. H4a was null, H4c was null, and the broad validation line remained negative at both the original and collapsed predictive surfaces. The retained H4b effects sit inside that failed line and depend on a changed target definition. In the frozen V2 audit, Benjamini-Hochberg FDR values were 3.93167135294686e-05 for entropy, 0.000192835821237218 for contrast, and 6.04179283005966e-05 for homogeneity. These values should be interpreted as association-level evidence tied to variance across four collapsed consensus modules, not as confirmation of the original cell-type heterogeneity endpoint.

The defensible statement is therefore narrow: a texture-versus-heterogeneity association remained reproducible within a fallback-derived target inside an otherwise negative and method-fragile validation line.

## 10. Practical Recommendations

First, freeze validation gates before interpretation becomes invested in the bridge. Agreement thresholds, abundance criteria, predictive cutoffs, and robustness expectations should be explicit before paired analysis begins.

Second, prefer targets that are abundant enough, stable enough, and biologically continuous enough across methods to remain interpretable at patient scale. Highly specific cell states may still be worth studying, but they should not automatically become primary imaging endpoints.

Third, treat public paired cohorts as validation opportunities with known ceilings. Public resources are invaluable for execution, benchmarking, and transparent closure, but they often lack the sample structure or metadata needed for strong externalizable claims.

Fourth, report negative and method-fragile results as first-class outputs. The field benefits when a study states clearly that the atlas was useful, the paired workflow was analyzable, the deconvolution target failed agreement, and a residual association did not rescue the line.

## 11. Conclusions

LEMPA shows that cell atlases can produce biologically meaningful organ-specific resources while still failing to support a robust patient-level radiogenomic bridge under current public paired-data conditions. That is not a contradiction. Atlas quality and translational validation sit on different evidentiary tiers. The atlas layer remains informative as a normal-lung metabolic reference. The paired NSCLC branch remains valuable as a transparent negative benchmark that identifies where the bridge failed.

The durable contribution of the manuscript is therefore a practical framework for how atlas-guided radiogenomics should be challenged before strong language is used: agreement must hold, target definitions must remain stable, predictive thresholds must be met on the intended endpoint, robustness surfaces must exist, and residual associations must stay subordinate when the broader line fails.

## Data and Code Availability

This manuscript currently relies on copied local project artifacts preserved in the publication package. Final submission requires public data accession references, a code repository or archive DOI, software environment documentation, and exact instructions for reproducing the V1/V2 evidence tables.

## Ethics Statement

The current manuscript is based on public and previously collected datasets. Final submission should add the exact data-use and ethics language required by the source cohorts and by the corresponding author's institution.

## Conflict of Interest

To be completed by the author team before submission.

## Funding

To be completed by the author team before submission.

## References

See `submission/BIBLIOGRAPHY_LOCKED_CORE.md` for the current locked core bibliography. Final manuscript conversion to journal style remains required.

