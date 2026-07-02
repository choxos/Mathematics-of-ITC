# Revision log: Chapter 10, Adjustment Methods

Revised for pedagogical accessibility per STYLE.md Section 10, addressing both
reviewer files (`feedback/chatgpt/ch10-adjustment-methods.md` and
`feedback/glm/ch10-adjustment-methods.md`). All existing labels, theorem
statements, and proofs are preserved verbatim; every change is additive
scaffolding, intuition, tables, signposts, or an inline gloss on a step a
reviewer flagged as opaque.

## Highest-priority fixes addressed

ChatGPT reviewer:
1. Plain-language intuition before the balancing-score and Rosenbaum-Rubin
   material: added a curse-of-dimensionality bridge, a *Reader translation* with
   verbal histogram picture after `@def-balancing-score`, a "coarsest points the
   other way" intuition paragraph, and `@exm-adj-coarsest` (two covariates
   collapsing to one propensity value) before `@thm-rosenbaum-rubin`.
2. Concrete observed-data example: added `@exm-adj-observed`, a ten-patient table
   with columns $X$, $T$, $Y$, $\hat e(X)$, weight, $\hat m_1$, $\hat m_0$, then
   naive / Hajek-IPW / g-computation / ESS worked on those rows (new subsection
   `#sec-adj-observed`).
3. Positivity / overlap / extrapolation in health terms: new paragraph after
   `@prp-ipw-variance` translating positivity to graded overlap (eligibility,
   prescribing habit, sparse cells) plus the cost-of-overlap table
   `@tbl-adj-overlap` ($\varepsilon\in\{0.4,0.2,0.1,0.05\}$).
4. Connection to ITCs: expanded intro bridge (transport / target population), plus
   explicit end-of-section callbacks: IPW -> MAIC (`@tbl-adj-weights` context),
   standardization -> STC (`#sec-adj-att`), AIPW -> ML-NMR, EIF -> shared variance
   ceiling.
5. EIF reframed as advanced: added an "Advanced material; one-paragraph takeaway"
   box, a frontloaded Cramer-Rao analogy, and a three-ideas list separating
   influence function / efficient influence function / semiparametric bound /
   regular estimator, plus a *Why this matters* linking $V^\ast$ to poor overlap
   and wide MAIC confidence intervals.
6. Estimator recipe boxes (IPW, g-computation, AIPW) and difficulty-labeled
   exercises (see below).

GLM reviewer:
- Plain-English assumptions box after Standing assumptions (A); a gathered
  glossary box defining $P_X$, $\sigma(W)\vee\mathcal G$, $\operatorname*{ess\,inf}$,
  graphoid G2/G4, "nuisance function," and $\blacktriangleleft$.
- Defined "surface" and unpacked the "insurance property" in the opening.
- `@lem-ci-binary-criterion`: added the warning that binary $T$ is essential and
  the shortcut collapses for 3+ levels. `@lem-ci-factorization`: explained
  bounded-vs-integrable and the truncation / dominated-convergence step.
- `@thm-rosenbaum-rubin` proof: inserted the measure-theoretic fact (conditional
  expectation is measurable w.r.t. its conditioning $\sigma$-algebra) inline.
  `@thm-ps-sufficiency` proof: glossed $\sigma(b(X))\subseteq\sigma(X)$ as "b(X)
  carries no more information than X."
- `@eq-aipw-error`: corrected the "consistent precisely when" conflation by
  distinguishing functional-unbiasedness from estimator-consistency.
- Propensity estimand vs fitted model, and why $\hat e\to e$ uniformly rather than
  pointwise: added to the `@def-propensity-score` translation and the IPW
  *Why this matters*.
- Stabilized / Hajek / raw weights table `@tbl-adj-weights`.
- ATT-vs-ATE promoted from a parenthetical to `#sec-adj-att` with the estimand
  rewritten under $P(X\mid T=1)$ (`@eq-adj-att`) and the anchored/unanchored hook.
- Neyman orthogonality promoted from a remark to `#sec-adj-neyman` with the
  two-layer (first-order killed, second-order survives) picture and an explicit
  answer on cross-fitting in MAIC/STC/ML-NMR. The original preview remark and its
  `@exr-neyman-orthogonality` reference are retained inside the new subsection.
- Non-collapsibility scope stated up front (difference-scale assumption) in the new
  "what this chapter does not do" paragraph, so it no longer first appears in the
  references. Also states what breaks when ignorability fails (-> Chapter 28).
- Early concrete example `@exm-adj-running` (two diabetes drugs, severity
  confounder) reused at the IPW opener, the ATT translation, the overlap table,
  and the observed-data table; numbers match the existing `@exm-adjustment-worked`.

## New labeled environments added (no existing label removed or renamed)

- `#sec-adj-running`, `#exm-adj-running` (running clinical example)
- `#tbl-adj-estimators` (estimator roadmap), `#tbl-adj-weights` (raw/stabilized/
  Hajek), `#tbl-adj-overlap` (cost of poor overlap)
- `#exm-adj-coarsest` (two covariates -> one propensity)
- `#sec-adj-att`, `#eq-adj-att` (ATE vs ATT)
- `#sec-adj-neyman` (Neyman orthogonality subsection)
- `#sec-adj-observed`, `#exm-adj-observed` (ten-patient finite-sample table)
- `#exr-adj-warmup-naive`, `#exr-adj-ipw-byhand`, `#exr-adj-interpret-overlap`
  (accessible warm-up / interpretation exercises; unstarred, since Appendix F has
  no solutions for them)

All new ids checked for collision against the whole book (1893 existing ids); none
collide. Div fences balanced 59/59; `$$` and inline `$` balanced; no non-ASCII in
math; no bare align/equation/gather; no `\not` on extensible arrows; tables have
consistent columns and correctly spaced `{#tbl-...}` captions.

## Exercises

Added the standard convention line ("A starred exercise, marked $\star$, has a
full worked solution in Appendix F") and a warm-up sentence, a
`### Warm-ups and interpretation` subsection with three accessible exercises, and a
`### Computation and proof` subheading before the existing eight exercises. The two
originally starred exercises (`@exr-stabilized`, `@exr-eif-control`, which are the
two solved in `appendices/F-solutions.qmd`) keep their `($\star$)` markers; nothing
else was starred.

## Reader translations / Why-this-matters added

`@def-balancing-score`, `@def-propensity-score` (translations);
`@lem-adj-regression-identity`, `@thm-rosenbaum-rubin`, `@thm-ps-sufficiency`,
`@thm-ipw-unbiased`, `@prp-ipw-variance`, `@thm-g-computation-unbiased`,
`@thm-aipw-double-robust`, `@thm-eif-bound` (why-this-matters), each tying the
result to regression, MAIC, STC, ML-NMR, or the overlap/ESS diagnostic. Matches the
established italic `*Reader translation.*` / `*Why this matters.*` convention of
chapters 1 to 8.

## Deliberately left unchanged

- Every theorem/lemma/proposition statement and all 13 proofs (only inline
  parenthetical glosses were added where a reviewer named a specific opaque step;
  no mathematics deleted or shortened).
- `@exm-adjustment-worked` (population worked example) kept intact; the finite
  ten-patient version was added alongside it, not in place of it.
- `@lem-ci-factorization` was NOT relocated into the IPW proof (GLM suggestion 8).
  Reordering a labeled div risks cross-reference and proof-flow errors for a
  marginal pacing gain, so instead a "skim now, return when first used" signpost
  was added in the technical-interlude remark. Deliberate risk-averse choice.
- No finite-sample simulation histogram was drawn (GLM wished for one); the book is
  analytic and figure-free here, so the ten-patient table plus a written caution
  about finite-sample scatter and AIPW's asymptotic-only efficiency stands in for
  it.
- No new machine-checked tags: none of the added environments have Coq
  counterparts, consistent with the existing note that `@thm-eif-bound` has none.

## Sources and notation

- No new citations: all nine keys used (`@rosenbaum1983`, `@hernan2020whatif`,
  `@horvitzthompson1952`, `@robins1986`, `@robins1994`, `@bangrobins2005`,
  `@hahn1998`, `@vandervaart1998`, `@tsiatis2006`) already exist in
  `references.bib` and were already used by the chapter. No new bib entry needed.
- Notation flagged for the orchestrator (defined inline in the chapter, per STYLE
  rule 3): $P_X$ (marginal law of $X$) is used throughout and is currently absent
  from `notation.qmd`; consider adding it to the probability table. Also introduced
  $\tau_{\mathrm{ATT}}$ (ATT estimand) and used $\operatorname*{ess\,inf}$; both are
  defined inline and could optionally be folded into `notation.qmd`. No conflicting
  symbols introduced.
