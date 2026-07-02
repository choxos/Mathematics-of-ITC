# Revision log: Chapter 15, Network Meta-Analysis: Models and Identifiability

File revised: `chapters/part3/15-network-meta-analysis.qmd` (1221 -> 1605 lines).
Reviewers addressed: `feedback/chatgpt/ch15-network-meta-analysis.md` and
`feedback/glm/ch15-network-meta-analysis.md`. Both files were read in full; each reviewer's
highest-priority list was worked through item by item. No mathematics was deleted or shortened; every
existing theorem, lemma, proposition, proof, definition, equation, example, and exercise label is intact.
All additions are scaffolding: a running example, tables, plain-language remarks, signposts, and two
warm-up exercises.

## Highest-priority fixes addressed

ChatGPT reviewer (numbered as in their "Highest-priority fixes"):

1. Concrete network diagram and trial table before the first formal model. Added new section
   `## A running example and a reader's toolkit {#sec-nma-running}` immediately after the Introduction,
   containing `exm-nma-running`: a placebo / Drug A / Drug B network, a four-trial table, an ASCII
   treatment-comparison graph, and a spelled-out reading of direct vs indirect evidence, connectedness,
   and the loop. The model `theta = X beta` now arrives after the reader has seen the picture.
2. Multi-arm trials clarified. New remark after `def-nma-arm-model` ("Multi-arm trials: clinical pairs
   versus contrast rows") separates the clinical direct pairwise evidence of a three-arm trial from the
   `A_j - 1` independent contrast rows created by choosing a study baseline, and shows the omitted
   pairwise contrast is recovered by subtraction and correlated with the kept rows.
3. Notation and sign-orientation guide. `sec-nma-running` now carries a graph-vocabulary table (graph
   term vs trial meaning), a symbol-orientation table (theta_jk, mu_j, delta, d_k, d_ab, t_{j,1},
   tilde-d with plain meanings and running-example instances), and a "Reading the sign of a contrast"
   remark giving the `d_ab = d_b - d_a` convention with odds-ratio interpretations in both directions.
4. Intuition for consistency, connectedness, identifiability, testability strengthened. Added: a numeric
   triangle before `thm-consistency-closure`; a "Why this matters, and how loops carry the constraints"
   headline folded into the loops remark; a "reader in a hurry may skip" forward-pointer at the head of
   `sec-nma-rank`; a "What this buys us" remark after `lem-incidence-rank`; a blunt
   "identifiability is connectivity" sentence before `thm-fe-nma-identifiability`; a "Plain-language
   takeaway" remark and a concrete disconnected-network drug example (with ASCII figure) after it; and a
   SUTVA-consistency signpost distinguishing NMA consistency from the Chapter 9 usage.
5. Arm-based to contrast-based transition made procedural. Expanded the "Arm-based and contrast-based
   likelihoods" remark with a two-equation display (subtracting the baseline arm removes mu_j) and an
   explicit five-step recipe ending in "carry their covariance".
6. Worked example (`exm-nma-triangle`) made guided. Added a row-label table to Step 1 (row, study,
   contrast, design row, data); a fit table in Step 6 (observed, fitted, residual, variance, deviance
   contribution); a degrees-of-freedom reconciliation showing the contrast count (5 - 2 = 3) matches the
   arm count (9 - 6 = 3); a note explaining why the study-4 rows fit exactly (a coincidence of the
   numbers, not structural); and a "Clinical reading" paragraph interpreting d_2, d_3, d_23 as odds
   ratios with a confidence interval that includes 1.
7. Advanced end material rebalanced. Added bridge framing to `sec-nma-ipd` ("a reader meeting NMA for
   the first time can note the result and return to it later", plus a one-covariate LDL-cholesterol
   reading) and to `sec-nma-deviance` ("a practical checklist rather than new network theory ... a reader
   focused on identifiability can skim it").

GLM reviewer (numbered as in their "Suggestions"):

1. Figures of networks: two ASCII diagrams added (the running network in `exm-nma-running`; a
   disconnected two-cluster network in the identifiability section).
2. Running example moved forward: `exm-nma-running` is introduced right after the Introduction and
   referenced at each transition (arm-model remark, design-assembly paragraph, closure numeric triangle,
   correlation remark, node-split remark); `exm-nma-triangle` now opens with "We now complete the running
   example of `@exm-nma-running`".
3. Drugs named: placebo / Drug A / Drug B used throughout the new material, the Bucher remark, the
   closure numeric triangle, the disconnected example, the worked example, and the IPD example.
4. One-paragraph "why this chapter" motivation added to `sec-nma-intro` (borrows strength, respects
   structure, makes coherence testable).
5. `sec-nma-rank` reordered in spirit via a forward-pointer paragraph stating what each lemma is for and
   telling a hurried reader they may skip to `sec-nma-equivalence`.
6. Jargon glossed on first use: "saturated" (as many free parameters as arms), "profiling out"
   (eliminating baselines from the likelihood), `J_m` (restated as the m-by-m all-ones matrix in
   `thm-re-nma-correlation`), and the tilde-d padding convention (glossed in-proof and in the toolkit
   table).
7. Intuition before heavy theorems: the "surplus is where inconsistency lives" idea now appears in a
   motivating paragraph and a baseline-shift/reference-treatment correspondence table BEFORE
   `thm-parameterization-equivalence` (the fuller "Why the surplus is harmless" remark is retained
   after); the loop-testability and disconnection headlines are stated before their theorems.
8. The tau^2/2 arm-level variance is explained at the point of introduction (before
   `thm-re-nma-correlation`): the half is chosen so each contrast has variance tau^2.
9. Residual-deviance and DIC rules of thumb given with a source: both now cite `@dias2018nma` and state
   the yardstick (D_res near N - p because a chi-square has mean equal to its degrees of freedom; DIC
   differences below ~3 / above ~5 flagged as a convention, not a theorem).
10. Notation collisions resolved (see below), and `J_m` restated inline.

Also incorporated from the reviewers' detailed lists: the g / g-inverse "circularity" dispelled with a
numeric logit example (0.5 -> 0.62); the theta vector unpacked entry-by-entry; the incidence matrix
described in words as "a labeling of vertices mapped to edge-wise differences"; a "reader's translation"
after `lem-nma-gram`, `lem-half-correlation-forced`, `def-node-splitting`, and both parameterization
definitions; the "node-splitting splits evidence, not a node" clarification with a forward pointer to
Step 5; the numeric one-half punchline in the sampling-covariance remark; and the reminder that random
effects model heterogeneity but do not repair inconsistency.

## Notation collisions resolved (chapter-local; noted for the orchestrator)

- The number of connected components was written `c`, colliding with `C` (within-study contrast count of
  `@eq-nma-totalcontrasts`) and with the enumeration labels (a)-(e). Renamed the component count to `q`
  throughout `lem-incidence-rank`, `thm-fe-nma-identifiability`, and the notes. Enumeration markers
  "(c)", the triple index in `a = b = c`, and the constant `c` in `prp-dic-pd` were deliberately left
  unchanged. Verified by grep that no stray count-`c` remains and the identity of every "(c)" marker is
  preserved.
- The consistent-contrast-family space was the bare script `C` inside the proof of
  `thm-consistency-closure`, colliding with the column-space operator `C(.)` and with `S_cons`. Renamed
  to `D_cons` (proof-internal only), and added a one-line caution in the equivalence section
  distinguishing `D_cons` (contrast families) from `S_cons` (arm-mean vectors).

These two symbols (`q`, `D_cons`) are new chapter-local notation. They are consistent with the existing
scheme and are introduced with inline glosses; no change to `notation.qmd` is strictly required, but the
orchestrator may wish to record `q` = number of connected components of the treatment graph.

## New labeled environments added (no existing label removed or renamed)

- `#sec-nma-running` : the early running-example section.
- `#exm-nma-running` : the running clinical network (placebo, Drug A, Drug B; four trials).
- `#exr-nma-draw` : warm-up exercise (draw the network, identify direct/indirect/loop/consistency).
- `#exr-nma-sign` : warm-up interpretation exercise (contrasts as odds ratios, sign direction).

A one-line note was added at the top of `sec-nma-exercises` stating that starred (`$\star$`) exercises
have full solutions in Appendix F, and pointing to the two warm-ups first.

## Deliberately left unchanged (with reasons)

- Section and theorem ordering. The GLM reviewer wondered whether `thm-consistency-closure` should sit
  after both parameterizations. I did not reorder, to avoid disturbing cross-chapter references and the
  numbered flow; instead I added connective tissue (the numeric triangle framing and the loops "why this
  matters" line) so the closure theorem no longer reads as a standalone algebra lemma.
- All proofs are intact and unshortened; the only proof edits are added clarifying clauses (part 4 of
  `thm-consistency-closure`, the "labeling to edge differences" sentence in `lem-incidence-rank`, and the
  tilde-d gloss in `thm-parameterization-equivalence`) plus the `c -> q` and script-`C -> D_cons`
  renames.
- The intro roadmap that previews later theorem labels was kept (it is a roadmap by design); the
  motivation paragraph was added ahead of it.

## Sources

No new bibliography keys introduced. The only citations added are to `@dias2018nma` (already in
`references.bib`), used to source the residual-deviance and DIC rules of thumb. All other citations
(`@bucher1997`, `@dersimonian1986`, `@phillippo2019thesis`, `@phillippo2020mlnmr`, `@phillippo2016tsd18`)
were already present in the chapter.

## Build-safety checks performed

- File is ASCII-only in and out of math (verified programmatically).
- No bare `align` / `gather` / `equation` environments inside `$$`; displays use `pmatrix`, `cases`, and
  aligned inline forms only.
- No Unicode star; the `$\star$` macro is used for the exercise convention.
- No `\not` applied to an extensible arrow.
- Two ASCII network diagrams are in fenced code blocks (not math), each with blank lines before and
  after; code fences balanced (4 fence lines = 2 blocks).
- Every `::: {...}` div is closed (59 openers, 59 closers).
- Every real section heading has a blank line before it; the flagged "no blank line" cases are all
  `## Title` lines inside `::: {#...}` divs, which is the required Quarto theorem grammar.
- Notation chapter linked as `[Notation](/notation.qmd)` (unchanged from the original).
- All 71 labels accounted for: every original label preserved, four new labels added, all unique.
