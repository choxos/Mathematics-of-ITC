# Revision log: Chapter 13, Pairwise Meta-Analysis

Revised for pedagogical accessibility per the two reviewer files
(`feedback/chatgpt/ch13-pairwise-meta-analysis.md`, `feedback/glm/ch13-pairwise-meta-analysis.md`),
following STYLE.md sections 10 (accessibility) and 11 (PDF build safety). All existing labels, theorems,
and proofs are preserved; every change is additive scaffolding plus one expanded proof step and two
short in-line glosses.

## Highest-priority fixes addressed

ChatGPT reviewer:
1. **Bridge from health problem to fixed-effect model, and what "one common effect" means.** Added a
   "Reader translation" remark after `@def-fixed-effect-ma` (same effect for whom, on what scale), plus
   an early link-scale paragraph and the running example.
2. **Make inverse-variance weighting intuitive before proving it.** Added a "Why these weights?"
   intuition remark before `@thm-fixed-effect-blue` with the concrete comparison (study C has 1/4 the
   variance of D, so 4x the weight; reciprocal SE would give only 2x) and the running-trio pooled value.
3. **Q to I^2 to DerSimonian-Laird transition.** Added a "From detection to description to estimation"
   roadmap table at the start of the I^2 section and a one-line "excess Q converted into tau^2"
   statement before `@thm-dersimonian-laird`; reader-translation remarks connect the three.
4. **Fixed-effect vs random-effects interpretation.** Added a six-row comparison table (assumption,
   estimand, weights, meaning, large-heterogeneity behavior, ITC relevance) and a plain-language
   statement of the reweighting principle in the main text of `@sec-ma-random`.
5. **Soften REML.** Added a "What REML is trying to fix" orientation paragraph before `@thm-reml-tau2`
   (downward MLE bias, n vs n-1, too-narrow intervals, error contrasts, previews the sanity check) and a
   numerical REML fixed-point iteration on the running trio after the equal-variance remark.
6. **More ITC motivation throughout.** ITC ties added to the Cochran, random-effects, Bayesian, and
   Egger "Why this matters" remarks and the closing decision-impact paragraph.
7. **Worked-example style earlier.** A three-study running trio (C, D, E) is now threaded through IVW,
   Q, I^2, DL, random-effects reweighting, REML, and HK, with the full five-study capstone unchanged.

GLM reviewer (numbered suggestions):
1. Running example threaded through (trio C, D, E), capstone preserved.
2. Forest plot (early) and funnel plot (Egger) added as ASCII schematics in verbatim code blocks (the
   book uses no figure files; ASCII keeps the pdflatex build safe).
3. Random-effects reweighting intuition stated explicitly in main text and in the DL remark
   (C's weight share falls 73% to 47%).
4. Hartung-Knapp working-model explanation previewed before `@thm-hartung-knapp`.
5. Whitening softened via a "how to read the proof" remark between theorem and proof (glosses whiten,
   S^{-1/2}, 1_k, positive definite, bijection).
6. Plain-language motivation before each distributional result (Cochran = heterogeneity p-value; REML =
   fix for downward bias; HK = widen when k small).
7. Link-scale / non-collapsibility introduced near the start (forward refs to `@def-collapsibility`,
   `@thm-noncollapsibility-or-hr`).
8. Index-collision mnemonic added to the indexing remark ("a study is a single data point").
9. Invoked Part I results reminded in line: Fisher information and Cramer-Rao (efficiency remark),
   spectral theorem and mvn-affine-closure and idempotence (pre-lemma gloss), sigma^2 unbiased and
   t-statistic (HK preview), conjugate-normal (Bayesian reader translation).
10. Funnel plot described with axis meaning ("precision" = 1/s) plus the ASCII funnel.
11. Weighted sum-of-squares identity spelled out in full inside the `@prp-expected-q` proof.
12. Glossary table ("Terms you will meet") added: contrast, heterogeneity, whiten, positive definite,
    idempotent, projector, error contrasts, working model, type-II ML, funnel plot.

## What was added (by location)

- Front matter (before `@sec-ma-fixed`): two-stage reader translation; link-scale paragraph; running
  example `@exm-ma-running` (five-trial table); ASCII forest plot; glossary table; roadmap paragraph.
- Indexing remark: mnemonic sentence.
- Fixed-effect section: model reader-translation; IVW intuition remark; why-BLUE/how-to-read-the-proof
  remark; efficiency "Why this matters" remark.
- Cochran section: reader-translation bridge (Q as weighted RSS, trio Q = 4.82); idempotence/spectral
  reminder before the lemma; lemma reader-translation; theorem "Why this matters" (heterogeneity
  p-value, verbal k-1); expanded weighted-SS identity in `@prp-expected-q`; b_i reader-translation.
- I^2 section: roadmap table; reader-translation plus H^2/hat-matrix collision note; "What I^2 is not"
  warning; sigma^2_typ gloss with trio I^2 = 59%.
- Random-effects section: FE-vs-RE table and reweighting paragraph; model reader-translation;
  identifiability concrete reader-translation.
- DL section: one-line conversion-factor framing; reader-translation with trio tau^2_DL = 0.048.
- REML section: orientation paragraph; iteration remark (trio 0.048 to 0.045).
- HK section: working-model preview; running-trio interval remark (t_2 = 4.303, interval widens).
- Bayesian section: NMA-are-hierarchical motivation; posterior reader-translation with trio numbers;
  "completing the square" and type-II ML glosses in the marginal-likelihood remark.
- Egger section: funnel-plot description and ASCII funnel; "Why this matters for ITC" remark.
- Capstone: decision-impact paragraph (FE vs RE-Wald vs HK intervals).
- Exercises: starred-convention line; two accessible warm-ups; hints on the Cauchy-Schwarz, REML,
  Hartung-Knapp, and Egger exercises.

## New labels added (none removed or renamed)

- `#exm-ma-running` (running example)
- `#exr-ma-warmup-weights` (warm-up exercise, unstarred)
- `#exr-ma-i2-interpretation` (interpretation exercise, unstarred)

New exercises are intentionally unstarred: Appendix F solves only the two existing starred exercises
`@exr-ma-fe-pipeline` and `@exr-ma-reml-balanced`, and I did not edit Appendix F.

## Numerical verification

All running-trio and capstone numbers were checked programmatically. The capstone values reproduce the
existing worked example exactly (theta_FE = 0.2663, Q = 5.714, I^2 = 30.0%, c = 141.57, tau^2_DL =
0.01211, theta_R = 0.3036, q = 0.963). Trio (C, D, E): theta_FE = 0.264, Q = 4.818, p = 0.090, I^2 =
58.5%, c = 59.09, tau^2_DL = 0.048, theta_R = 0.365, C weight share 73% to 47%, REML fixed point
converges to about 0.045, HK interval (-0.27, 1.00) with t_2 = 4.303.

## Notation and sources

- No new notation symbols introduced. `sigma^2_typ` was already in the original chapter; the glossary and
  mnemonic reuse existing symbols only.
- No new bibtex keys used. All `@`-citations in added prose (`@dias2018nma`, `@dersimonian1986`) already
  exist in `references.bib`. The original "Notes and references" list of not-yet-in-bibliography sources
  (Higgins-Thompson 2002, Hartung 1999, Hartung-Knapp 2001, Sidik-Jonkman 2002, IntHout 2014,
  Viechtbauer 2005/2010, Egger 1997, Gelman 2006, Veroniki 2016) is unchanged; no new source added.

## What was left unchanged

- Every theorem, lemma, proposition, definition, corollary statement and its full proof; the only proof
  edit expands the weighted sum-of-squares identity in `@prp-expected-q` (adds algebra, deletes nothing).
- All existing labels, equation numbers, the YAML title, and the "Notes and references" attribution
  section.
- The indexing convention (i indexes studies) was kept as in the original, per the hard constraint not
  to rename; a mnemonic was added rather than switching to j, since Appendix F and later chapters may key
  off the current statements.

## PDF build safety

ASCII-only in math; `$\star$` used (no Unicode star); no `\not` on extensible arrows; all display math
uses single-line chains or existing `aligned`/`cases`; forest and funnel plots are plain verbatim code
blocks; `[Notation](/notation.qmd)` link preserved; all `#sec-` ids unique; blank line before every
section heading. Automated checks confirmed: 0 non-ASCII characters, 0 em/en dashes, balanced code
fences (2 blocks) and `:::` divs (66/66), all 52 original labels present.
