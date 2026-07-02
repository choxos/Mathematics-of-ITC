# Revision log: Appendix C, Probability Distributions

File: `appendices/C-distributions.qmd`. Kind: reference (distributions catalogue).
Before: 311 lines. After: 616 lines. Agent: Opus 4.8 revision pass.

## Reviewers addressed

Both `feedback/chatgpt/appendix-C-distributions.md` and `feedback/glm/appendix-C-distributions.md`.

### ChatGPT highest-priority fixes (all addressed)

1. **Distribution-to-modeling-role table.** Added `@tbl-dist-roles` (new `## How to read this appendix
   {#sec-dist-howto}` section at the top) mapping each family to its typical health-data object, its role
   (likelihood / prior / covariate model / discrete aggregation device / survival baseline / integration
   device), and the chapters that use it. Preceded by a six-item enumeration of the modeling roles.
2. **Novice worked examples.** Added `@exm-dist-pobin` (Poisson binomial aggregation of three unequal
   risks, with full mass function, mean, variance, and the binomial-comparison variance check),
   `@exm-dist-betabinom` (beta-binomial update Beta(1,1) + 7/10 -> Beta(8,4), with the explicit convex
   combination), and `@exm-dist-weibull` (hazard values at three times for k = 0.5, 1, 2, as a table).
3. **Plain-language for support / density vs probability / rate vs scale / concentration / pseudo-counts
   / simplex.** Added a plain-language block opening `@sec-dist-conventions` (support, mass vs density),
   the `@tbl-dist-param` parametrization cheat sheet (rate/scale/hazard + precision), pseudo-count and
   concentration glosses in the beta and Dirichlet sections, and a plain-language simplex definition.
4. **ML-NMR connection explicit.** Rewrote the standard-normal closing paragraph to explain that
   `\Phi^{-1}` turns uniform QMC points into correlated normal covariate draws over which an individual
   likelihood is averaged, with pointers to `@sec-qmc-pit` and `@sec-qmc-gaussian`; MVN section now lists
   the Gaussian-copula integration role explicitly.
5. **Advanced-reference marking.** Tagged the hyperplane/degenerate-MGF explanation, the beta `${}_1F_1$`
   MGF, the Dirichlet Lebesgue-measure detail, the MVN Schur complement, and the Mills ratio each with an
   explicit "Advanced; skip on a first pass" (or equivalent) signpost.

### GLM reviewer suggestions (addressed)

- Per-distribution "what it models in HTA" sentence: added via `@tbl-dist-roles` plus role sentences in
  each of the discrete and continuous prose blocks.
- Forward-reference navigation: `@tbl-dist-roles` "Where it appears" column; new pointer to `@sec-pobin`
  for the Poisson binomial (previously it had no forward reference).
- Multinomial included: new `@def-dist-multinomial` with mass `@eq-dist-multinomial`, mean/variance/
  covariance, and the note that it reduces to binomial at K=2 and is the likelihood in the Dirichlet
  conjugate row.
- Inverse-gamma: added a remark in `@sec-dist-conjugacy` stating the book does NOT catalogue it, because
  it uses half-normal / half-t priors on the between-study standard deviation instead (verified: Chapter
  13 line ~1096 explicitly prefers half-normal/half-t over inverse-gamma near zero; Chapter 8 places the
  prior on tau). This is the accurate resolution of the reviewer's "add it or say it is not used."
- Expanded discrete section to one labeled prose block per family (Bernoulli, binomial, Poisson binomial,
  Poisson), with the plain-language gloss of the Poisson binomial mass and the Poisson exposure/person-
  time note (lambda = rate x exposure).
- Beta shape stories (a=b=1 uniform; a=b>1 unimodal; a>b, a<b; a,b<1 U-shaped) and pseudo-count reading;
  demoted `${}_1F_1$` to an advanced parenthetical.
- Exponential memorylessness stated explicitly; gamma shape stories and prior-on-rate/precision role.
- Weibull shape stories (k<1 decreasing, k=1 constant, k>1 increasing hazard) plus the worked table.
- MVN conditioning interpreted as a linear regression with coefficients Sigma_12 Sigma_22^{-1} and a
  conditional covariance free of x_2; added `@exm-dist-mvn-predict` (impute a missing covariate).
- MGF intuition ("differentiate e^{tX} and pull down a factor of X"); convexity-direction reminder in the
  Poisson binomial remark; "right tail too heavy" made concrete (integral diverges for t >= beta);
  Weibull sub-linear-exponent explanation for why the MGF fails when k<1.
- `\succ 0` glossed as positive definite in the MVN section.
- B(alpha) linked to scalar B(a,b) as the K=2 case.
- Notes section converted from one dense paragraph to a scannable bullet list (all citations preserved).

### Deliberately skipped (with reason)

- **Section reordering** (both reviewers, low priority). Left the section order unchanged to avoid any
  risk to cross-reference stability and the pdflatex build; added signposting instead. All existing
  `#sec-` ids keep their positions and every cross-reference still resolves.
- **Density plot figures** (GLM suggestion 5). The orchestrator renders with pdflatex and executable
  R/Python chunks are not part of this appendix's build path; a broken chunk would break the PDF.
  Substituted prose "shape stories" (which the reviewer explicitly called what a clinician needs) and the
  numeric Weibull-hazard table for the same intuition, without a rendered figure. Per task scope, no
  running example or new exercises were forced (this is a reference appendix with no Exercises section).

## New labeled environments and tables added

`#sec-dist-howto`, `#tbl-dist-roles`, `#tbl-dist-param`, `#exm-dist-pobin`, `#def-dist-multinomial`,
`#eq-dist-multinomial`, `#exm-dist-weibull`, `#exm-dist-mvn-predict`, `#exm-dist-betabinom`. All verified
unique across `chapters/`, `appendices/`, and `notation.qmd`.

## Mathematical errors fixed

None found. The reviewers flagged no incorrect identity in this appendix; their asks were pedagogical
(intuition, roles, examples, advanced-marking). All new worked examples were checked by hand:
`@exm-dist-pobin` masses sum to 1 (0.252 + 0.514 + 0.216 + 0.018), mean 1.0, variance 0.54 vs Bin(3,1/3)
variance 0.667; `@exm-dist-betabinom` posterior Beta(8,4), mean 8/12 = 0.667, matching the convex
combination (2/12)(0.5) + (10/12)(0.7); `@exm-dist-weibull` hazards h(x)=k x^{k-1} at x = 0.25, 1, 4;
`@exm-dist-mvn-predict` N(1.2, 0.64) from rho = 0.6, x_2 = 2.

## Preservation confirmation

- All 24 original labels present and unchanged: `sec-dist-conventions`, `eq-dist-gamma-function`,
  `eq-dist-beta-function`, `sec-dist-discrete`, `tbl-dist-discrete`, `sec-dist-continuous`,
  `tbl-dist-continuous`, `eq-dist-beta-mgf`, `sec-dist-mvn`, `tbl-dist-mvn`, `sec-dist-dirichlet`,
  `def-dist-dirichlet`, `eq-dist-dirichlet-density`, `eq-dist-dirichlet-moments`, `tbl-dist-dirichlet`,
  `sec-dist-standard-normal`, `eq-dist-phi`, `eq-dist-phi-derivs`, `eq-dist-normal-moments`,
  `eq-dist-Phi-erf`, `eq-dist-mills`, `sec-dist-conjugacy`, `tbl-dist-conjugacy`, `sec-dist-notes`.
- All load-bearing original formulas byte-intact (PoBin mass, beta MGF, Mills bound, MVN Schur
  conditional, Dirichlet density and moments, normal even moments) via fixed-string grep.
- No `[machine-checked: ...]` tags or `theories/*.v` pointers exist in this appendix (none to preserve).
- No new `@bibkey` citations: only the pre-existing keys `@billingsley1995`, `@dias2018nma`,
  `@phillippo2025general` are cited. `@phillippo2016tsd` is not cited here; no `...tsd` without `18`.

## Build safety

ASCII-only in math mode (the sole non-ASCII, the section sign in the Notes citation to Billingsley, is in
prose and was in the original). No bare `align`/`equation`/`gather` inside `$$`; worked examples use
`aligned`. Even `$$` count (34) and even `:::` fence count (18). Blank line before every top-level
heading; the `##` titles that follow `:::` fences are the standard Quarto theorem-environment grammar
(matching the original `def-dist-dirichlet`). No `\not` on an extensible arrow. Every new `#sec-` id
unique across the book.
