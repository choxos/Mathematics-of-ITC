# Revision log: Chapter 17 - Population Adjustment Theory

File: `chapters/part4/17-population-adjustment-theory.qmd`
Before: 1118 lines. After: 1474 lines (+356).
Reviewers addressed: both `feedback/chatgpt/ch17-...md` and `feedback/glm/ch17-...md`.

## Running example introduced (single highest-value addition)

An anticoagulant anchored-ITC thread: `C` = warfarin (shared comparator), `A` = new oral anticoagulant
(IPD trial vs warfarin), `B` = established DOAC (AgD trial vs warfarin), outcome = major bleed
(worse is larger), effect modifier `X` = age 75 or over. The `AC` trial is younger
(Pr(X=1)=0.25), the `BC` trial older (0.75), target 0.50. Introduced in the intro as a `.remark`
(clinical skin, no numbers), given numbers in `@sec-pat-setup` (the same risk table the capstone
`@exm-pat-anchored` reuses: mu_A = 0.20/0.50, mu_B = 0.30/0.30, mu_C = 0.40/0.40), then re-instantiated
at conditional constancy, absolute constancy, EM-vs-PV, the anchored theorem, the unanchored section,
SEMA, the worked example, and the two new warm-up exercises.

## ChatGPT highest-priority fixes

1. Target population/estimand story earlier with a concrete example: DONE. Clinical vignette in intro;
   numeric running example + per-chapter symbol table + forward pointer to estimand sections in
   `@sec-pat-setup`; plain marginal-vs-conditional numeric example before `@eq-pat-marg`/`@eq-pat-cond`.
2. Plain-language guide to the anchored theorem (conditional vs marginal recovery): DONE. Added a
   "plan in words" paragraph + implication roadmap table + "Reader translation of the theorem" remark
   before `@thm-anchored-paic-consistency`; reframed part (c) bold label; added "Why this matters" after.
3. Scale table (g, h, collapsibility, non-collapsibility, misalignment): DONE. Scale cheat-sheet table in
   `@sec-pat-estimand-scales` (RD/RR/OR/HR/RMST rows) plus a directly-collapsible vs collapsible gloss.
4. SEMA clinical intuition + why untestable: DONE. "Reader translation" remark after `@def-sema`
   (plausible = same-class drugs modified alike by severity; implausible = biomarker-targeted A vs
   broad B); foregrounded counting/hyperplane intuition in `@sec-pat-testable`.
5. Bridge text on AgD limits, overlap, unanchored needing PVs: DONE. Importance-sampling/overlap remark
   after `@prp-pat-conditional-transport`; overlap practical meaning in the unanchored reader-translation
   remark; clinical "when unanchored arises" paragraph; density-ratio-vs-entropy-balancing reconciliation
   in the methods preview.

## GLM suggestions

1. Plain-English Bucher recap before dense intro: DONE (opening paragraph, no cross-references).
2. Interleave stripped-down worked example: DONE (running-example remarks threaded throughout).
3. Network diagram for the two architectures: DONE (ASCII schematic in a fenced code block in
   `@sec-pat-architectures`; build-safe verbatim, no dash-punctuation concern in code).
4. Reframe part (c): DONE. Bold label now "The recovered estimand is the conditional effect, not a
   non-collapsible marginal one." (mathematical statement and all labels/eqs preserved).
5. One-sentence glosses for class-wise necessity / directly-vs-collapsible / overlap-positivity /
   prognostic-vs-EM: DONE (intro gloss for class-wise; cheat-sheet gloss for collapsibility grades;
   "equivalently the positivity condition" at first overlap use; one-line EM/PV definitions + 2x2 table).
6. Clinical skin (A/B/C/X as real drugs): DONE (anticoagulant thread; labels added atop `@exm-pat-anchored`).
7. Expand methods preview: DONE (entropy-balancing reconciliation + one-sentence-each operational summary).
8. Foreground testability takeaway: DONE (foregrounded in `@sec-pat-testable` opening and in the intro).
9. Overlap practical meaning where invoked: DONE (importance-sampling remark; unanchored remark).
10. Reconcile f*/f density ratio vs entropy-balancing weight: DONE (methods preview MAIC bullet).

Also: named SPFA (shared prognostic factor assumption) in the unanchored section, resolving the GLM
note that notation.qmd defines SPFA but the chapter never used it; noted the m_t vs bar-mu alias is
dropped; added an injectivity gloss of "identified" in the SEMA identifiability proof; added ESS
mechanics and collapsibility-gap intuition inside the worked example.

## New labeled environments (added; none removed or renamed)

- `#exr-pat-warmup-empv` (warm-up, interpretation)
- `#exr-pat-warmup-architecture` (warm-up, interpretation)

Plus 6 new tables (not labeled): per-chapter symbol table, running-example risk table, "what changes by
architecture" table, scale cheat sheet, effect-modifier-vs-prognostic 2x2 table, anchored-theorem
implication roadmap. Plus one ASCII architecture diagram. Plus ~11 new unlabeled `.remark` blocks
(reader translations / why-this-matters).

## Preservation confirmation

- All 67 original labeled environments preserved (label count 69 = 67 + 2 new; explicit baseline
  missing-list empty). No `#thm/#lem/#def/#eq/#prp/#cor/#sec/#exm/#exr` id was removed or renamed.
- All 12 `::: {.proof}` blocks preserved; no proof shortened. Only additions and non-label prose rewording
  (the part (c) bold sub-label) were made.
- Labels I was tempted by but preserved: the part (c) bold label "Non-recovery of a non-collapsible
  marginal effect" (reworded prose only, `#thm-anchored-paic-consistency` id and all its equation ids
  untouched); tempted to move `@thm-target-population-estimand` earlier (GLM/ChatGPT) but kept its
  position and added a "clean summary" framing sentence instead.

## Build safety

Pure ASCII in math; no bare align/equation/gather; no `\not` on extensible arrows; `$\star$` marker in
exercises; div fences balanced (59/59); fenced code block balanced; citation `@phillippo2016tsd18`
already correct (no bare key); no new `@bibkey` introduced. Not rendered (orchestrator renders).
