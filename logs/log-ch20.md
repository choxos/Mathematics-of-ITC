# Work log: Chapter 20, Multilevel Network Meta-Regression I: The Aggregation Principle

Author pass by the Ch20 agent. File written: `chapters/part5/20-mlnmr-aggregation.qmd` (stub removed, YAML
title preserved). First chapter of Part V. Chapter length about 6,500 words; 8 proved results (3 owned
catalogue theorems plus the identity-link converse, 2 supporting lemmas, 1 probit proposition, and the
two-part aggregation/likelihood theorem), 2 definitions, 2 fully worked numerical examples (the logit
discrete-covariate example is the headline; the log-Gaussian example is a second worked computation), 8
exercises (2 starred for Appendix F).

## Sources consulted

- `~/Documents/GitHub/ITC_Coq/proofs/H_ml_nmr.md` (catalogue H.1 to H.7): the base draft. Every sketch was
  expanded into a complete proof in the book's notation. H.1, H.2 became definitions; H.3 became the
  aggregation theorem with three proved parts; H.4 the aggregation-bias theorem plus a leading-order
  expansion lemma; H.5 identity-link exactness (proved in full generality, plus a converse); H.6 the
  log-link MGF closed form; H.7 the logit non-elementarity, restated and corrected (see Decisions).
- `~/Documents/GitHub/ITC_Coq/manuscript/10_ml_nmr.md` (companion prose, Sections 10.1 to 10.8 and 10.24):
  used for narrative framing (the "individual model integrated over the covariate distribution" viewpoint,
  the four-aims list, the three-link organization) and for the confirmation in 10.24 that the Coq
  development does not formalize ML-NMR.
- `~/Documents/GitHub/ITC_Coq/theories/` directory listing: confirmed there is NO `ML_NMR.v` or analogous
  file. Files present: Axioms, BalancingScore, BasicTypes, Bucher, CausalAssumptions, Comparison,
  ConditionalIndep, DoublyRobust, EffectModifiers, IPWEstimator, MAIC, OutcomeRegression, PotentialOutcomes,
  PropensityScore, STC. Hence NO machine-checked tags in this chapter, consistent with manuscript 10.24.
- Sibling chapters read for exact slugs, statements, and voice:
  - `chapters/part1/04-probability.qmd`: `@thm-jensen` (A.7, with the strict case and the explicit "the gap
    will be aggregation bias" foreshadowing), `@def-mgf`, `@thm-mgf-sum`, `@thm-mgf-uniqueness`,
    `@def-mvn` / `@eq-mvn-mgf` (Gaussian MGF), `@thm-mvn-linear` (affine image), `@thm-cov-psd`,
    `@thm-fubini-tonelli` (A.10), `@cor-total-expectation` (tower, A.9), `@def-poisson-binomial`.
  - `chapters/part1/07-glm.qmd`: `@def-link-function` (link is C^2 strictly monotone, used in the
    identity-link converse), `@def-non-collapsibility`.
  - `chapters/part1/08-hierarchical-bayes.qmd`: `@def-random-effects`, `@def-exchangeability`.
  - `chapters/part2/11-effect-modification-collapsibility.qmd`: `@def-effect-modifier`.
  - `chapters/part3/16-limits-of-nma.qmd`: `@def-ecological-bias` / `@eq-ecological-bias` (sign convention
    EB = plug-in minus integrated, matched exactly), `@thm-failure-of-bucher`, and crucially
    `@lem-limits-probit-integral` / `@eq-limits-probit-integral` (the Gaussian probit integral, reused for
    the probit closed form `@prp-agg-probit-closed-form`).
  - `chapters/part4/17-population-adjustment-theory.qmd`: `@def-sema`, `@thm-target-population-estimand`.
  - `chapters/part4/18-maic.qmd`: voice/structure model; `@thm-maic-exponential-weights` and the
    first-moment-matching/identity-scale remark cross-referenced.
  - `chapters/part4/19-stc.qmd`: `@thm-marginal-stc-unbiased` (STC's plug-in is the same naive aggregation),
    and the second-order-Taylor proof style for the bias expansion lemma.
- `notation.qmd` and `logs/STYLE.md` for the authoring contract; `logs/log-ch19.md` for cross-chapter
  conventions and the proposed-notation status format.
- Citations used (all keys verified present in `references.bib`): `@phillippo2020mlnmr`,
  `@phillippo2019thesis`, `@owen1956` (probit integral provenance), `@sklar1959`, `@sobol1967` (forward
  pointers to Chapter 22's machinery). No new bibliography entries required for this chapter.

## Catalogue coverage (owns H.1 to H.7)

- H.1: `@def-individual-model` (`@eq-agg-individual-model`). The network individual-level GLM with study
  baseline, prognostic `beta_1`, effect-modifier `beta_{2,k}`, treatment effect `gamma_k`, reference
  constraints, and the total slope `beta_{tot,k} = beta_1 + beta_{2,k}`. Remark connects the four terms to
  their causal roles and to SEMA (`@def-sema`).
- H.2: `@def-aggregate-model` (`@eq-agg-aggregate-mean`). The aggregate mean as the integral of the inverse
  link against `f_j`; the "integrate the response scale, not the link scale" remark.
- H.3: `@thm-aggregation`. Expanded from a one-line sketch into a three-part theorem with full proofs:
  (a) marginal individual likelihood via chain rule + Tonelli (`@eq-agg-marginal-likelihood`); (b) the
  headline aggregate-mean identity `E[Y] = theta_bullet` via the tower property (`@eq-agg-mean-identity`);
  (c) conditional-independence factorization of the aggregate likelihood (`@eq-agg-aggregate-likelihood`),
  with the `pi_Agg` summary-likelihood step.
- H.4: `@thm-aggregation-bias` (`@eq-agg-bias`, `@eq-agg-eb`) plus `@lem-agg-bias-expansion`
  (`@eq-agg-bias-expansion`). Jensen on `g^{-1}` for the qualitative sign and exact equality conditions
  (affine link or degenerate linear predictor, the latter = `beta_tot' Sigma_j beta_tot = 0`); the lemma
  gives the second-order Taylor expansion with Lagrange-remainder bound, leading bias
  `(1/2)(g^{-1})''(m) v`. Explicitly identified as the resolution of `@thm-failure-of-bucher` and the
  ecological bias of `@def-ecological-bias`.
- H.5: `@thm-identity-link-exact` (`@eq-agg-identity`). Proved for EVERY covariate distribution (not only
  Gaussian) by linearity, plus a converse: a link exact for all covariate laws on an open set must have
  affine `g^{-1}` there (midpoint-affine + continuity from `@def-link-function`).
- H.6: `@thm-log-link-mgf` (`@eq-agg-log-mgf`). Proved via `@thm-mvn-linear` (eta is Gaussian) and the
  scalar Gaussian MGF `@eq-mvn-mgf` at t = 1. The exact multiplicative plug-in bias `e^{v/2}` is read off
  and reconciled with both `@thm-aggregation-bias` and `@lem-agg-bias-expansion`.
- H.7: `@thm-logit-no-closed-form` (`@eq-agg-logit-integral`). Structural facts proved in full:
  (a) reflection `J(m,tau) = 1 - J(-m,tau)` hence `J(0,tau) = 1/2` exactly (no bias at the symmetric point);
  (b) strict monotonicity in m; (c) leading-order bias sign (plug-in underestimates for m < 0, overestimates
  for m > 0). Part (d), absence of an elementary closed form, is explained rather than proved from an
  impossibility theorem (see Decisions), with an honest delineating remark.

## Auxiliary results introduced (new slugs, `agg-` namespaced; globally unique, verified)

- `@lem-agg-bias-expansion`: leading-order aggregation bias (supports H.4, the worked examples, H.7(c)).
- `@lem-agg-heat-flow`: the aggregate mean under Gaussian covariates is the heat semigroup
  `e^{(tau/2) d^2/dm^2}` applied to `g^{-1}`, solving `du/dtau = (1/2) d^2u/dm^2` with initial data
  `g^{-1}`. Unifies H.5/H.6/H.7 and the probit case as one object; not in the catalogue or manuscript.
- `@prp-agg-probit-closed-form`: the probit aggregate mean `Phi(m/sqrt(1+tau))`, reusing
  `@lem-limits-probit-integral`; the foil that explains why logit has no closed form.
- `@exm-agg-logit-discrete`, `@exm-agg-log-gaussian`: the two worked examples.
- Exercises `@exr-agg-prevalence` (starred), `@exr-agg-identity-uniqueness` (starred),
  `@exr-agg-log-multiplicative`, `@exr-agg-heat-verify`, `@exr-agg-second-moment`, `@exr-agg-correlated`,
  `@exr-agg-nma-reduction`, `@exr-agg-jensen-gap-bound`.

## Decisions

1. **Corrected the catalogue's H.7 claim.** The catalogue (and manuscript 10.8) state that "expit(eta) has
   no antiderivative in elementary functions." This is false: the indefinite integral of expit is the
   elementary softplus `log(1 + e^z)`. The true obstruction is the GAUSSIAN-WEIGHTED integral (the
   logit-normal mean). The chapter states the corrected version and isolates the obstruction explicitly,
   contrasting with the probit case where the analogous Gaussian-weighted integral IS elementary
   (`@prp-agg-probit-closed-form`, via `@lem-limits-probit-integral`).
2. **H.7(d) non-elementarity is explained and cited, not proved.** A Liouville/Risch impossibility proof is
   out of scope, and no named impossibility theorem in `references.bib` covers the logit-normal integral. I
   prove the structural facts (a) to (c) in full and state (d) as a known fact (`@phillippo2020mlnmr`) with
   an explanatory argument (the Gaussian-weight obstruction; the probit contrast). A dedicated remark labels
   precisely what is proved versus cited. This is the intended reading of the deliverable's "(H.7,
   explain)".
3. **Added the heat-flow lemma** as the structural backbone unifying the three links: identity is the fixed
   point (`psi'' = 0`), log is the exponential orbit (`e^{m+tau/2}`), probit maps to a rescaled probit, logit
   has no elementary flow. This is a genuine addition beyond the catalogue and gives the cleanest account of
   why log and probit keep closed forms (their inverse links are stable under Gaussian convolution) while
   logit does not.
4. **H.3 stated with the aggregate-mean identity as the headline** (part b), since the deliverable phrases
   H.3 as "the aggregate mean is the integral of the inverse link against the covariate density"; the
   likelihood identity (a) and factorization (c) accompany it.
5. **Deferred discrete-outcome and numerical-integration content** (catalogue H.8 to H.19) to Chapters 21
   and 22 as assigned, mentioning only `pi_Agg` and `@def-poisson-binomial` in passing so Chapter 20 stays
   focused on the aggregation principle.
6. **Worked example design.** The headline example uses a binary (two-point) covariate so the logit integral
   is a finite sum, hand-checkable to 5 dp, and uses two arms to exhibit the sign reversal of the logit bias
   and the clean identity that the plug-in marginal log-OR equals the conditional-at-the-mean
   `gamma_B + beta_2 x-bar`. All numbers were recomputed to 5 dp; the integrated marginal log-OR is
   1.22000 versus the naive 1.30000 (ecological bias 0.08000 on the log-odds scale, OR inflation 1.0833).
   The probit-substitution constant was corrected to `kappa = sqrt(pi/8) ~ 0.6267` (origin-slope match).

## Proposed notation additions (for the orchestrator to fold into `notation.qmd`)

`notation.qmd` already supplies `g`, `g^{-1}`, `eta_{ijk}`, `theta_{ijk}`, `mu_j`, `beta_1`, `beta_{2,k}`,
`gamma_k`, `f_j`, `F_j`, `x-bar_j`, `Sigma_j`, `L_i`, `bar L_j`, `xi`, `d_{ab(P)}`. This chapter introduces,
consistently with that scheme, the following, which I recommend adding:

- `eta_{jk}(.)`: the linear predictor as a FUNCTION of the covariate vector, with
  `eta_{ijk} = eta_{jk}(x_{ijk})`. (notation lists only the indexed scalar `eta_{ijk}`.)
- `theta_{bullet jk}`: the aggregate-level (covariate-averaged) mean outcome on arm k of study j; the bullet
  subscript denotes averaging over individuals.
- `theta^{naive}_{bullet jk}`: the plug-in aggregate mean `g^{-1}(eta_{jk}(x-bar_j))`.
- `beta_{tot,k} = beta_1 + beta_{2,k}`: the total covariate slope on arm k.
- `EB_{jk}`: the ecological/aggregation bias `theta^{naive} - theta_bullet` (matches `@def-ecological-bias`).
- `pi_Ind`, `pi_Agg`: the individual-level and aggregate-level outcome families.
- `expit(z) = e^z/(1+e^z)`: the standard logistic / inverse-logit (notation already has logit implicitly via
  `g`; expit is used heavily here).
- `J(m,tau)`: the logit-normal integral (the logit aggregate mean under Gaussian eta).

These are local introductions in the chapter and do not conflict with any existing symbol; folding them into
`notation.qmd` is optional but would help Chapters 21 to 26, which reuse `theta_bullet`, `beta_{tot}`, and
`expit`.

## Gaps left for review

- **Machine-checked tags: none.** Confirmed no `theories/ML_NMR.v`. If a future formalization of the
  aggregation identity `@thm-aggregation` is added (it is one application of chain rule + Fubini + tower,
  all available in the probability libraries), a tag could be attached then.
- **H.7(d) citation.** The non-elementarity of the logit-normal integral is cited to the ML-NMR literature
  (`@phillippo2020mlnmr`) and explained; if the harmony pass wants a special-functions citation for the
  logit-normal mean, one could be added to `references.bib` (none currently present).
- **Forward references.** The chapter points to Chapter 21 (discrete outcomes, `pi_Agg`, Poisson binomial),
  Chapter 22 (copulas, Sobol', Koksma-Hlawka), Chapter 23 (target populations, identifiability,
  NMA/IPD-NMR reduction), and Chapter 26 (ML-UMR). These chapters must define the slugs they own; Chapter 20
  only refers to them in prose, never via `@`-cross-reference, so there are no dangling links.
- **Notation folding.** The proposed additions above are used in-chapter without waiting on `notation.qmd`;
  the orchestrator should reconcile during the consistency pass.
