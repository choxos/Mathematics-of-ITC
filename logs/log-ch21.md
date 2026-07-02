# Work log: Chapter 21, ML-NMR II (Discrete Outcomes and Approximation Theory)

File authored: `chapters/part5/21-mlnmr-discrete.qmd` (stub overwritten with the complete chapter; YAML
title kept, stub callout dropped).

## Scope and catalogue coverage

Owns and proves catalogue results **H.8 to H.11** (`proofs/H_ml_nmr.md`):

- **H.8** the aggregate count for Poisson outcomes. Split into `@lem-poisson-convolution` (sum of
  independent, possibly non-identical, Poissons is Poisson; proved twice, by convolution + binomial
  theorem and by MGF + uniqueness) and `@thm-poisson-aggregate` (conditional aggregate is exactly Poisson;
  the marginal over random covariates is a *mixed* Poisson, overdispersed by `n*sigma_W^2` via the law of
  total variance; closed-form relative overdispersion `exp(beta_tot^T Sigma beta_tot) - 1` under Gaussian
  covariates). Faithful to the catalogue's corrected statement that the marginalized count is mixed
  Poisson, not Poisson.
- **H.9** `@thm-poisson-binomial-pgf`. Introduces the probability generating function (`@def-pgf`), proves
  the product form `prod(1-p_i+p_i z)`, recovers the subset-expansion PMF by coefficient extraction, and
  derives mean and variance from `G'(1)`, `G''(1)`. Builds on `@def-poisson-binomial` (Ch4).
- **H.10** `@thm-le-cam-tv`. FULL self-contained coupling proof of Le Cam's TV bound
  `||PoBin - Poi(lambda)||_TV <= sum p_i^2`. Supporting lemmas all proved: `@def-total-variation`,
  `@lem-tv-characterization` (sup = half-L1 = 1 - overlap), `@lem-coupling-inequality`,
  `@lem-exp-inequality` (`1 - e^{-p} <= p`). The proof builds an explicit Bernoulli-Poisson pair coupling,
  takes the couplings independent, and uses the chapter's own `@lem-poisson-convolution` to identify the
  summed Poisson. Convention fixed: `||mu-nu||_TV = sup_A |mu(A)-nu(A)| = (1/2) sum_k |mu_k - nu_k|`, which
  is what makes Le Cam's constant exactly `sum p_i^2`.
- **H.11** `@thm-adjusted-binomial`. Derives the two-parameter adjusted binomial by moment matching:
  `pi* = nu/lambda`, `N* = lambda^2/nu`. Proves `pi* >= bar p` and `N* <= n` (Cauchy-Schwarz; the ESS
  functional), identifies `N*` with the effective sample size of Ch18, and is explicit that this is a
  two-moment surrogate with NO total-variation guarantee (kept cleanly separate from H.10, per the
  catalogue's emphasis).

Added one supporting original result, `@prp-marginal-binomial` (the integrated binomial aggregate
likelihood `Bin(n, theta_bullet)`), to ground the worked example's "integration route." Clearly labeled as
an exact consequence of `@thm-aggregation`, not a catalogue result.

Worked example `@exm-aggregate-binomial`: a binary AgD arm with risks `(0.1,0.3,0.4,0.5,0.7)` computed
three ways (integrated `Bin(5,0.4)`, exact `PoBin` via the PGF, adjusted `Bin(4,0.5)`) with `Poi(2)`
alongside. All values verified independently in Python: PoBin PMF `(0.0567,0.2574,0.3834,0.2384,0.0599,
0.0042)`, mean 2.0, var 1.0; `TV(PoBin, Bin(4,0.5)) = 0.0200`; `TV(PoBin, Poi(2)) = 0.1707`; variance
reconciliation `nu - lambda^2/n = 0.20 = n s_p^2`; third central moments `0.12` (PoBin), `0` (adjusted),
`0.24` (integrated).

## Sources consulted

- `proofs/H_ml_nmr.md` sections H.0-H.11 (base draft; every sketch expanded to a full proof in book
  notation). `proofs/00_concepts_index.md`, `00_coverage_matrix.md` for catalogue framing.
- `notation.qmd` (symbols: `||.||_TV`, `PoBin(p)`, `Poi`, `Bin`, `Ber`, MGF, `theta_{bullet jk}`,
  `eta_{jk}`, `beta_1`, `beta_{2,k}`).
- Ch4 `chapters/part1/04-probability.qmd`: verified and reused `@def-mgf`, `@thm-mgf-sum`,
  `@thm-mgf-uniqueness`, `@def-bernoulli`, `@def-binomial`, `@def-poisson`, `@def-normal`,
  `@thm-poisson-limit`, `@def-poisson-binomial`. (Note: Ch4 line 808-809 explicitly forward-references
  this chapter for the Le Cam TV bound; that promise is now fulfilled by `@thm-le-cam-tv`.)
- Ch7 `@def-link-function`; Ch8 `@def-random-effects`; Ch16 `@def-ecological-bias`; Ch18
  `@thm-maic-ess-bound` (all verified present in their files).
- `chapters/part4/18-maic.qmd` skimmed for voice/structure (intro arc, worked-example style, Notes and
  Exercises format).
- Citations used (all keys present in `references.bib`): `@phillippo2020mlnmr`, `@phillippo2019thesis`,
  `@lecam1960`, `@phillippo2025general`, `@mccullagh1989glm`.

## Cross-references to siblings

Verified-present slugs: Ch4 (`@def-mgf`, `@thm-mgf-sum`, `@thm-mgf-uniqueness`, `@def-bernoulli`,
`@def-binomial`, `@def-poisson`, `@def-normal`, `@thm-poisson-limit`, `@def-poisson-binomial`),
Ch7 (`@def-link-function`), Ch8 (`@def-random-effects`), Ch16 (`@def-ecological-bias`),
Ch18 (`@thm-maic-ess-bound`).
Slug-map-guaranteed (not yet written at authoring time): Ch20 (`@def-individual-model`,
`@def-aggregate-model`, `@thm-aggregation`, `@thm-identity-link-exact`, `@thm-log-link-mgf`,
`@thm-logit-no-closed-form`), Ch22 (`@thm-koksma-hlawka`, `@thm-mc-rmse`),
Ch23 (`@thm-target-population-integral`), Ch25 (`@thm-general-likelihood-mlnmr`).

## Slugs defined (owned by this chapter)

Definitions: `def-pgf`, `def-total-variation`.
Lemmas: `lem-poisson-convolution`, `lem-tv-characterization`, `lem-coupling-inequality`,
`lem-exp-inequality`.
Proposition: `prp-marginal-binomial`.
Theorems (the four owned catalogue results): `thm-poisson-aggregate`, `thm-poisson-binomial-pgf`,
`thm-le-cam-tv`, `thm-adjusted-binomial`.
Example: `exm-aggregate-binomial`.
Exercises: `exr-poisson-twopoint`, `exr-pobin-pgf-compute`, `exr-lecam-coupling` (starred),
`exr-adjbin-moments`, `exr-adjbin-thirdmoment` (starred), `exr-overdispersion-gaussian`.
Sections: `sec-discrete-intro`, `sec-discrete-setup`, `sec-poisson`, `sec-pobin`, `sec-lecam`,
`sec-adjusted`, `sec-discrete-example`, `sec-discrete-notes`, `sec-discrete-exercises`.
Labeled equations: `eq-integrated-binomial`, `eq-poisson-convolution`, `eq-poisson-agg-conditional`,
`eq-poisson-agg-marginal`, `eq-poisson-agg-moments`, `eq-poisson-agg-overdisp`, `eq-pgf-def`,
`eq-pobin-pgf`, `eq-pobin-pmf`, `eq-pobin-moments`, `eq-tv-def`, `eq-tv-three-forms`, `eq-coupling-ineq`,
`eq-lecam-bound`, `eq-lecam-pair`, `eq-lecam-pairbound`, `eq-adjbin-moments`, `eq-adjbin-solution`,
`eq-ex-pvec`, `eq-ex-binom`, `eq-ex-pgf`, `eq-ex-pobin`, `eq-ex-adjbin`, `eq-ex-poisson`.

Two starred exercises for Appendix F: `exr-lecam-coupling` (the coupling, the bound, and its leading-order
sharpness) and `exr-adjbin-thirdmoment` (moment matching stops at two; third central moments disagree).

## Machine-checked tags

NONE. Confirmed by grep over `~/Documents/GitHub/ITC_Coq/theories/*.v` for
`poisson|binomial|lecam|le_cam|pobin|generating`: no matches. The Coq development covers the causal and
weighting core (Parts II-IV); the discrete-outcome approximation theory of Part V is analytic and is not
formalized. The Notes section states this explicitly; no result carries a machine-checked tag.

## Proposed additions for the orchestrator

### Bibliography (`references.bib`) - referenced by attribution, not yet keyed

The Le Cam remark attributes the sharper bound and Stein's-method machinery to three sources not in
`references.bib`. They appear in prose as named attributions (no `@key`), but should be added for
completeness:

```bibtex
@article{barbour1984,
  author  = {Barbour, A. D. and Hall, Peter},
  title   = {On the rate of {Poisson} convergence},
  journal = {Mathematical Proceedings of the Cambridge Philosophical Society},
  volume  = {95}, number = {3}, pages = {473--480}, year = {1984}
}
@article{chen1975,
  author  = {Chen, Louis H. Y.},
  title   = {Poisson approximation for dependent trials},
  journal = {The Annals of Probability},
  volume  = {3}, number = {3}, pages = {534--545}, year = {1975}
}
@book{barbour1992,
  author    = {Barbour, A. D. and Holst, Lars and Janson, Svante},
  title     = {Poisson Approximation},
  publisher = {Oxford University Press}, series = {Oxford Studies in Probability}, year = {1992}
}
```

If keyed, the four prose attributions in `@sec-lecam` and `@sec-discrete-notes` can become `@barbour1984`,
`@chen1975`, `@barbour1992`.

### Notation (`notation.qmd`)

- Probability generating function `G_X(z) = E[z^X]` introduced in `@def-pgf`. Suggest a one-line entry in
  the "Probability and random variables" table next to the MGF row: `G_X(z) = E[z^X]` (probability
  generating function). Used only in this chapter so far; harmless to add.
- `@def-total-variation` fixes the convention `||mu-nu||_TV = sup_A|mu(A)-nu(A)| = (1/2) sum_k|mu_k-nu_k|`.
  The TV symbol is already in `notation.qmd`; recommend the orchestrator confirm sibling chapters that use
  TV (none in the current wave) adopt the same half-L1 convention so Le Cam's constant stays `sum p_i^2`.

## Decisions and notes

- **Conditional vs marginal aggregate law.** The chapter foregrounds the distinction (a dedicated remark in
  `@sec-discrete-setup`) because conflating them is the field's main hazard. The marginal binomial
  `Bin(n, theta_bullet)` (the default ML-NMR likelihood) and the conditional `PoBin` (approximated by the
  adjusted binomial) are both presented, and the worked example reconciles them via `nu - lambda^2/n`.
- **Risk vector choice.** Kept the non-symmetric `(0.1,0.3,0.4,0.5,0.7)` because it yields integer adjusted
  parameters `(N*, pi*) = (4, 0.5)` and round summaries `lambda=2, nu=1`, making the entire example
  hand-checkable. An initial draft wrongly described this vector as symmetric about 0.5; corrected during
  self-review (the vector is mildly right-skewed, PoBin third central moment `0.12`). All four affected
  passages were fixed and the skew is now used as a teaching point for the two-moment limitation.
- **Le Cam tightness.** Included the classical law-of-small-numbers special case (`Bin(n,p) -> Poi(np)`,
  bound `np^2`) tying back to `@thm-poisson-limit`, and were honest that the bound is loose at moderate
  risks (worked example: actual TV 0.17 vs bound 0.5), motivating the adjusted binomial as the practical
  choice.

## Gaps / items for the harmony pass

- Cross-references to Ch20/22/23/25 rely on the slug-map contract; the consistency pass should confirm
  those chapters define `@def-individual-model`, `@def-aggregate-model`, `@thm-aggregation`,
  `@thm-log-link-mgf`, `@thm-logit-no-closed-form`, `@thm-koksma-hlawka`, `@thm-mc-rmse`,
  `@thm-target-population-integral`, `@thm-general-likelihood-mlnmr` with these exact slugs.
- The three Barbour/Chen sources are attributed in prose only; fold the bibtex above into `references.bib`
  and convert to `@key` form if desired.
- No render performed (full-book render is task #12). Local checks done: dash-punctuation scan (clean,
  only the YAML `---` delimiters), `:::` fence balance (39 open / 39 close), cross-ref enumeration, British
  spelling scan (clean), numeric verification of every figure in the worked example and exercises.
