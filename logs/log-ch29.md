# Work log: Chapter 29, Simulation Study Theory

Author pass: Opus 4.8. File overwritten:
`chapters/part6/29-simulation.qmd` (stub callout dropped, YAML title kept).

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (notation single source of truth).
- `~/Documents/GitHub/ITC_Coq/proofs/K_simulation_study.md` (base catalogue draft, K.1 to K.7).
- `~/Documents/GitHub/ITC_Coq/manuscript/15_simulation.md` (base manuscript draft).
- `~/Documents/GitHub/ITC_Coq/proofs/00_concepts_index.md` (verified K.1 to K.7 labels and the
  K.7 dependency labels F.7, F.10, G.6, H.20, M.12).
- `~/Documents/GitHub/ITC_Coq/theories/*.v` (confirmed NO simulation/MSE/coverage content exists in the
  Coq sources; grep of `.v` files for simulation|mse|coverage|monte returned nothing, so the chapter
  carries no `[machine-checked]` tag and the Notes state this accurately).
- Voice model: `chapters/part4/18-maic.qmd`.
- Cross-reference targets read or grep-verified to exist: `chapters/part1/05-inference.qmd`
  (`#thm-cramer-rao`, `#def-efficient-estimator`, `#cor-mle-efficient`, `#thm-mle-asymptotic-normality`,
  `#def-sandwich-variance`, `#def-m-estimator`, `#def-regular-model`, `#thm-slutsky`,
  `#thm-continuous-mapping`, `#thm-delta-method`); `chapters/part1/04-probability.qmd` (`#thm-jensen`);
  `chapters/part4/18-maic.qmd` (`#thm-maic-ess-bound`, `#thm-maic-no-extrapolation`,
  `#thm-maic-sandwich-variance`, `#exm-maic-twocov`); `chapters/part4/17-...qmd`
  (`#thm-unanchored-paic-consistency`, `#def-sema`, `#def-conditional-constancy-absolute`);
  `chapters/part4/19-stc.qmd` (`#thm-maic-stc-equivalence`); `chapters/part5/20-...qmd`
  (`#thm-aggregation`, `#thm-aggregation-bias`); `chapters/part3/16-...qmd` (`#thm-failure-of-bucher`);
  `chapters/part3/14-bucher.qmd` (`#thm-bucher-unbiased`); `chapters/part2/11-...qmd`
  (`#def-effect-modifier`); `chapters/part2/12-...qmd` (`#def-transportability`, `#thm-sema-insufficient`);
  `chapters/part1/07-glm.qmd` (`#def-non-collapsibility`). Sibling-wave slug `@def-probabilistic-bias-analysis`
  (Ch28) referenced per the wave slug map.

## Catalogue identifiers covered

K.1 (ADEMP), K.2 (bias and Monte Carlo SE), K.3 (empirical vs model-based SE; coverage),
K.4 (MSE = Bias^2 + Var), K.5 (coverage under (mis)specification), K.6 (power and Type I error),
K.7 (Phillippo empirical robustness finding). All seven owned and discharged.

## Slugs defined

Owned (assigned): `def-ademp`, `def-bias-mcse`, `def-coverage`, `thm-mse-decomposition`,
`thm-coverage-misspecification`, `def-power-type1`, `prp-phillippo-robustness`.

Auxiliary (new, `sim-` namespaced to avoid collision): `def-sim-performance-functional`,
`lem-sim-bias-unbiased`, `cor-sim-replications-bias`, `lem-sim-empse-unbiased`, `lem-sim-coverage-binomial`,
`cor-sim-replications-coverage`, `cor-sim-mse-trace`, `lem-sim-mse-empirical-identity`,
`lem-sim-coverage-unimodal`, `cor-sim-fixed-bias-collapse`, `cor-sim-correct-coverage`, `thm-sim-power`,
`prp-sim-efficiency-baseline`, `exm-sim-miniature`, plus exercises `exr-sim-mcse-arithmetic`,
`exr-sim-replications`, `exr-sim-coverage-curve`, `exr-sim-modse-empse`, `exr-sim-power`,
`exr-sim-bias-variance-tradeoff`. Section anchors `sec-sim-*`. Equation labels `eq-sim-*`.

Starred exercises for Appendix F: `exr-sim-power` and `exr-sim-bias-variance-tradeoff`.

## Expansion beyond the base draft

The base draft (K and manuscript 15) was sketch-level. Expanded to full proofs and added new rigorous
results not in the catalogue:

- Formalized "performance measure as a functional of the sampling distribution F_n" and the two-sample-size
  (n vs R) double-asymptotics framing (`def-sim-performance-functional`).
- Proved exact finite-R unbiasedness and Var = Var_n/R of the Monte Carlo bias estimator
  (`lem-sim-bias-unbiased`), and the replication-count corollaries (`cor-sim-replications-bias`,
  `cor-sim-replications-coverage`).
- Proved unbiasedness of the empirical variance and derived the normal-theory MCSE of EmpSE via the
  chi-square law and delta method (`lem-sim-empse-unbiased`); proved the coverage estimator is a binomial
  proportion with exact MCSE (`lem-sim-coverage-binomial`).
- Proved the MSE decomposition (K.4) AND an exact finite-sample empirical identity
  MSE_hat = Bias_hat^2 + (R-1)/R * EmpSE^2 (`lem-sim-mse-empirical-identity`), plus the vector/trace form.
- Upgraded K.5 from an informal "argument" to a full theorem (`thm-coverage-misspecification`): limiting
  Wald coverage = Phi(z-b) - Phi(-z-b) under standardized asymptotic bias b, with the b=±infinity collapse
  to 0 proved by a bounding argument, and the unimodality of the coverage curve proved separately
  (`lem-sim-coverage-unimodal`). Corollaries for correct specification (nominal) and fixed bias (collapse).
- Proved K.6 (`thm-sim-power`) as the dual of K.5: asymptotic level = alpha, two-term power formula
  Phi(Delta - z) + Phi(-Delta - z) with the one-sided approximation recovered, consistency under fixed
  alternatives.
- Added an efficiency-baseline proposition (`prp-sim-efficiency-baseline`) tying EmpSE to the asymptotic
  variance and the Cramer-Rao floor (@thm-cramer-rao), with the uniform-integrability caveat cited.
- Stated K.7 (`prp-phillippo-robustness`) explicitly as EMPIRICAL, anchoring each ranked claim to a proved
  theorem or to the cited simulation.
- Fully worked miniature ADEMP simulation (`exm-sim-miniature`) reusing the @exm-maic-twocov geometry:
  by-hand bias/EmpSE/MCSE/coverage/MSE with the exact identity verified (0.21 = 0.01 + 0.20), plus a
  theory table showing naive-method coverage collapsing 0.830 -> 0.484 -> 0.001 as sigma_n shrinks.

## Notation

No new symbols introduced; reused [Notation](/notation.qmd) throughout. Chose `v`/`Var_n` style names in
prose for the per-replication sampling variance to avoid clashing with the matrix `V`/`\mathbb{V}`
(sandwich) symbols; `sigma_n` is the standardizing scale sequence in the asymptotic theorems. No proposed
additions to `notation.qmd`.

## Bibliography

No new entries needed. Bibtex keys used and confirmed present in `references.bib`: `@morris2019ademp`,
`@phillippo2019thesis`, `@chandler2025mlumr`, `@billingsley1995`.

## Verification performed

- Div fences balanced (100 `:::` lines = 50 blocks); every labeled div id unique; all 7 owned slugs present
  exactly once.
- All `@`-cross-references grep-verified against existing chapter files (list above); all 4 bib keys exist.
- No dash-punctuation connectors (no em/en dash, no `--`, no spaced ` - `); no British spellings detected.
- Worked-example and exercise arithmetic checked by hand (incl. the exact MSE identity and the standard
  normal table values in the coverage-collapse table).

## Gaps / notes for the harmony pass

- Did not render with Quarto (not run in this environment). A render pass should confirm cross-project
  `@`-refs resolve once all Part VI siblings (Ch27, Ch28, Ch30) leave stub state; in particular
  `@def-probabilistic-bias-analysis` depends on Ch28 defining that slug as listed in the wave map.
- `prp-sim-efficiency-baseline` part (2) cites the Hajek convolution / local-asymptotic-minimax optimality
  from Chapter 5's existing citation (no new reference); if the harmony pass wants an explicit bib key for
  it, `@vandervaart1998` (already in `references.bib`) is the natural target.
- K.5/K.6 here are pen-and-paper only; consistent with the confirmed absence of any simulation content in
  `ITC_Coq/theories/`. Chapter 30 should not claim a machine-checked counterpart for any K result.
