# Revision log: Chapter 23 (ML-NMR IV: Estimands, Identifiability, Generality)

File: `chapters/part5/23-mlnmr-estimands.qmd`. Catalogue H.20 to H.23.
Before: 1020 lines. After: 1201 lines. All 34 pre-existing labels preserved; all 7 proof
divs preserved (none shortened; several proofs expanded with clarifying sentences). No
`#thm/#lem/#def/#eq/#prp/#cor/#sec` renamed or removed.

## Running example introduced
The **anticoagulant decision**: $A$ = a new oral anticoagulant, $B$ = warfarin, $C$ = the
shared comparator; outcome = a major bleed (unfavorable); effect modifier $X$ = age
($X=1$ older); IPD trial on $\{A,C\}$ (younger), AgD trial on $\{B,C\}$ (older); NICE UK NHS
target older than both trials. Its coefficients are the same numbers ($\beta_1=0.4$,
$\beta_2=0.5$, $\gamma_A=0.8$, $\gamma_B=0.3$) that the pre-existing worked example
`@exm-mlnmr-new-target` computes, so the frame is introduced early (new
`@exm-mlnmr-anticoagulant`) and pays off in the existing worked example. It reappears at the
model recall, the estimand stakes box, the contrast-key table, the two-study ledger/SEMA
block, the no-SEMA numeric example, the roadmap, and the worked example's word translation.

## New labeled environments added (all globally unique, verified)
- `#sec-mlnmr-est-running` (new section: running clinical decision problem)
- `#exm-mlnmr-anticoagulant` (running example)
- `#exm-mlnmr-sema-fail` (numeric no-SEMA failure, two observationally identical pairs)
- `#exr-mlnmr-which-population`, `#exr-mlnmr-inputs-checklist` (two warm-up exercises)
- Tables: `#tbl-mlnmr-params`, `#tbl-mlnmr-contrast-key`, `#tbl-mlnmr-scales`,
  `#tbl-mlnmr-inputs`, `#tbl-mlnmr-triangle`, `#tbl-mlnmr-ledger`, `#tbl-mlnmr-ladder`,
  `#tbl-mlnmr-roadmap`, `#tbl-mlnmr-semafail` (9 tables)
- Numerous unlabeled `::: {.remark}` intuition/why-this-matters boxes.

## ChatGPT reviewer: highest-priority fixes (all addressed)
1. **What ML-NMR estimates, plainly** -> new "stakes, before the definitions" remark at the
   top of `@sec-mlnmr-est-estimand` (target arm means, then contrast; identity=risk diff,
   logit-after-averaging=marginal log OR) plus the running-example "in one breath" remark.
2. **Practical role of target baseline $\mu_{*}$** -> "Where does the target baseline come
   from?" remark (registry/epidemiology/comparator arm; scenario input; uncertainty is real)
   plus `@tbl-mlnmr-inputs`.
3. **SEMA before the identifiability proof** -> new pre-theorem block: `@tbl-mlnmr-triangle`
   (anchored triangle), `@tbl-mlnmr-ledger` (unknowns vs data), clinical + parameter-count
   restatement of SEMA, and a three-plain-step proof preview.
4. **`Delta_{ab}` misread warning** -> `@tbl-mlnmr-contrast-key` and an explicit "do not read
   left to right" remark.
5. **Bridge into generality theorem** -> `@tbl-mlnmr-roadmap` (implication roadmap: which
   term drops, which integral collapses) placed before the theorem, plus a one-line MAIC/STC
   practical upshot.

Also addressed from ChatGPT "under-explained/unclear": order-of-operations motivation before
part (c); transport g-formula two-sentence recap before `@thm-target-population-integral`;
prognostic-variables-matter-for-marginal-OR remark; outcome-scale table (`@tbl-mlnmr-scales`)
so the chapter is not logit-only; expit defined; sign/word translation of one contrast;
non-technical identifiability ledger; exchangeable-EM interpretation; difficulty labels on
exercises.

## GLM reviewer: highest-priority / suggestions (addressed)
1. Clinical scenario opener -> running example (see above).
2. "Superpower and its price" moved up front -> stakes box (original remark also retained).
4. Part (c) convexity subtlety -> expanded proof: strict Jensen per arm; expit convex-then-
   concave, strictly nonlinear on every nondegenerate interval; the two per-arm displacements
   differ because arms sit at different baselines/slopes.
5. Numeric example for `@prp-mlnmr-sema-necessary` -> `@exm-mlnmr-sema-fail` with the running
   coefficients: pairs $(0.3,0.5)$ and $(0.5717,0)$ reproduce the identical AgD proportion
   $0.6909$ but give conditional $A$-vs-$B$ contrasts $0.500$ vs $0.528$ at $\bar x=0.6$ and
   $0.500$ vs $0.328$ at $\bar x=0.2$ (arithmetic checked).
6. Collapsibility tied to the regulatory estimand debate -> "math behind a regulatory debate"
   remark (ICH E9(R1); estimand-based HTA via `@chandler2026transport`).
7. `s_{jk}` defined inline as combined intercept; `$\dot g_0,\dot g_1$` evaluation points
   spelled out (at the $X=0$ and $X=1$ $B$-arm linear predictors); `s_0,s_1` glossed.
8. Correct-specification-on-target-support remark expanded with a concrete extrapolation
   scenario (frailer/older target than the IPD trial) and a sensitivity-analysis recipe.
9. Intro slowed with a concrete frame and a "probability limit" gloss (definition inline).
   NOTE: I did not delete the original three-question cross-referenced paragraphs (hard
   constraint: preserve content); I added the concrete layer ahead of/around them instead.
Other GLM points: affine-vs-linear clarified inline; "$p$-dimensional manifold", "implicit
function theorem", "generic target" glossed in plain words before the proposition; monotonicity
lemma given a "dimmer switch" reader-translation and its finiteness argument spelled out for
the bounded (logit) and unbounded (log) ranges; exchangeable-EM proof expanded (bounded
likelihood on a noncompact space; prior-identified vs likelihood-identified); `@tbl-mlnmr-ladder`
defines what "Bayesian only" identification means.

## Deliberately skipped, with reason
- **Literal figures (GLM suggestion 3).** The book renders to BOTH PDF (pdflatex) and HTML;
  raw TikZ does not render in HTML and mermaid/PDF needs tooling the pdflatex-only pipeline
  may lack, so an image would risk the build (Section 11). Substituted a Markdown schematic
  (`@tbl-mlnmr-triangle`) and prose descriptions of the surface. A proper figure is left as a
  deferred enhancement for the orchestrator.
- **Editing `notation.qmd` (GLM suggestion 10).** File discipline forbids editing another
  file. Defined `\operatorname{expit}` (inline at first use, line ~314, and in the worked
  example), "probability limit", and $\mu_t^{\mathcal P}(x)$ inline instead. PROPOSED for the
  orchestrator to fold into `notation.qmd`: add `$\operatorname{expit}(z)=1/(1+e^{-z})$`
  (inverse-logit), $\mu_t^{\mathcal P}(x)$ (population-$\mathcal P$ conditional mean), and a
  one-line "probability limit" entry.

## Proofs expanded (not cut)
part (b) of `@thm-target-population-integral` (prognostic-shift parenthetical); part (c)
(Jensen-per-arm); `@lem-mlnmr-aggregate-monotone` finiteness (two range regimes);
`@prp-mlnmr-sema-necessary` (derivative evaluation points, $s_0,s_1$ gloss);
`@thm-mlnmr-identifiability-large` part 3 (bounded likelihood; prior- vs likelihood-identified).

## Build-safety checks run (all pass)
34/34 original labels present; 14/14 new labels defined exactly once and globally unique;
`::: {` openers = `:::` closers (46/46); every `##` heading has a preceding blank line (or
follows a div opener, the established theorem-title pattern); no unicode dash, no double-hyphen
connector, no spaced-hyphen connector in prose (only YAML `---` and Markdown `|---|`); `$$`
fences even (58); one `aligned` and one `array`, both balanced, no bare align/equation/gather;
no `\not` on an extensible arrow; star marker is `$\star$` (no unicode); `@phillippo2016tsd18`
intact (1), no bare `@phillippo2016tsd`; no new `@bibkey` introduced (regulatory framing uses
existing `@chandler2026transport` and prose mention of ICH E9(R1)).

## Labels I was tempted to touch but preserved
Kept the `$\Delta_{ab}$ = b versus a` convention exactly (added a warning table rather than
renaming). Kept `@def-mlnmr-target-contrast`, `@thm-target-population-integral`'s four-part
structure, and every `#eq-` label as-is. Kept the original "superpower and its price",
"No overlap is required", "ladder of assumptions", and "Where each hypothesis is spent" remarks
in place (added shorter up-front versions rather than moving/deleting them).
