# Revision log: Chapter 19 (STC) pedagogical accessibility pass

File: `chapters/part4/19-stc.qmd`. Before: 1101 lines. After: 1469 lines (+368, all additive scaffolding; no
mathematics cut). Catalogue G.1 to G.7 unchanged.

## Running example introduced

A single autoimmune-disease scenario carried through the chapter: new drug `A` vs competitor `B`, common
comparator (standard of care) `C`; index trial `AC` reports IPD, comparator trial `BC` is aggregate-only; one
binary covariate `x` (high-risk vs low-risk), outcome an unfavorable disease flare within six months; target
`BC` mix 0.8 high-risk vs index 0.5. These are exactly the numbers of the existing worked example
`@exm-stc-logistic`, so the new material is a genuine rehearsal for it (I also renamed the worked example's
"binary biomarker/unfavorable event" to the named running-example covariate/flare, and linked its opening line
to `@sec-stc-picture`).

## New labeled environments (all additive; nothing renamed)

- `#sec-stc-picture` — new numbered on-ramp section "A concrete picture and the STC workflow" (running example,
  triangle schematic, g-computation recap, five-step box, contrast table, when-to-use, sign/scale/notation
  tables).
- `#exm-stc-two-stratum` — "Two patients, one broken average," the concrete non-collapsibility example placed
  before the counterexample theorem.
- `#exr-stc-warmup-table` — warm-up computation exercise (full STC table by hand).
- `#exr-stc-warmup-interpret` — warm-up interpretation exercise (scale/average/overlap in words).

## New tables (5 Markdown tables + 1 ASCII schematic)

1. Conditional STC (plug-in) vs marginal STC contrast table (the task-required contrast).
2. Sign-convention table (`Lambda`/`ell_AC` = active-minus-reference vs `d_AC` = reference-first).
3. Scale table (natural outcome scale = response scale vs link scale).
4. STC-specific notation glossary table.
5. Two-stratum probability table (per-stratum vs marginal log odds ratio) before the counterexample.
Plus an ASCII anchored-triangle schematic (fenced code block; both reviewers asked for a triangle figure,
delivered as ASCII since the orchestrator renders and I cannot emit images).

## Intuition after every definition (6 additions)

"Reader's translation" paragraphs after `def-stc-outcome-model`, `def-stc-conditional`, `def-stc-estimands`,
`def-stc-marginal`; an inline plain-language gloss of "pushforward" inside `def-stc-bayes`; and a plain
one-sentence gloss ("a curved link makes the prediction at the mean covariate differ from the mean of the
predictions") before `thm-conditional-stc-bias`.

## "Why this matters" additions (5 tagged, plus equivalence numeric remark)

After `thm-stc-outcome-mle` (every STC estimator is a functional of xi-hat), after `thm-conditional-stc-bias`
(HTA stakes: cost-effectiveness model prices for the population, not the average patient), after
`thm-marginal-stc-unbiased` (licenses the method; g-computation analogue; seed of ML-NMR), after
`thm-bayesian-g-computation` (Bayesian = frequentist interval asymptotically), after `thm-stc-consistency`
(covariate-selection rule; anchored vs unanchored). The equivalence theorem `thm-maic-stc-equivalence` received
an inline "one-line numeric check" remark closing with why the two methods agree in practice.

## Reviewer points addressed

ChatGPT highest-priority fixes (all 7):
1. STC-in-five-steps workflow box — added in `@sec-stc-picture`.
2. Conditional vs marginal clarified before the bias theorem — contrast table + slogan reader-translation +
   pre-theorem gloss + two-stratum table.
3. Sign conventions tabulated — sign-convention table.
4. Covariate simulation from aggregate data — dedicated remark (proportions/means only, correlations, copula,
   impossible combinations, wrong-`f_BC` bias).
5. "No overlap required" tempered — appended definability-vs-credibility warning + diagnose/report extrapolation.
6. Non-collapsibility made intuitive — two-stratum probability table + `exm-stc-two-stratum` before the algebra.
7. Practical uncertainty checklist — four-source remark in `@sec-stc-bayes`.
Also: fixed the numeric inconsistency the reviewer flagged (`-1.44270` -> `-1.44261` in the closing-triangle
remark, now consistent with Step 2's `1.44261`).

GLM reviewer suggestions (1 to 15):
1 running clinical scenario — done, reused in worked example.
2 g-computation two-sentence recap — done.
3 "when would you use STC?" box — done (trust a model vs trust an overlap, up front).
4 anchored-triangle figure — ASCII schematic.
5 plug-in vs marginal figure — delivered as the contrast table + two-stratum numeric table (cannot emit images).
6 plug-in historical motivation — added at `def-stc-conditional` (needs only published means).
7 MLE-section framing — added purpose paragraph at head of `@sec-stc-outcome-model`.
8 bias-proof sub-labels + Taylor gloss — Parts relabeled with one-line summaries; plain gloss added.
9 promote misspecification remark — kept the remark, added a "why this matters" before it and a concrete
  quadratic-truth misspecification example after it (I did not convert it to a corollary to avoid touching the
  surrounding label structure; the emphasis and example deliver the reviewer's intent).
10 define pushforward/tower property/M-estimator — glossed inline at first use.
11 standardize scale vocabulary — added a scale table defining "natural outcome scale" = response scale, and
  adopt that phrase; did not rewrite every legacy occurrence (kept edits additive).
12 inline numeric check in equivalence — added.
13 unanchored case illustrated — "Two data scenarios" remark with a concrete prognostic variable (age).
14 move the sign-orientation remark after the worked example — DELIBERATELY NOT MOVED (see below).
15 "what is simulated" paragraph near `eq-stc-marg-mean` — added reader-translation at `def-stc-marginal`.

## Deliberate deviations / labels preserved

- GLM #14 asked to relocate the unlabeled "Orientation of the contrast" remark to after the worked example. I
  did NOT move it: it introduces the `ell_AC` notation that the worked example already uses, so moving it would
  create a forward reference. Instead I added an early sign-convention table in `@sec-stc-picture` that
  introduces `Lambda`, `ell_AC`, and `d_AC` cleanly before the remark, which resolves the reviewers' confusion
  without a risky relocation.
- All 61 pre-existing labels (`sec-`, `def-`, `thm-`, `prp-`, `cor-`, `exm-`, `eq-`, `exr-`) preserved verbatim,
  each still defined exactly once (verified by grep). No theorem or proof shortened or deleted; every addition
  is scaffolding around the existing mathematics. No new `@bibkey` citations introduced (`@caro2010stc`,
  `@phillippo2016tsd18`, etc. already exist; the `tsd18` form is already correct).

## Build safety verified

ASCII-only in math; `$\star$` used for the exercise marker (no Unicode star); no em/en dash or minus-sign
connector (only YAML `---` and Markdown `|---|` separators); no bare `align`/`equation`/`gather` inside `$$`;
no `\not` on an extensible arrow; fenced block balanced; every `{#sec-}` heading has a preceding blank line; all
5 new/existing Markdown tables have blank lines before and after.
