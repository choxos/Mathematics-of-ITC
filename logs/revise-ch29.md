# Revision log: Chapter 29, Simulation-Study Theory

File: `chapters/part6/29-simulation.qmd`. Revision pass addressing both reviewer feedback files
(`feedback/chatgpt/ch29-simulation.md`, `feedback/glm/ch29-simulation.md`) under STYLE.md Section 10
(pedagogical accessibility) and Section 11 (PDF build safety).

Before/after line count: **1154 -> 1533** (+379 lines). All additions are scaffolding; no mathematics,
proof, theorem, or label was cut or shortened.

## Running example introduced (highest-value addition, demanded by both reviewers)

A named plaque-psoriasis anchored indirect comparison, introduced in `@sec-sim-intro` as a `.remark` and
reused at every transition and in the worked study:

> New interleukin-23 inhibitor A vs established interleukin-17 inhibitor B for moderate-to-severe plaque
> psoriasis; ustekinumab C the common anchor; index trial AC has IPD, comparator trial BC reports only arm
> means; endpoint = reduction in PASI score at week 16 (points, identity scale); effect modifier x1 =
> baseline severity, prognostic covariate x2 = age; estimand theta = d_{AB(P_BC)}.

Chosen to be numerically consistent with the pre-existing miniature (`@exm-sim-miniature`, identity scale,
d_BC=3.0, theta=1.5), so every symbolic number now carries a clinical unit (PASI points). Flagged as
illustrative, not real efficacy. The miniature and the misspecification section were explicitly re-skinned
to this scenario.

## Notation disambiguation (both reviewers, highest priority)

The overloaded `$\theta_0$` was split. The **working-model target** was renamed `$\theta_0` ->
`$\theta_{\mathrm{work}}$` throughout `@sec-sim-misspec` (paragraph, C1/C3, theorem proof, both corollaries,
final remark) and in the miniature (`$\theta_0^{\mathrm{adj}}` -> `$\theta_{\mathrm{work}}^{\mathrm{adj}}$`,
same for `naive`), and the cross-reference `$\theta_0^{\mathrm{true}}$` in `@thm-sim-power` ->
`$\theta_{\mathrm{work}}$`. The **null value** `$\theta_0$` is preserved unchanged in `@sec-sim-power`
(`@def-power-type1`, `@thm-sim-power`, `@exr-sim-power`) so the test-statistic subscript `T_{0,n}` stays
sensible. Verified by script: every remaining `\theta_0` is either the null (power section/exercise) or the
one sentence explaining the distinction. This is a **symbol** rename only; no `#`-label was touched.

## ChatGPT highest-priority fixes (all addressed)

1. Concrete ADEMP table before/after `@def-ademp`: added, instantiating all five components for the running
   psoriasis comparison, plus a "which pieces are fixed/varied/derived/output" bridge that also defines
   **scenario** inline and gives the plain "a method is a program returning (estimate, SE, interval)" gloss.
2. Plain bridge DGM -> known estimand, including how the truth is computed: added `.remark` "How the truth
   is known, and how it is computed" (identity-scale integral; marginal standardization on non-collapsible
   log-OR scale via `@def-non-collapsibility`; large auxiliary simulation for survival/probit).
3. Glossary separating statistical SE from MCSE: added a glossary table at end of `@sec-sim-intro` with an
   explicit final paragraph on `$\widehat{\mathrm{SE}}_n$` (one analysis) vs MCSE (the simulation summary).
4. Coverage-collapse theorem unpacked in words before the formal conditions: added "The phenomenon in plain
   words" `.remark` (reverses order per GLM), a "How to read the theorem below" note defining theta,
   theta_work, sigma_n, b (incl. what b=+/-infinity means), and the expanded working-target paragraph.
5. Replication planning as a workflow: added a four-step pilot->variance->tolerance->solve `.remark` plus a
   R = 500/1000/2000/5000 coverage-MCSE table.
6. Worked example: added "Anatomy of one replication" (generative draws) + explicit "each row is one full
   simulated dataset" + why R=5 is pedagogical; added a decision `.remark` (valid/overconfident/next step).
7. Power-section null notation distinguished from working-model target (the theta_0 split above).

## GLM highest-priority / recurring points (all addressed)

- Running clinical scenario with named drugs/endpoint/units: done (above).
- Front-loaded the miniature: added "Numbers to hang the symbols on" `.remark` after `@sec-sim-ademp`
  giving the R=5 numbers early; full example kept at the end.
- Reversed order in `@sec-sim-misspec` (plain English + collapse table preview first, then lemma/theorem);
  promoted the "telltale signature" to its own `.remark` callout.
- Defined inline: **functional** (intro), **scenario** (ADEMP), **local alternatives** (power), **regular**
  and **uniform integrability** (efficiency, with a skip-path and the MAIC-dominating-weight motivation).
- Requested figures rendered as tables (no image files, PDF-safe): two-sample-size schematic (intro),
  coverage-curve h(b) value table (misspec).
- Quantified "adequate overlap": ESS-as-fraction-of-n diagnostic tied to `@thm-maic-ess-bound` and the
  no-extrapolation limit; stated honestly that the literature has no single fixed cutoff.
- Rebuilt the unanchored paragraph into itemized 7/8/9 continuing the anchored 1-6 list.
- Sandwich-variance two-line refresher added at the empirical-vs-model remark.
- Softened the uniform-integrability step with the "What the baseline buys" `.remark` (skip-path + what UI
  rules out); the proof itself is unchanged.
- sigma_n (theoretical) vs SE_n (operational) gloss added at first use.
- Infinite-b bounding argument given an English gloss inside the proof (no math removed).
- 1/sqrt(R) numerical intuition table added after `@cor-sim-replications-bias`.
- Concrete MAIC omitted-EM instance theta_work ~ theta + beta1 * Delta xbar1 added.
- Worked power/sample-size instance (1.0-point PASI at 80% power -> sigma_n=0.36) added to power remark.

## New labeled environments (unique, verified no collision)

- `#exr-sim-interpret-mcse` (warm-up interpretation: bias vs its MCSE).
- `#exr-sim-interpret-collapse` (warm-up interpretation: coverage-vs-n as bias-vs-inefficiency diagnostic).

Everything else added is unlabeled `::: {.remark}` scaffolding or bare Markdown tables (chapter style uses
bare tables, no `#tbl-` ids).

## New tables (7)

1. Two-sample-size schematic (`@sec-sim-intro`).
2. Symbol/quantity glossary separating SE from MCSE (`@sec-sim-intro`).
3. ADEMP checklist instantiated for the psoriasis comparison (`@sec-sim-ademp`).
4. 1/sqrt(R) bias/coverage MCSE table (`@sec-sim-bias`).
5. Replication-count vs coverage-MCSE planning table (`@sec-sim-coverage`).
6. Coverage-curve h(b) values at z=1.96 (`@sec-sim-misspec`).
7. Robustness ordering summary (methods x assumption/bias/variance/coverage) (`@sec-sim-robustness`).

## Exercises

Added the one-line `$\star$`-convention note (full solution in Appendix F) and a progression sentence; added
two accessible warm-up interpretation exercises before the proof-heavy ones; tagged existing exercises by
type (computation/interpretation/design/proof); added solving hints to `@exr-sim-coverage-curve` (inverse
problem) and `@exr-sim-power` (sample-size algebra).

## Preservation and build safety (verified by script)

- All original labels present: `#sec-`, `#def-`, `#thm-`, `#lem-`, `#cor-`, `#prp-`, `#eq-`, `#exm-`,
  `#exr-` all intact; zero renamed, zero removed. No duplicate ids.
- Every existing theorem, lemma, corollary, proposition, and proof preserved in full; only scaffolding and
  intuition were added around them.
- No machine-checked tags exist in this chapter (by design; the Notes section explains why). The two
  "machine-checked" mentions are prose in `@sec-sim-notes`, preserved unchanged.
- American English; no dash punctuation (scan: only YAML `---` and Markdown `|---|` table rules).
- ASCII-only in math mode; the only non-ASCII is "Cramer" spelled with an accent in prose (pre-existing,
  allowed). `$\star$` used, never the Unicode star.
- No `\not` on extensible arrows; no bare `align`/`equation`/`gather` inside `$$`; `$$` (72) and inline `$`
  (2002) both balanced; all tables column-consistent; `:::` divs balanced (64 open / 64 close).
- No new `@bibkey` citations introduced; `@phillippo2016tsd18` form not needed (chapter does not cite it).

## Deliberately skipped / not done

- Literal figure files (two-sample-size schematic, coverage-curve plot): rendered as tables instead, to
  keep the PDF build (pdflatex) safe and match the chapter's figure-free style. The pedagogical content the
  reviewers wanted from the figures (the two-axis structure, the bell-shaped h(b) with the three collapse
  points) is delivered by tables 1 and 6.
- Did not trim the intro roadmap paragraph (GLM pacing suggestion): cutting prose risks other chapters'
  forward references and violates the "add, do not cut" constraint; concreteness was instead added via
  fast-reading tables.
