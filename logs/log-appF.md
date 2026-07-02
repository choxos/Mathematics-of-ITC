# Work log: Appendix F, "Solutions to Selected Exercises"

Authored `appendices/F-solutions.qmd`: full, rigorous solutions to every starred ($\star$) exercise in the
book. The stub callout was removed; the YAML `title: "Solutions to Selected Exercises"` was kept. Solutions
are organized by chapter in book order (30 level-2 chapter headings), each solution headed
`### Solution to @exr-<slug>`.

## Method

- Located starred exercises by scanning every `::: {#exr-...}` environment for the `$\star$` marker
  (`grep -rn 'star' chapters/part*`), then read each exercise and the chapter results it references (by
  slug) to solve it in the book's notation, citing those slugs.
- A starred exercise is one whose statement carries the `$\star$` marker (usually `**($\star$) ...**` in the
  heading, or `$\star$` opening the body under a "(starred)" / "(starred challenge)" heading).
- Excluded one false positive: `@exr-sim-coverage-curve` (ch 29) contains `\star` only as the notation
  `$b^\star$` in its body, with no `($\star$)` marker, so it is not a starred exercise and was not solved.
- Verified completeness and uniqueness programmatically: 60 solution headings, 60 distinct slugs, matching
  exactly the 60 starred exercises across the chapters (no missing, no extra once the camelCase slug
  `exr-mlumr-identify-alphaB` is accounted for).

## Starred exercises solved, by chapter (60 total; 2 per chapter)

- Ch 1 (Linear Algebra I): `@exr-la1-dim-sum`, `@exr-la1-gram-rank`
- Ch 2 (Linear Algebra II): `@exr-parallelogram`, `@exr-oblique-vs-orthogonal`
- Ch 3 (Linear Algebra III): `@exr-ata-aat-spectrum`, `@exr-weyl-inequality`
- Ch 4 (Probability): `@exr-cov-psd-construction`, `@exr-graphoid-counterexample`
- Ch 5 (Inference): `@exr-information-equality-fail`, `@exr-sandwich-derivation`
- Ch 6 (Linear Regression): `@exr-lr-gm-weighted`, `@exr-lr-general-hypothesis`
- Ch 7 (GLM): `@exr-glm-irls-probit`, `@exr-glm-noncollapse`
- Ch 8 (Hierarchical/Bayes): `@exr-james-stein-sure`, `@exr-reml-one-way`
- Ch 9 (Potential Outcomes): `@exr-po-positivity-failure`, `@exr-po-selection-bias-proof`
- Ch 10 (Adjustment Methods): `@exr-stabilized`, `@exr-eif-control`
- Ch 11 (Effect Modification/Collapsibility): `@exr-emcoll-or-attenuation`, `@exr-emcoll-anchored-unanchored`
- Ch 12 (Transportability): `@exr-transport-attenuation`, `@exr-transport-scale-misalignment`
- Ch 13 (Pairwise Meta-Analysis): `@exr-ma-fe-pipeline`, `@exr-ma-reml-balanced`
- Ch 14 (Bucher): `@exr-bucher-correlated`, `@exr-bucher-transitivity-bias`
- Ch 15 (Network Meta-Analysis): `@exr-nma-pooling`, `@exr-nma-ipd-collinear`
- Ch 16 (Limits of NMA): `@exr-limits-pv-cancellation`, `@exr-limits-general-attenuation`
- Ch 17 (Population Adjustment Theory): `@exr-pat-unanchored-bias`, `@exr-pat-noncollapsible-target`
- Ch 18 (MAIC): `@exr-maic-bias-decomp`, `@exr-maic-sandwich-vs-naive`
- Ch 19 (STC): `@exr-stc-loglink-cancellation`, `@exr-stc-delta`
- Ch 20 (ML-NMR Aggregation): `@exr-agg-prevalence`, `@exr-agg-identity-uniqueness`
- Ch 21 (ML-NMR Discrete): `@exr-lecam-coupling`, `@exr-adjbin-thirdmoment`
- Ch 22 (ML-NMR Integration): `@exr-qmc-gaussian-copula-cov`, `@exr-qmc-logit-pipeline`
- Ch 23 (ML-NMR Estimands): `@exr-mlnmr-sema-gap`, `@exr-mlnmr-stc-reduction`
- Ch 24 (Computation): `@exr-comp-rhat-floor`, `@exr-comp-gpd`
- Ch 25 (General Likelihoods): `@exr-genlik-mhr-attenuation`, `@exr-genlik-rmst-transport`
- Ch 26 (ML-UMR): `@exr-mlumr-identify-alphaB`, `@exr-mlumr-rmst-transport`
- Ch 27 (Distance Matching): `@exr-distance-affine-invariance`, `@exr-distance-secondmoment`
- Ch 28 (QBA): `@exr-qba-itc-evalue-star`, `@exr-qba-norta-margins-star`
- Ch 29 (Simulation): `@exr-sim-power`, `@exr-sim-bias-variance-tradeoff`
- Ch 30 (Coq): `@exr-coq-discrete-vs-named`, `@exr-coq-faithfulness`

Every chapter has at least one starred exercise, so no representative substitution was needed.

## Numerical answers given (worked exercises)

Selected closed-form/numerical results computed and reported in full:
- Ch 7 non-collapsibility example: marginal OR `2.8966` (between `1` and `omega=4`).
- Ch 10 stabilized weights: cell values `2.0, 0.6667, 0.75, 1.5`, `P`-weighted mean `1`; control bound
  `V_0^* = 8.5` versus treated `V^* = 14.333`.
- Ch 12 risk-difference misalignment: conditional `0.2583` (x=0), `0.1931` (x=1); marginals `0.2453`,
  `0.2061`.
- Ch 13 fixed-effect pipeline: `theta_FE = 1.0481`, `SE = 0.2164`, `Q = 1.645`, `I^2 = 0`, `c = 13.005`,
  `tau^2_DL = 0` (no detectable heterogeneity).
- Ch 14 transitivity bias: marginal `d_BC = 0.62` (BC), `0.38` (AB); true `d_AB = 0.22`; Bucher `-0.02`;
  bias `-0.24`.
- Ch 17 non-collapsible target: marginal log OR `-0.122, 0.228, 0.545` across `Pr(X=1) in {0.25,0.50,0.75}`,
  with non-collapsibility gaps `0.070, 0.074, 0.044`.
- Ch 20 prevalence: integrated `theta = 0.3015, 0.5509`; plug-in `0.2994, 0.5622`; contrast ecological
  bias `+0.0558`.
- Ch 21 third moment: PoBin third central moment `0.120` versus adjusted-binomial `0`.
- Ch 22 QMC pipeline: four-point estimate `0.5402` at rho=0.5, `0.5601` at rho=0.
- Ch 23 SEMA gap: reproduced `0.022502` at the chapter's inputs.
- Ch 26 alphaB: `alpha_B ~= -1.20`; conditional log OR `~= 1.00`, marginal `~= 0.96`. RMST transport:
  contrast differs by `0.00277` years between pi*=0.5 and pi*=0.3 at tau=10.
- Ch 28 ITC E-value: `K = 0.495`, `Delta(2.0) = -1.105`, `BF_obs = 3.019`, `RR_UD = 2.226`,
  `E_ITC = +infinity`; finite-formula check `2.25`.
- Ch 29 power: `n = 197` for power 0.80; dropped two-sided term `~ 1e-6`.

## PDF-build-safety checks (STYLE Section 11), all passing

- ASCII-only in math; `$\star$` used, never the Unicode glyph (0 occurrences of the glyph; 0 non-ASCII
  bytes in the file).
- No bare `align`/`equation`/`gather`; display math uses `aligned`, `cases`, `pmatrix`, `array`. Verified
  no `$$ ... $$` block contains a bare `\\` outside a matrix/aligned environment.
- No `\not` applied to an extensible arrow.
- American English; no dash punctuation as connector or parenthetical (only Markdown table separators
  `|---|` match a hyphen run).

## Files touched

- Wrote: `appendices/F-solutions.qmd` (overwrote the stub), `logs/log-appF.md` (this log).
- Did not edit any chapter, `_quarto.yml`, `notation.qmd`, or `references.bib`.

## Notes / gaps for review

- `@exr-pat-noncollapsible-target` (ch 17): the chapter's table @exm-pat-anchored has an A-versus-B
  contrast that is itself effect-modified on the logit scale (conditional log OR moves from `-0.539` at
  `x=0` to `+0.847` at `x=1`), so the cross-population movement of the marginal odds ratio combines effect
  modification with non-collapsibility. The solution computes the three marginal log ORs faithfully, then
  isolates the pure non-collapsibility component as the marginal-minus-population-standardized-conditional
  gap, and points to the SEMA worked example `@sec-worked-binary` (constant conditional OR) as the clean
  isolation of non-collapsibility behind `@thm-sema-insufficient`. Flag for a reviewer in case the
  exercise's phrasing ("pure non-collapsibility effect") is meant to be read more loosely.
- No new notation or bibliography entries were introduced; all symbols are from `notation.qmd` and all
  citations are existing chapter slugs.
