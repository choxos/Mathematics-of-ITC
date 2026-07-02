# Revision log: Chapter 7 (Generalized Linear Models)

Pedagogical-accessibility revision pass. Target reader: novice health researcher with weak mathematics.
Addressed both feedback files: `feedback/chatgpt/ch07-glm.md` and `feedback/glm/ch07-glm.md`, prioritizing
each reviewer's "highest-priority fixes". No existing label was removed or renamed; every theorem, lemma,
proposition, corollary, and its full proof was preserved (11 proofs before and after). All additions are
scaffolding: examples, intuition paragraphs, reader translations, "why this matters" lines, jargon
definitions, and warm-up exercises. Chapter grew from 1416 to 1587 lines.

## Context: this chapter was already partially revised

An earlier interrupted pass had already added a large amount of the requested scaffolding. To avoid
duplication I first inventoried what was present, then added only what the two reviewers still ask for.
Already present (NOT duplicated): the running trial example `#exm-glm-running` and the local
GLM-objects-and-scales table in `#sec-glm-map`; the "Why a single family" motivation; the "Why trial data
arrive as a proportion with a weight" remark; the term-by-term Bernoulli decomposition `#exm-edf-bernoulli`
placed before `@thm-glm-mean-variance`; the softened measure-theoretic opening of `#sec-edf`; the reader
translation gloss on `@eq-edf-density`; the explicit `@eq-edf-normalization` derivation; the cumulant
function vs cumulant generating function disambiguation; the "strategy of the proof" paragraph and the
motivated `theta' = theta + t a(phi)` substitution with the intermediate `ty + ...` line; the openness /
intermediate-value-theorem justification for the mean space; reader translations after `@def-link-function`,
`@def-canonical-link`, `@def-glm`; the "why this matters" after `@prp-canonical-eta-theta`; the
information-equality restatement inside `@prp-glm-information`; the three-step chain-rule unpacking in the
`@thm-glm-score` proof; the "logistic score in its familiar form" remark; the "IRLS in words" remark; and
`\nu` in the reused-symbols remark. These map to glm suggestions 1, 2, 3, 11, 12 and ChatGPT
highest-priority 1, 2, and part of 3, which were therefore already satisfied.

## Feedback points addressed in THIS pass (what I added)

### ChatGPT highest-priority fixes
1. (map before EDF) Already present; left as is.
2. (grouped binomial) Already present; left as is.
3. (logistic-specific derivation beside general score AND IRLS) Score half already present. Added the IRLS
   half: new remark "One IRLS step, with numbers" immediately after the "IRLS in words" remark in
   `#sec-glm-estimation`, computing one working response and weight on the `@sec-glm-worked` data and
   landing `beta^(1)=(-1.2,2.0)`. This is also glm suggestions 4 and 10.
4. (bridge conditional link-scale to marginal population estimand before non-collapsibility) Added a
   sentence at the end of `#sec-logistic` making the word "conditional" load-bearing and forward-pointing;
   added a clinical frame plus an explicit conditional-vs-marginal systematic-review paragraph at the top
   of `#sec-noncollapsibility`.
5. (deviance more intuitive before saturated models and Bregman) Expanded the two-sentence opening of
   `#sec-deviance` into a full RSS-to-deviance bridge paragraph; added a "reader translation" after
   `@def-deviance`; added a boxed Bregman-divergence definition (see 7 below).
6. (soften/explain universal attenuation) Added, after `@exm-noncollapsible-or`, a justification that the
   marginal odds ratio always lands strictly between 1 and the conditional value, tied to logit convexity
   and Jensen, with an explicit pointer to the starred `@exr-glm-noncollapse` for the general proof.

### glm reviewer suggestions
- (4/10 numeric IRLS interlude) Added, see ChatGPT 3 above.
- (5 figure) DELIBERATELY NOT ADDED; see "Left unchanged" below.
- (6 clinical frame up front for non-collapsibility) Added preamble paragraph with the concrete OR 3.5
  in both age strata pooling to about 3.14, matching the exact numbers of `@exm-noncollapsible-or`.
- (7 define or remove Bregman divergence) Added a `.remark` "Bregman divergence (a named building block)"
  defining `D_b(u,v)` before `@prp-deviance-nonneg`, and softened the proof's re-introduction of the term
  to reference that definition (wording only; no math changed).
- (8 expand hazard-ratio subsection) Added the Jensen display `bar S_t(u) > e^{-E[H_t]}` with an explicit
  `@thm-jensen` reference and an explicit "this subsection is only a conceptual preview" signpost noting
  the full proof is deferred.
- (9 what asymptotic normality is for) Added a "Why this matters" after `@cor-glm-asymptotic-normality`
  stating this is what makes fitting software report standard errors and confidence intervals.
- (11/12) Already present.

### glm "what was unclear" / "not elaborated" / "missing motivation" items
- (`@def-saturated-model` derivative step) Added the explicit `d/dtheta_i[y_i theta_i - b(theta_i)] =
  y_i - b'(theta_i) = 0` step.
- (`@def-non-collapsibility` heavy quantifier) Added a plain-language gloss ("collapsible when a
  conditional effect identical in every stratum is inherited unchanged by the pooled population, no matter
  how large or small the strata are").
- (linear-is-special shown, not asserted) Added the one-line display
  `E[mu_1] - E[mu_0] = E[mu_1 - mu_0] = delta` at the top of `#sec-noncollapsibility`.
- (`@prp-glm-information` bridge to standard errors) Added a "Why this matters" tying `X^T W X` to the
  Chapter 6 `X^T X` and to the printed standard errors.
- (analysis of deviance = ANOVA F-test) Added a sentence in the "Reading an analysis-of-deviance table"
  remark making the linear-model ANOVA analogy explicit.

### ChatGPT "under-explained" items
- (variance function trial motivation) Added a sentence to the "Why the variance is tied to the mean"
  remark: uncertainty near p = 1/2 exceeds that near 0 or 1; count scatter grows with the mean.
- (overdispersion) Added a `.remark` "Overdispersion: where the dispersion re-enters" explaining that phi
  cancels from beta-hat but rescales standard errors, with quasi-likelihood / negative-binomial /
  random-effects remedies and a pointer to Chapter 8.
- (separation health example) Added a concrete subgroup instance (all 8 treated respond, 0 of 6 controls)
  to the separation remark so the divergence of the estimate is tangible.
- ("why this matters for ITC" after estimation) Added a `.remark` "Why this matters for indirect
  comparison" at the end of `#sec-glm-estimation` (before Deviance).
- (clinical framing on `@exm-noncollapsible-or`) Added a one-sentence reading of X as an age group with the
  two columns as control/active response probabilities.

### Exercises (task requirement + both reviewers)
- The starred-exercise convention line was already present; extended it to note the first four exercises
  are low-barrier. Added four accessible exercises before the existing proof-heavy ones, matching the four
  types ChatGPT listed: `#exr-glm-fitted-prob` (warm-up, fitted probability from a linear predictor and an
  odds ratio), `#exr-glm-interpret-or` (interpretation, reading a coefficient as a conditional OR, reusing
  `@exm-glm-running`), `#exr-glm-identify-link` (warm-up, name family/link/variance function), and
  `#exr-glm-cond-marg-words` (interpretation, conditional vs marginal in words). Labeled (Warm-up.) /
  (Interpretation.).

## New labels added (all unique; verified no collision)
- Exercises: `#exr-glm-fitted-prob`, `#exr-glm-interpret-or`, `#exr-glm-identify-link`,
  `#exr-glm-cond-marg-words`.
- No new theorem/lemma/proposition/corollary/definition/equation labels. Two display equations I initially
  labeled (`eq-linear-collapses`, `eq-hr-jensen`) were converted back to unlabeled displays because nothing
  cross-references them (STYLE: label only equations you will reference).
- New unlabeled callouts (`.remark`): "One IRLS step, with numbers"; "Overdispersion: where the dispersion
  re-enters"; "Why this matters for indirect comparison"; "Bregman divergence (a named building block)".

## Notation / references
- No new notation symbols introduced; all symbols already in `notation.qmd` or defined in the chapter.
- No new bibtex keys used. Citations used in additions (`@dias2018nma`, `@thm-jensen`, and internal cross
  references) already exist. No new source needed.
- No machine-checked tags added or changed; the existing `@prp-collapsibility-rd-rr` tag is untouched.

## PDF build safety (STYLE Section 11) verification
- ASCII-only in math confirmed by scan: zero non-ASCII characters in the file.
- Star marker uses `$\star$` only; no Unicode star.
- No bare `align`/`equation`/`gather` inside `$$`; new displays are single expressions or use `\bigl...`.
- No `\not` applied to an extensible arrow.
- All Quarto divs balanced (63 opens / 63 closes); blank line precedes every heading.
- No `#sec-` ids added or duplicated; `[Notation](/notation.qmd)` link style preserved.
- American English and the no-dash rule respected in all additions (semicolons/colons used as connectors;
  the only in-file double hyphens are the YAML fence and Markdown table separators; the only spaced hyphen
  is a LaTeX minus sign inside math).

## Deliberately left unchanged
- No figure was added (glm suggestion 5, ChatGPT figure request). Rationale: PDF build safety is a hard
  constraint, there are no image assets in the repo for this chapter, and a hand-authored TikZ/graphic
  risks the pdflatex build. The IRLS geometry is instead carried by the existing "IRLS in words" remark
  plus the new numeric interlude, which together give the synthetic-response / weighted-regression picture
  in words and numbers. Flagged here for a future pass if a figure pipeline is added.
- `@sec-glm-worked` was left at the end of the chapter rather than relocated (glm suggestion 10). The
  reviewers said a numeric interlude inside `#sec-glm-estimation` would suffice "even if it duplicates part
  of `@sec-glm-worked`"; that interlude was added, so the full worked example stays where it caps the
  formal development.
- The hazard-ratio non-collapsibility proof remains a forward reference to the survival chapters, now with
  an explicit conceptual-preview signpost and a Jensen display; the deferral itself is intended (the
  survival machinery is not yet available) and is documented in `#sec-glm-notes`.
- No mathematics was cut or shortened anywhere.
