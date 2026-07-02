# Revision log: Chapter 26 (ML-UMR: Multilevel Unanchored Meta-Regression)

File: `chapters/part5/26-ml-umr.qmd`. Before: 1379 lines. After: 1786 lines (+407).
Reviewers addressed: `feedback/chatgpt/ch26-ml-umr.md` and `feedback/glm/ch26-ml-umr.md`.
No existing labels removed or renamed; all theorems and proofs preserved (only scaffolding and intuition
added). No new `@bibkey` citations introduced. `@phillippo2016tsd18` already correct (no bare form existed).

## Running example introduced (single highest-value addition)

`@exm-mlumr-running`: a single-arm oncology comparison. Index = a new therapy A in advanced melanoma with
IPD (age, PD-L1-style biomarker, response or survival); comparator = standard chemotherapy B with only a
published aggregate report (response rate or Kaplan-Meier curve, covariate means); no shared arm; an HTA
decision population `P*`. Numeric thread reused everywhere and completed in `@sec-mlumr-example`:
alpha_A = -0.5, beta_PF = 1.0 (logit), 77/200 comparator responders, biomarker prevalence 0.5. The worked
example's covariate was renamed from "high-risk indicator" (which confusingly gave a *higher* good-outcome
probability) to a favorable biomarker; the survival coda's covariate was clarified as a poor-prognosis
marker (elevated LDH) so direction is coherent.

## New labeled environments and tables (all globally unique; verified 0 prior occurrences)

Sections: `sec-mlumr-roadmap` (plain-language data-flow roadmap before the first formal estimand).
Definition: `def-mlumr-model-types` (Type 1 vs Type 2 models).
Examples: `exm-mlumr-running`, `exm-mlumr-relaxed-subgroups` (two-subgroup identification, counting vs
non-degeneracy), `exm-mlumr-km-inversion` (three-event KM inversion by hand).
Tables: `tbl-mlumr-methods` (ML-UMR vs unanchored MAIC/STC vs ML-NMR vs Bucher),
`tbl-spfa-sema` (SEMA vs SPFA contrast, per chapter-specific guidance),
`tbl-mlumr-identifies` (what data source identifies/reconstructs/assumes each parameter),
`tbl-mlumr-survival-estimands` (which survival estimand to report and whether it is transportable),
`tbl-mlumr-worked` (every worked-example number by covariate stratum, with the SPFA-violation column).
Exercises: `exr-mlumr-data-picture`, `exr-mlumr-spfa-belief`, `exr-mlumr-when-method` (conceptual warm-ups
before the proof-heavy ones); a top-of-section line explains the `$\star$` = Appendix F convention.

## ChatGPT highest-priority fixes (all addressed)

1. Novice roadmap before the first estimand -> `sec-mlumr-roadmap` (four-step data flow in words) plus a
   "reader translation" of `@eq-mlumr-estimand` (average on the natural scale first, then contrast on the
   link scale; spreadsheet mental model).
2. Clarify SPFA / absolute-effect constancy / difference from SEMA -> plain-language SPFA box (plausible and
   implausible clinical case) + `tbl-spfa-sema` immediately after `@def-spfa`.
3. Side-by-side ML-UMR / unanchored STC / ML-NMR (+ MAIC, Bucher) -> `tbl-mlumr-methods` in the roadmap.
4. Practical "what identifies what" table -> `tbl-mlumr-identifies` after `@thm-mlumr-model`.
5. Expand the survival bridge (KM -> integrated likelihood -> RMST/hazard) -> five-stage survival workflow
   recipe opening `@sec-mlumr-tte`; `tbl-mlumr-survival-estimands`; `exm-mlumr-km-inversion`; concrete
   two-value RMST scale-misalignment check ("Part (e) in two numbers").
6. Worked-example clinical clarity -> covariate renamed to a biomarker, outcome-direction reminders added,
   `tbl-mlumr-worked` shows p_A, fitted p_B, and true (violated) p_B by stratum with the calibration and
   bias made visible.

## GLM reviewer suggestions (addressed 1-12)

1 HTA scenario box -> `exm-mlumr-running`. 2 skeleton example early -> numbers previewed in the running
example and roadmap; full version stays in `@sec-mlumr-example`. 3 estimand gloss -> added. 4 restate
beta_1/beta_2,k at `@eq-mlumr-two-arm` -> added in place. 5 define identified / conflated intercept /
Type 1-2 / frailty -> all glossed inline; Type 1/2 as `def-mlumr-model-types`. 6 spell out theta_bullet_B,
pi_Ind, pi_Agg, beta_PF on first use -> done inline (see proposed notation.qmd additions below). 7 hypothesis
(iii) in plain terms -> "for the logit link, the observed proportion is strictly between 0 and 1". 8 lead
SPFA-vs-SEMA with the picture -> plain box + table now precede `@prp-spfa-vs-sema`. 9 figure -> deferred
(see below); replaced by prose "pictures" (spreadsheet metaphor, covariate-cloud metaphor, level-shift
projection already in `@lem-spfa-absolute-constancy`). 10 decision table -> `tbl-mlumr-methods` + prose
ML-UMR-vs-ML-NMR triage in the "When to use" remark. 11 how case (2) constraints are tested -> posterior
predictive check / LR-vs-Type-2 sentence added. 12 Hardy-Krause gloss -> "not too wiggly" clause added.

Also from GLM narrative: uncertainty-propagation reason to fit jointly vs two-step (HMC as black box);
STC-equivalence motivation moved up front; "automatic weighting is not robustness" reinforced with a
"Why this matters" note.

## Counts

Intuition / plain-language additions (reader translations and jargon glosses): ~16
(estimand gloss; identified + conflated intercept; beta_1/beta_2 restatement; beta_PF spell-out; SPFA plain
box; identification-in-one-breath with pi_Ind/pi_Agg/theta_bullet glosses; hypothesis (iii) gloss;
Type 1/2 def; HMC/uncertainty gloss; subgroup counting intuition; QMC "why an integral" bridge; Hardy-Krause
gloss; survival workflow + direction reminder; frailty gloss; part (e) two-number check; KM no-covariate
emphasis; STC-equivalence motivation).
Explicit "Why this matters" additions: 2 new headers (after `@thm-mlumr-model`, after
`@thm-mlumr-joint-likelihood`), plus motivation lead-ins for the STC-equivalence theorem and the survival
estimand table; the chapter already carried strong why-remarks after the other major theorems, which were
preserved.
New tables: 5. New examples: 3. New definition: 1. New section: 1. New exercises: 3 (+ star-convention line).

## Numbers verified by hand (rigor book)

KM inversion (d_j = 4,3,2; c_j = 2,1,0; S = 0.800, 0.629, 0.503) self-consistent. Relaxed two-subgroup
solve: logit(0.30) = -0.85, logit(0.55) = 0.20, beta_B = 1.05. RMST part (e): Delta(0) = 1.142,
Delta(1) = 1.156; population averages 1.149 (pi=0.5) vs 1.146 (pi=0.3), matching the coda's RMST_A = 5.32,
RMST_B = 4.17. Worked-example table (p_A, fitted p_B, true p_B) reproduces the pre-existing Steps 4 and 6
(comparator-weighted means both 0.385; index-weighted 0.3383 vs 0.2989).

## Labels I was tempted by but preserved

None removed or renamed. Preserved the capital-B slug `exr-mlumr-identify-alphaB` and every `#eq-`, `#thm-`,
`#lem-`, `#def-`, `#prp-`, `#sec-` id. Every original theorem and its full proof is intact; all additions
are new environments, tables, remarks, and glosses.

## Proposed notation.qmd additions (not edited here per file discipline; for the orchestrator)

- `theta_{\bullet k}` : aggregate arm-k mean, the response-scale outcome averaged over a covariate
  distribution (bullet marks the averaged-out covariate). Used as `theta_{\bullet B}`.
- `pi_{Ind}` : individual-level outcome distribution (GLM likelihood kernel for one patient).
- `pi_{Agg}` : aggregate-level distribution of a reported summary (binomial count, normal mean).
- `beta_{PF}` : shared prognostic slope under SPFA (already implied by the PF = prognostic factor gloss).

## Deferred

Figure (GLM #9: disconnected network + two covariate densities + SPFA level-shift projection). Not added as
TikZ to avoid an unverifiable pdflatex build risk; substituted with prose pictures and the level-shift
equation `@eq-spfa-projection`. Recommend the orchestrator add a TikZ/Excalidraw figure in a later pass.

## PDF-safety confirmation

ASCII-only in math; `$\star$` used (no Unicode star); no dash punctuation introduced (em/en/double-hyphen
grep clean); no bare align/equation/gather inside `$$`; display-math `$$` count even (72); `:::` fences even
(124); the one new section heading has a blank line before it; all new `#sec-`/`#tbl-`/`#exm-`/`#def-`/
`#exr-` ids unique across the book; every cross-reference resolves to a defined label.
