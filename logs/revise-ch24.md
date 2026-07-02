# Revision log: Chapter 24, Bayesian Computation and Diagnostics

File: `chapters/part5/24-computation.qmd`. Before: 1122 lines. After: 1610 lines (+488).
Reviewers addressed: `feedback/chatgpt/ch24-computation.md` and `feedback/glm/ch24-computation.md`.

## Running example introduced (the single highest-value addition)

A two-study plaque psoriasis network with a binary PASI 75 outcome: IPD study `AB` (A vs B, per-patient
data, covariates age and severity) and AgD study `BC` (B vs C, arm summaries), target the indirect
`d_AC` contrast. It has exactly one study per contrast, so the heterogeneity `tau` is weakly identified
(prior-dominated funnel). Introduced in the new section `@sec-comp-running` and reused verbatim at every
transition: the funnel (`@sec-comp-param`), which R-hat quantities to check (`@sec-comp-rhat`), the
2D `BC` covariate integral (`@sec-comp-integration`), the pointwise-unit question (`@sec-comp-ic`), the
influential-study `k-hat` (`@sec-comp-psis`), the workflow summary table, and the worked-example framing.

## New labeled environments added (5; nothing removed or renamed)

- `#sec-comp-hmc-primer` "The sampler in one page: HMC, NUTS, warmup, and divergences" (GLM highest-value
  + ChatGPT highest-priority #1).
- `#sec-comp-running` "A running example: a two-study evidence network".
- `#sec-comp-workflow` "How to use this chapter in practice: a diagnostic workflow" (ChatGPT
  highest-priority #3 and #4).
- `#exr-comp-read-table` and `#exr-comp-classify`, two warm-up interpretation exercises before the
  proof-heavy ones (both reviewers asked for a "read a Stan table in words" exercise first).

## New tables added (6)

1. HMC/NUTS/warmup/divergence glossary table (`@sec-comp-hmc-primer`).
2. Two-regime neck/mouth curvature map after `@thm-comp-param`.
3. AR(1) phi / tau_int / efficiency / N_eff table after `@exm-comp-ar1`.
4. Diagnostic stoplight table (detects / threshold-action) in `@sec-comp-workflow` (chapter-specific
   guidance + ChatGPT stoplight ask).
5. DIC/WAIC/LOO scorecard table after `@thm-dic-waic-loo`.
6. Realistic Stan summary table (mean, sd, bulk/tail N_eff, R-hat, with a flagged tau row) in the
   workflow section, interpreted in HTA language (odds ratio, refit action).

## Intuition additions after definitions/lemmas (7 reader-translation remarks)

After `@def-centered-noncentered`, `@lem-comp-reparam` (diffeomorphism/change-of-variables/Jacobian in
words), `@def-comp-rhat-pieces`, `@def-mcmc-ess`, `@def-integration-error-monitoring` (plus near-zero /
transformed-scale caution), `@def-comp-criteria`, `@def-psis-loo` (what is smoothed; shape k as tail
heaviness). Plus the "What is an observation in ML-NMR?" remark in `@sec-comp-ic` (ChatGPT
highest-priority #2: pointwise unit is a patient for IPD, an arm-cell for AgD).

## "Why this matters" additions (7)

Pre-lemma motivation for `@lem-comp-leapfrog-stability` (why a page on a harmonic oscillator earns its
place); "Why this matters, and a map of the two regimes" after `@thm-comp-param`; "Why this matters, and
the three ways R-hat fails" after `@thm-gelman-rubin`; ITC message after the AR(1) table; "Why not just
use a huge grid?" (cost sits inside the likelihood) after the integration budget remark; "Why this
matters, and a scorecard" plus "Comparison is not checking" after `@thm-dic-waic-loo`; "Why this matters:
an influential study in the running network" after `@thm-comp-psis-reliability`.

## Inline jargon glosses (define-at-first-use)

MCMC/HMC/NUTS/leapfrog/step size/mass matrix/warmup/typical set/divergent transition (primer); leapfrog
integrator restated inline before `@lem-comp-leapfrog-stability`; `c_j = 0` explained (flat likelihood =>
small second derivative) in `@lem-comp-funnel`; "second-order stationary" defined at first use in
`@lem-comp-within`; Hardy-Krause variation and star discrepancy glossed in `@sec-comp-integration`; the
`Psi` transform put "in words"; "observed information" tied to Fisher information; "cumulant generating
function"/"cumulant"/"third cumulant" defined in a strategy paragraph before the `@thm-dic-waic-loo`
proof; "self-normalized" importance sampling glossed in the `@lem-comp-loo-identity` proof; strategy
paragraph added before the `@lem-comp-loo-identity` proof.

## Reordering / forward-reference fixes

- Added a "bottom line first" statement of R-hat = sqrt(V-hat/W) and its plain reading at the top of
  `@sec-comp-rhat` (GLM suggestion 5: punchline before the proof), without moving the labeled theorem.
- The forward reference to `@prp-comp-acf-variance` inside the `@thm-gelman-rubin` proof now carries an
  explicit signpost that it is proved independently in `@sec-comp-ess` with no circular dependence (GLM
  suggestion 6). I did NOT physically move the proposition, to avoid disturbing the labeled structure.
- Opened `@sec-comp-param` with the funnel picture (trumpet-bell prose) before any algebra (both
  reviewers; GLM suggestion 1). No figure asset was added: a plot was requested but I used vivid prose +
  the neck/mouth table to keep the pdflatex build safe (image/TikZ assets are risky and the orchestrator
  renders). Noted here as the one reviewer ask deliberately met by substitution.

## Points deliberately not done (with reasons)

- GLM suggestion 9 asked to SPLIT `@thm-dic-waic-loo` into two theorems. Preserved as one theorem
  (hard constraint: never remove/rename a label). Instead added the strategy/vocabulary paragraph, the
  scorecard, and the "why this matters" bridge to reduce its density.
- No new `@bibkey` citations introduced. Neal, Vehtari, Watanabe, Geyer, Stan already appear by name in
  the Notes section; only `@carpenter2017stan`, `@phillippo2020mlnmr`, `@phillippo2016tsd18` exist in
  `references.bib` for this material, and the chapter does not cite `@phillippo2016tsd` (no fix needed).

## Preservation and build safety confirmed

- All original labels preserved: 30 original labeled environments intact, 32 now (+2 exercises); the 3
  new section ids and 2 new exercise ids are unique across the book. Every existing theorem, lemma,
  proof, definition, corollary, proposition, equation label, and example is unchanged; only additive
  scaffolding was inserted.
- Div-fence depth balanced (0). No em/en dash, en dash, spaced-hyphen connector, double hyphen, or
  Unicode math glyph; star marker is `$\star$`. No bare align/equation/gather inside `$$`. Blank line
  precedes each new `#sec-` heading. American English throughout.
