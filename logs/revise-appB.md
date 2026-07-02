# Revision log: Appendix B (Matrix Calculus Identities)

File: `appendices/B-matrix-calculus.qmd`. Kind: proved.
Before: 786 lines. After: 1325 lines. Net +539 lines (expansion only; nothing cut).

## Reviewer points addressed

### ChatGPT reviewer, highest-priority fixes
1. **Differentials as first-order changes, with scalar analogy and matrix example.** Added a new section
   `#sec-mc-warmup` ("A scalar warm-up") recalling `f(x+h)=f(x)+f'(x)h+o(h)`, working `f(x)=x^2` to
   `df=2x dx`, and framing matrix calculus as the same statement with an inner product. Added a plain-words
   paragraph in `#sec-mc-differential` explaining `dX` (bookkeeping symbol for a small change in every
   entry) and `dF` (its first-order effect), with the noncommutativity caution.
2. **Applied likelihood bridge.** Added the multivariate normal / REML log-likelihood
   `-1/2 log det V - 1/2 r^T V^{-1} r` as `#eq-mc-mvn-loglik` at the head of `#sec-mc-trace-inverse-det`,
   and a fully worked assembly of the variance-component score `#exm-mc-variance-score` (equation
   `#eq-mc-variance-score`) that differentiates it term by term using the log-det and inverse identities.
3. **Trace-trick pedagogy.** Added the four-step "canonical-form recipe," an explicit cyclic-vs-arbitrary
   warning (`tr(ABC)=tr(BCA)=tr(CAB)` but not `tr(ACB)`), a `tr(A dX B)` mini example, and a from-scratch
   worked example `#exm-mc-trace-derivative` for `tr(X)` and `tr(AX)`.
4. **Woodbury less abstract + V collision.** Expanded `#sec-mc-woodbury` intro to map `A,U,C,V` to
   diagonal residual variance, random-effect loading, random-effect covariance, and `U^T`; added an
   explicit warning that plain `V` here is not the covariance `\mathbf{V}` nor a vector space; pointed to
   the ML-NMR marginal likelihood as the ITC instance.
5. **Compound-symmetry health framing.** Added a paragraph defining `n`, `sigma^2` (within-study/residual
   variance), `tau^2` (between-study heterogeneity), `\mathbf{1}_n`, and `\mathbf{1}_n\mathbf{1}_n^T`
   (single shared random effect, rank one) in meta-analysis terms, and why the `tau^2` derivative is
   needed (it is the variance-component score).
6. **Shape checks and "where used."** Added parenthetical shape checks throughout the reader translations;
   added a "Used in the book for" column to the summary table plus two new rows (Woodbury inverse, matrix
   determinant lemma).

### GLM reviewer, highest-priority items
- **Scalar warm-up** (`#sec-mc-warmup`); **layout convention** named (numerator vs denominator, we use
  denominator/same-shape, with the "off by a transpose is a layout difference" warning); **two early
  worked examples** (`#exm-mc-trace-derivative`, `#exm-mc-quadratic`); **worked ITC example** added as new
  section `#sec-mc-logistic` (logistic-regression score `#eq-mc-logistic-score` = `X^T(y-p)`, Hessian
  `#eq-mc-logistic-hessian` = `-X^T W X`, Fisher information, numeric 2x2 instance, IRLS link);
  **Hessian expanded** (curvature, min/max/saddle, Fisher information = negative expected Hessian, Newton
  step); **dense sections broken up** with examples and a displayed 2x2 derivation in the symmetric-gradient
  remark; **jargon defined at first use** (minor/cofactor/adjugate/Cramer before the inverse derivative;
  `C^2`, open set, Landau `o`/`O`, submultiplicative, capacitance, `\mathbf{1}_n`); **why-differentials
  demonstration** (entrywise vs differential contrast in the trace-derivative reader translation and the
  recipe); **bold-matrix convention flagged** ("A note on symbols used only here"); **purpose mapping
  moved up** into the intro "How to read this appendix" plus per-identity reader translations.
- Other specific under-explanations closed: `nabla f = J_f^T` paradox resolved (two arrangements of the
  same partials); Frobenius inner product explained as the flattened dot product; identification-lemma
  usefulness sentence added; inverse-derivative index collapse explained (`E_ij` has one nonzero entry);
  Jacobi key step unpacked plus an "accept on first reading" signpost; chain-rule flattening shown to be
  order-independent; Schur factorization verified for all four blocks; determinant-lemma block matrix `P`
  motivated; Sherman-Morrison verified on a 2x2 (`#exm-mc-sherman-morrison`).

## Deliberately skipped (with reason)
- **No Exercises section / star-convention line.** The appendix has no Exercises section; per the scope
  note, warm-up exercises and the `$\star$` line apply only if one already exists. Not forced.
- **No single running narrative example.** Per the appendix-specific guidance (proved-identities
  appendix), the requested form is a tiny 2x2 / 2-vector worked instance per load-bearing identity plus a
  lookup table, which is what was added, rather than one threaded story.

## Mathematical errors
- No pre-existing mathematical error was found; neither reviewer flagged an incorrect identity, and every
  identity was re-checked. All new numeric instances were verified by hand (compound-symmetry 2x2/3x3,
  Sherman-Morrison 2x2, symmetric-gradient 2x2, Jacobian at (1,2), quadratic gradient at (1,1), logistic
  score and 2x2 Fisher information). One transient artifact I introduced mid-edit (a stray word and an
  incorrect triple-sum index expression in the trace-derivative reader translation) was corrected before
  finalizing.

## New labeled environments and tables
- Sections: `#sec-mc-warmup`, `#sec-mc-logistic`.
- Examples: `#exm-mc-trace-derivative`, `#exm-mc-jacobian`, `#exm-mc-quadratic`,
  `#exm-mc-sherman-morrison`, `#exm-mc-variance-score`.
- Equations: `#eq-mc-scalar-deriv`, `#eq-mc-mvn-loglik`, `#eq-mc-variance-score`,
  `#eq-mc-logistic-score`, `#eq-mc-logistic-hessian`.
- Tables: expanded the existing summary table (`#sec-mc-summary`) with a "Used in the book for" column and
  two new rows (Woodbury, matrix determinant lemma). No brand-new standalone table added.
- Reader translations / glosses added: ~38 (after every definition, identity, and worked instance).

## Preservation confirmation
- Every existing `#thm-`, `#lem-`, `#cor-`, `#def-`, `#eq-`, `#sec-` label preserved verbatim; none
  renamed or removed. Tempted by but preserved: `def-mc-jacobian`, all `eq-mc-*`, `thm-*`, `lem-*`,
  `cor-*`, `sec-mc-*` (referenced across the appendix and potentially elsewhere).
- Every existing theorem, lemma, corollary, proof, and worked computation preserved; all additions are
  scaffolding, intuition, examples, and cross-links.
- Machine-checked tags: the appendix carries none by design (its identities sit below the statistical/causal
  layer of `ITC_Coq`); none were removed and none were added.
- Citations: only `@strang2016` and `@dias2018nma` appear (both pre-existing in `references.bib`); no new
  bib keys introduced. No `@phillippo2016tsd` occurrence exists here, so no `18` fix was needed.

## Build safety
- ASCII-only in math mode; `$\star$` not used; no `\not` on extensible arrows; no bare
  `align`/`equation`/`gather` inside `$$` (only `aligned`/`pmatrix`/`smallmatrix`); every `#sec-` id
  unique; blank line before every document section heading (theorem-title `##` lines sit inside `:::`
  divs by design). Verified: 40/40 div fences balanced, no non-ASCII, no dash punctuation, all 36
  intra-appendix cross-references resolve.
