# Work log: Appendix E (Reference Implementations: multinma, mlumr, uitc)

## Scope and deliverable

Overwrote `appendices/E-reference-implementations.qmd` (was a stub) with the complete appendix. This is a
reference appendix (per STYLE.md rule 6, reference material, not proofs): precise prose + mapping tables +
minimal code, bridging the book's mathematics to the three reference R packages. Wrote this log. Did not
touch `_quarto.yml`, `notation.qmd`, `references.bib`, or any chapter/other appendix.

## Structure

- E.1 Purpose and scope (correspondence principle; version caveat in a `.remark` div).
- E.2 `multinma` (ML-NMR): pipeline table (`set_ipd`, `set_agd_arm`, `set_agd_contrast`, `set_agd_surv`,
  `combine_network`, `add_integration`, `nma`); aggregation integral (with the load-bearing Stan excerpt
  from `binomial_1par.stan` and the adjusted-binomial n'/p' from `binomial_2par.stan`); QMC integration
  (`add_integration` arg table); target-population estimand (`relative_effects` / `predict` /
  `marginal_effects`); object-to-code map; Stan model file table.
- E.3 `mlumr` (ML-UMR): pipeline; SPFA vs relaxed (with Stan excerpt of the comparator AgD aggregation
  integral); benchmarks `naive` and `stc`; survival (`set_agd_surv`, KM reconstruction, RMST/loghr);
  object-to-code map; Stan file naming scheme.
- E.4 `uitc`: `uitc()` dispatcher; MAIC (Ch 18); STC + doubly-robust `dr_estimator()` (Ch 19, Ch 10);
  QBA (Ch 28: E-value, NORTA, tipping point, probabilistic, classical); comparator distance (Ch 27);
  object-to-code map.
- E.5 Using the three together (decision table + name-collision note).
- E.6 Notes and references.

## Sources consulted

- `~/Documents/GitHub/multinma`: `README.md`, `NAMESPACE` (exports + S3 methods), `vignettes/vignette_overview.Rmd`,
  `R/nma.R` and `R/integration.R` (signatures), `man/{set_ipd,set_agd_arm,set_agd_surv,combine_network,
  relative_effects,predict.stan_nma,marginal_effects}.Rd` (usage), and Stan files
  `inst/stan/{binomial_1par,binomial_2par,survival_param}.stan` + `include/transformed_parameters_common.stan`.
  Confirmed: `binomial_1par.stan` uses `agd_arm_r ~ binomial(agd_arm_n, theta_agd_arm_bar)` with
  `theta_agd_arm_bar = mean(...)`; `binomial_2par.stan` adds the moment-matched n'/p' adjusted binomial.
  Confirmed `add_integration` uses `randtoolbox::sobol` + Gaussian copula with `cor_adjust`
  (spearman/pearson/none/legacy).
- `~/Documents/GitHub/mlumr`: `README.md`, `NAMESPACE`, `vignettes/introduction.Rmd`,
  `man/{set_ipd,set_agd,set_agd_surv,combine_data,add_integration,mlumr,stc,naive,marginal_effects,
  predict.mlumr_fit,conditional_effects}.Rd`, and Stan files `inst/stan/mlumr_binary_{spfa,relaxed}.stan`.
  Confirmed SPFA = single shared beta; relaxed = beta_index/beta_comparator with reported
  `delta_beta`; AgD likelihood = `binomial(n_agd[k], mean(p_int))`; generated quantities compute
  marginal lor/rd/rr in index (IPD) and comparator (integration-point) populations.
- `~/Documents/GitHub/uitc`: `README.md`, `NAMESPACE`, `R/{uitc.R,dr.R}` (dispatcher + DR internals),
  `man/{uitc,dr_estimator,maic_unanchored,estimate_weights,prepare_maic,balance_table,
  qba_unmeasured_itc,qba_tipping_itc,qba_prob_itc,confounders_evalue,probsens}.Rd`. Confirmed `uitc()`
  dispatches maic/stc/mlumr/naive/dr; `dr_estimator()` augments MAIC/IOW weighting with a G-computation
  outcome model (double robustness) and uses NORTA for the comparator profile.

## Citations used (all verified present in references.bib)

`@phillippo2020mlnmr`, `@chandler2025mlumr`, `@carpenter2017stan` (required), plus `@phillippo2025general`,
`@signorovitch2010maic`, `@caro2010stc`, `@vanderweele2017evalue`, `@lash2021qba`, `@sobol1967`,
`@sklar1959`, `@guyot2012`. All 11 confirmed by grep against `references.bib`.

## Cross-references

Used 71 distinct `@thm-/@eq-/@def-/@lem-/@cor-/@prp-/@sec-` references into Chapters 18, 19, 20, 22, 23,
26, 27, 28. Verified programmatically that every one resolves to a `#slug` defined in `chapters/` (script:
compare used refs against all defined slugs; result "All cross-references resolve."). All of the appendix's
own section anchors are namespaced `#sec-impl-*` and equation labels `#eq-impl-*` to avoid collision.

## New notation

None. The appendix reuses notation.qmd symbols only ($\eta_{ijk}$, $g^{-1}$, $\theta_{ijk}$, $f_j$,
$\bar{\mathbf{x}}_j$, $\boldsymbol{\Sigma}_j$, $d_{ab(\mathcal{P})}$, ESS, SPFA, $\Omega$, $\Phi$). Two new
local equation labels introduced for self-contained restatement (`@eq-impl-mlnmr-model`,
`@eq-impl-aggregation`, `@eq-impl-adjusted-binomial`, `@eq-impl-qmc`); these duplicate, in the appendix's
own namespace, results already proved in Chapters 20/22 and are cross-referenced back to the originals.

## Proposed bib entries (gaps for the orchestrator)

Two methods are described in the appendix but their primary sources are NOT yet in `references.bib`. I
deliberately did NOT cite undefined keys (would render as `??`); instead I referenced the book's own
theorems for these methods. If the orchestrator wants direct attribution, add:

1. `uitc`'s `dr_estimator()` (doubly-robust augmented weighting, "DRAWE"). `R/dr.R` attributes it to
   "Remiro-Azocar et al. 2025". Candidate key `@remiroazocar2025drawe`:
   Remiro-Azocar A, et al. (2025). Doubly robust augmented weighting estimators for
   population-adjusted indirect comparisons / externally controlled single-arm trials. (Verify exact
   title/venue.) Currently I map DR to Chapter 10 (AIPW) + @thm-maic-exponential-weights + @prp-stc-gcomp.
2. `uitc`'s `qba_unmeasured_itc()` (NORTA-based ITC QBA). README attributes it to "Ren, Y. (2025).
   Sensitivity analysis for unmeasured confounding in indirect treatment comparisons via the NORTA
   copula (in preparation)." Candidate key `@ren2025norta`. Currently I map it to @thm-norta-copula and
   @eq-qba-norta in Chapter 28.

## Decisions

- Treated the appendix as a "map, not a tutorial": at most one short workflow code block per package plus
  two load-bearing Stan excerpts (the aggregation-integral lines), since those lines literally *are* the
  mathematical object @thm-aggregation / @eq-mlumr-model-agg.
- Used named arguments in `distr()` examples (`mean=`, `sd=`, `prob=`) to match the packages' documented
  usage exactly.
- Verified absence of dash punctuation connectors and em/en dashes (grep clean). American English used.

## Gaps left for review

- The two missing bib keys above (DRAWE / Ren NORTA). No undefined keys were emitted into the qmd.
- Function signatures were read from the current source; the appendix states the version caveat in a
  remark. Orchestrator's consistency pass should re-confirm signatures if packages are bumped.
- No machine-checked tags added (reference appendix; no theorems owned).
