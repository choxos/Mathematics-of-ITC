# Work log: Chapter 28, Quantitative Bias Analysis for Indirect Comparisons

Author agent: Opus 4.8. Part VI, this wave. File overwritten:
`chapters/part6/28-qba.qmd` (stub callout dropped, YAML title kept).

## Status

Complete. Motivating intro, full development with complete proofs, one fully worked hand-checkable
example, Notes and references, and seven exercises (two starred for Appendix F). All cross-references and
equation labels verified to resolve against `chapters/`. No prohibited dash punctuation; American
spelling; no Unicode dashes or smart quotes.

## Sources consulted

- **`itc_courses/Unanchored_ITC_and_Bias_Analysis_with_uitc/`** lessons (lesson.yaml):
  - `10_QBA_Confounding_and_the_E_value` — confounding bias factor `(p1(RR-1)+1)/(p0(RR-1)+1)`;
    Ding-VanderWeele bias factor `BF = RR_eu RR_ud/(RR_eu+RR_ud-1)`; E-value quadratic
    `E^2/(2E-1)=RR_obs` giving `E = RR + sqrt(RR(RR-1))`.
  - `11_QBA_Selection_Misclassification_Probabilistic` — selection/misclassification corrections (mentioned
    in passing in the framework section); systematic vs total interval; valid-fraction discarding.
  - `12_QBA_for_ITC_Unreported_Covariates` — unanchored estimand, g-computation, NORTA imputation,
    Gaussian copula with IPD-borrowed dependence; the FIXTURE/psoriasis validation narrative.
  - `13_QBA_for_ITC_Tipping_Point_and_E_value` — probabilistic ITC QBA (systematic vs total),
    tipping point via root-finding, ITC E-value `rr_eu = BF(rr_ud-1)/(rr_ud-BF)`, the infinite-certificate
    special case `rr_ud <= BF`.
- **`uitc/R/`** source:
  - `qba_confounders.R` — `confounders()` bias-factor implementation (basis of @lem-qba-confounding-factor).
  - `qba_itc_core.R` — family-aware STC marginalization, `stc_marginal`, `predict_natural`.
  - `qba_itc_copula.R` — `simulate_agd_copula` (NORTA), `spearman_to_normal_pearson`
    (`2 sin(pi rho/6)`), `regularize_correlation` (nearest-correlation repair). Basis of @thm-norta-copula,
    @lem-qba-spearman-matching, and the PD-projection remark.
  - `qba_itc_tipping.R` — `standard_evalue_from_ratio`, `itc_evalue_from_parts` (the exact three-case
    formula in @eq-qba-itc-evalue, including the `Inf` branch), `find_crossing` (root-finding).
  - `qba_itc_prob.R` — `qba_prob_itc`, systematic vs total intervals, `benefit_probability`. Basis of
    @def-probabilistic-bias-analysis and @thm-qba-pba-convergence.
- **`documentation/refs/qba/markdown/`** — Fox, MacLehose, Lash, *Applying Quantitative Bias Analysis to
  Epidemiologic Data*, 2nd ed. (Springer, 2021) = `@lash2021qba`. Used for the bias-triangle framework and
  the probabilistic systematic/total decomposition.
- **`ITC_Coq/manuscript/`** — confirmed there is no QBA chapter; this chapter is new material.
- **`chapters/part5/22-mlnmr-integration.qmd`** — confirmed the exact statements/labels of
  `@thm-inverse-cdf`, `@eq-qmc-galois`, `@def-copula`, `@thm-sklar`, `@def-gaussian-copula`,
  `@prp-gaussian-copula-is-copula`, which the NORTA proof reuses.
- **`chapters/part4/18-maic.qmd`** — voice/structure model.

## Proof catalogue identifiers

None. This chapter is explicitly new material ("Ch 28 ... new (E-value, NORTA, tipping point)" in the
STYLE.md assignment table) and has no catalogue entry and no `ITC_Coq` machine-checked counterpart. The
Notes section states this accurately; no `[machine-checked:]` tags were added.

## Slugs defined

Owned (from the assignment): `def-quantitative-bias-analysis`, `thm-evalue-derivation`, `def-itc-evalue`,
`def-tipping-point`, `thm-norta-copula`, `def-probabilistic-bias-analysis`.

Supporting (new, namespaced `qba`/`itc`/`evalue`; verified globally unique, count = 1 each):
`lem-qba-confounding-factor`, `lem-qba-sharp-bound`, `prp-itc-evalue`, `lem-qba-spearman-matching`,
`prp-qba-tipping-monotone`, `thm-qba-pba-convergence`.

Exercises: `exr-qba-evalue-compute`, `exr-qba-protective`, `exr-qba-itc-evalue-star` (★),
`exr-qba-sharp-bound-binary`, `exr-qba-norta-margins-star` (★), `exr-qba-tipping-monotone`,
`exr-qba-pba-prior`. Starred two: `exr-qba-itc-evalue-star`, `exr-qba-norta-margins-star`.

Sections: `sec-qba-intro`, `sec-qba-framework`, `sec-qba-evalue`, `sec-qba-itc-evalue`, `sec-qba-norta`,
`sec-qba-tipping`, `sec-qba-probabilistic`, `sec-qba-example`, `sec-qba-notes`, `sec-qba-exercises`.

Equations: `eq-qba-correction`, `eq-qba-bias-factor`, `eq-qba-sensitivity-params`, `eq-qba-bf`,
`eq-qba-b-ratio`, `eq-qba-b-ab`, `eq-qba-evalue`, `eq-qba-unanchored-estimand`, `eq-qba-itc-evalue`,
`eq-qba-norta`, `eq-qba-norta-joint`, `eq-qba-spearman-transform`, `eq-qba-tipping`.
(Note: two labels initially used an uppercase `B`; renamed to lowercase `eq-qba-b-ratio`/`eq-qba-b-ab` for
Quarto crossref compatibility.)

## Cross-references into sibling chapters (all verified to resolve)

`@thm-bucher-unbiased` (14); `@def-effect-modifier` (11); `@thm-sema-insufficient`,
`@def-conditional-constancy-absolute`, `@thm-unanchored-paic-consistency` (17); `@def-transportability`
(12, in prose); `@thm-inverse-cdf`, `@eq-qmc-galois`, `@thm-sklar`, `@def-gaussian-copula`,
`@prp-gaussian-copula-is-copula` (22). Chapters 19, 26, 27 referenced in prose only (27 is a sibling stub
this wave; avoided `@`-slug references to it).

## Proposed bibliography additions (not in `references.bib`; for the orchestrator to merge)

The chapter currently cites only keys already present (`@lash2021qba`, `@vanderweele2017evalue`,
`@sklar1959`). Prose attributions were written for the following sources without a `@key`; adding these
keys and converting the attributions would tighten the citations:

- `ding2016sensitivity` — Ding P, VanderWeele TJ. "Sensitivity Analysis Without Assumptions."
  *Epidemiology*. 2016;27(3):368-377. (The sharp bias-factor bound proved in @lem-qba-sharp-bound; I prove
  it in full but attribute it in prose to "Ding and VanderWeele".)
- `cario1997norta` — Cario MC, Nelson BL. "Modeling and Generating Random Vectors with Arbitrary Marginal
  Distributions and Correlation Matrix." Technical Report, Dept. of IE/MS, Northwestern University, 1997.
  (The NORTA method named in @thm-norta-copula.)
- `nelsen2006copula` — Nelsen RB. *An Introduction to Copulas*, 2nd ed. Springer, 2006. (Arcsine law for
  the grade correlation of the Gaussian copula, used in @lem-qba-spearman-matching.)
- `schlesselman1978` — Schlesselman JJ. "Assessing Effects of Confounding Variables." *Am J Epidemiol*.
  1978;108(1):3-8. (The binary-confounder bias factor of @lem-qba-confounding-factor; attributed in
  prose.)
- `ren2025` (exact citation to confirm) — Ren and colleagues, 2025, the QBA framework for covariates
  measured in IPD but unreported by the comparator in unanchored ITC; the basis of @def-itc-evalue and the
  `uitc`/`mlumr` implementation. Currently attributed in prose as "Ren and colleagues, 2025". The course
  lessons cite "Ren et al. (2025)"; full bibliographic details should be confirmed before adding the key.

## Proposed notation additions (for `notation.qmd`)

Symbols introduced here, consistent with the existing scheme; flagged for folding in:

- `U` — unmeasured (confounding sense) or unreported (ITC sense) scalar covariate, distinct from the
  measured covariate vector `x`.
- `b` (bold lowercase) in `B` — bias-parameter vector `b ∈ 𝓑`; `B(b)` bias function; `h(θ̂_obs, b)`
  the QBA correction.
- `E` (plain italic) — the E-value; deliberately distinguished from `𝔼[·]` (expectation).
- `RR_obs, RR_true, RR_crude, RR_adj` — observed/true/crude/adjusted risk ratios; `BF_U` confounding bias
  factor; `RR_EU, RR_UD` the two E-value sensitivity parameters.
- `E_ITC` — indirect-comparison E-value; `BF_obs` — observed (ITC) bias factor.
- `Δ(m)` — sensitivity curve in the assumed comparator marginal `m`; `m†` tipping point;
  `[m_lo, m_hi]` plausible range.
- `ρ^S, ρ^N` — Spearman and Gaussian-copula (Pearson) correlations, with transform
  `ρ^N = 2 sin(π ρ^S / 6)`.
- `G_sys, G_tot` — systematic and total PBA distributions; `P̂_ben` — probability of benefit.

## Decisions and gaps

- **Worked example design.** Chose a log link, independence copula, and normal margins so the
  marginalization @eq-qba-unanchored-estimand reduces to the normal MGF and the sensitivity curve becomes
  affine, `Δ(m) = 0.300 − 0.5 m`. This makes the E-value, tipping point, ITC E-value (both the infinite
  certificate and the finite formula), and probabilistic interval all exactly hand-checkable. Every number
  in @sec-qba-example was recomputed and verified. The deliberate cost is that the general NORTA
  marginalization is not closed-form; this is stated.
- **Standardization in @lem-qba-sharp-bound.** Proved the sharp bound for the effect-on-treated
  standardization (cleanest exact derivation; bias factor = ratio of the unexposed-risk function averaged
  over the two confounder distributions). The same bound for total-population standardization is stated
  and attributed to @vanderweele2017evalue rather than reproved. The full vertex + two-cell optimization
  is given for general categorical `U`, so the owned theorem is complete.
- **Arcsine law cited not proved.** @lem-qba-spearman-matching proves rank-correlation invariance under
  the marginal transforms in full, but takes the Gaussian-copula identity `ρ^S = (6/π) arcsin(ρ^N/2)` as a
  classical fact (proposed `nelsen2006copula`). A full derivation is a self-contained bivariate-normal
  geometry exercise, deemed out of scope per STYLE rule 6 (cite standard prerequisites).
- **Discrete-margin caveat.** @thm-norta-copula(2) (copula uniqueness) is proved for continuous margins;
  the binary-`U` case is handled honestly in a remark (marginal recovery still exact; copula non-unique;
  PD repair needed), and `exr-qba-norta-margins-star` asks the reader to construct the failure.
- **No machine-checked tags.** Verified against `ITC_Coq/manuscript` that no QBA material exists; the
  chapter says so explicitly. If a future Coq development adds, e.g., the E-value quadratic or the NORTA
  marginal-recovery lemma, tags can be added in the harmony pass.
