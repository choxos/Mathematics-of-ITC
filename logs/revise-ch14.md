# Revision log: Chapter 14, Indirect Comparison and Bucher's Theorem

Reviser: Opus 4.8 agent. Scope: pedagogical accessibility pass for a novice health researcher,
addressing `feedback/chatgpt/ch14-bucher.md` and `feedback/glm/ch14-bucher.md`. Rigor, every theorem,
every proof, and every existing label preserved; scaffolding, examples, tables, and signposts added.

## Hard constraints honored

- No existing label removed or renamed. Verified all 52 original labels (`#sec-`, `#def-`, `#eq-`,
  `#lem-`, `#prp-`, `#thm-`, `#cor-`, `#exm-`, `#exr-`) still present by script.
- Every theorem/lemma/proposition/corollary and its full proof preserved verbatim (Bucher identity,
  unbiasedness, variance, baseline cancellation, unanchored bias, log-odds variance, transitivity
  consistency, variance-of-a-difference). Only surrounding scaffolding was added.
- All 5 machine-checked tags preserved exactly (`Definition transitivity`, `Lemma transitivity_subtract`
  + `Lemma subtract_transitivity`, `Theorem bucher_identity`, `Theorem bucher_unbiased`,
  `Theorem bucher_variance`); confirmed `theories/Bucher.v` exists.
- Starred exercises `@exr-bucher-correlated` and `@exr-bucher-transitivity-bias` (both solved in
  Appendix F, verified in `appendices/F-solutions.qmd`) kept with their `$\star$` marks and labels.
- PDF build safety: file is fully ASCII; no Unicode in math; `$\star$` used (no Unicode star); no bare
  `align`/`equation`/`gather` inside `$$` (the one new multiline display uses `aligned`); no `\not` on
  extensible arrows; all `%` escaped as `\%`; blank line before every real heading; env titles follow the
  `::: {#id}` / `## Title` grammar; `[Notation](/notation.qmd)` link used (no `@sec-notation`); every
  `#sec-` id unique. Verified 69 balanced div open/close pairs.
- No dash punctuation as connector/parenthetical in prose; American English; YAML title unchanged.
- Only cited existing bibtex keys (`bucher1997`, `dias2018nma`, `phillippo2019thesis`). No new sources.
- Did not edit `_quarto.yml`, `notation.qmd`, `references.bib`, or any other chapter.

## New labeled environments added (all cross-references verified to resolve)

- `#sec-bucher-running` — new early section "A running example and a map of the argument."
- `#def-additive-arm-decomposition` — promotes the additive arm decomposition from a remark to a
  definition (keeps `#eq-bucher-decomp` inside it, so every reference to that equation still resolves).
- `#exm-anchored-vs-unanchored` — numeric anchored-vs-unanchored side-by-side on the running data.
- `#exm-transitivity-failure` — numeric transitivity-failure illustration with a specific bias.
- `#exr-bucher-warmup`, `#exr-bucher-interpret` — two accessible warm-up/interpretation exercises.

## ChatGPT highest-priority fixes (all addressed)

1. Sign-orientation burden. Added a four-row applied-phrase/symbol/formula/meaning orientation table in
   `#sec-bucher-running`; an orientation reminder in the `@def-anchored-comparison` reader-translation
   remark; an explicit "Orientation check" opening the worked example; and a "Final interpretation, in
   both orientations" remark ("odds for B are 1.33x those for A; equivalently A is 0.75x B"). Expanded the
   index-order remark near `@sec-bucher-algebra` with the practical "positive means second-slot is worse"
   rule.
2. Transitivity intuition before the formal definition. Added a plain-language lead-in, a "what must be
   similar / may differ / cannot be fixed by more data" table, and a clinical instance remark (age
   modifying the statin-B effect; younger BC trial) all BEFORE `@def-transitivity`; added reader
   translations after `@def-constancy-relative-effects` and `@def-transitivity`, including how a reviewer
   checks transitivity in practice and the "population-level no-confounding" analogy expanded.
3. Numerical baseline-risk example for anchoring. Added `@exm-anchored-vs-unanchored` using the running
   data: naive comparison wrongly finds OR = 1 (statin arms have equal event rates), anchored finds OR =
   4/3, and the whole 0.288 gap is the placebo-baseline difference. Verified numerically.
4. Approximate/large-sample unbiasedness. Added a "Consistent, and unbiased to first order" remark after
   `@prp-trial-unbiased` stating the empirical log-OR is not exactly unbiased in finite samples, that
   every "unbiased" in the chapter is the large-sample sense, and warning that "consistent" has two
   unrelated meanings here (estimator convergence vs NMA agreement).
5. Reader-facing worked example. Added an orientation check, a five-step "Bucher from published trials"
   recipe box (recover SE from CI, align orientation, subtract, add variances, back-transform), and a
   final both-orientations clinical interpretation naming the transitivity dependence.

## GLM suggestions (all addressed, with one adaptation)

1. Named clinical example opening: new statin A vs established statin B, each vs placebo C, cardiovascular
   event outcome; introduced in the first paragraph and reused throughout (running example, worked
   example, anchored-vs-unanchored, transitivity-failure).
2. Triangle figure: ASCII triangle (nodes A, B, C; solid AC, BC legs; dashed AB) in `#sec-bucher-running`,
   referenced from the algebra section.
3. Estimator introduced early: "The object, stated once, up front" callout states
   `d_AB = d_AC - d_BC` with the running numbers immediately after the introduction.
4. Additive decomposition promoted to `@def-additive-arm-decomposition`, with an ASCII picture of shared
   `alpha_k` and study-specific `mu_j`, and a plain gloss of each.
5. `@def-transitivity` expanded with in-body clinical examples of holding and failing (not deferred).
6. Sign-convention table added (`#sec-bucher-running`), reused by reference near the algebra.
7. Numeric anchored-vs-unanchored side-by-side added (`@exm-anchored-vs-unanchored`) on the same tables.
8. Log-odds variance proof (`@prp-logodds-variance`): ADAPTED. The hard constraint forbids deleting a
   proof, so the proof is kept intact; a "You may skip the proof on a first reading" signpost now states
   the boxed formula first and marks the delta-method derivation as optional/faith-based, meeting the
   reviewer's momentum concern without cutting mathematics.
9. `@prp-trial-unbiased` softened: added a "What the proof said, in plain words" remark (ignorability,
   positivity, vacuous conditioning explained) and the consistency-vs-unbiasedness remark.
10. Inline one-sentence glosses added at first use for: "square-integrable" (= finite variance),
    "homoskedastic random-effects model" (= all contrasts same variance) with the shared-arm intuition
    for the one-half correlation, "ecological bias" (group-level relationship not holding at the
    individual level), and "node-splitting" (splits a comparison into direct and indirect parts and
    checks agreement).
11. Notation reconciliation done in-chapter: the marginal `eta_{k(P)}` is explicitly distinguished from
    the individual-level `eta_{ijk}` of notation.qmd (coarser object, same letter), and `mu_j` is
    explicitly identified with the study-j baseline (intercept) of notation.qmd, with the reference
    treatment normalized (`alpha_C = 0`, so `mu_j` is the placebo arm's link-scale outcome), answering
    "is mu_AC the same kind of quantity as mu_BC?" (yes: placebo log-odds in two populations).
12. `@sec-bucher-failure` expanded with `@exm-transitivity-failure`: a diabetes effect modifier with a
    prevalence table yields a specific bias of -0.24 on the log-OR scale (~21% multiplicative), verified
    numerically, plus a full paragraph bridging to transportability (Chapter 12) rather than a one-line
    cross-reference.

## Additional STYLE Section 10 requirements

- Reader translations added after every definition (`@def-marginal-link-position`,
  `@def-constancy-relative-effects`, `@def-transitivity`, `@def-anchored-comparison`,
  `@def-unanchored-comparison`, `@def-additive-arm-decomposition`).
- "Why this matters" lines added after `@lem-relative-effect-algebra`, `@thm-bucher-unbiased`,
  `@thm-bucher-variance`, `@prp-baseline-cancellation`.
- "Concrete first" running example placed immediately after the introduction and reused at transitions.
- Jargon defined/signposted: contrast, link scale, population (applied meaning), consistency (two senses),
  effect modifier vs prognostic variable, non-collapsibility (one-line arithmetic illustration added),
  the four terms in item 10 above.
- Tables added: sign-orientation table, argument roadmap, transitivity "what must be similar" table,
  transitivity forward/converse implication roadmap, anchored-vs-unanchored comparison table,
  transitivity-failure prevalence table.
- Motivation added: why prove the trivial algebra lemma (one paragraph before it); why the unanchored
  comparison gets a definition (stated as a foil at the point of definition); the "first exact, then
  stochastic" framing before the two unbiasedness results.
- Pacing: the estimator now appears immediately after the intro; the triangle and orientation are early.
- Pythagorean/quadrature intuition added for why the variance adds; the "shared error partly subtracted
  away" intuition added for the covariance case.

## Exercises

- Added the one-line convention at the top of `#sec-bucher-exercises`: a `$\star$` exercise has a full
  solution in Appendix F.
- Added two accessible warm-ups: `@exr-bucher-warmup` (identify anchor, choose sign, compute Bucher, state
  transitivity in plain words; clean numbers Bucher = 0.20, SE = 0.25, OR = 1.22) and `@exr-bucher-interpret`
  (what breaks transitivity and what does not).
- Tagged all existing exercises by kind (Warm-up / Interpretation / Computation / Proof / challenge) in
  their bold titles without changing any `#exr-` id.

## Notation / new-symbol notes for the orchestrator

- The chapter-local terms "marginal link-scale position" and the symbol `eta_{k(P)}` (population-level,
  marginal) are not in `notation.qmd`. Both reviewers flagged this. I glossed them in-chapter and
  reconciled against `eta_{ijk}`; consider adding a one-line entry to `notation.qmd`:
  "`eta_{k(P)}` marginal link-scale position of treatment k in population P (population-averaged; distinct
  from the individual-level linear predictor `eta_{ijk}`)."
- The additive-decomposition symbols `mu_j` (study baseline) and `alpha_k` (treatment shift) are used
  consistently with `notation.qmd`'s `mu_j` (study-j intercept); `alpha_k` matches the reference-treatment
  parameterization used in Chapter 15. No conflict; no change requested beyond the note above.

## Left unchanged (deliberately)

- All mathematics, theorem statements, and proofs (verbatim).
- The Notes and references section content and its many forward cross-references (GLM suggested trimming;
  I left it intact to preserve label references and attribution; the length does not affect correctness).
- The word "cancelling" inside the preserved proof of `@prp-baseline-cancellation` (original author's
  text; not altered under the preserve-proofs constraint; it is an accepted variant spelling).
