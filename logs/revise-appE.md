# Revision log: Appendix E, Reference Implementations (multinma, mlumr, uitc)

File: `appendices/E-reference-implementations.qmd`
Kind: code (math-object to package-function map).
Line count: 413 before, 819 after.
Reviewers addressed: `feedback/chatgpt/appendix-E-reference-implementations.md` and
`feedback/glm/appendix-E-reference-implementations.md` (both read in full; highest-priority fixes
prioritized).

## Highest-priority fixes addressed

ChatGPT reviewer:
1. Package-choice decision guide moved to the front. Added `## Orientation for the first-time reader`
   with a `### Which package answers which question` decision-guide table plus a one-paragraph HTA
   scenario per package. (Original routing table at `@sec-impl-together` preserved.)
2. Data-requirements table added: `### What data each method needs` (columns: method/package, network,
   IPD needed, AgD outcome summary, covariate summary, survival input, main output).
3. Concrete running example added (drug A IPD, drug B AgD, placebo P, PASI 75 outcome, age/sex
   covariates, target population age 48 / 40 percent female) in a remark box, then reused in the toy
   data frames, the model-term table, and the illustrative estimand result.
4. Conditional vs marginal explained in plain language in the estimand section, with which one an HTA
   submission reports and why (marginal, because the OR is non-collapsible).
5. Bridge text added before QMC (approximating the comparator distribution from summaries), adjusted
   binomial (mixture variance), SPFA (age example), survival (KM reconstruction staging), and QBA
   (workflow ladder).
6. Cross-method comparison guidance added twice: naive/stc/mlumr in `@sec-impl-mlumr-benchmarks`, and
   the full MAIC/STC/DR/ML-UMR panel in `@sec-impl-together` (what agreement/disagreement means).

GLM reviewer:
1. Worked/illustrative numbers added (illustrative log-OR -0.82, 95 percent CrI -1.21 to -0.43),
   explicitly marked "illustrative, not from a real fit."
2. Both Stan snippets annotated inline: `binomial_1par` (stacked-array slice, `~` sampling statement)
   and `mlumr_binary_spfa` (`Xq_int[k] * beta_tilde`, `inv_link_binary_vec`, `mean(p_int)`, `~`).
3. QMC four-step pipeline-arrow table added, ordered by data flow (Sobol point, normal scores,
   correlate/back-to-uniform, marginal quantile), each row with the R argument that produces it.
4. Jargon defined at first use in the appendix body and in a glossary table: anchored/unanchored, SPFA,
   SEMA, non-collapsible, G-computation, ESS, conditional/marginal, QMC, copula, effect modifier,
   prognostic variable, `trt_effects` (fixed/random), `center = TRUE`, `distr()`, love plot / SMD,
   RMST, pseudo-IPD.
5. Survival subsection expanded from ~10 to ~28 lines (digitized-KM input format, family-choice rule of
   thumb, non-collapsibility gloss, RMST-vs-HR interpretability) with an explicit "read Chapter 25 and
   the vignette first" defer.
6. Toy 3-row IPD and 2-row AgD data frames printed before the first `set_ipd()` call, with a column-by-
   column gloss (including the `r = r` argument-name-vs-column-name ambiguity).
7. "How to choose `n_int`" paragraph added (default 64, empirical doubling check, cost scaling, tie to
   Koksma-Hlawka).
8. Aggregation section now leads with the motivation (naive plug-in is biased, `@thm-aggregation-bias`)
   before any code.
9. `qba_tipping_itc()` vs `qba_prob_itc()` differentiated in prose (deterministic root-finding vs prior
   plus Monte Carlo).
10. `dr_estimator()` worked call added (the one estimator native to `uitc`), plus a residual-vs-
    weighted_gcomp augmentation gloss and an `n_sim` vs `n_int` clarification.

Also addressed: `distr()` closure explanation with a tiny example; Gaussian-copula two-sentence
intuition plus Chapter 22 pointer; MAIC weight-solve shown as annotated pseudocode (centered covariates,
convex objective Q, gradient = imbalance, weights); ESS and love-plot/balance diagnostics described with
the |SMD| < 0.1 rule of thumb; ML-NMR-collapses-to-NMA promoted from a subordinate clause to a callout;
Stan-file audience note added; `add_integration()` difference between multinma (many AgD studies) and
mlumr (single comparator population) stated; per-package HTA motivation added; reading-workflow note
("what this appendix is for") added at the top.

## New labeled environments / tables / code

New `#sec-` ids (all confirmed unique across the repo before adding):
- `#sec-impl-orientation`, `#sec-impl-which-package`, `#sec-impl-data-needed`, `#sec-impl-glossary`.

New tables (6): which-package decision guide; data-needed table; terms glossary; model-term walkthrough;
multinma call argument gloss; QMC four-step pipeline-arrow table.

New code blocks (3 R): toy IPD/AgD data frames; MAIC weight-solve pseudocode; `dr_estimator()` call.
Two existing Stan blocks annotated in place (lines preserved, comments added around them).

New callout: "Sanity check: ML-NMR contains NMA" remark; plus the running-example remark.

Intuition/plain-language gloss insertions: roughly 35 distinct additions across the three package
sections (motivation leads, reader translations after equations and tables, jargon glosses,
"what output should I look at" notes).

## Reviewer-flagged item that was NOT a math error

The GLM reviewer found the adjusted-binomial reparametrization `@eq-impl-adjusted-binomial` opaque, not
wrong. The identities are correct: `n' p' = n * theta_bar` (the product is unchanged) and
`p' = theta2_bar / theta_bar >= theta_bar` (since `theta2_bar >= theta_bar^2`). No incorrect identity
was present, so nothing was corrected; instead the missing derivation chain was ADDED, showing the
per-patient probability moments and that their gap `theta2_bar - theta_bar^2` is the variance of the
probabilities (>= 0), which is the dispersion the second parameter carries. This is a clarification, not
a fix.

No forward-reference/`??` bugs were present. The "term used before defined" complaints (distr, SPFA,
anchored) were pedagogical and are resolved by the early glossary table plus inline first-use
definitions.

## Preservation confirmation

- All 22 original `#sec-impl-*` labels preserved (now 26 with the 4 new orientation ids).
- All 4 `#eq-impl-*` labels preserved exactly (`eq-impl-mlnmr-model`, `eq-impl-aggregation`,
  `eq-impl-adjusted-binomial`, `eq-impl-qmc`).
- All ~70 `@thm-/@eq-/@def-/@prp-/@cor-/@sec-` cross-references preserved (verified by grep; zero
  dropped).
- No `[machine-checked: ...]` tag or `theories/*.v` pointer exists in this appendix; none added or
  removed.
- Every existing listing, mapping table, and object-to-code map preserved; content only added.

Labels/structures I was tempted to change but PRESERVED:
- The `## Using the three packages together` routing table: reviewers asked to "move it to the start." I
  did NOT move or delete it; I added a separate early decision guide (`@sec-impl-which-package`) and left
  the original table and its name-collision advice intact.
- The two Stan snippets and `@eq-impl-adjusted-binomial`: preserved verbatim, only wrapped with comments
  and surrounding prose.

## Build-safety checks (Section 11)

- Pure ASCII (grep for non-ASCII returned nothing); no em/en dash, no Unicode math glyphs.
- No prose dash connectors. The single ` - ` hit is `beta_index - beta_comparator` inside an inline code
  span (subtraction; pre-existing, legitimate).
- All display math uses bare `$$ ... $$` with `\qquad`/`\frac`/`\sum`; no bare `align`/`equation`/
  `gather`.
- No `\not` on an extensible arrow.
- Blank line before every real heading (the two awk hits are R `#` comments inside a fenced block).
- 16 code fences = 8 balanced pairs; 3 `:::` opens = 3 closes.
- No `@phillippo2016tsd` citation present (nothing to fix); no new bib keys introduced (all citations
  already in `references.bib`).

## Gaps left

- Illustrative numeric results are hand-written placeholders, not executed output (the appendix cannot
  run code at render time); they are labeled as illustrative. A future pass could substitute real
  vignette output from the `multinma` plaque-psoriasis example if the orchestrator wants executed
  numbers.
