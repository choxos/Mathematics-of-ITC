# Revision log: Appendix F (Solutions to Selected Exercises)

File: `appendices/F-solutions.qmd`. Kind: solutions. Agent: Opus 4.8 (max effort).
Before: 2254 lines. After: 3258 lines (+1004). No solution deleted or renumbered; all 60 solution
headings and their `@exr-` slugs preserved.

## Reviewers addressed

Both `feedback/chatgpt/appendix-F-solutions.md` and `feedback/glm/appendix-F-solutions.md`, prioritizing
each reviewer's highest-priority list.

## Correctness fixes (mathematics changed)

1. **`@exr-graphoid-counterexample` (ChatGPT + GLM, highest priority).** The original counterexample was
   wrong: it set `X=Y=Z` with `W` degenerate, but conditioning on `Z` then makes `X` a constant, so
   `X ⊥ (Y,W) | Z` actually HOLDS and the claimed failure does not occur. Replaced with the correct
   construction: `X = Y = W = U` (three copies of one Bernoulli bit) and `Z` degenerate. Now both premises
   hold by degeneracy under conditioning, while the conclusion `X ⊥ (Y,W) | Z` genuinely fails
   (`P(X=1,(Y,W)=(1,1)) = 1/2 ≠ 1/4`). Also restated the G5 axiom in the solution, defined positivity, and
   added a positivity-versus-zero-probability common-mistake note.
2. **`@exr-glm-noncollapse` (ChatGPT).** Deleted the false claim that `a/(1+a)` is "strictly convex"; it is
   strictly concave for `a>0`. Reworded so the covariance inequality is correctly attributed to monotonicity
   of two like-increasing functions, with the concavity connected to Jensen from the marginal-risk viewpoint.
3. **`@exr-james-stein-sure` (ChatGPT).** Removed the overstated claim that positive-part James-Stein has
   "weakly smaller loss pointwise." Restated as risk dominance (weakly smaller risk for every theta, strictly
   when the truncation event has positive probability), explicitly noting it is not a realized-loss guarantee
   for every sample and theta.
4. **`@exr-qba-norta-margins-star` (ChatGPT + GLM).** Part (b) conflated identification of the Gaussian
   parameter rho^N with Sklar non-uniqueness of the copula. Rewrote to separate the two: within the Gaussian
   family rho^N is identified (the cell probability is strictly increasing hence injective), whereas the
   Sklar non-uniqueness is a statement about the copula function being pinned only on the discrete marginal
   grid. Part (c) started from the degenerate rho^N = 1 (which gives corr = 1 = rho^N, no strict inequality);
   rewrote to flag that case as degenerate and demonstrate strict inequality with rho^N = 0.5, deriving the
   lognormal Pearson-correlation formula (e^{sigma^2 rho^N} - 1)/(e^{sigma^2} - 1) from the Gaussian MGF.

## Opening reader guide (ChatGPT #1, GLM #10)

Replaced the terse selection-policy opening with: a "How to use these solutions" workflow (attempt first,
read the Strategy line if stuck, then the full derivation); a "Reading aids" paragraph explaining the
Strategy / Uses / Common-mistake scaffolds; and a "Coverage" paragraph asserting completeness across
Chapters 1-30.

## Navigability: plain titles on all 60 headings (both reviewers)

Every `### Solution to @exr-slug` now reads `### Solution to @exr-slug: <plain descriptive title>`, e.g.
`Solution to @exr-stc-delta: Delta-method variance of the marginal STC contrast` (the exact example ChatGPT
requested). No slug removed or renamed.

## Strategy / Uses scaffolds and expanded algebra (GLM detailed list, ChatGPT #3)

Added `Strategy` and/or plain-language `Uses` lines to the hard solutions, and expanded every
compressed-algebra passage the GLM reviewer flagged. Specifically:
- `@exr-la1-dim-sum`: motivated defining `z = sum gamma_s b_s` (isolate the W-only part).
- `@exr-oblique-vs-orthogonal`: added a 4-property roadmap table; motivated the test vector `v = m + t w`
  and the t-down/t-up squeeze; added a hat-matrix/OLS-residual closing.
- `@exr-ata-aat-spectrum`: wrote out the swapped injection `u -> A^T u` explicitly; added a concrete 2x3
  numerical example with singular values.
- `@exr-weyl-inequality`: plain-language reading of Courant-Fischer min-max; derived Rayleigh additivity;
  motivated the "apply the upper bound to A+B and -B" symmetry; added a 2x2 numerical check and a
  covariance-stability closing.
- `@exr-cov-psd-construction`: added the missing intermediate line for the factor 2 in `Var(X1-X2)`.
- `@exr-information-equality-fail`: wrote out the Leibniz variable-limit rule and the boundary term.
- `@exr-sandwich-derivation`: defined "working" (M-estimation) and the overdispersion ratio kappa before use.
- `@exr-glm-irls-probit`: wrote the Hessian out; computed `c'(eta)` explicitly and showed it is not
  identically zero.
- `@exr-james-stein-sure`: expanded the divergence (quotient rule for `d/dy_j [y_j/||y||^2]` and the
  sum-combination step); added a "why J >= 3" block (J=2 gives g=0, J=1 gives infinite `E[1/Y^2]`).
- `@exr-reml-one-way`: defined "error contrast" and `1_{In}`; derived the two chi-square facts.
- `@exr-lr-general-hypothesis`: wrote the quadratic expansion `||r - Xd||^2 = ||r||^2 - 2 d^T X^T r + d^T X^T X d`.
- `@exr-limits-general-attenuation`: split into labeled (a)/(b)/(c); derived `E[Phi(a+rho X)]` via an
  auxiliary standard normal.
- `@exr-maic-sandwich-vs-naive`: defined bread/meat/influence function/block-lower-triangular; added the
  M-estimation expansion chain and the explicit `-A^{-1} psi` row extraction.
- `@exr-stc-loglink-cancellation`: showed the `(b1+b2)^T Sigma (b1+b2) - b1^T Sigma b1` expansion.
- `@exr-qmc-logit-pipeline`: showed the `Var(aX+bY)` line giving `Var(eta) = 1.25 + rho`.
- `@exr-comp-gpd`: showed the factor-out step for `f(x) ~ C x^{-1/k-1}`; defined PSIS-LOO / importance
  ratios / self-normalized estimator.
- `@exr-genlik-mhr-attenuation`: derived `g'(c) = -Var_c(rho)` by the quotient rule; defined
  survivor-weighted / risk-set mean.
- `@exr-qba-itc-evalue-star`: derived the constant `K` from the log-linear model via the Gaussian MGF.
- `@exr-emcoll-or-attenuation`: restated the change-of-measure (tilt-derivative) identity.
- `@exr-transport-attenuation`: expanded the `phi''` log-differentiation, term by term.
- `@exr-pat-noncollapsible-target`: showed the subtractions producing the Jensen-gap values.
- `@exr-mlnmr-sema-gap`: split into (a)-(d) and broke the three-line gap expression into named pieces.

## Glosses, common-mistake notes, applied closings, examples (GLM jargon list, ChatGPT #5/#6)

- Jargon defined at first use: "working" and kappa (sandwich), "error contrast"/`1_{In}` (REML),
  "Hajek-form" (stabilized), efficiency bound (eif-control), bread/meat/influence function
  (maic-sandwich), survivor-weighted/risk-set (mhr), Frechet bounds/comonotone/countermonotone/Sklar
  (qba-norta), PSIS-LOO (comp-gpd), proof tiers F/P and named premise (coq).
- Five Common-mistake notes, one per ChatGPT-listed confusion: positivity vs zero probability
  (graphoid), non-collapsibility vs effect modification (glm-noncollapse), collapsibility vs
  transportability (genlik-rmst-transport), naive vs sandwich MAIC variance (maic-sandwich-vs-naive),
  latent vs observed correlation (qmc-gaussian-copula-cov).
- Applied closings strengthened for early/mathematical solutions: la1-gram-rank (unique drug-effect
  estimate), oblique (hat matrix/OLS residuals), weyl (covariance stability), glm-noncollapse (HTA
  conditional-vs-marginal), po-positivity-failure (concrete MAIC/STC no-elderly-patients overlap),
  distance-secondmoment (regulators should not accept a small Mahalanobis distance as a validity
  certificate).
- New numeric/tabular content: 4-property table (oblique), 2x3 example (ata-aat), 2x2 check (weyl),
  marginal-OR-vs-prevalence table (glm-noncollapse), N=4 R-hat floor 0.866 (comp-rhat-floor), illustrative
  Coq snippet in a fenced ```coq block (coq-discrete-vs-named).

## Deliberately not done (scope)

- No explicit "advanced / optional" tags on individual proof blocks (ChatGPT). The Strategy lines serve the
  same function (state the takeaway before the algebra) without a 60-solution structural change that would
  risk inconsistency.
- No per-chapter "starred exercises covered: N" checklist (GLM #10). Addressed instead by the opening
  Coverage paragraph. A full checklist would duplicate the chapter exercise sections.
- Star-convention line and new warm-up exercises: not applicable (this appendix has no Exercises section of
  its own), per the task's appendix-specific guidance.

## Preserved (hard constraints)

- All 60 `@exr-` solution labels/slugs preserved; none deleted, renamed, or renumbered.
- Every existing proof, identity, and numerical result preserved; additions are scaffolding, intuition,
  and expanded intermediate steps only.
- No existing `@thm-`/`@lem-`/`@def-`/`@eq-`/`@prp-`/`@cor-`/`@sec-` cross-reference removed or renamed.
- No `[machine-checked: ...]` tag or `theories/*.v` pointer exists in this file (solutions appendix), so
  none altered. The single occurrence of "machine-checked" is prose in the coq-solution title line.

## Build-safety verification (Section 11)

- File is 100% ASCII (no non-ASCII characters anywhere; verified by scan). No Unicode in math mode; star
  marker already `$\star$`.
- `$$` delimiters balanced (344 tokens, even); total `$` even (5108); inline `$` after removing display
  blocks even (4420). `aligned`/`cases`/`pmatrix` begin/end all matched; zero bare
  `align`/`equation`/`gather`.
- Every `#`/`##`/`###`/`####` heading has a preceding blank line. Tables and the fenced ```coq block have
  surrounding blank lines.
- No `@phillippo2016tsd` without the trailing `18`. No new `@bibkey` bibliography citations introduced;
  all references are to existing labeled environments.
- Did NOT render (orchestrator renders).
