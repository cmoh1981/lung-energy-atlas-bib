# BIB Bibliography Lock Plan

Scope: Task 8 only. This plan uses the current manuscript, source manuscript, and finalization package as the source of truth. It does not add new external claims. Any citation not fully recoverable from local materials is marked `TO VERIFY`.

## 1. Cell atlases and HCA Lung Atlas

### Needed citations
- Sikkema L et al. 2023, *An integrated cell atlas of the lung in health and disease*.
- Travaglini KJ et al. 2020, *A molecular cell atlas of the human lung from single-cell RNA sequencing*.
- Madissoon E et al. 2023, *A spatial multi-omics map of normal human lung* only if retained in atlas-context or future-work text.
- LungMAP overview / consortium paper only if lifespan or developmental framing remains in scope.

### Current source if known
- `finalization/jcr5_package/manuscript_jcr5_draft.md:91`
- `references/reading_queue.md:9-12`
- `finalization/jcr5_package/manuscript_jcr5_draft.md:21,29,75`

### Verification status
- Sikkema 2023: `PARTIAL` (required by current package and named repeatedly, but not yet present as a full locked bibliography entry in the local reference list).
- Travaglini 2020: `PARTIAL` (full title and year appear locally; source manuscript reference list includes it).
- Madissoon 2023: `TO VERIFY`.
- LungMAP overview paper: `TO VERIFY`.

### Missing items
- Final journal-formatted entry for Sikkema 2023.
- Decision on whether Madissoon 2023 and LungMAP overview remain necessary in the BIB draft.

## 2. Radiogenomics and NSCLC-Radiogenomics

### Needed citations
- Bakr S et al. 2018, NSCLC-Radiogenomics public dataset paper.
- One general radiogenomics background/review citation if the Introduction keeps discipline-level framing beyond the dataset description (`TO VERIFY`).

### Current source if known
- `C:/Users/ohbry/OneDrive/Apps/beta cell/manuscript_draft.md:519`
- `finalization/jcr5_package/manuscript_jcr5_draft.md:33,75,91`
- `docs/04-report/nsclc_radiogenomics.report.md:19`
- `OPENCODE_FINALIZE_JCR5_PROMPT.md:59`

### Verification status
- Bakr 2018: `PARTIAL` (named consistently, with local manuscript reference text, but still needs final bibliography lock/format check).
- General radiogenomics background citation: `TO VERIFY`.

### Missing items
- Confirm final Bakr 2018 formatting against the target manuscript style.
- Decide whether a separate radiogenomics field review is required or whether Bakr 2018 plus dataset framing is sufficient.

## 3. Deconvolution methods

### Needed citations
- CIBERSORTx-related citation if the source-manuscript "CIBERSORTx-style" wording is retained.
- Scaden citation for the V2 secondary deconvolution path.
- MuSiC / BayesPrism / EPIC / Bisque citations only if these blocked alternatives are discussed in the final BIB manuscript or supplement.

### Current source if known
- `C:/Users/ohbry/OneDrive/Apps/beta cell/manuscript_draft.md:201-211`
- `docs/04-report/nsclc_radiogenomics.report.md:42-45,91-96`
- `results/v2_preflight/multimethod_environment_readiness.md:36-43`
- `finalization/jcr5_package/manuscript_jcr5_draft.md:33,47,61,71`

### Verification status
- CIBERSORTx-style NNLS method citation: `TO VERIFY`.
- Scaden citation: `TO VERIFY`.
- MuSiC / BayesPrism / EPIC / Bisque citations: `TO VERIFY` and probably unnecessary unless retained for blocked-method discussion.

### Missing items
- Replace or support the source-manuscript "CIBERSORTx-style" wording with a locked citation.
- Lock the Scaden citation if V2 method-dependence evidence remains central.
- Trim unsupported alternative-method name-dropping unless citations are added deliberately.

## 4. Single-sample pathway scoring / GSVA / ssGSEA

### Needed citations
- Hanzelmann S et al. 2013, GSVA method paper.
- Liberzon A et al. 2015, MSigDB Hallmark collection.
- Subramanian A et al. 2005, GSEA background paper if retained.
- ssGSEA-specific citation for the `gseapy.ssgsea` caveat if the BIB manuscript explicitly uses ssGSEA terminology rather than only "GSVA-style" scoring (`TO VERIFY`).

### Current source if known
- `C:/Users/ohbry/OneDrive/Apps/beta cell/manuscript_draft.md:523-527`
- `finalization/jcr5_package/manuscript_jcr5_draft.md:31,37,71,91`
- `results/v1/V1_FINAL_SUMMARY.md:41`
- `docs/04-report/nsclc_radiogenomics.report.md:34,64`
- `OPENCODE_FIX_H4ac.md:39-40`

### Verification status
- GSVA 2013: `PARTIAL` (full local reference text exists in source manuscript).
- MSigDB Hallmark 2015: `PARTIAL` (full local reference text exists in source manuscript).
- GSEA 2005: `PARTIAL` (full local reference text exists in source manuscript).
- ssGSEA-specific method citation: `TO VERIFY`.

### Missing items
- Decide whether the final wording is GSVA, GSVA-style, or ssGSEA-specific.
- If ssGSEA is named explicitly in the final BIB draft, lock the exact ssGSEA citation rather than relying on generic GSVA language.

## 5. Radiomics feature extraction / PyRadiomics

### Needed citations
- PyRadiomics method/software citation.
- Any IBSI-style standardization citation only if the final manuscript claims standardized radiomics compliance (`TO VERIFY`).

### Current source if known
- `docs/04-report/nsclc_radiogenomics.report.md:33`
- `results/v1/V1_FINAL_SUMMARY.md:15`
- `docs/02-design/features/nsclc_radiogenomics_v2.design.md:22`
- `progress.md:259`
- `OPENCODE_FINALIZE_BIB_PROMPT.md:318`

### Verification status
- PyRadiomics citation: `TO VERIFY`.
- Additional radiomics-standardization citation: `TO VERIFY`.

### Missing items
- Add the canonical PyRadiomics reference; no full local bibliography entry is currently locked.
- Decide whether a second radiomics-standardization citation is actually needed for BIB framing.

## 6. Prediction-model reporting / TRIPOD

### Needed citations
- TRIPOD statement citation for prediction-model reporting.
- Updated TRIPOD-AI / extension citation only if the final manuscript explicitly invokes an extension rather than generic TRIPOD-style transparency (`TO VERIFY`).

### Current source if known
- `finalization/jcr5_package/checklists/TRIPOD_transparency_mapping.md:1-61`
- `finalization/jcr5_package/journal_strategy/jcr5_target_strategy.md:59`
- `OPENCODE_FINALIZE_BIB_PROMPT.md:319`

### Verification status
- Base TRIPOD citation: `TO VERIFY`.
- Any extension citation: `TO VERIFY`.

### Missing items
- Lock one exact TRIPOD statement paper appropriate to the manuscript's reporting scope.
- Avoid citing extensions unless they are actually used in the final text.

## 7. Observational reporting / STROBE

### Needed citations
- STROBE statement citation for observational reporting.

### Current source if known
- `finalization/jcr5_package/checklists/STROBE_mapping.md:1-48`
- `finalization/jcr5_package/journal_strategy/jcr5_target_strategy.md:59`
- `OPENCODE_FINALIZE_BIB_PROMPT.md:320`

### Verification status
- STROBE citation: `TO VERIFY`.

### Missing items
- Lock one exact STROBE statement paper.
- Ensure the final manuscript uses STROBE as an observational-reporting scaffold, not as a claim of full checklist completion unless true at submission.

## 8. Negative results / reproducibility / benchmarking if relevant

### Needed citations
- One reproducibility / benchmarking / negative-results framing citation only if the BIB manuscript explicitly generalizes beyond the internal LEMPA audit trail.
- No external citation is mandatory if the final text keeps this section anchored to project-specific evidence and reporting checklists alone.

### Current source if known
- `finalization/jcr5_package/journal_strategy/jcr5_target_strategy.md:9,24,33,39,42,59-64,68`
- `finalization/jcr5_package/checklists/reproducibility_package.md:5-58`
- `finalization/jcr5_package/editor_summary.md:13,19,35,39,43`
- `OPENCODE_FINALIZE_BIB_PROMPT.md:321`

### Verification status
- External benchmarking / reproducibility citation: `TO VERIFY`.
- Internal relevance: `VERIFIED` (the current package clearly frames reproducibility, benchmarking discipline, and instructive negative findings as central).

### Missing items
- Decide whether BIB framing needs one or more external reproducibility / benchmarking citations, or whether internal package artifacts are sufficient.
- If retained, lock exact citation(s) rather than leaving generic "reproducibility" language unsupported.

## Lock priorities

1. Core must-lock citations: Sikkema 2023, Travaglini 2020, Bakr 2018, GSVA 2013, MSigDB Hallmark 2015.
2. Reporting must-lock citations if named in manuscript: TRIPOD and STROBE.
3. Method must-lock citations if named in manuscript: PyRadiomics, Scaden, and any retained CIBERSORTx-style deconvolution reference.
4. Optional framing citations: negative-results / reproducibility / benchmarking, only if the final BIB draft makes those outward-facing claims explicitly.

## Current blocker summary

- The local package already identifies the required citation families, but the bibliography is not locked.
- The largest method-specific hole is the absence of a fully specified PyRadiomics citation in the current local manuscript/finalization materials.
- TRIPOD and STROBE are operationally present as checklist frameworks, but their exact statement citations are still `TO VERIFY`.
