# Work log: Chapter 26, Multilevel Unanchored Meta-Regression (ML-UMR)

Author agent: Opus 4.8. File written: `chapters/part5/26-ml-umr.qmd` (full chapter; stub replaced).
Catalogue coverage: M.1 to M.12 (all owned results stated and proved).

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (single source of truth for symbols).
- Proof catalogue base draft: `~/Documents/GitHub/ITC_Coq/proofs/M_ml_umr.md` (M.1 to M.12 sketches,
  dependency table). Every sketch expanded into a complete proof in the book's notation.
- Companion manuscript: `~/Documents/GitHub/ITC_Coq/manuscript/11_ml_umr.md` (Sections 11.1 to 11.15).
- Reference implementation: `~/Documents/GitHub/mlumr` (README.md, `man/mlumr.Rd`, `man/ndmm_ipd.Rd`,
  `man/set_agd_surv.Rd` listing, `vignettes/survival-outcomes.Rmd.orig`). Used for the SPFA/relaxed model
  names ("Type 1"/"Type 2"), the survival pipeline (`set_agd_surv`, `predict(type="loghr")`, RMST default),
  the `check_integration()` doubling diagnostic, the documented caveats (no between-study heterogeneity,
  weakly identified relaxed slope, HR non-collapsibility, integration convergence), and the multiple-myeloma
  PFS application (lenalidomide vs thalidomide) that motivates the survival sections.
- Voice match: `chapters/part4/18-maic.qmd`.
- Sibling Part V chapters read for exact cross-reference slugs/equations and statements: Ch20
  (`20-mlnmr-aggregation.qmd`), Ch21, Ch22 (`thm-hypercube-integration`, copula/Sobol'), Ch23
  (`23-mlnmr-estimands.qmd`: `lem-mlnmr-aggregate-monotone`, `thm-target-population-integral`,
  `thm-mlnmr-identifiability-2study`, `thm-mlnmr-generalizes-nma`, `eq-mlnmr-est-model`), Ch24
  (`def-integration-error-monitoring`, `eq-qmc-fixed-nodes`), Ch25 (`25-general-likelihoods.qmd`: full
  survival apparatus). Part IV: Ch17 (constancy defs, unanchored PAIC), Ch19 (`def-stc-marginal`,
  `thm-marginal-stc-unbiased`, `thm-stc-consistency`, `def-stc-bayes`).

Two forward references from already-written chapters point into this chapter and were honored exactly:
- Ch25, remark after `@thm-rmst-collapsible`, cites `@thm-mlumr-tte` for the unanchored scale-misalignment
  of RMST: delivered as `@thm-mlumr-tte` part (e), proved.
- Ch25, remark after `@thm-aggregate-marginal-likelihood`, cites `@thm-pseudo-ipd-reconstruction`:
  delivered and proved (exact KM product-limit inversion).
- Ch19 (`def-stc-bayes` remark) and Ch22/Ch23 remarks refer forward to "Chapter 26"; consistent.

## Slugs defined (owned, all 12 present)

`def-unanchored-network` (M.1), `def-spfa` (M.2), `thm-mlumr-model` (M.3), `thm-spfa-relaxation` (M.4),
`thm-mlumr-qmc-marginalization` (M.5), `thm-mlumr-tte` (M.6), `thm-pseudo-ipd-reconstruction` (M.7),
`thm-mlumr-joint-likelihood` (M.8), `thm-mlumr-target-survival` (M.9), `thm-mlumr-stc-equivalence` (M.10),
`prp-spfa-vs-sema` (M.11), `thm-mlumr-identifiability` (M.12).

Helper slugs introduced (topic-namespaced, globally unique, not in the owned list but needed for rigor):
- `lem-mlumr-single-arm-conflation` (rank deficiency: single-arm study conflates baseline and treatment
  effect; the algebraic root of "unanchored").
- `lem-spfa-absolute-constancy` (SPFA = conditional constancy of absolute effects; the projection identity).

Section ids: `sec-mlumr-intro`, `-setting`, `-spfa`, `-model`, `-relaxed`, `-qmc`, `-tte`, `-pseudo`,
`-joint`, `-target`, `-stc`, `-spfa-sema`, `-limits`, `-example`, `-notes`, `-exercises`.

Exercises: `exr-mlumr-conflation`, `exr-mlumr-identify-alphaB` (★), `exr-mlumr-continuous-closed-form`,
`exr-mlumr-relaxed-counting`, `exr-mlumr-stc-reduction`, `exr-mlumr-marginal-hr`,
`exr-mlumr-rmst-transport` (★), `exr-mlumr-spfa-violation`. Two starred for Appendix F:
`exr-mlumr-identify-alphaB` and `exr-mlumr-rmst-transport`.

Key equation labels owned: `eq-mlumr-estimand`, `eq-mlumr-two-arm`, `eq-spfa`, `eq-spfa-predictors`,
`eq-spfa-constant-contrast`, `eq-spfa-projection`, `eq-mlumr-model-ind`, `eq-mlumr-model-agg`,
`eq-mlumr-alphaB-solve`, `eq-spfa-relaxed-agg`, `eq-mlumr-qmc-pullback`, `eq-mlumr-qmc`,
`eq-mlumr-qmc-error`, `eq-mlumr-ph`, `eq-mlumr-cond-loghr`, `eq-mlumr-rmst-transport`,
`eq-mlumr-censored-agg`, `eq-km-product`, `eq-km-inversion`, `eq-mlumr-joint-lik`,
`eq-mlumr-target-functionals`, `eq-mlumr-stc-equiv`.

Verification run: all `@`-cross-references resolve against book-wide slugs; all 12 owned slugs present;
no em/en dash, spaced-hyphen, or double-hyphen connectors; no British spellings; worked-example arithmetic
checked numerically (binary LOR example and exponential-survival coda).

## Machine-checked tags

None. Confirmed there is no `theories/ML_UMR.v` (nor any ML-NMR file) in
`~/Documents/GitHub/ITC_Coq/theories/`; the manuscript states ML-UMR is not formalized. Per the contract
(Part V results are mostly computational; tag only if present) no `[machine-checked: ...]` tags were added.
The prose Notes section explains the nearest Coq relatives (`EffectModifiers.v` cancellation, `STC.v`
`STC_consistent` / `methods_agree_when_correct`) without tagging, since the unanchored absolute-effect
transport is a different algebraic structure and is not mechanized.

## Proposed bibliography additions (not yet in references.bib; cited in the chapter)

Two cited keys are not yet present and should be merged by the orchestrator:

```bibtex
@article{guyot2012,
  author  = {Guyot, Patricia and Ades, A. E. and Ouwens, Mario J. N. M. and Welton, Nicky J.},
  title   = {Enhanced secondary analysis of survival data: reconstructing the data from published
             Kaplan-Meier survival curves},
  journal = {BMC Medical Research Methodology},
  volume  = {12},
  pages   = {9},
  year    = {2012},
  doi     = {10.1186/1471-2288-12-9}
}

@misc{chandler2026survival,
  author       = {Chandler, Conor and Ishak, K. Jack},
  title        = {Surviving Unanchored Indirect Comparisons: An Extension of Multilevel Unanchored
                  Meta-Regression (ML-UMR) for Survival Analyses},
  howpublished = {ISPOR 2026, poster MSR131, Value in Health 29(S6)},
  year         = {2026}
}
```

Note: `guyot2012` is also referenced (as a proposed entry) in Chapter 25's notes; one shared entry suffices.
All other cited keys already exist in `references.bib`: `chandler2025mlumr`, `chandler2026transport`,
`phillippo2019thesis`, `phillippo2020mlnmr`, `phillippo2025general`, `phillippo2016tsd18`, `sobol1967`,
`sklar1959`, `owen1956`, `carpenter2017stan` (and `dias2018nma`, available though not finally cited).

## Proposed notation note (no edit made to notation.qmd)

The chapter uses arm-specific intercepts `\alpha_A, \alpha_B` for the two single-arm sources and
`\boldsymbol\beta_{\mathrm{PF}}` for the shared prognostic slope, matching the proof catalogue's M-notation.
These are defined in-text and reconciled with the book's `\mu_j` (study baseline), `\gamma_k` (treatment
effect), `\boldsymbol\beta_1` (prognostic), `\boldsymbol\beta_{2,k}` (effect modifiers) via
`\alpha_k = \mu + \gamma_k` (conflated, `lem-mlumr-single-arm-conflation`) and
`\boldsymbol\beta_{\mathrm{PF}} = \boldsymbol\beta_1` under SPFA. `SPFA` and `SEMA` already appear in the
notation table. Optional addition for the orchestrator: a one-line glossary entry for `\alpha_A,\alpha_B`
("single-arm conflated arm intercept, ML-UMR") and `\boldsymbol\beta_{\mathrm{PF}}` ("shared prognostic
slope under SPFA"). Not required; everything is defined on first use.

## Decisions and notes

- Mapped the catalogue's loose "SPFA rules out effect modification entirely" to a precise statement:
  in the two-treatment network with the index arm as reference (`\boldsymbol\beta_{2,A}=0`), SPFA is
  `\boldsymbol\beta_{2,B}=0`, hence no EM; `prp-spfa-vs-sema` proves SPFA strictly stronger than SEMA by
  proper set inclusion (a shared nonzero interaction satisfies SEMA, violates SPFA) and proves the
  anchored-cancellation vs unanchored-necessity dichotomy.
- `thm-spfa-relaxation` (M.4) and `thm-mlumr-identifiability` (M.12 case 3) proved via the inverse/implicit
  function theorem: the Jacobian of the subgroup-mean map is the hazard-weighted subgroup moment matrix `M`;
  local identification iff `Z >= d+1` and `rank(M)=d+1`; non-identification (single mean) gives a
  `d`-dimensional solution manifold. This sharpens the catalogue's counting heuristic into a proved
  rank/dimension statement (local identifiability, stated honestly as local).
- `thm-pseudo-ipd-reconstruction` (M.7) proved as exact product-limit inversion in the idealized
  noiseless/known-at-risk case; Guyot's realistic algorithm described in a remark as the noisy/coarse-grid
  version. This is the cleanest defensible theorem; the empirical digitization is acknowledged as a limit.
- `thm-mlumr-tte(e)` (scale misalignment) proved by exhibiting that the conditional RMST contrast is a
  non-constant function of the frailty `r(x)=exp(x'β_PF)` even under SPFA (no EM on log-hazard), so its
  population average depends on the whole target distribution. This is exactly what Ch25 forward-cited.
- `thm-mlumr-stc-equivalence` (M.10): the comparator-population equivalence rests on the exact-calibration
  identity (exponential-family mean matching: at the MLE the fitted aggregate mean equals the observed
  comparator outcome), so ML-UMR's arm-B value at `P_B` is the observed comparator outcome, identical to
  unanchored STC's use of it. Extension to other targets is powered by SPFA (`lem-spfa-absolute-constancy`).
- Empirical poster results (bias/coverage under SPFA violation) are presented strictly as "simulation
  evidence under specified data-generating mechanisms," not theorems, per the manuscript's scope note. The
  qualitative pattern (robust at comparator, fragile at non-comparator targets) is additionally *derived
  analytically* by hand in the worked example Step 6, so the chapter does not rely on the simulations for
  its claims.
- Worked example: fully hand-checkable binary logit case (one binary covariate makes every integral an
  exact two-point sum, no QMC error) plus an exponential-PH survival coda. All numbers verified with a
  calculator script: identification of `\alpha_B` by the monotone solve; comparator-population LOR 0.4706;
  index-population LOR 0.4745; conditional LOR 0.5 (non-collapsibility/attenuation shown); SPFA-violation
  bias 0 at comparator, -0.1814 (about -28%) at index; survival marginal HR 1.500 -> 1.398 -> 1.491 (time
  varying); RMST_A=5.32, RMST_B=4.17, diff 1.15.

## Gaps / items for the consistency pass

1. Merge `guyot2012` and `chandler2026survival` into `references.bib` (entries above). Until merged, these
   two `@`-citations render as `?`.
2. Optional notation-glossary lines for `\alpha_A,\alpha_B,\boldsymbol\beta_{\mathrm{PF}}` (see above);
   not required for correctness.
3. Starred-exercise solutions (`exr-mlumr-identify-alphaB`, `exr-mlumr-rmst-transport`) to be added to
   Appendix F when that appendix is authored.
4. `references.bib` currently has `chandler2025mlumr` with `year = {2026}` and an arXiv 2026 id even though
   the key says 2025 (it is the ISPOR Europe 2025 poster later posted to arXiv in 2026). I cited it as the
   primary ML-UMR reference per the brief; no change made. Flagging only so the harmony pass is aware the
   key/year look mismatched by design.
