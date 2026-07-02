# Work log: Chapter 06, Linear Regression from First Principles

File authored: `chapters/part1/06-linear-regression.qmd` (overwrote the stub; YAML title kept).

## Scope and approach

This is the first "prove everything" chapter (STYLE rule 6). Every lemma, theorem, proposition, and
corollary is proved in full. Routine prerequisites (existence of bases, the rank-nullity and
four-subspaces theorems, the projection theorem, the spectral theorem, the SVD, the multivariate normal
and its MGF, the Cramer-Rao inequality) are cited to the owning sibling chapters or to `@strang2016`,
never silently assumed.

Two derivations of OLS are given as required: by calculus (gradient of the residual sum of squares,
convexity certified directly via $S(\mathbf b)-S(\hat{\boldsymbol\beta})=\|\mathbf X\mathbf d\|^2\ge0$)
and by orthogonal projection (`@thm-projection-theorem`). The normal-theory distribution results are
proved from the spectral decomposition of the idempotent residual maker `M` and from two
multivariate-normal lemmas proved locally via the MGF. The chapter closes the "why squares" question
three ways: projection (closest point), Gauss-Markov (BLUE), and Cramer-Rao (UMVUE under normality), and
proves OLS = MLE under Gaussian errors.

## Sources used

- `@bingham2010regression` (Regression: Linear Models in Statistics): Gauss-Markov theorem, the t / chi
  squared / F distribution theory, the normal-errors MLE identity. Primary source as assigned.
- `@strang2016` (Introduction to Linear Algebra): the projection / column-space / four-subspaces
  viewpoint, the QR remark, the trace and rank arguments.
- Confirmed there is NO `ITC_Coq` proofs markdown file for linear regression (the catalogue files are
  `A_...md` to `O_...md`, none on the linear model; this chapter is "new" content per the STYLE
  assignment table, so no catalogue identifiers A-O are claimed).
- Checked `~/Documents/GitHub/ITC_Coq/theories/*.v` for an OLS / Gauss-Markov / normal-equations / hat
  matrix counterpart: none exists. `OutcomeRegression.v` formalizes the causal outcome-regression
  estimator, not the linear-algebraic least-squares theory. Therefore NO `[machine-checked: ...]` tags
  were added. Noted in the chapter's Notes section.

## Slugs defined (all globally unique, topic-namespaced)

Owned (from the assignment, all present and defined):
`def-linear-model`, `thm-ols-normal-equations`, `def-hat-matrix`, `thm-ols-blue`, `thm-ols-moments`,
`thm-sigma2-unbiased`, `thm-betahat-normal`, `thm-rss-chisq`, `thm-betahat-s2-independence`,
`thm-ttest`, `thm-ftest`, `def-r-squared`, `thm-ols-mle-normal`.

Helper results I created (needed and load-bearing; namespaced under the chapter topic):
- `lem-gram-nullspace` (N(X^T X) = N(X); invertibility / positive-definiteness of the Gram matrix)
- `def-sums-of-squares` (RSS, TSS, ESS_reg, the objective S)
- `lem-hat-properties` (H, M symmetric idempotent; HM=0; HX=X, MX=0; tr H = p, tr M = n-p; projections)
- `prp-fitted-residual-geometry` (yhat in C(X), r in C(X)^perp, orthogonality, residuals sum to zero)
- `lem-mvn-affine-closure` (affine image of an MVN is MVN; proved via `@def-mgf`)
- `lem-gaussian-block-independence` (uncorrelated jointly Gaussian blocks are independent; via MGF)
- `prp-anova-decomposition` (Pythagorean TSS = ESS_reg + RSS)
- `cor-rsquared-range` (0 <= R^2 <= 1; R^2 = rho_xy^2 in SLR, via `@thm-cauchy-schwarz-ip`)
- `cor-ols-efficient-normal` (Fisher info = X^T X / sigma^2; OLS attains the Cramer-Rao bound, UMVUE)
- `prp-rank-deficient-pseudoinverse` (consistency, invariance of fitted values, estimability,
  minimum-norm solution X^+ y via `@thm-svd`)

Equation labels: `eq-linear-model`, `eq-normal-equations`, `eq-betahat`, `eq-betahat-error`,
`eq-hat-matrix`, `eq-cov-betahat`, `eq-gm-decomp`, `eq-anova`, `eq-ttest`, `eq-fstat`, `eq-loglik`.

Section labels: `sec-lr-intro`, `sec-lr-model`, `sec-lr-ols`, `sec-lr-gm`, `sec-lr-normal`,
`sec-lr-inference`, `sec-lr-anova`, `sec-lr-mle`, `sec-lr-rank`, `sec-lr-example`, `sec-lr-notes`,
`sec-lr-exercises`.

Exercise labels (9 total; two starred for Appendix F): `exr-lr-simple-formulas`, `exr-lr-centering`,
`exr-lr-leverage`, `exr-lr-anova-noint`, `exr-lr-gm-weighted` (★), `exr-lr-general-hypothesis` (★),
`exr-lr-prediction`, `exr-lr-mle-sigma-bias`, `exr-lr-rank-example`.
The two starred exercises (generalized/weighted Gauss-Markov, and the general linear hypothesis F) are
the ones whose solutions belong in Appendix F.

## Sibling cross-references used (for the harmony pass to verify)

- Ch01: `@thm-rank-nullity`, `@thm-four-subspaces`, `@def-column-space`.
- Ch02: `@thm-projection-theorem`, `@thm-gram-schmidt`, `@def-projection-matrix`, `@thm-cauchy-schwarz-ip`.
- Ch03: `@thm-spectral-theorem`, `@thm-svd`, `@thm-pd-characterization`, `@def-quadratic-form`,
  and `@def-pseudoinverse` (see gap 1 below).
- Ch04: `@def-mgf`.
- Ch05: `@thm-cramer-rao`, `@def-fisher-information`, `@thm-mle-asymptotic-normality`,
  `@def-sandwich-variance`.
- Ch07: `@def-non-collapsibility`, `@def-link-function`.

All other `@`-references resolve to labels defined within this chapter (audited mechanically: every
reference matches a defined label except `@def-pseudoinverse`).

## Notation

No new symbols beyond `notation.qmd` are required for the core development; I used `H`, `M`, `RSS`,
`TSS`, `ESS_reg`, `sigma^2`, `s^2`, `R^2`, `X`, `y`, `yhat`, `beta`, `betahat`, `epsilon`, `r` exactly
as defined there. A handful of standard, locally scoped symbols are introduced and defined on first use,
all consistent with the existing scheme and none conflicting:
- `S(b)` for the residual-sum-of-squares objective;
- `S_xx`, `S_xy`, `S_yy` and `rho_xy` for the simple-regression sums and the sample correlation (worked
  example and `cor-rsquared-range`);
- `h_ii` for hat-matrix leverages (exercise);
- the labels (G1), (G2), (G3) for the Gauss-Markov / normality assumptions.

PROPOSED optional additions to `notation.qmd` (not required, but would standardize usage if other
chapters reuse them): `\rho_{xy}` (sample Pearson correlation) and `h_{ii}` (leverage). I did not edit
`notation.qmd`.

## Bibliography

No new bib entries needed. Both assigned keys (`@bingham2010regression`, `@strang2016`) already exist in
`references.bib`. I did not edit `references.bib`.

## Gaps / items for the consistency-and-harmony pass

1. `@def-pseudoinverse` is referenced in `prp-rank-deficient-pseudoinverse` and the Ch06 brief explicitly
   instructs referencing it, but it is NOT in the cross-chapter slug map for any chapter. Its natural
   owner is Ch03 (the SVD chapter); `notation.qmd` already lists the symbol `A^+`. ACTION for the
   harmony pass: have Ch03 define `#def-pseudoinverse` (Moore-Penrose pseudoinverse), or reassign the
   slug. To fail gracefully if it stays unresolved, the chapter's prose defines the pseudoinverse inline
   via the thin SVD (`@thm-svd`), so the argument is self-contained regardless.

2. `lem-mvn-affine-closure` and `lem-gaussian-block-independence` restate multivariate-normal facts that
   properly live in Ch04. I proved them locally (via `@def-mgf` and MGF uniqueness/factorization) to
   honor the "PROVE EVERYTHING in this chapter" instruction and keep the chapter self-contained. The
   Ch04 slug map exposes only `thm-mvn-conditional`, `thm-jensen`, `def-mgf`, `thm-cov-psd`,
   `def-probability-space`; none is exactly affine-closure or uncorrelated-implies-independent.
   SUGGESTION: if Ch04 adds slugs such as `thm-mvn-affine` and `thm-mvn-uncorrelated-independent`, the
   harmony pass may replace my two local lemmas with cross-references. Until then the local proofs stand.

3. The chi-squared, Student t, and Snedecor F distributions are recalled narratively as "Chapter 4"
   facts (definition as sums/ratios of independent standard normals and chi-squareds). If Ch04 exposes
   slugs for these distributions, the harmony pass can convert the narrative mentions to `@`-references.

4. No machine-checked tags were added (confirmed no Coq counterpart, item under "Sources").

## Verification performed

- Worked example arithmetic verified numerically (Python/numpy/scipy): betahat = (0.6, 0.8); fitted and
  residuals as stated; residuals and x-weighted residuals sum to exactly zero; RSS = 3.6, TSS = 10,
  ESS_reg = 6.4, R^2 = 0.64; s^2 = 1.2; SEs (1.1489, 0.3464); t = (0.522, 2.309); F = 5.3333 = t_1^2;
  tr(H) = 2, tr(M) = 3; eigenvalues of M are {0, 0, 1, 1, 1} (rank n-p = 3), illustrating `thm-rss-chisq`.
  Every number in the example is hand-verifiable.
- Mechanical checks on the .qmd: 60 opening and 60 closing div fences (balanced); 20 proof divs each
  ending in `$\square$`; no em/en dashes, no double-hyphen connectors, no spaced-hyphen connectors; no
  British spellings; stub callout removed; YAML title preserved; all 13 owned slugs present.
