# Revision log: Chapter 6, Linear Regression from First Principles

File revised: `chapters/part1/06-linear-regression.qmd`
Reviewer files addressed: `feedback/chatgpt/ch06-linear-regression.md`, `feedback/glm/ch06-linear-regression.md`.
Both reviewers' "highest-priority fixes" were prioritized. Rendered standalone to HTML with Quarto 1.8.26:
the document builds with no Markdown, div, or math errors; the only warnings are cross-chapter crossrefs
that resolve in the full book build.

## Hard constraints honored

- No existing label removed or renamed. All original `#sec-`, `#def-`, `#thm-`, `#lem-`, `#cor-`,
  `#prp-`, `#eq-`, `#exr-` ids verified still present (script check passed with zero MISSING).
- Every existing theorem and proof preserved in full. Edits to proofs only added labels, bridge
  sentences, and references; no mathematics was cut or shortened.
- PDF build safety (STYLE Section 11) checked: ASCII only in math (the sole non-ASCII is the accented
  "e" in Cramer-Rao, all in prose, which was already in the original and is permitted); `$\star$` used,
  no Unicode star; no `\not` on an extensible arrow; no bare `align`/`equation`/`gather` inside `$$`;
  no new `#sec-` ids (subsections use plain `###` headers, so no uniqueness risk); div openers and
  closers balanced (77/77); the three ASCII schematics are fenced verbatim code blocks (6 fences).
- American English and the no-dash rule kept throughout.

## New labeled environments added (all slugs verified globally unused before adding)

- `#exm-lr-running` (example): the running two-arm trial, introduced right after the intro.
- `#exm-lr-betahat` (example): numeric estimate from the running trial, placed right after the normal
  equations.
- `#lem-idempotent-rank-trace` (lemma + proof): "rank of a symmetric idempotent equals its trace,"
  isolated as its own named result (GLM reviewer's request).
- `#def-loewner-order` (definition): the Loewner partial order, with a scalar translation.
- `#thm-general-linear-hypothesis` (theorem + full proof) and `#eq-glh-stat` (its display): promotes the
  general linear hypothesis from a remark-plus-exercise to a stated, proved theorem.
- `#def-estimable` (definition): promotes "estimable" from a parenthetical to a definition box with a
  reader translation and a treatment-contrast example.
- `#exr-lr-warmup-design`, `#exr-lr-interpret-coef`, `#exr-lr-warmup-compute` (exercises): accessible
  warm-up and interpretation problems placed before the proof-heavy exercises.

No bib keys invented. New cross-references to existing Part II labels `@def-prognostic-variable` and
`@def-effect-modifier` were added (both confirmed to exist). Software names (R's `lm()` and
`linearHypothesis()`) are mentioned as tools, not citations. The "Laplace error model" remark needs no
citation (it is the standard MLE-of-absolute-deviations fact, stated, not attributed).

## ChatGPT reviewer: highest-priority fixes

1. Concrete health design-matrix example after the linear-model definition: added `#exm-lr-running`
   (design-matrix role table mapping columns to coefficients, concrete 6-patient X and y) immediately at
   the start of @sec-lr-model, before the formal definition.
2. Bridge from coefficient interpretation to prognostic variables, effect modifiers, and treatment
   effects before non-collapsibility: rewrote the coefficient-interpretation remark in @sec-lr-model with
   a three-bullet health bridge (treatment effect, prognostic effect, effect modifier) using the running
   example; non-collapsibility now comes last.
3. Roadmaps before the Gauss-Markov and chi-squared proofs: added "Roadmap of the proof" paragraphs
   before @thm-ols-blue and @thm-rss-chisq (and also before @thm-ftest); added a recap after the
   chi-squared proof.
4. Clinically interpretable worked example / treatment mini example: gave @sec-lr-example a clinical
   reading (x = baseline severity, y = change in outcome) with interpretation of slope, residuals, CI,
   and the nonsignificant test, all without changing the arithmetic; the treatment-covariate example is
   carried by `#exm-lr-running`/`#exm-lr-betahat`.
5. ITC throughline throughout: added "Why this matters (ITC)" notes after the normal equations (STC
   predict-at-comparator), Gauss-Markov (MAIC as weighted GLS), the rank-deficiency proposition
   (estimability of contrasts in networks), and a closing "Tying it back" paragraph in the worked
   example.

## GLM reviewer: key points

- Four optimality principles enumerated (i) to (iv) with one sentence on why each differs, in the intro.
- "Why squares" preview added immediately after the question in the intro, pointing to @sec-lr-mle and
  contrasting Gaussian (squares) with Laplace (absolute) errors; the payoff is restated at @sec-lr-mle.
- "How to read this chapter" note: proofs may be skipped on first reading; plus a four-layer reader-map
  table.
- G2 homoskedasticity: added a plain-language remark with a fanning-band picture, when a health
  researcher should expect failure (clustered trials, scale-dependent scatter), and a one-line sandwich
  gloss.
- error vs residual: added a notation-role table after the definition that fixes which symbols are
  observed and which are population unknowns.
- `@lem-gram-nullspace` proof split into four labeled steps; `rank(X^T) = rank(X)` is now spelled out as
  row-rank-equals-column-rank.
- `@thm-ols-normal-equations`: quadratic-form glossed, scalar reading of the gradient added, the iff
  split into explicit "Forward direction" and "Reverse direction," and a plain consistency gloss ("always
  solvable, may not be unique").
- "normal" = perpendicular explained in a remark at the normal equations.
- Trace trick stated as its own remark before @thm-sigma2-unbiased, referencing Chapter 1.
- MGF intuition (fingerprint; factorization equals independence) added before the two MVN lemmas;
  @sec-lr-normal split into "### Two facts about the multivariate normal" and "### The three
  distributional pillars."
- `@thm-rss-chisq`: new `#lem-idempotent-rank-trace` carries the crux; the proof now cites it and
  explains why there are exactly n-p unit eigenvalues; a recap and an ASCII rotation schematic added.
- `@thm-ftest`: the P^2 four-term expansion annotated; "PM_1 = 0 implies orthogonal ranges implies
  independent Gaussians" spelled out; rank(P) = tr(P) now cites the idempotent lemma.
- General linear hypothesis promoted to `#thm-general-linear-hypothesis` with a full proof; "whitening"
  defined in line; `@exr-lr-general-hypothesis` reframed to the nested-model equivalence with a hint.
- "estimable" promoted to `#def-estimable` with example and a four-fundamental-subspaces table giving
  each subspace its regression meaning.
- Loewner order defined (`#def-loewner-order`) with the variance translation, before its first use.
- Hat matrix motivated by a diagnostics remark (leverage, Cook's distance, pointer to
  @exr-lr-leverage); idempotence given a plain meaning.
- Profile likelihood argument spelled out and the term "profile log-likelihood" defined in
  @thm-ols-mle-normal; @sec-lr-mle given subsection headers; Cramer-Rao block-diagonal argument expanded
  with a reader translation.
- Quantile notation `t_{n-p,1-alpha/2}` interpreted; "pivotal quantity" glossed.
- ESS_reg vs ESS trap flagged in a remark at first use of ESS_reg.
- t and F health readings added; R-squared reader translation added; what `lm()` actually computes noted.
- Exercises: star convention stated in one line at the top; three warm-up/interpretation exercises added
  before the proof-heavy ones; the two starred exercises kept starred but given motivation and stronger
  hints.

## Reader translations and "Why this matters" coverage

Reader translations added after the linear-model definition, the sums-of-squares definition, the Gram
lemma, the hat-matrix definition, the projection derivation, `@prp-fitted-residual-geometry`, the moments
theorem, the Loewner definition, the idempotent lemma, the R-squared definition, and the estimable
definition. "Why this matters" lines added after the normal equations, Gauss-Markov, the variance
estimator, hat-matrix properties, normality of beta-hat, the chi-squared theorem, the t test, the F test,
the MLE theorem, Cramer-Rao, the general linear hypothesis, and the rank-deficiency proposition.

## Figures (deliberate decision)

The book uses no figures or TikZ anywhere (confirmed by grep). Rather than introduce binary image files
or a TikZ dependency that could threaten the pdflatex build, the three figure requests (projection
geometry, ANOVA right triangle, chi-squared rotation) were met with build-safe ASCII schematics inside
fenced verbatim code blocks. If the maintainers later add a figure pipeline, these are the three places
to upgrade to real diagrams.

## Deliberately not changed

- The original n=5 worked example arithmetic is untouched; only a clinical reading was layered on, as the
  reviewers requested (they liked the arithmetic).
- `notation.qmd` not edited (out of scope). The ESS_reg vs ESS trap, which the GLM reviewer flagged, is
  handled by an in-chapter remark; notation.qmd already footnotes it.
- The two starred exercises were not de-starred: the `$\star$` marker is the book-wide signal that a full
  solution lives in Appendix F, so de-starring would break that contract. They were instead given
  motivation (MAIC and network hypotheses) and stronger hints.
- No machine-checked tag added: the chapter has no `ITC_Coq` counterpart, as the existing notes state.

## Suggested follow-up for the orchestrator

- Appendix F (`appendices/F-solutions.qmd`) is still a stub. Solutions for the starred exercises
  `@exr-lr-gm-weighted` and `@exr-lr-general-hypothesis` should be authored there to honor the star
  convention now stated at the top of this chapter's exercises.
