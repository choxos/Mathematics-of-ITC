# Work log: Chapter 15, Network Meta-Analysis: Models and Identifiability

File written: `chapters/part3/15-network-meta-analysis.qmd` (overwrote the stub; kept the YAML title,
dropped the stub callout). Roughly 6,500 words plus a fully worked numerical example.

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (notation single source of truth).
- Proof catalogue: `ITC_Coq/proofs/D_network_meta_analysis.md`, items D.5 to D.14 (the assigned, owned
  range). D.1 to D.4 read for context but belong to Ch14; referenced, not reproduced. The catalogue's
  D.7 carries a self-correction (the BS/RT spaces are not square-equal in general; equivalence holds on
  the consistency-constrained subspace) which I followed and proved in full.
- Companion manuscript: `ITC_Coq/manuscript/05_nma_bucher.md`, sections 5.5 to 5.10 (expanded every
  sketch into a complete proof; the rank toolkit lemmas, the symmetry-forcing characterization of the
  one-half correlation, the population-level IPD-NMR identifiability proof, the p_D trace identity, the
  node-split distribution proof, and the entire worked example are new development, not in the base).
- Coq theories: read `ITC_Coq/theories/Bucher.v` in full; confirmed it formalizes only D.2/D.3 (the
  Bucher algebra, Ch14). Confirmed by directory listing and grep that there is no NMA/identifiability/
  deviance/node-split Coq file. Therefore Ch15 carries NO machine-checked tags (see below).
- Sibling chapters for voice and exact cross-reference slugs: `chapters/part3/14-bucher.qmd` (primary
  voice model; reused `@lem-relative-effect-algebra`, `@sec-bucher-failure`, the Bucher theorems),
  `chapters/part3/13-pairwise-meta-analysis.qmd` (IVW / `@thm-fixed-effect-blue`), and grepped Ch1, Ch3,
  Ch5, Ch6, Ch7, Ch8, Ch11 for the foundational slugs cited.

## Catalogue identifiers covered (owned, D.5 to D.14)

- D.5 baseline-shift parameterization -> `@def-baseline-shift-param`.
- D.6 reference-treatment parameterization -> `@def-reference-treatment-param`.
- D.7 equivalence on the consistency-constrained subspace -> `@thm-parameterization-equivalence`.
- D.8 fixed-effect identifiability via incidence rank -> `@thm-fe-nma-identifiability`
  (engine lemma `@lem-incidence-rank`, rank=K-c, full elementary proof).
- D.9 one-half contrast correlation -> `@thm-re-nma-correlation` (plus `@lem-half-correlation-forced`,
  showing 1/2 is the unique basis-invariant correlation, which is new).
- D.10 consistency closure -> `@thm-consistency-closure` (antisymmetry, additivity, generation,
  converse/uniqueness, and the count of $\binom{K-1}{2}$ independent loop constraints).
- D.11 node-splitting -> `@def-node-splitting` and `@prp-node-split-test` (mean-zero null and variance
  derived from `@thm-bucher-unbiased`/`@thm-bucher-variance`), plus `@prp-network-contrast-pooling`.
- D.12 IPD network meta-regression -> `@thm-ipd-nmr-identifiability` (population-level injectivity proof
  via incidence rank propagation of both contrasts and interactions; full failure-mode discussion).
- D.13 residual deviance -> `@def-residual-deviance` (binomial formula derived from `@def-deviance`).
- D.14 DIC -> `@def-dic` and `@prp-dic-pd` (trace identity for $p_D$, flat-prior $p_D\approx p$).

## Slugs defined

Owned (exactly as required by the prompt/slug map): `def-baseline-shift-param`,
`def-reference-treatment-param`, `thm-parameterization-equivalence`, `thm-fe-nma-identifiability`,
`thm-re-nma-correlation`, `thm-consistency-closure`, `def-node-splitting`, `thm-ipd-nmr-identifiability`,
`def-residual-deviance`, `def-dic`.

New, namespaced `nma-`/topic (globally unique, checked against the slug map for collisions; none):
`def-nma-arm-model`, `lem-incidence-rank`, `lem-nma-gram`, `lem-half-correlation-forced`,
`prp-network-contrast-pooling`, `prp-node-split-test`, `prp-dic-pd`, `exm-nma-triangle`.

Exercises: `exr-nma-design`, `exr-nma-incidence`, `exr-nma-threearm-cov`, `exr-nma-closure-count`,
`exr-nma-dic`, `exr-nma-recompute`, `exr-nma-pooling` (starred), `exr-nma-ipd-collinear` (starred). Two
starred exercises have solutions promised in Appendix F.

Equation labels (all `eq-nma-*`): `totalarms`, `totalcontrasts`, `linpred`, `bs`, `rt`,
`consistency-constraint`, `pairwise`, `triangle`, `loopcount`, `incidence-rank`, `gram-kernel`, `design`,
`gls`, `half`, `re-moments`, `re-cov`, `pooling`, `omega`, `omega-moments`, `ipdnmr`, `ipd-match`,
`ipd-sep`, `deviance-binom`, `dic-parts`, `dic`, `pd-trace`, `quadform`.

Section anchors (all `sec-nma-*`): `intro`, `glm`, `param`, `consistency`, `rank`, `equivalence`,
`identifiability`, `random`, `nodesplit`, `ipd`, `deviance`, `example`, `notes`, `exercises`.

## Machine-checked tags added

None. Confirmed by reading `theories/Bucher.v` and by directory/grep that the Coq development covers only
the Bucher algebra (D.2/D.3, owned by Ch14). All Ch15 results are linear-algebra and likelihood arguments
over the incidence and design matrices and have no Coq counterpart. This is stated explicitly in the
Notes section. If the orchestrator later adds an `Incidence.v`/`NMA.v` to the Coq tree, the natural
candidates for tagging would be `@lem-incidence-rank`, `@thm-consistency-closure`, and
`@thm-re-nma-correlation` (all purely algebraic).

## Cross-references out of this chapter (all confirmed to resolve)

- Ch1: `@thm-rank-nullity`, `@lem-injective-trivial-kernel`.
- Ch3: `@thm-spectral-theorem`, `@thm-pd-characterization`, `@def-definiteness`, `@prp-matrix-square-root`,
  `@lem-trace-cyclic`.
- Ch5: `@thm-mle-asymptotic-normality`, `@thm-delta-method`.
- Ch6: `@thm-ols-blue`.
- Ch7: `@def-link-function`, `@def-glm`, `@def-exponential-family`, `@def-deviance`,
  `@def-saturated-model`, `@prp-deviance-nonneg`, `@thm-deviance-test`, `@def-non-collapsibility`.
- Ch8: `@thm-conjugate-normal`, `@def-random-effects`.
- Ch11: `@def-effect-modifier`, `@def-prognostic-variable`.
- Ch13: `@thm-fixed-effect-blue`, `@thm-dersimonian-laird`, `@def-i-squared`.
- Ch14: `@def-transitivity`, `@def-constancy-relative-effects`, `@thm-bucher-unbiased`,
  `@thm-bucher-variance`, `@lem-relative-effect-algebra`, `@sec-bucher-failure`.
- Ch16 (forward, in this wave's map; verified to resolve, the sibling chapter now defines them):
  `@thm-failure-of-bucher`, `@def-ecological-bias`.

`@def-collapsibility` and `@thm-bayesian-ma-conjugate` were available in the map but not needed; not used.

## Worked example

`@exm-nma-triangle`: a 3-treatment network (reference 1, plus 2, 3) with three two-arm trials closing the
triangle and one three-arm trial (the "extra arm"). $K=3$, $J=4$, $N=9$, $C=5$. Constructed so that all
arithmetic is exact and hand-verifiable: GLS gives $\hat d_2=0.60$, $\hat d_3=0.90$ (SE $0.2327$ each,
covariance $0.020833$), $\hat d_{23}=0.30$ (SE $0.2582$); the multi-arm block is $0.10(I_2+J_2)$ with
correlation exactly $1/2$; the node-split of the 2-vs-3 edge gives direct $0.1$ (var $0.20$) vs indirect
$0.40$ (var $0.10$), $\hat\omega=-0.30$, SE $0.5477$, $z=-0.55$; the inverse-variance blend of direct and
indirect reproduces the full-network $0.30$ to confirm `@prp-network-contrast-pooling`; the
normal-likelihood residual deviance is $0.40$ on $3$ df. The example exercises every owned result.
Original to this text.

## Proposed bibliography additions (for the orchestrator to merge)

Main citations are routed through keys already in `references.bib`: `@dias2018nma` (primary),
`@phillippo2019thesis`, `@phillippo2016tsd18`, `@phillippo2020mlnmr`, `@bucher1997`, `@dersimonian1986`.
The following primary sources are attributed in prose (by author, lightly) but lack bib keys; full entries
proposed in case the orchestrator prefers explicit citation keys over prose attribution:

- `lu2004` : Lu, G. and Ades, A. E. (2004). "Combination of direct and indirect evidence in mixed
  treatment comparisons." *Statistics in Medicine* 23(20):3105-3124. (Multi-arm covariance / the
  one-half correlation; @thm-re-nma-correlation.)
- `dias2010nodesplit` : Dias, S., Welton, N. J., Caldwell, D. M., Ades, A. E. (2010). "Checking
  consistency in mixed treatment comparison meta-analysis." *Statistics in Medicine* 29(7-8):932-944.
  (Node-splitting; @def-node-splitting.)
- `spiegelhalter2002dic` : Spiegelhalter, D. J., Best, N. G., Carlin, B. P., van der Linde, A. (2002).
  "Bayesian measures of model complexity and fit." *JRSS B* 64(4):583-639. (DIC; @def-dic.)

The chapter renders without these keys (prose attribution by author name only). No code change to the
chapter is required either way; if the orchestrator merges them, the proper-noun attributions in
`sec-nma-notes` can be upgraded to bracketed `@key` citations.

## Proposed notation additions

None required. The chapter uses only symbols already in `notation.qmd`: $\theta_{jk}$, $\mu_j$,
$\delta_{j,t_1 t_k}$, $d_{ab}$, $\hat d_{ab(j)}$, $g$, $\boldsymbol\beta_1$, $\boldsymbol\beta_{2,k}$,
$\gamma_k$/$d_k$, $\mathbf X$, $I_n$, $J_n$, $\mathcal C(\cdot)$, $\mathcal N(\cdot)$,
$\operatorname{rank}$, $A\succ0$, plus the standard GLS/inference symbols. Local, self-explanatory
symbols introduced inline (no global entry needed): $\mathbf B$ (signed incidence matrix), $G$ (treatment
graph), $C$ (within-study contrast count), $\mathcal S_{\mathrm{cons}}$ (consistency-constrained
subspace), $\hat\omega_{AB}$ (inconsistency statistic), $p_D$, $\bar D$, $D_{\mathrm{res}}$. If the
orchestrator wishes to standardize $\mathbf B$, $G$, and $C$ across Part III, they could be added to the
"Studies, treatments, and populations" table; Ch16 likely reuses $G$ and $\mathbf B$.

## Validation performed

- Quarto div grammar: 48 openers (`::: {...}`) and 48 bare closers (`:::`), balanced.
- Every proof ends in `$\square$` (11 proof divs / 11 `\square`); every definition, example, and remark
  ends in `$\blacktriangleleft$` (18 / 18).
- Display math `$$` delimiters even (84). Markdown table for the example data well-formed.
- No dash punctuation as connector/parenthetical: grep for em/en dash and `--` returns only the YAML
  `---` fences and the table separator; all ` - ` hits are minus signs inside `$...$`/`$$...$$`.
- American English throughout (no behaviour/colour/standardise/modelling/favourable/centre).
- All 10 owned slugs present and correctly prefixed; all 8 new slugs globally unique.
- 8 exercises, exactly 2 starred for Appendix F.
- All 32 external `@`-references resolve to defining files in `chapters/` (Ch1, Ch3, Ch5, Ch6, Ch7, Ch8,
  Ch11, Ch13, Ch14, and the Ch16 forward refs, which now resolve since the sibling chapter defines them).
- No forbidden `@sec-notation`; notation pointed to via `[Notation](/notation.qmd)`.

## Numerical verification of the worked example (independent hand recomputation)

- $\det\mathbf A=(65^2-25^2)/9=3600/9=400$; $\mathbf A^{-1}=\frac1{1200}\begin{psmallmatrix}65&25\\25&65
  \end{psmallmatrix}$. $\hat{\mathbf d}=\mathbf A^{-1}(5.5,14.5)^\top=(720,1080)^\top/1200=(0.60,0.90)$.
- $\operatorname{Var}(\hat d_{23})=(65+65-50)/1200=80/1200=0.066\overline 6$, SE $=0.2582$.
- Indirect (drop study 3): $\hat{\mathbf d}_{\mathrm{ind}}=(440,760)^\top/800=(0.55,0.95)$,
  $\hat d^{\mathrm{ind}}_{23}=0.40$, var $80/800=0.10$. Blend $(5\cdot0.1+10\cdot0.4)/15=0.30$ = full fit.
- Residual deviance $0.1+0.1+0.2+0=0.40$ on $5-2=3$ df.
All figures reproduce.

## Gaps left for review

1. Three bib keys (`lu2004`, `dias2010nodesplit`, `spiegelhalter2002dic`) proposed above; currently
   prose attribution by author name. Orchestrator to merge or to keep prose-only.
2. No `quarto render` run (single-file render needs the full project build); validation was structural
   and reference-resolution based.
3. The Ch16 forward slugs `@thm-failure-of-bucher` and `@def-ecological-bias` were unresolved at the
   start of this session and resolved by end (sibling Ch16 authored in parallel); the harmony pass should
   confirm the exact spellings match once both chapters are frozen.
4. Possible Part III notation standardization of $\mathbf B$, $G$, $C$ (see "Proposed notation
   additions"); left local for now to avoid editing `notation.qmd`.
