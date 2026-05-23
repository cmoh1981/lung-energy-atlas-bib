# Glossary

Companion to `manuscript/v2_BIB_JCR5_manuscript_draft.md`. Terms are listed alphabetically. Definitions are scoped to the LEMPA case study and the staged validation framework introduced in the manuscript; common bioinformatics terms with universal meaning (e.g., RNA-seq, cross-validation) are not redefined here.

---

**Abundance dilution.** Loss of recoverable target signal that occurs when the atlas-defined target is a low-abundance cell-type fraction. As the fraction approaches the noise floor of either the deconvolution method or the bulk RNA-seq, predictive performance is bounded above by target noise rather than by the radiomic predictor space.

**Atlas-guided radiogenomics.** A subset of radiogenomics in which the prediction target is derived from a single-cell or integrated cell atlas (e.g., a cell-type fraction or an atlas-derived pathway score) rather than from a clinical endpoint or a generic transcriptomic signature.

**CAVEATED PASS.** Gate-G6 outcome assigned to a residual association that reproduces exactly from frozen artifacts and passes leakage and join-integrity checks but depends on a fallback-derived target. The label signals that the association is reportable but interpretively subordinate to the line-level outcome.

**CLOSED NEGATIVE.** Final closure state assigned to a paired radiogenomic line that failed the primary preregistered endpoint, lacks a credible held-out robustness surface, and has no external replication. The closure can be reopened only when explicit reopening criteria are met.

**Cross-method target agreement (gate G2).** The Pearson correlation, computed across paired patients, between the cell-type fraction columns produced by two independent deconvolution methods on the same bulk RNA-seq and the same reference atlas. The gate is summarized at the top-L abundance subset by the median across cell types and the count meeting a per-cell-type threshold.

**Cross-source robustness (gate G5).** Performance of the predictive model evaluated under at least one technical or cohort stratification (site, scanner manufacturer, batch, histology) using a leave-one-stratum-out scheme. The gate is *estimable* only when the cohort contains enough variation in the stratification variable.

**Deconvolution.** The procedure by which a bulk RNA-seq mixture is decomposed into estimated cell-type fractions using a reference signature derived from a single-cell or integrated cell atlas. The LEMPA execution used non-negative least squares (NNLS) as the primary method [25] and Scaden [9] as the secondary.

**Executability (gate G1).** Whether the chosen analysis pipeline runs end-to-end without degeneracy (no all-zero fraction columns, no NaN propagation, no row-sum-zero patients). Executability is a precondition for evidence generation; it is not by itself evidence of validation.

**Failure-mode taxonomy.** The set of named, reusable patterns by which atlas-guided radiogenomic studies typically fail. The LEMPA case study reveals six such modes (Section 5 of the main manuscript): target rarity and abundance dilution; cross-method target instability; predeclared fallback as target redefinition; cohort attrition with intact analyzability; absent robustness surface; surviving association with target dependence.

**Fallback-derived target.** A scientifically different target adopted because the originally intended target failed an upstream gate (typically G2 cross-method agreement). The LEMPA V2 four-module consensus is a fallback-derived target relative to the V1 cell-type endpoint.

**Frozen artifact.** A file written once and never modified, used as the authoritative input to downstream stages. Target freeze (gate G3) requires that the target table be a frozen artifact before predictive evaluation runs.

**Gate.** A discrete, predeclared evaluation step with a pass criterion and a predeclared action on failure. The LEMPA framework defines six gates (G1–G6) plus a pairing-integrity precondition (G0).

**H4 family.** The family of preregistered hypotheses linking imaging features to molecular targets in the LEMPA paired NSCLC line. H4a tests glycolysis pathway score against PET/CT first-order features; H4b tests CT texture features against cell-type heterogeneity variance; H4c tests OXPHOS pathway score against PET/CT first-order features. Family-wise FDR control uses Benjamini–Hochberg [27] across five tests.

**H4B_INTERPRETABLE_WITH_MAJOR_CAVEATS.** The gate-G6 audit verdict assigned to LEMPA's H4b residual association. The verdict acknowledges exact reproducibility, predictor-target independence, and join integrity, but it ties interpretation to a fallback-derived target (the four-module consensus variance) that differs from the original V1 heterogeneity construct.

**Held-out robustness.** See *cross-source robustness*.

**Heterogeneity variance.** The per-patient variance across cell-type fractions or module fractions, used as a scalar summary of intra-tumoral compositional heterogeneity. The V1 construction used variance over 50 cell-type weighted-capacity scores; the V2 construction used variance over four collapsed consensus module fractions.

**Line-level classification.** The binary or trinary verdict assigned to the entire validation line: `POSITIVE`, `NEGATIVE`, `METHOD-FRAGILE NEGATIVE`, or `INCONCLUSIVE`. The classification should appear in the abstract of any atlas-guided radiogenomic study.

**METHOD-FRAGILE NEGATIVE.** A line-level classification indicating that (i) the pipeline ran without degeneracy, (ii) one or more upstream gates (typically G2) failed, (iii) downstream gates evaluated on the predeclared fallback also failed, and (iv) the negative outcome is conditional on the particular method stack used. The LEMPA V2 outcome is `METHOD-FRAGILE NEGATIVE`.

**Module collapse.** The predeclared act of summing constituent cell-type fractions into broader functional or anatomical modules when the cell-type-level target fails the agreement gate. The LEMPA fallback collapses 50 cell types into four modules: epithelial, immune, endothelial, stromal.

**Pairing integrity (gate G0).** The condition that the inner join between imaging, molecular, and metadata tables yields one row per patient with no duplicate expansion. Failure here invalidates all downstream interpretation.

**Phase C.** Internal project codename for the post-V2 reopening phase of the LEMPA paired NSCLC line. Phase C is dormant in this manuscript and will be reopened only if one of the four reopening triggers (Section 7.2) is met.

**Predictive validation (gate G4).** The cross-validated Pearson correlation between radiomic-predicted target and frozen target, evaluated against a predeclared success rule that specifies a minimum count of targets exceeding a minimum r threshold.

**Reopening criteria.** The prespecified conditions under which a closed paired radiogenomic line can be reopened for new analysis. LEMPA's four triggers are: a new paired cohort with sufficient cross-source variation; a restored method stack including canonical GSVA-R and ≥1 additional deconvolution method; a new annotation level resolving rare-cell labels; or an independent imaging modality (PET or MRI).

**Residual association.** A positive-looking statistical association that survives in a frozen analysis output after the primary preregistered endpoint has failed. Residual associations should be reported only as caveated remainders, never as project rescue.

**Secondary-association audit (gate G6).** The auditing procedure applied to any retained residual association before it can be reported as a caveated remainder. Required checks: exact reproducibility from frozen artifacts, predictor-target independence (no leakage), join integrity, sign coherence under partial adjustment, and explicit target-dependence acknowledgment.

**Target freeze (gate G3).** The predeclared act of writing the target table to a timestamped artifact before downstream evaluation runs. Target freeze prevents silent analytic drift in which a target is implicitly redefined during the evaluation step.

**Target redefinition.** A change in the scientific definition of the target between versions or fallback steps that materially affects the meaning of any positive or negative result. The V1→V2 change in heterogeneity variance from cell-type weighted-capacity variance (50 components) to four-module consensus variance is a target redefinition.

**Trigger criteria.** See *reopening criteria*.

**Worked case study.** The role of LEMPA in this manuscript: a concrete, fully traceable execution of the framework rather than a stand-alone novelty claim. The case study's contribution is methodological rigor in a transparent negative benchmark, not the residual H4b association.
