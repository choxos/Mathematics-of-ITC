# Work log: Chapter 04, Probability and Distributions

Author pass on `chapters/part1/04-probability.qmd`. Status: complete draft, full proofs, one
multi-part worked example plus a second worked count example, notes, and eight exercises (two starred).

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (symbol source of truth), read in full and
  followed for theorem-proof grammar, slug namespacing, dash-free American English, and citation rules.
- `~/Documents/GitHub/ITC_Coq/proofs/A_probability_foundations.md` (results A.1 to A.13) and
  `~/Documents/GitHub/ITC_Coq/manuscript/01_probability.md`, for alignment of statements and notation.
  This chapter owns and expands A.1 to A.10; A.11 to A.13 (delta method, Slutsky, continuous mapping)
  are deliberately deferred to Chapter 5 per the catalogue assignment table in STYLE.md.
- `~/Documents/GitHub/ITC_Coq/theories/ConditionalIndep.v` and `AXIOMS.md`, to confirm the
  machine-checked counterpart of the graphoid axioms (see tag note below).
- Citations used in-text: `@hernan2020whatif` (causal framing of conditioning and identification),
  `@bingham2010regression` (multivariate normal / linear-models treatment). Chapter 3 sibling results
  `@thm-spectral-theorem` and `@thm-pd-characterization` are referenced for the covariance PSD theorem
  and the symmetric square root.

## Slugs defined (all globally unique, topic-namespaced)

Owned per assignment (all present): `def-probability-space`, `def-random-variable`,
`thm-tower-property`, `thm-jensen`, `thm-cauchy-schwarz-exp`, `thm-cov-psd`, `def-mgf`, `def-mvn`,
`thm-mvn-linear`, `thm-mvn-conditional`, `def-poisson-binomial`.

Additional slugs introduced to cover the assigned content (noted here for the harmony pass; none collide
with the cross-chapter map):

- `lem-sigma-algebra-closure` (A.1 closure properties)
- `prp-law-is-measure` (A.2 pushforward is a probability measure)
- `thm-monotone-convergence`, `thm-dominated-convergence` (A.3, stated and cited)
- `thm-expectation-linearity` (A.4 linearity, proved)
- `def-variance-covariance`, `cor-total-variance` (second-moment apparatus; law of total variance)
- `def-conditional-expectation` (A.5, existence via Radon-Nikodym cited, uniqueness proved)
- `cor-total-expectation` (A.9 total expectation / total probability)
- `def-independence`, `def-conditional-independence`, `thm-graphoid-axioms` (A.6)
- `lem-supporting-line` (supporting line for convex functions; feeds Jensen)
- `thm-fubini-tonelli` (A.10, stated and cited)
- `def-mgf` plus `thm-mgf-moments`, `thm-mgf-uniqueness`, `thm-mgf-sum`
- `def-bernoulli`, `def-binomial`, `def-poisson`, `thm-poisson-limit`, `def-normal`
- `prp-mvn-density`, `lem-normal-uncorrelated-independent`
- Section anchors: `sec-prob-intro`, `sec-prob-space`, `sec-random-variables`, `sec-expectation`,
  `sec-conditional`, `sec-independence`, `sec-inequalities`, `sec-jensen`, `sec-cauchy-schwarz`,
  `sec-cov-psd`, `sec-mgf`, `sec-distributions`, `sec-mvn`, `sec-prob-worked`, `sec-worked-bvn`,
  `sec-worked-pobin`, `sec-prob-notes`, `sec-prob-exercises`.
- Exercises: `exr-borel-cantelli`, `exr-variance-identities`, `exr-jensen-am-gm`,
  `exr-uncorrelated-not-independent`, `exr-mgf-poisson-sum`, `exr-conditional-bivariate`,
  `exr-cov-psd-construction` (starred), `exr-graphoid-counterexample` (starred).

Labeled display equations: `eq-countable-additivity`, `eq-pushforward`, `eq-change-of-variables`,
`eq-var-quadratic-form`, `eq-cond-exp-defining`, `eq-tower`, `eq-tower-mean`, `eq-total-variance`,
`eq-supporting-line`, `eq-jensen`, `eq-cauchy-schwarz`, `eq-mvn-mgf`, `eq-mvn-density`,
`eq-mvn-conditional`.

## Catalogue coverage (A.1 to A.10)

A.1 -> `def-probability-space`, `lem-sigma-algebra-closure`; A.2 -> `def-random-variable`,
`prp-law-is-measure`; A.3 -> `thm-monotone-convergence`, `thm-dominated-convergence`; A.4 ->
`thm-expectation-linearity`, `thm-tower-property`; A.5 -> `def-conditional-expectation`; A.6 ->
`def-conditional-independence`, `thm-graphoid-axioms`; A.7 -> `thm-jensen`; A.8 ->
`thm-cauchy-schwarz-exp`; A.9 -> `cor-total-expectation`; A.10 -> `thm-fubini-tonelli`.

## Proposed bibliography additions (do not edit references.bib; merge in harmony pass)

Two standard measure-theoretic probability references are cited by key but not yet in
`references.bib`. Proposed entries:

```bibtex
@book{billingsley1995,
  author    = {Billingsley, Patrick},
  title     = {Probability and Measure},
  edition   = {3rd},
  publisher = {John Wiley \& Sons},
  year      = {1995},
  address   = {New York},
  series    = {Wiley Series in Probability and Mathematical Statistics}
}

@book{williams1991,
  author    = {Williams, David},
  title     = {Probability with Martingales},
  publisher = {Cambridge University Press},
  year      = {1991},
  address   = {Cambridge}
}
```

Used for: Caratheodory extension, CDF-law correspondence, monotone/dominated convergence,
Radon-Nikodym existence of conditional expectation, Fubini-Tonelli, and MGF uniqueness/continuity
(`@billingsley1995`); the defining-property development and operational properties of conditional
expectation (`@williams1991`). If the orchestrator prefers to avoid new keys, every such citation could
instead be redirected to `@bingham2010regression`, but that text does not cover the pure measure theory,
so adding the two entries is the cleaner choice.

## Notation used, consistent with notation.qmd

All primary symbols come from the "Probability and random variables" block of `notation.qmd`
($(\Omega,\mathcal{F},P)$, $\mathbb{E}$, $\mathrm{Var}$, $\mathrm{Cov}$, $\boldsymbol{\Sigma}$,
$X\perp Y\mid Z$, $\mathcal{N}_p(\boldsymbol{\mu},\boldsymbol{\Sigma})$, $\mathrm{Bin}$, $\mathrm{Poi}$,
$\mathrm{Ber}$, $\mathrm{PoBin}(\mathbf{p})$, $\Phi$, $\phi$, $F_X$, $F_X^{-1}$, $M_X(\mathbf{t})$).

Minor auxiliary symbols introduced (standard, bold-uppercase-matrix scheme respected; flagged for
possible folding into `notation.qmd`):

- $\mathcal{B}(\mathbb{R}^d)$ Borel sigma-algebra; $P_X$ pushforward law (already implicit in A.2).
- $L^1$, $L^2$ integrability classes.
- $\boldsymbol{\Sigma}^{1/2}$ symmetric positive-semidefinite square root (built from
  `@thm-spectral-theorem`); $\boldsymbol{\Sigma}_{1\mid 2}$ Schur-complement conditional covariance.
- $\mathrm{Var}(Y\mid X)$ conditional variance; $\varphi'_{\pm}$ one-sided derivatives of a convex
  function.

None of these conflict with existing entries.

## Machine-checked tag

`thm-graphoid-axioms` carries
`[machine-checked: theories/ConditionalIndep.v, Lemmas cond_indep_symmetry, cond_indep_decomposition;
Theorems cond_indep_weak_union, cond_indep_contraction]`. Verified that these four results exist in
`ConditionalIndep.v` (lines 382, 407, 590, 611). Caveat for the consistency pass: the Coq proofs verify
(G1) through (G4) for a concrete discrete joint distribution `q` built in that file, whereas the chapter
states the axioms for general random vectors; the tag is faithful in spirit but the orchestrator may
wish to qualify it as "discrete model" if tags are meant to assert identical generality. (G5)
intersection is not formalized and is cited, matching catalogue A.6.

## Decisions and proof choices

- Defined the multivariate normal through its MGF (`eq-mvn-mgf`), which handles singular
  $\boldsymbol{\Sigma}$ uniformly and makes the affine-map and conditional theorems one-line MGF
  computations. Density (`prp-mvn-density`) derived separately for the nonsingular case via the
  $\boldsymbol{\mu}+\boldsymbol{\Sigma}^{1/2}\mathbf{Z}$ change of variables.
- `thm-mvn-conditional` proved by the regression-residual decomposition plus
  `lem-normal-uncorrelated-independent` and a conditional-MGF identification, rather than by brute-force
  density algebra; this reuses owned results and is the cleanest fully rigorous route.
- Jensen proved from a self-contained supporting-line lemma (`lem-supporting-line`) derived from the
  convex slope inequality, so the chapter does not import subgradient machinery.
- `thm-mgf-moments` differentiation-under-the-integral step was written with an explicit
  $r<r'<r''<\delta$ domination to make the dominated-convergence application airtight.

## Verification performed

- Pandoc parse (`pandoc -f markdown -t native`) succeeds with no errors.
- Fence balance: 63 opening div fences, 63 closing fences; 61 display-math blocks (122 `$$`).
- All 11 owned slugs present; no dash connectors (em/en/double/spaced) in the prose.
- Worked-example arithmetic checked by hand: bivariate normal eigenvalues $(3\pm\sqrt5)/2$,
  $\det\boldsymbol{\Sigma}=1$, conditional law $\mathcal{N}(x_2-1,1)$, affine map $\mathcal{N}(3,5)$,
  Jensen gap $=\mathrm{Var}(X_1)=2$, total-variance check $1+1=2$; Poisson binomial pmf
  $(0.08,0.42,0.42,0.08)$ summing to 1, mean 1.5, variance 0.57.

## Gaps left for review

1. Bib keys `@billingsley1995` and `@williams1991` must be merged into `references.bib` before the book
   render, or the citations will render unresolved. Full entries provided above.
2. Cross-references `@thm-spectral-theorem` and `@thm-pd-characterization` depend on Chapter 3 defining
   those exact slugs (they are in the cross-chapter map, so this should resolve automatically).
3. Replaced all `psmallmatrix` (mathtools, unavailable in MathJax/KaTeX) with `pmatrix` for portable
   rendering; if the project pins a LaTeX-PDF engine with mathtools, this is harmless.
4. The machine-checked tag generality caveat noted above.
