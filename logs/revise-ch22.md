# Revision log: Chapter 22 - ML-NMR III: Numerical-Integration Theory

File: `chapters/part5/22-mlnmr-integration.qmd`. Revision pass against Section 10 (pedagogical
accessibility) and both reviewer files. Before: 1069 lines. After: 1564 lines (net +495).

## Running example introduced (single highest-value addition)

`#exm-qmc-psoriasis` "an aggregate psoriasis arm": an AgD arm reports mean age 45 (SD 12), mean baseline
severity 18 (SD 6), proportion biomarker-positive 0.30 (d=3 covariates); margins normal/normal/Bernoulli,
correlation borrowed from IPD; target is the arm's average response probability, whose contrast is the odds
ratio the HTA agency acts on. Reused at every transition: quadrature curse (5^3 vs 5^8 nodes, named
covariates), Monte Carlo (simulate synthetic patients), PIT (age/biomarker inversion), Sklar (age-severity
pairing), Gaussian copula (borrowed correlation), pipeline (7-step recipe), and specialized to the end
worked example (single standardized severity covariate = `#exm-qmc-logit`). Also a 1D numerical teaser right
after `@eq-qmc-pullback` (3 points -> 0.6143, within 0.012 of the true 0.6020).

## Reviewer points addressed

### ChatGPT highest-priority fixes
1. Plain-language bridge before transport map / unit cube: added "T is the recipe that turns uniform
   numbers into a plausible covariate profile" in `@sec-qmc-reduction`, glossed "pullback" inline, removed
   the bare "pushforward measure" phrase, added the "renaming the variable of integration" sentence.
2. Applied intuition before Hardy-Krause and Koksma-Hlawka: new transition paragraph (probabilistic ->
   deterministic; error = unevenness x roughness); "Reader translation: discrepancy is unevenness";
   "Reader translation: variation is total roughness" (defines alternating difference, 2D faces, anchor).
3. Gaussian copula assumption clarified: new "Which correlation is which" TABLE (latent Omega / covariate
   Pearson / Spearman rank / tail dependence) + "borrow the dependence of a normal, keep your margins"
   translation + dedicated tail-dependence remark (definition + when it matters clinically).
4. Integration-error practical guidance: new remark in `@sec-qmc-pipeline` (doubling check, N vs N/2,
   error small relative to posterior SD and to decision-relevant differences, multinma defaults) + warm-up
   exercise `#exr-qmc-diagnostic-read`.
5. Worked example strengthened: stated 0.6020 came from a high-order Gauss-Hermite rule; expanded the
   two-covariate trace with a 4-point (quarter-points) TABLE showing x2 shrinkage from the copula.

### GLM (beginner) fixes
- Clinical framing paragraph at top of `@sec-qmc-intro` (wrong integral -> wrong OR -> wrong HTA) and
  foreshadowed the fixed-nodes organizing idea.
- Quadrature preamble states the Legendre orthogonality and Hermite interpolation facts, cites Stoer and
  Bulirsch, and adds "why prove in full then discard" (benchmark for QMC).
- Plain-language HMC sidebar ("why a jittery likelihood breaks the fit") + three point-set choices TABLE
  (fresh random / fixed pseudorandom / Sobol).
- Sobol' section: leads with the four user-facing properties (deterministic, evenly spread, nested, cheap),
  says why Sobol' specifically (Joe-Kuo direction numbers to d=21,200, ships in multinma/Stan), a two-
  sentence primitive-polynomial-over-F_2 primer, and the integer-vs-F_2 arithmetic caution.
- Scrambled/randomized nets defined qualitatively in a new remark.
- `#cor-margins-copula-determine` added and cited at the load-bearing step of the `@thm-hypercube-integration`
  proof (was an inline assertion).
- Discrete-margin micro-example `#exm-qmc-discrete-jump` (binary biomarker, shows the jump, explains 1D
  finite vs tilted-surface infinite Hardy-Krause variation).
- Fixed "quadrating them in turn" -> "already-quadrated axis / applying the one-dimensional rule"; explained
  the 2^{d-1} factor and the k-fixed reading of the exponent.
- expit glossed as "the logistic function"; 7-step numbered pipeline recipe; bulleted chapter roadmap;
  f-vs-f_j notation caution (kept generic f in the numerical theorems, added a clarifying note rather than
  renaming).

## New labeled environments (all globally unique, verified)
- `#exm-qmc-psoriasis`, `#exm-qmc-discrete-jump`, `#cor-margins-copula-determine`,
  `#exr-qmc-diagnostic-read`, `#exr-qmc-correlation-interp`.

## New tables (5)
1D teaser (reduction); three point-set choices (MC->QMC); discrete-margin jump; which-correlation-is-which
(Gaussian copula); 4-point copula trace (worked example). Total tables in file: 8.

## Intuition / why-this-matters tally
5 "Reader translation" remarks after definitions; 3 "Why this matters" remarks (curse, Koksma-Hlawka,
pipeline capstone) plus the intro clinical framing; 3 "in plain terms" sidebars; numerous inline glosses.
Star convention line added at top of Exercises; two accessible warm-up/interpretation exercises before the
proof-heavy ones.

## Preservation (hard constraints)
- All pre-existing `#thm-`, `#lem-`, `#cor-`, `#prp-`, `#def-`, `#exm-`, `#exr-`, `#eq-`, `#sec-` labels
  preserved; none renamed or removed. Every existing theorem and full proof preserved and untouched except
  for two purely additive parenthetical cross-references (`@cor-margins-copula-determine` in the pipeline
  proof; none deleted).
- Labels I was tempted by but preserved: (a) the GLM reviewer asked to rename the generic integrand `f` to
  `psi` inside `#thm-koksma-hlawka` and `#thm-quadrature-error`; I preserved `f` and its equation labels
  (`#eq-qmc-kh`, `#eq-qmc-gauss-error`, etc.) and instead added a notation-caution note, because the general
  numerical-analysis statements read cleaner with a generic `f`. (b) The reviewer suggested demoting the
  `#def-sobol-net` construction into an optional box; I preserved the definition intact and added an
  "optional reading" signpost + intuition preamble instead.

## Build safety verified
No em/en/figure dashes, no connector hyphens, no Unicode in math (only non-ASCII in file is the pre-existing
prose "Levy"), no bare align/equation/gather, all headings preceded by blank lines, all `#sec-` ids unique,
64 fenced-div opens = 64 closes, all 5 new/8 total tables column-consistent, no dangling local cross-refs.
`$\star$` used for the star marker. No `@phillippo2016tsd` occurrences (nothing to fix).

## Gaps left for orchestrator
- Reviewers requested actual figures (2D random-vs-Sobol scatter; pipeline flow diagram). Substituted with
  PDF-safe tables and the numbered recipe; genuine figures deferred (would need generated image assets).
- `\Phi_{\Omega}` notation is defined inline in `#def-gaussian-copula`; consider adding it to `notation.qmd`
  in the consistency pass.
