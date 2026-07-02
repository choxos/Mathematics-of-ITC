# Work log: Chapter 17, Population Adjustment Theory

Author pass: Opus 4.8. Part IV, chapter 17. File overwritten:
`chapters/part4/17-population-adjustment-theory.qmd` (stub replaced; YAML title kept).

## Scope and catalogue identifiers owned

Catalogue results E.4 to E.12 from `proofs/E_population_adjustment_theory.md`, each stated and proved
in full and tagged with "(corresponds to E.n in the proof catalogue)":

- E.4 conditional constancy of relative effects -> `@def-conditional-constancy-relative`
- E.5 conditional constancy of absolute effects -> `@def-conditional-constancy-absolute`
- E.6a to E.6e anchored consistency (scale-specific) -> `@thm-anchored-paic-consistency`
  (single theorem with parts (a) conditional recovery, (b) marginal recovery on an aligned collapsible
  scale, (c) non-recovery of a non-collapsible marginal effect, (d) scale misalignment / RMST,
  (e) class-wise necessity)
- E.7 unanchored consistency -> `@thm-unanchored-paic-consistency`
- E.8 shared effect modifier assumption (SEMA) -> `@def-sema`
- E.9 identifiability under SEMA in small networks -> `@thm-shared-em-identifiability`
- E.10 scale dependence of effect modifier status -> `@exm-scale-dependence-em`
- E.11 testable vs untestable constancy -> `@prp-testable-untestable-constancy`
- E.12 target-population estimands via the g-formula -> `@thm-target-population-estimand`

## Sources consulted

- `proofs/E_population_adjustment_theory.md` (E.0 to E.12), the base draft. Every sketch expanded into a
  complete proof in the book's notation.
- `manuscript/06_population_adj.md` (chapter 6), used for narrative framing and the scale-aware view.
- `theories/EffectModifiers.v` read in full to confirm exact Coq lemma names for machine-checked tags.
- Voice matched to `chapters/part3/14-bucher.qmd`.
- Sibling chapters read for exact statements I build on: Ch11 (`11-effect-modification-collapsibility.qmd`),
  Ch12 (`12-transportability.qmd`), Ch16 (`16-limits-of-nma.qmd`).
- Citations used (all keys present in `references.bib`): `@phillippo2019thesis`, `@phillippo2016tsd18`,
  `@chandler2026transport`, `@dias2018nma`, `@signorovitch2010maic`, `@caro2010stc`, `@phillippo2020mlnmr`,
  `@rosenbaum1983`.

## Slugs defined in this chapter

Owned (assigned): `def-conditional-constancy-relative`, `def-conditional-constancy-absolute`,
`thm-anchored-paic-consistency`, `thm-unanchored-paic-consistency`, `def-sema`,
`thm-shared-em-identifiability`, `exm-scale-dependence-em`, `prp-testable-untestable-constancy`,
`thm-target-population-estimand`.

Supporting (namespaced `pat-` to avoid collision): `def-pat-data-structures`, `def-pat-setups`,
`def-pat-imbalance`, `prp-pat-conditional-transport`, `prp-pat-absolute-implies-relative`,
`lem-pat-pv-cancellation`, `lem-pat-em-not-pv`, `lem-pat-conditional-additivity`, `cor-pat-anchored-algebra`,
`prp-pat-sema-constant`, `exm-pat-anchored`, and exercises `exr-pat-additivity`, `exr-pat-bias-recompute`,
`exr-pat-pv-cancellation`, `exr-pat-sema-identify`, `exr-pat-scale-status`, `exr-pat-unanchored-bias` (star),
`exr-pat-noncollapsible-target` (star). Equation labels namespaced `eq-pat-*`. Section labels `sec-pat-*`.

Two exercises starred for Appendix F: `exr-pat-unanchored-bias` (the unanchored bias formula and its
specialization, showing the anchored term is multiplied by zero) and `exr-pat-noncollapsible-target`
(non-collapsibility makes a fully adjusted anchored odds ratio population-specific).

## Machine-checked tags added (all confirmed by reading `theories/EffectModifiers.v`)

- `@lem-pat-pv-cancellation` -> `theories/EffectModifiers.v`, `Theorem anchored_PV_cancellation`
  (anchored cancellation of a purely prognostic covariate; not_EM implies the contrast is independent of w).
- `@lem-pat-em-not-pv` -> `theories/EffectModifiers.v`, `Theorem not_EM_does_not_imply_not_PV`
  (prognostic is strictly stronger than effect modifier; the same witness shows absolute constancy is
  strictly stronger than relative constancy).
- `@cor-pat-anchored-algebra` -> `theories/EffectModifiers.v`, `Theorem anchored_unbiased`
  (the adjusted Bucher identity: adjusted d_AC minus d_BC equals d_AB under identification plus transitivity).

The Coq file does NOT formalize E.6a to E.6e or E.7 (it says so explicitly); I tagged only the three
algebraic cores it does prove, and stated this clearly in the Notes section.

## Cross-references relied on (all verified present in sibling chapters)

Ch5 `@thm-mle-asymptotic-normality`; Ch7 `@def-link-function`, `@def-non-collapsibility`; Ch9
`@def-sutva`, `@thm-consistency-identity`, `@def-ignorability`, `@def-positivity`; Ch10
`@thm-g-computation-unbiased`, `@def-balancing-score`; Ch11 `@def-effect-modifier`,
`@def-prognostic-variable`, `@def-collapsibility`, `@def-marginal-effect`, `@def-conditional-effect`,
`@thm-noncollapsibility-or-hr`, `@prp-emcoll-rd-direct`, `@lem-emcoll-interaction`, `@eq-emcoll-cate`;
Ch12 `@def-transportability`, `@thm-conditional-transportability`, `@thm-collapsible-transport`,
`@thm-sema-insufficient`, `@def-scale-alignment`, `@eq-transport-gformula`; Ch14 `@def-transitivity`,
`@thm-bucher-unbiased`, `@def-constancy-relative-effects`, `@prp-baseline-cancellation`,
`@lem-relative-effect-algebra`; Ch15 `@thm-fe-nma-identifiability`, `@def-node-splitting`; Ch16
`@thm-failure-of-bucher`, `@eq-limits-bias`.

A single-file `quarto render` (v1.8.26) of the chapter succeeds with exit 0; all internal references
resolve and all cross-chapter references resolve to the correct book-level hrefs, and the three cited
bib keys render. Rendered artifacts were removed afterward.

## Mathematical decisions and a sharpening of the catalogue

1. Index convention. Followed Chapter 14 exactly: `d_{AC} = eta_C - eta_A` (comparator second), so the
   conditional contrast is `tau^g_{AC}(x) = g(mu_C(x)) - g(mu_A(x))`, matching Ch11 `@eq-emcoll-cate` and
   Ch16 `@thm-failure-of-bucher`. Pointwise additivity `tau^g_{AB} = tau^g_{AC} - tau^g_{BC}` then mirrors
   Bucher's `d_{AB} = d_{AC} - d_{BC}`.

2. Scale handling. Used `g` for the model link / effect-modification scale and `h` for the reporting
   (effect-measure) scale, with alignment `h = g` referenced as Ch12 `@def-scale-alignment`. This matches
   Ch11/Ch12 usage.

3. Sharpening E.6b. The catalogue's E.6b claims consistency for the MARGINAL log risk ratio under
   conditions (i) to (v) without naming SEMA. That is only rigorous when the conditional A-vs-B contrast is
   constant (no A-vs-B effect modification, e.g. under SEMA), because the log RR is collapsible but not
   directly collapsible. I therefore proved the anchored theorem in two explicit layers: (a) conditional
   recovery on any scale (the robust core), and (b) marginal recovery only when the measure is directly
   collapsible (identity) OR collapsible with a constant conditional contrast (log RR under SEMA), citing
   `@thm-collapsible-transport` and `@thm-sema-insufficient`. This is more precise than the catalogue and
   is in harmony with Ch12; flagged here for the harmony pass.

## Proposed additions for the orchestrator (no files edited besides my chapter and this log)

- Notation: `notation.qmd` lists the link `g` but not the effect-measure / reporting scale `h`, which is
  already used in Ch11 and Ch12 and is used here. Suggest adding a row: `h, h\circ g^{-1}` = reporting
  (effect-measure) scale and the scale-alignment composition. Also consider adding `m_t(\mathcal P) =
  \int \mu_t(x) f_{\mathcal P}(x)\,dx` (marginal mean), used in Ch12 and here; currently only Ch14's
  `\bar\mu_{t(\mathcal P)}` form is in notation implicitly. No bibliography additions needed (all keys
  present).

## Minor inconsistency noticed in siblings (for the harmony pass, not fixed by me)

The book overwhelmingly uses American "cancellation"/"cancel" (83 instances) but a few sibling chapters
contain 5 "cancelling" and 1 "cancelled" (British). I used American "canceling" in this chapter per the
authoring contract. The harmony pass may wish to normalize the sibling instances.

## Gaps / deferred

- E.6d (log hazard ratio) and E.6e (RMST) are stated within `@thm-anchored-paic-consistency` parts (c)
  and (d) at the level of the obstruction (non-collapsibility of the HR; nonlinearity of the RMST
  functional of the hazard). The full survival-specific machinery (time-varying marginal HR, RMST
  integral identification) is correctly deferred to the later chapters on general likelihoods and ML-UMR,
  as the catalogue's dependency table indicates (J.4, M.6).
