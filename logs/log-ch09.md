# Work log: Chapter 09, Potential Outcomes and Identification

File written: `chapters/part2/09-potential-outcomes.qmd` (overwrote the stub; ~5,760 words).

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (notation single source of truth).
- Proof catalogue: `ITC_Coq/proofs/B_causal_foundations.md`, items B.1 to B.5 (the assigned, owned
  range). B.6 to B.13 read for context but belong to Ch10 (B.6 to B.12) and Ch07/Ch11 (B.13); not
  reproduced here, only forward-referenced.
- Companion manuscript: `ITC_Coq/manuscript/02_causal.md`, sections 2.1 to 2.5 (expanded into full
  proofs; the worked example and the explicit selection-bias corollary are new).
- Coq theories, read in full to confirm exact object names for machine-checked tags:
  `ITC_Coq/theories/PotentialOutcomes.v` and `ITC_Coq/theories/CausalAssumptions.v`.
- Part I sibling chapters for cross-reference slugs and house style: `chapters/part1/04-probability.qmd`
  (tower property, total expectation, conditional independence, graphoid axioms),
  `chapters/part1/07-glm.qmd` (non-collapsibility), `chapters/part1/08-hierarchical-bayes.qmd`
  (Notes/Exercises format).

## Catalogue identifiers covered (owned)

- B.1 potential outcomes and SUTVA -> `@def-potential-outcome`, `@def-individual-effect`, `@def-sutva`.
- B.2 consistency identity -> `@thm-consistency-identity` (plus `@cor-consistency-swap`).
- B.3 ignorability (strong/weak/mean) -> `@def-ignorability`, `@lem-ignorability-hierarchy`.
- B.4 positivity/overlap -> `@def-positivity`.
- B.5 identification of the ATE (adjustment / g-formula) -> `@lem-mean-potential-identification`,
  `@thm-ate-identification`.
- Fundamental problem (from `PotentialOutcomes.v`) -> `@thm-fundamental-problem`.
- Estimands and decompositions -> `@def-ate`, `@def-att`, `@def-cate`, `@prp-ate-att-atc`.
- Naive contrast = ATT + selection bias (from `PotentialOutcomes.v`) -> `@thm-naive-selection-bias`,
  `@cor-naive-unbiased-rct`.

## Slugs defined

Owned (per slug map + prompt): `def-potential-outcome`, `def-sutva`, `thm-consistency-identity`,
`def-ignorability`, `def-positivity`, `thm-ate-identification`, `def-ate`, `def-att`.

New, namespaced to this chapter (globally unique, checked against the wave-2 map for collisions; none):
`def-individual-effect`, `def-cate`, `thm-fundamental-problem`, `cor-consistency-swap`,
`lem-ignorability-hierarchy`, `prp-ate-att-atc`, `lem-mean-potential-identification`,
`thm-naive-selection-bias`, `cor-naive-unbiased-rct`, `exm-confounding-gformula`.

Exercises: `exr-po-recompute`, `exr-po-masked-identity`, `exr-po-att-atc`, `exr-po-mean-vs-weak`,
`exr-po-positivity-failure` (starred), `exr-po-selection-bias-proof` (starred). Two starred exercises
have solutions promised in Appendix F.

Equation labels: `eq-consistency-identity`, `eq-consistency-masked`, `eq-consistency-swap`, `eq-ate`,
`eq-att`, `eq-cate`, `eq-ate-is-mean-cate`, `eq-ate-decomp`, `eq-positivity`, `eq-strict-positivity`,
`eq-gformula`, `eq-ate-identification`, `eq-naive-decomposition`.

Section anchors: `sec-po-rubin`, `sec-po-sutva`, `sec-po-estimands`, `sec-po-assumptions`,
`sec-po-identification`, `sec-po-selection`, `sec-po-example`, `sec-po-bridge`, `sec-po-notes`,
`sec-po-exercises`.

## Machine-checked tags added (all confirmed by reading the .v files)

From `theories/PotentialOutcomes.v`:
- `@def-potential-outcome`: `Record potential_outcomes`, `Definition potential_outcome`.
- `@thm-fundamental-problem`: `Lemma ITE_unobservable`.
- `@thm-consistency-identity`: `Definition consistency`, `Lemma consistency_equiv`,
  `Lemma consistency_expectation`.
- `@cor-consistency-swap`: `Lemma consistency_treated_mean`, `Lemma consistency_control_mean`.
- `@def-ate`: `Definition ATE`, `Lemma ATE_split`.
- `@def-att`: `Definition ATT`, `Definition ATC`.
- `@prp-ate-att-atc`: `Lemma ATE_decomposition`.
- `@thm-naive-selection-bias`: `Lemma selection_bias_decomposition`.

From `theories/CausalAssumptions.v`:
- `@def-sutva`: `Definition SUTVA`, `Lemma no_interference_unit_level`.
- `@def-ignorability`: `Definition strong_unconfoundedness`, `Definition weak_unconfoundedness`,
  `Lemma strong_implies_weak_unconf`.
- `@def-positivity`: `Definition weak_positivity`, `Definition strong_positivity`,
  `Lemma strong_implies_weak`.
- `@thm-ate-identification`: `Theorem ATE_identification`.

Note for the consistency pass: the Coq files state probabilistic facts (tower property, locality of
conditional expectation, the conditional-independence consequence) as named hypotheses over abstract
expectation operators; the pen-and-paper proofs here supply those facts from Chapter 4
(`@thm-tower-property`, `@cor-total-expectation`, `@thm-graphoid-axioms`, `@def-conditional-independence`).
The tags mark the algebraic/identification skeleton that is verified, not the measure theory.

## Cross-references out of this chapter

- Part I (confirmed to exist): `@thm-tower-property`, `@cor-total-expectation`, `@thm-graphoid-axioms`,
  `@def-conditional-independence`, `@def-non-collapsibility`, `@exm-noncollapsible-or`.
- Wave-2 siblings (from the slug map, expected to resolve once the wave renders together): Ch10
  `@def-balancing-score`, `@thm-rosenbaum-rubin`, `@thm-ps-sufficiency`, `@thm-ipw-unbiased`,
  `@thm-g-computation-unbiased`, `@thm-aipw-double-robust`, `@thm-eif-bound`; Ch11 `@def-collapsibility`;
  Ch12 `@def-transportability`; Ch16 `@def-ecological-bias`.
- The MAIC overlap limitation (catalogue F.10) is referenced descriptively as "Part IV" rather than by
  slug, since no Ch18 slug was provided in this wave's map. If Ch18 later exports a slug for the overlap
  failure theorem, this paragraph in `sec-po-bridge` should be updated to cite it.

## Proposed bibliography additions (for the orchestrator to merge)

`references.bib` currently has `@hernan2020whatif` and `@rosenbaum1983`, both cited. The following
foundational sources are attributed in prose and the Notes section but are not yet in `references.bib`;
full entries proposed:

- `neyman1923` : Neyman, J. (1923). "On the application of probability theory to agricultural
  experiments. Essay on principles. Section 9." Translated and reprinted (Dabrowska & Speed, trans.)
  in *Statistical Science* 5(4):465-472, 1990.
- `rubin1974` : Rubin, D. B. (1974). "Estimating causal effects of treatments in randomized and
  nonrandomized studies." *Journal of Educational Psychology* 66(5):688-701.
- `holland1986` : Holland, P. W. (1986). "Statistics and causal inference." *Journal of the American
  Statistical Association* 81(396):945-960.
- `robins1986` : Robins, J. M. (1986). "A new approach to causal inference in mortality studies with a
  sustained exposure period; application to control of the healthy worker survivor effect."
  *Mathematical Modelling* 7(9-12):1393-1512.

These are referenced lightly (single attributions). If the orchestrator prefers to keep the bibliography
lean, the prose already routes the main citation through `@hernan2020whatif`, which covers all four
historically; the chapter renders without the four keys above, in which case the proper-noun attributions
in `sec-po-notes` should drop the implied keys. No code change to the chapter is required either way.

## Proposed notation additions

None required. The chapter uses only symbols already in `notation.qmd`: `Y(0), Y(1), T, X, e(x),
mu_t(x), tau(x), tau`, plus standard `E[.|.]`. Two local, self-explanatory symbols are introduced inline
and do not need a global entry: `tau_T` (ATT), `tau_C` (ATC), `Delta_naive` (naive contrast),
`mu_t^obs(x)` for the observable outcome regression `E[Y | T=t, X=x]` (distinguished in text from the
counterfactual `mu_t(x) = E[Y(t)|X=x]`). If the orchestrator wants these standardized across Part II,
suggest adding `tau_{\mathrm{T}}, tau_{\mathrm{C}}` and `mu_t^{\mathrm{obs}}` to the causal-inference
table; Ch10 and Ch11 likely reuse them.

## Worked example

`@exm-confounding-gformula`: a two-stratum binary-covariate population with confounded propensities
e(0)=0.25, e(1)=0.75 and constant identity-scale CATE = 4. Fully hand-verifiable: naive contrast = 9,
selection bias = 5, ATT = 4, standardized ATE = 4, and the decomposition 9 = 4 + 5. Built on the
collapsible identity scale on purpose, to isolate confounding from the non-collapsibility of Ch07/Ch11.
Original to this text.

## Validation performed

- No dash punctuation as connector/parenthetical (grep clean; the only ` - ` hits are minus signs inside
  display math).
- All 34 fenced divs open and close (34 openers, 34 bare `:::` closers).
- Every proof ends in `$\square$` (9/9); every definition/example/remark ends in `$\blacktriangleleft$`.
- Math delimiters balanced: `$$` even (78), `\bigl`/`\bigr` 15/15, `\begin{aligned}`/`\end{aligned}` 3/3,
  both `\underbrace` have subscripts.
- All `@sec-` references resolve to locally-defined anchors; all `@thm-/@lem-/@def-/...` references are
  either self-defined, confirmed Part I slugs, or wave-2 map slugs.

## Gaps left for review

1. The four historical bib keys above are not yet in `references.bib`; orchestrator to merge or to
   confirm that routing everything through `@hernan2020whatif` is preferred.
2. Wave-2 sibling slugs (Ch10, Ch11, Ch12, Ch16) are referenced on faith from the slug map; the harmony
   pass should confirm those chapters define them with the exact spellings used here.
3. The Part IV (MAIC overlap, F.10) reference is descriptive, not a slug; upgrade to a slug if Ch18
   exports one.
4. Did not run `quarto render` (single-file render needs the whole project); structural validation only.
