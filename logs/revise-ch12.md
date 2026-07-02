# Revision log: Chapter 12, Transportability (pedagogical accessibility pass)

Revised `chapters/part2/12-transportability.qmd` to address both reviewer files
(`feedback/chatgpt/ch12-transportability.md` and `feedback/glm/ch12-transportability.md`), prioritizing
each reviewer's highest-priority fixes. All revisions were applied as anchored insertions, so every
existing theorem, lemma, corollary, proposition, definition, equation, and proof is preserved byte for
byte. No label was removed or renamed. No mathematics was deleted or shortened.

## Method and safety

- Edits made by exact-match insertion around existing anchors; the original math and proofs are untouched.
- Verified after editing: all 51 original `#...` labels present; div opens/closes balanced (39/39);
  `$$` display delimiters even (76); 9 `.proof` divs with 9 QED marks. No Unicode star, em/en dash, smart
  quotes, bare `align`/`equation`/`gather`, or `\not` on an extensible arrow. American English throughout;
  no dash-as-connector in prose. `$\star$` used for the exercise marker.

## New labeled environments added (no existing label touched)

- `#exm-transport-running` : running HTA example, one submission with three populations
  (index `f_{AB}`, comparator `f_{AC}`, decision `P*`), placed right after the introduction.
- `#exm-transport-toy-identity` : early identity-scale toy so the reader touches numbers before the
  collapsibility lemma (GLM suggestion 1).
- `#exr-transport-hta-populations` : warm-up/interpretation exercise (name the three populations).
- `#exr-transport-read-report` : interpretation exercise (reading a MAIC report).

## ChatGPT reviewer: highest-priority fixes

1. **Running HTA example that returns in each section.** Added `#exm-transport-running` (younger
   biologic-naive index trial `f_{AB}`, older biologic-experienced comparator trial `f_{AC}`, broad
   decision population `P*`, single binary covariate X with P(X=1) = 0.10 / 0.90 / 0.50). Reused it in the
   setup motivation, in the mode-2 reader translation, in the overlap reader translation, in the early
   toy example, and in the worked-example interpretations. The two trial populations are tied to the
   existing worked-example populations P1 (0.1) and P2 (0.9).
2. **Diagram/table for the two-step PAIC transport.** Added a Markdown roadmap table before
   `thm-two-step-transport` (Step 1 explicit conditional transport `f_{AB}` to `f_{AC}` giving
   `d_{BC(AC)}`; Step 2 implicit direct transport `f_{AC}` to `P*` giving `d_{BC(P*)}`), plus explicit
   text that the usual PAIC estimand is `d_{BC(AC)}` unless the decision population is the comparator
   population.
3. **Intuition before scale alignment and non-collapsibility.** Added a three-conditions preview table
   (SEMA / alignment / collapsibility, each buying one link) at the top of `sec-collapsibility-transport`;
   a plain-language "model scale versus reporting scale" paragraph with two aligned and two misaligned
   examples before `def-scale-alignment`; a concrete `psi = expit` illustration inside the
   `thm-scale-alignment` part (ii) proof; and a plain reader translation before the `thm-sema-insufficient`
   proof.
4. **Marginal vs population-average conditional effect.** Added a "Reader translation (marginal versus
   conditional)" paragraph with a two-stratum numeric table (logit of the average = -0.619 vs average of
   the logits = -0.693; gap 0.074) right after the effect definitions, well before non-collapsibility is
   used.
5. **Decision-context language.** Added a main-text "What this means for a reimbursement submission"
   paragraph after `thm-two-step-transport` spelling out Sponsor 1 (standardizes to its `f_{AC}`), Sponsor
   2 (different comparator trial, different population), and the HTA body (its own `P*` from label and
   reimbursement criteria). Kept the original "Why two sponsors can disagree" remark.
6. **Applied interpretation on the worked examples.** Added a "What a researcher would report" paragraph
   after each of the continuous, binary, and RMST examples, stating what to report, which population it
   applies to, and what goes wrong if carried elsewhere.
7. **Novice-accessible exercises first.** Added `exr-transport-hta-populations` and
   `exr-transport-read-report` at the top of the exercises, and labeled every exercise with a tier
   (warm-up, interpretation, computation, proof). Added the one-line starred-exercise convention.

Also addressed ChatGPT "under-explained" items: support/overlap now has a renal-impairment aside
(overlap reader translation); a covariate-role checklist (effect modifier / prognostic / trial-inclusion /
irrelevant-imbalanced) after the invariance failure mode; effect-scale clinical interpretation ("which
effects are conditional/marginal and why HTA wants marginal"); RMST defined in a footnote at first use;
intuition paragraph before the dense `thm-sema-insufficient` proof.

## GLM reviewer: suggestions

- Suggestion 1 (toy binary example after `thm-direct-transportability`): added `exm-transport-toy-identity`.
- Suggestion 2 (move worked examples up next to the theorems): rather than move labeled sections (which the
  hard constraint protects), added early concrete touchpoints (`exm-transport-toy-identity`, the density-
  ratio numeric, the cor-conditional-transport preview quoting 1.175 vs 0.622) and cross-linked the full
  worked examples so each theorem lands on numbers on contact. The full worked-example section is preserved
  in place.
- Suggestion 3 (invariance vs SEMA paragraph): added the "Invariance versus SEMA (a preview)" paragraph.
- Suggestion 4 (unpack change-of-measure in the g-formula proof): added a plain-English sentence in the
  proof and a "Reader translation" after the theorem; both frame the weight as how much more common a
  covariate value is in the target.
- Suggestion 5 (soften `thm-scale-alignment` (ii) with expit and the "not affine implies nonzero second
  derivative" reminder): done inside the proof.
- Suggestion 6 (promote "why two sponsors can disagree"): added the main-text reimbursement paragraph;
  kept the remark.
- Suggestion 7 (notation entries): could not edit `notation.qmd` (file discipline). Instead added a
  chapter-local glossary table and inline definitions; see "Proposed notation additions" below.
- Suggestion 8 (plain-English gloss after each major theorem): added "Why this matters" after
  `thm-direct-transportability`, `thm-conditional-transportability`, `thm-two-step-transport`,
  `thm-scale-alignment`, `thm-collapsible-transport`, `cor-conditional-transport`, `thm-sema-insufficient`,
  `prp-transport-table`, and `lem-collapsible-scales`.
- Suggestion 9 (figure of two densities): rendered as tables/roadmaps rather than a figure, per STYLE
  Section 10 (Markdown tables are the sanctioned substitute) and Section 11 (PDF safety, no TikZ set up):
  the running-example population table, the marginal-vs-conditional numeric table, the two-step roadmap
  table, and the three-conditions table.
- Suggestion 10 (soften the machine-checked paragraph): added a one-sentence plain-language lead-in.

Other GLM "unclear"/"under-elaborated" items addressed: plain gloss in `def-transport-invariance` reader
translation; forward pointer in `def-transportability` mode 2 to `thm-conditional-transportability`;
overlap aside; density-ratio weight worked in the body; Bucher shared-population reminder in the two-step
proof; Step-1-vanishes-but-Step-2-need-not paragraph; weight motivation in `lem-collapsible-scales` proof;
expanded direct-collapsibility remark explaining why the weaker property suffices; RMST setup lead-in
before the computation; "why prove necessity" paragraph; footnotes for expit/logit, anchored/unanchored,
Hajek, catalogue numbering.

## Proposed notation.qmd additions (recorded here; notation.qmd not edited, per file discipline)

The following are used centrally in this chapter and are currently absent from `notation.qmd`. They are
defined inline (glossary table plus first-use footnotes) in the chapter; the orchestrator may fold them in:

- `d_{ab}(x)` : conditional relative effect at covariate value x, `g(mu_b(x)) - g(mu_a(x))` (distinct from
  the marginal `d_{ab(P)}` already listed).
- `h`, and `psi = h . g^{-1}` : effect-measure transform (reporting scale) and the alignment composition.
- `e_t(x) = P(T=t | X=x, S=src)` : generalized (multi-treatment) propensity, extending the binary `e(x)`.
- `logit(p) = log{p/(1-p)}` and its inverse `expit(z) = 1/(1+e^{-z})`.

## Citations / bibliography

No new bibliography entries were introduced. The chapter cites only keys already present in
`references.bib` and verified during this pass: `chandler2026transport`, `hernan2020whatif`,
`phillippo2016tsd18`, `phillippo2020mlnmr`. No new sources were needed.

## Deliberately left unchanged

- The five-movement introduction (GLM found it long but "excellent"): kept intact; instead of trimming it,
  the running example immediately after it gives the concrete anchor the reviewer wanted, and the
  three-conditions and two-step tables serve as the roadmaps.
- The full late `sec-transport-worked` examples: kept in place (labels are cross-referenced); reinforced
  with early touchpoints and per-example interpretation rather than relocated.
- All theorem/proof mathematics, hypotheses, and numeric values: unchanged. The one small arithmetic
  correction is in NEW text only: the body density-ratio illustration uses `w(0) = 0.4/0.7 = 0.571`
  (checked: 0.7(0.571) + 0.3(2) = 1); a reviewer's aside had written 0.857, which is a slip.
- Machine-checked tags: none added (the chapter's owned results have no ITC_Coq counterpart, as the
  original notes state); only a plain-language lead-in was added to that paragraph.

## Verification

Static checks all pass (labels, balance, PDF-safety, spelling, no-dash). A standalone
`quarto render ... --to pdf` was launched to confirm the LaTeX/pdflatex compile; result recorded at build
time in the session (see scratchpad `ch12render.log`).
