# Work log: Chapter 16, The Limits of Standard Network Meta-Analysis

Author pass by the Ch16 agent. File written: `chapters/part3/16-limits-of-nma.qmd`
(stub removed, YAML title preserved).

## Sources consulted

- `~/Documents/GitHub/ITC_Coq/proofs/E_population_adjustment_theory.md`, especially E.3
  (failure-of-Bucher, scale-aware) and the surrounding E.0 to E.4 framing of marginal vs
  average-conditional estimands. The catalogue's one-line proof of E.3 was expanded into the full
  statement (`thm-failure-of-bucher`) with the vanishing and genuineness clauses and an explicit
  derivation from `@thm-bucher-unbiased`.
- `~/Documents/GitHub/ITC_Coq/manuscript/06_population_adj.md` (companion prose, Chapter 6 intro and
  Section 6.5). Used for the narrative framing of the two estimand scales and the bias decomposition.
- `~/Documents/GitHub/ITC_Coq/theories/EffectModifiers.v`: read in full. Confirmed
  `Theorem anchored_PV_cancellation` (line 158) and `Theorem not_EM_does_not_imply_not_PV` (line 279).
  Only `anchored_PV_cancellation` is tagged here (on `cor-limits-pv-no-bias`), because it is the exact
  algebraic fact (the anchored contrast is invariant to a purely prognostic component) that the corollary
  rests on. The file's header comment explicitly states it does NOT formalize the scale-specific PAIC
  bias theorems, so `thm-failure-of-bucher` and `thm-ecological-norecovery` carry no machine-checked tag.
- Sibling chapters read for exact slugs, statements, and voice: `chapters/part3/14-bucher.qmd` (Bucher
  unbiasedness, variance, transitivity, constancy, the failure preview in `sec-bucher-failure`),
  `chapters/part2/11-effect-modification-collapsibility.qmd` (effect modifier, prognostic variable,
  collapsibility and direct collapsibility, scale dependence, non-collapsibility of OR/HR, EM=interaction
  lemma), `chapters/part1/07-glm.qmd` (`def-non-collapsibility`, `def-link-function`),
  `chapters/part1/04-probability.qmd` (Jensen, Cauchy-Schwarz, MGF sum and uniqueness).
- `notation.qmd` and `logs/STYLE.md` for the authoring contract.
- Citations used (all keys present in `references.bib`): `@phillippo2020mlnmr` (ecological/aggregation bias,
  ML-NMR integration), `@phillippo2016tsd18` (NICE TSD 18, justification of constancy and scale),
  `@phillippo2019thesis` (modern EM/PV formulation), `@chandler2026transport` (estimand-based marginal vs
  average-conditional distinction, direct collapsibility), `@bucher1997` and `@dias2018nma` implicitly via
  the Ch14 cross-references.

## Catalogue coverage

- E.3 (failure-of-Bucher, scale-aware): owned and fully proved as `thm-failure-of-bucher`, with the exact
  bias decomposition `@eq-limits-bias`, the iff vanishing characterization, and the genuineness clause.
- Ecological bias: new material (not a numbered E item). Defined precisely as `def-ecological-bias`;
  supported by the Jensen-gap lemma `lem-limits-aggregation-jensen`, the Gaussian probit integral
  `lem-limits-probit-integral`, and the non-recovery theorem `thm-ecological-norecovery` (closed-form
  probit shrinkage). Tied explicitly to `@def-non-collapsibility` (both are the same Jensen gap for the
  inverse link).

## Slugs defined (owned)

- `thm-failure-of-bucher` (catalogue E.3).
- `def-ecological-bias` (new).

## Helper slugs introduced (new, globally unique; flagged for the orchestrator)

Definitions/results: `def-conditional-marginal-contrast`, `prp-limits-collapse-link`,
`lem-limits-conditional-additivity`, `lem-limits-em-breaks-transitivity`, `cor-limits-pv-no-bias`,
`lem-limits-aggregation-jensen`, `lem-limits-probit-integral`, `thm-ecological-norecovery`.
Worked examples: `exm-limits-bucher-rd`, `exm-limits-probit-eco`.
Exercises: `exr-limits-recompute-bias`, `exr-limits-zero-bias-trap`, `exr-limits-logit-compound`,
`exr-limits-jensen-sign`, `exr-limits-probit-recompute`, `exr-limits-pv-cancellation` (starred,
Appendix F), `exr-limits-general-attenuation` (starred, Appendix F).
Equation labels: `eq-limits-marg`, `eq-limits-avgcond`, `eq-limits-cond-additivity`, `eq-limits-target`,
`eq-limits-bias`, `eq-limits-jensen-gap`, `eq-ecological-bias`, `eq-limits-probit-integral`,
`eq-limits-shrinkage`, `eq-limits-b2`.
Section slugs: `sec-limits-intro`, `sec-limits-setup`, `sec-limits-two-constancies`,
`sec-limits-failure-bucher`, `sec-limits-ecological`, `sec-limits-example`, `sec-limits-gap`,
`sec-limits-notes`, `sec-limits-exercises`.

## Cross-references to siblings (all verified to exist or owned this wave)

- Ch4: `@thm-jensen`, `@thm-cauchy-schwarz-exp`, `@thm-mgf-sum`, `@thm-mgf-uniqueness`.
- Ch7: `@def-link-function`, `@def-non-collapsibility`.
- Ch11: `@def-effect-modifier`, `@def-prognostic-variable`, `@def-collapsibility`, `@eq-emcoll-direct`,
  `@lem-emcoll-interaction`, `@prp-emcoll-rd-direct`, `@thm-noncollapsibility-or-hr`,
  `@thm-emcoll-em-pv-distinct`.
- Ch14: `@thm-bucher-unbiased`, `@thm-bucher-variance`, `@def-transitivity`,
  `@def-constancy-relative-effects`, `@lem-relative-effect-algebra`, `@prp-trial-unbiased`,
  `@eq-bucher-reldef`, `@sec-bucher-failure`.
- Ch15 (this wave): `@def-node-splitting`, `@thm-consistency-closure` (will resolve once Ch15 is authored;
  both are in the slug map and already forward-referenced from Ch14).

## New notation proposed (NOT added to notation.qmd; for the orchestrator to fold in)

- `$\tilde d_{ab(\mathcal P)}$`: average-conditional relative effect (the covariate average of the
  conditional contrast $\tau^g_{ab}$), to sit beside the existing marginal $d_{ab(\mathcal P)}$. Consistent
  with the bold/tilde scheme; used throughout Parts IV and V.
- `$\Delta^{\mathrm{Cond},g}_{ab}(\mathcal P)$`: population-average conditional contrast on scale $g$
  (catalogue E.0/E.12 estimand). Recommend adding to the population-adjustment block of notation.qmd
  alongside `$\Delta^{\mathrm{Marg},g}$`, which later chapters (17 onward) will also need.
- `$\mathrm{EB}_t(f)$`: ecological (aggregation) bias of arm $t$; local to this chapter and Ch20.
- `$b_2$` versus `$\beta_2$`: ecological vs individual effect-modification coefficient; local.
- `$\rho_t$`: arm-specific slope of the linear predictor; local to the probit example.
- `$h(\rho)=\rho/\sqrt{1+\rho^2\sigma^2}$`: probit shrinkage function; local to the proof of
  `thm-ecological-norecovery`.

No conflicting symbols introduced. $\alpha,\beta_1,\gamma,\beta_2$ follow the Ch11 model `@eq-emcoll-model`;
$\Phi,\phi,g,g^{-1},\mu_t,f_{\mathcal P},\bar{\mathbf x}$ are from notation.qmd.

## Decisions and ordering

- The failure-of-Bucher theorem is stated for the population-average conditional estimand
  $\Delta^{\mathrm{Cond},g}$, where `@eq-limits-bias` is exact on any scale (pure linearity), and the
  marginal-trial-report subtlety is handled by `prp-limits-collapse-link` plus a remark. This matches the
  catalogue E.3 phrasing and keeps the first worked example (risk-difference scale) exact and
  hand-checkable. The non-collapsible compounding is set as `exr-limits-logit-compound`.
- Conditional constancy of relative effects (catalogue E.4) is owned by Ch17, so it is stated inline as a
  named hypothesis inside the theorem rather than via a `@def-` cross-reference; a forward pointer to
  Chapter 17 is given. No Ch17 slug was invented.
- The probit-normal closed form was chosen for the ecological non-recovery theorem because it yields the
  exact shrinkage `@eq-limits-b2`, an honest closed-form witness that the aggregate slope $b_2$ strictly
  attenuates $\beta_2$ and that the attenuation depends on the within-trial variance $\sigma^2$ (the
  information aggregate data lack). The logit link has no equally clean closed form; it is left to
  Chapter 20's numerical-integration machinery.
- Two starred exercises for Appendix F: `exr-limits-pv-cancellation` (anchored cancellation depends only
  on the EM marginal; where it breaks for unanchored) and `exr-limits-general-attenuation` (second-order
  Taylor attenuation for a general link, recovering the probit leading term).

## Gaps left for review

1. `@def-node-splitting` and `@thm-consistency-closure` resolve only once Ch15 (same wave) is authored;
   slugs taken from the cross-chapter map, already forward-referenced from Ch14. Expected, not an error.
2. The machine-checked tag on `cor-limits-pv-no-bias` points to `anchored_PV_cancellation`, the core
   contrast-invariance fact; the corollary's integration step (bias depends only on the EM marginal) is
   not itself in Coq. Tag scope is explained in the corollary proof and the Notes section. A reviewer may
   prefer to move the tag to a bare restatement of the cancellation lemma; flagged for the harmony pass.
3. New notation `$\tilde d$` and `$\Delta^{\mathrm{Cond},g}$` should be folded into notation.qmd by the
   orchestrator so Chapters 17 to 26 inherit them; used here without modifying notation.qmd per file
   discipline.

## Self-checks run

- Div fences balanced (32 openers, 32 bare closers; 64 `:::` lines total). 8 `.proof` blocks, 8
  `$\square$` endings. 9 `$\blacktriangleleft$` closers (2 definitions, 2 examples, 5 remarks).
- No dash punctuation as connector or parenthetical anywhere (only YAML `---`, the markdown table rule,
  and math-mode minus signs). American spelling throughout.
- Every `@`-citation resolves to a key in `references.bib`; every cross-reference slug resolves to an
  owned slug, a verified sibling slug, or a same-wave Ch15 slug.
- All locally referenced equation labels are defined in-file; the only non-local equation references are
  `@eq-bucher-reldef` (Ch14) and `@eq-emcoll-direct` (Ch11), both verified.
- Both worked examples recomputed by hand: the risk-difference Bucher bias ($-0.06$, sign-reversing,
  verified through `@eq-limits-bias`) and the probit ecological attenuation ($b_2=0.18903$ vs
  $\beta_2=0.6$, both trial contrasts and the Jensen gap checked).
