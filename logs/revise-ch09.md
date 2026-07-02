# Revision log: Chapter 9, Potential Outcomes and Identification

Reviewers addressed: `feedback/chatgpt/ch09-potential-outcomes.md` and `feedback/glm/ch09-potential-outcomes.md`.
Target reader: novice health researcher with weak mathematics. Both files' "highest-priority fixes" were
prioritized. Every existing label and every theorem/proof was preserved; all changes are additive
scaffolding plus prose clarifications inside proofs (no mathematics deleted, no proof shortened).

## Highest-priority fixes addressed

ChatGPT highest-priority list:
1. Plain-language bridges before every formal definition (potential outcomes, SUTVA, ignorability,
   positivity, identification): added an intuition paragraph before each `def-`/`thm-`, plus a bold
   "Reader translation" after each definition.
2. ITC motivation made visible throughout, not only intro/bridge: added ITC-facing lines after SUTVA
   (common-comparator), consistency (IPW hinge), estimands (which estimand ITC targets), positivity
   (covariate overlap between studies), and identification ("what MAIC/STC/ML-NMR estimate").
3. Clarified target-population averaging and the meaning of `E_X`: new `@def-observed-regression` block
   plus an explicit paragraph stating that the outer `E_X` averages over the target population's covariate
   distribution `P_X`, defined in-text.
4. Quarantined the technical ignorability-hierarchy proof: added a "Reader's note" marking it skippable on
   first reading, restated graphoid G1/G2 inline, explained the truncation, and named the reference. Full
   proof retained.
5. Concrete positivity/overlap failure: clinical "frail patients never treated" example and the ITC
   "elderly-only vs young-only trials" overlap failure, both before the propensity-score inequalities.
6. Unpacked the ITC bridge into a full three-part section (within-study, across-study, what becomes central)
   with an AB/AC anchor table.

GLM numbered suggestions: (1) intuition paragraph before `@def-potential-outcome` with clinical numbers
(Alice/Bob) done; (2) `P_X` and `E_X` defined in-text (and flagged for notation.qmd, see below); (3)
`@def-observed-regression` named block contrasting mu_t^obs with mu_t done; (4) three steps of
`@lem-mean-potential-identification` inline-labeled (Step 1 tower / Step 2 ignorability / Step 3
consistency); (5) stripped-down preview example `@exm-gformula-preview` right after
`@thm-ate-identification`; (6) AB/AC anchor schematic table in `@sec-po-bridge`; (7) non-collapsibility
aside softened to a one-sentence "you do not need this yet" signpost; (8) `@sec-po-bridge` expanded with
estimand target, overlap-failure picture, transport-as-ignorability+positivity-across-populations; (9)
graphoid G1/G2 restated inline and conditional dominated convergence tied to `@thm-dominated-convergence`;
(10) health-domain gloss after `@def-ignorability` and `@def-positivity`; (11) motivation stated for the
add-and-subtract choice in `@thm-naive-selection-bias`; (12) Appendix F confirmed to exist with solutions
for both starred exercises (see below); (13) machine-checked tags: added an early navigational note telling
readers they can skip them, and pointed auditors to Appendix G (tags left in place, not removed, to keep the
orchestrator's verification intact).

## What was added (by section)

- New `## A running clinical example {#sec-po-running}`: Alice (favorable baseline, scores 24/20) and Bob
  (poor baseline, 14/10), reused at every transition. Their numbers equal the stratum means of the existing
  worked example `@exm-confounding-gformula`, so the running thread and the worked example are one
  population.
- Intro: "recall from Chapter 5 / `@def-conditional-expectation`" pointer; one-clause glosses for
  Neyman-Rubin, SUTVA, consistency identity, ignorability, positivity in the roadmap; in-text definition of
  `P_X` and `E_X`; navigational note on machine-checked tags and Part I citations.
- Neyman-Rubin: "omega is one patient; the space is 'draw a patient at random'" paragraph; lowercase-t vs
  uppercase-T callout at the label formula; Reader translations; plain-English restatement of
  `@thm-fundamental-problem` before the formal statement; "Why this matters" (warrant for targeting
  averages).
- SUTVA: Reader translation; ITC-relevant SUTVA-2 failure (oncology chemo-dose across trials); a
  patient-level table (Alice/Bob/Carol: T, Y(0), Y(1), observed, hidden); motivation for the masked
  identities (isolating one arm, IPW); rewrote the `@cor-consistency-swap` locality argument to cite the
  defining property of conditional expectation (`@def-conditional-expectation`, `@eq-cond-exp-defining`)
  instead of the mis-landed original citation; Reader translation of the swap.
- Estimands: target-population paragraph (trial vs cohort vs ITC target); Reader translations for ATE/ATT/
  ATC/CATE; a four-row estimand table with ITC roles; statement that most methods target a marginal
  (ATE-type) effect in a stated target population; softened non-collapsibility aside.
- Assumptions: identification-vs-estimation and "functional = map from distributions to a number" glosses;
  up-front motivation for three ignorability strengths; health gloss and a three-row ignorability table; the
  skippable-proof note and inline G1/G2 + truncation + DCT reference; an inline two-row "equal means,
  different variances" table illustrating mean-holds-weak-fails; a "What to remember" paragraph (promoted
  from the old terse remark) including the untestability example (RA/oncology severity); positivity
  intuition before the inequalities; `P_X` defined at `@def-positivity`; variance/stability rationale pulled
  up next to `@eq-strict-positivity`.
- Identification: `@def-observed-regression` (mu_t^obs) with Reader translation and `E_X` explanation;
  inline step labels in the lemma proof; "Why this matters" after `@thm-ate-identification`;
  `@exm-gformula-preview` (ATE=4 vs naive=9 at a glance); reorganized the forward-pointer paragraph to lead
  with G-computation and IPW (kept all forward refs); expanded the closing remark into a full paragraph on
  why we state strong ignorability though mean suffices (randomization gives strong free; balancing theory
  needs it).
- Selection bias: pre-theorem schematic (treated healthier -> built-in head start); motivation for the
  add-and-subtract choice; "Why this matters"; clarified "marginally randomized experiment" = simple RCT
  (one coin for all), contrasted with a stratified trial.
- Worked example: framing tying it to Alice/Bob; added a paragraph distinguishing prognostic variable vs
  confounder vs effect modifier (with `@def-prognostic-variable`, `@def-effect-modifier` signposts),
  addressing the reviewer worry that a novice may treat any baseline imbalance as an ITC bias on every
  scale. Numbers, parts, and results (4, 9, 5.0) unchanged.
- Bridge: expanded to three labeled paragraphs plus an AB/AC anchor table (d_BC = d_AB - d_AC), the
  overlap-failure picture, and the "what becomes central later" list (estimand, effect modification, scale).
- Exercises: one-line `$\star$` = Appendix-F-solution note at the top; two new accessible exercises first
  (`@exr-po-warmup-ite` reading potential outcomes; `@exr-po-interpret-estimand` choosing the right
  estimand); category tags (Warm-up / Interpretation / Computation / Proof / Challenge) on every exercise;
  scaffolding hint added to `@exr-po-mean-vs-weak` (two-row template) and a "draw the 2x2 and mark the empty
  cell" preliminary to `@exr-po-positivity-failure` (kept parts (a)(b)(c) intact so the Appendix F solution
  still matches).

## New labels added (all verified collision-free)

- `#sec-po-running` (running-example section)
- `#def-observed-regression` (mu_t^obs, the observable regression)
- `#exm-gformula-preview` (stripped-down ATE-vs-naive preview)
- `#exr-po-warmup-ite`, `#exr-po-interpret-estimand` (two accessible warm-up/interpretation exercises)

No existing `#thm-/#lem-/#cor-/#prp-/#def-/#eq-/#sec-/#exm-/#exr-` label was renamed or removed. Verified:
all 47 pre-existing labels present exactly once; all 12 bracketed `[machine-checked: ...]` tags preserved
verbatim.

## New cross-references introduced (all resolve)

`@def-conditional-expectation`, `@eq-cond-exp-defining`, `@thm-dominated-convergence` (Chapter 4);
`@def-prognostic-variable`, `@def-effect-modifier` (Chapter 11); `@robins1986` (already in references.bib).
All confirmed to exist. No new bibtex keys were cited beyond those already in `references.bib`.

## Proposed additions for the orchestrator (I did not edit these files)

- notation.qmd: add `P_X` = marginal law (distribution) of covariates `X`; and `E_X[.]` = expectation over
  that covariate distribution, `E_X[h(X)] = \int h(x) dP_X(x)`. Both are used heavily from
  `@lem-mean-potential-identification` onward and are currently defined only in-text here.
- references.bib: the notes section still attributes Neyman (1923, transl. 1990), Rubin (1974), and Holland
  (1986); these remain not-yet-in-bib sources (unchanged from the prior draft). Robins is now cited via the
  existing `@robins1986` key for the g-formula.

## Appendix F check (reviewer request)

Confirmed `appendices/F-solutions.qmd` exists and contains full solutions for both starred exercises,
`### Solution to @exr-po-positivity-failure` and `### Solution to @exr-po-selection-bias-proof`. The
starred pointers do not dangle. I kept the parts (a)/(b)/(c) structure of `@exr-po-positivity-failure`
unchanged so the existing solution still maps; the added "draw the 2x2, mark the empty cell" step is a
preliminary that precedes (a).

## Deliberately left unchanged

- All theorem/lemma/corollary/proposition statements and their proofs (content, symbols, numbering). Proof
  text was augmented for clarity (inline glosses, step labels, better citation in the locality argument) but
  never shortened; no line of mathematics was removed.
- The worked example `@exm-confounding-gformula` numbers and every derived value (ATE 4, naive 9, selection
  bias 5.0), because exercises and both reviewers reference them.
- The 12 machine-checked tags (kept in place rather than moved to footnotes, to preserve the orchestrator's
  verification pass and the book-wide tagging convention; addressed the "noise" concern with an early
  skip-on-first-reading note instead).
- The forward references to Chapter 10-12 results (`@thm-ipw-unbiased`, `@thm-g-computation-unbiased`,
  `@thm-aipw-double-robust`, `@thm-eif-bound`, `@def-balancing-score`, `@thm-rosenbaum-rubin`,
  `@thm-ps-sufficiency`, `@def-transportability`, `@def-ecological-bias`, `@def-non-collapsibility`,
  `@def-collapsibility`, `@exm-noncollapsible-or`): all retained (none break other chapters), but the dense
  forward-pointer paragraph was reorganized to lead with the two central estimators and to read as prose
  rather than a table of contents.

## Build-safety checks run (STYLE Section 11)

ASCII-only in math (no non-ASCII anywhere in the file); `$\star$` used for stars (no Unicode star); no bare
`align`/`equation`/`gather` inside `$$` (only `aligned`); no `\not` on an extensible arrow (`\not\equiv`
only); notation chapter linked as `[Notation](/notation.qmd)`; blank line before every section heading;
div-title `##` headings correctly follow their `::: {#...}` openers; `:::` fences balanced (38 open, 38
close). American English and the no-dash-as-connector rule observed throughout the new prose.
