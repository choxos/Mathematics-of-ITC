# Revision log: Chapter 18 (MAIC)

File: `chapters/part4/18-maic.qmd`. Before: 1401 lines. After: 1927 lines (+526).
Revision goal: address both reviewer files (`feedback/chatgpt/ch18-maic.md`, `feedback/glm/ch18-maic.md`)
per STYLE.md Section 10 (pedagogical accessibility) and Section 11 (PDF build safety).

## Running example introduced (single highest-value addition)

A one-covariate, four-patient anchored MAIC (new section `#sec-maic-first-look`, example `#exm-maic-running`):
index trial `AC` (immunotherapy A vs chemotherapy C), covariate = standardized disease severity
(x = +1 severe, x = -1 mild), two severe + two mild, comparator mean severity 0.5. Every number is exact
and hand-checkable: balancing weights (severe 1.5, mild 0.5), exponential form w(x) = e^{-0.144+0.549 x},
ESS = 3.2, variance inflation 1.25, and the identity-scale benefit corrected from 4 (index) to 5
(comparator). It is deliberately the one-covariate shadow of the terminal two-covariate example
`#exm-maic-twocov` (same tanh beta = 0.5, e^{2beta} = 3), and it is reused at each transition (entropy
objective, exponential-weights dual, ESS collapse table, worked example).

## Reviewer points addressed

ChatGPT highest-priority fixes:
1. Pre-proof intuition for weights: added "What a weight means, in patient terms" (setup), the running
   example, "Entropy keeps any one patient from taking over" remark, and the pre-theorem roadmap for
   `#thm-maic-exponential-weights`.
2. Anchored vs unanchored made concrete: anchored/unanchored contrast table, unanchored failure scenario
   (oncology A vs B, age prognostic and unbalanced), operational SEMA restatement, EM-vs-PV table in setup.
3. ESS/variance as reporting diagnostics: ESS reader translation + ESS-collapse table, overlap-diagnostics
   remark, practitioner checklist section `#sec-maic-checklist`.
4. Nonlinear link / non-collapsibility bridge: worked logit example `#exm-maic-logit-moments` (same mean,
   different spread => different marginal risk 0.731 vs 0.690 and marginal log-OR 0.500 vs 0.407), plus an
   expanded "What non-collapsibility demands, concretely" remark in the anchored proof.
5. Exercises: added star-convention line, three accessible warm-up/interpretation exercises first
   (`#exr-maic-interpret-weights`, `#exr-maic-em-vs-pv`, `#exr-maic-diagnose-report`, the last is the
   "judge a published MAIC" applied check both reviewers asked for), tagged all exercises by type.

GLM (beginner) points addressed:
- Named concrete trial (A immunotherapy, B competitor, C chemotherapy) + trial-naming gloss + effect-modifier
  plain gloss in first paragraph.
- Jargon glossed in line: "conditioning vacuous", "feature map" (+ numeric illustration), "coercive",
  "relative interior/affine hull" (triangle/segment picture), "self-normalized", density-vs-probability,
  "Hadamard/Frechet-differentiable", "Schur-convex"/"majorizes", softmax-derivative parenthetical, and the
  no-alpha-in-balance-block explanation.
- KL algebra spelled out step by step (p_i = w_i/n substitution, +/- log n cancellation) in an aligned block.
- Lagrangian-to-dual bridge added before `#thm-maic-exponential-weights`.
- Convex-hull geometry: three-case table (inside/boundary/outside -> feasible-positive / feasible-with-zeros
  / infeasible) substituting for the requested figure (a drawn figure is not feasible in this pipeline;
  provided a verbal sketch + table instead).
- "Why this matters" leads added before/at each major theorem (exponential weights, existence, anchored,
  unanchored, no-extrapolation, sandwich, bootstrap); no-extrapolation now opens with the age-80 punchline.
- Finite-sample-bias mechanism explained ("same patients used twice").
- Reading-path remark added to the introduction to address pacing/reordering without physically moving
  sections (which would risk cross-reference breakage).

## Deliberately skipped / substituted

- Physical reordering (ESS before existence; moving the worked example up). Substituted a reading-path
  signpost in the intro plus a skip-signpost before the existence Part-2 proof, because reordering large
  labeled blocks risks harmony/cross-reference breakage and the hard constraints forbid disturbing labels.
- Actual figure for the convex hull: replaced by a three-case table + verbal description (no figure
  toolchain available; ASCII/tikz would be build-fragile).
- New starred exercises left unstarred (no Appendix F solutions authored here); existing starred exercises
  kept their stars.

## New labeled environments / tables added (nothing removed or renamed)

New sections: `#sec-maic-first-look`, `#sec-maic-checklist`.
New examples: `#exm-maic-running`, `#exm-maic-logit-moments`.
New exercises: `#exr-maic-interpret-weights`, `#exr-maic-em-vs-pv`, `#exr-maic-diagnose-report`.
New tables (6): effect-modifier vs prognostic-variable; convex-hull three-case overlap; MAIC vs standard
IPW; anchored-consistency assumption checklist; anchored vs unanchored contrast; ESS-collapse table.

## Labels preserved (verified programmatically)

All 17 original `#sec-`, 3 `#def-`, 1 `#lem-`, 10 `#thm-`, 26 `#eq-`, 1 original `#exm-`, and 6 original
`#exr-` labels are intact (0 missing, 0 duplicates). Every existing theorem and its full proof is
unchanged; all additions are scaffolding (leads, remarks, glosses, tables, examples, exercises).

## Build-safety checks (all pass)

- ASCII-only in math mode; no unicode dashes anywhere; star marker is `$\star$` (no unicode star).
- `$$` delimiters balanced (126); `:::` divs balanced (61/61).
- Two new `aligned` blocks, both correctly nested inside `$$ ... $$`; no bare `align`/`equation`/`gather`.
- No `\not` on an extensible arrow.
- Both new `#sec-` ids unique across the book (grep-checked); every new heading has a blank line before it.
- Citations: chapter already uses `@phillippo2016tsd18` (no bare `@phillippo2016tsd`); no new bibkeys
  introduced (only existing keys and internal `@thm-/@def-/@exm-/@sec-` cross-references reused).
