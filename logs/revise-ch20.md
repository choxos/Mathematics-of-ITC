# Revision log: Chapter 20 — ML-NMR I: The Aggregation Principle

File: `chapters/part5/20-mlnmr-aggregation.qmd`
Before: 948 lines. After: 1261 lines (+313). Catalogue H.1 to H.7.

## Running example introduced (single highest-value addition)

A plaque psoriasis network carried through the whole chapter: outcome **PASI 75** (binary, 75% PASI
reduction by week 12); one binary effect modifier **biologic-naive status** ($x=1$ naive, $x=0$
experienced); an **IPD trial** of placebo $A$ vs new IL-17 inhibitor $B$, and an **AgD trial** of placebo
$A$ vs competitor $C$; the estimand is the marginal $B$-vs-$C$ effect an HTA body needs. The story reappears
at every transition: model-term translation table, mini two-point aggregation ($0.60/0.10$ subgroup risks →
true $0.35$ vs naive $0.29$), the $37/100$ AgD likelihood, and the closing worked example (whose parameters
now have clinical dress: naive OR $e^{1.30}=3.67$ vs correct marginal $e^{1.22}=3.39$). All numbers verified
numerically before writing.

## Reviewer points addressed

### ChatGPT highest-priority fixes (all 7)
1. Running health example before the formal model — new `## A running clinical example {#sec-agg-running}`.
2. IPD vs AgD likelihood distinction concrete — new remark "IPD and AgD contributions, side by side"
   (37/100 binomial vs per-patient Bernoulli); plus the running-example asymmetry paragraph.
3. Bridge sentences around aggregation and Jensen theorems — "in words, before the symbols" paragraph
   before `@thm-aggregation`; marginal/conditional gloss before `@thm-aggregation-bias`; "why this matters
   for an indirect comparison" remark after it.
4. Explain $f_j$ as case mix (known vs reconstructed) — new remark "What is known about $f_j$" (Gaussian
   copula, correlation 0.3 aside) + running-example case-mix paragraph.
5. Heat-flow labeled optional — prominent "Optional section" signpost remark at head of `@sec-agg-heat`,
   payoff stated before the PDE. (Did not physically move it; see "preserved" below.)
6. Tiny numeric aggregation example earlier — "A first taste of the gap" remark right after
   `@def-aggregate-model`.
7. Treatment-contrast consequence stated directly — "Why this matters for an indirect comparison" remark
   (biases add, not cancel, across arms in the contrast).

### GLM (beginner) suggestions (all 10)
1. Concrete scenario opening — running-example section.
2. Small numerical example after the theorem — first-taste remark + IPD/AgD 37/100 remark.
3. expit convex/concave "figure" — realized as a **curvature table** (m, risk, sign of expit'', bias
   direction) before the logit theorem (a real figure was avoided for pdflatex safety).
4. Heat-flow labeled optional — done (signpost remark).
5. Glossed jargon: **affine**, **outcome family** ($\pi_{\mathrm{Ind}}$), **tower property** (= law of
   iterated expectations), **Gaussian convolution / heat semigroup**, **Jensen's functional equation**,
   the **bullet subscript** ("dot-mean"), **marginal vs conditional**.
6. SEMA expanded — new remark "Why a shared effect modifier assumption is needed", with the failure mode
   (AgD single summary cannot separate treatment effect from case-mix artifact).
7. Worked-example parameters given clinical meaning — PASI 75, biologic-naive covariate, IL-17 inhibitor B,
   comparator C; HTA odds-ratio reading added.
8. Poisson-binomial promoted from remark to main text — new main-text paragraph after `@def-aggregate-model`.
9. NMA reduction proved inline — new remark "Reduction to standard network meta-analysis (the bridge from
   Chapter 15)" showing $\theta_{\bullet jk}=g^{-1}(\mu_j+\gamma_k)$.
10. Non-collapsibility subsection — new `## Aggregation bias and non-collapsibility {#sec-agg-noncollapse}`
    with the odds-ratio case (marginal 3.39 attenuated from conditional 3.67), tying Ch 7 to logit
    aggregation bias.

### Additional Section-10 requirements
- Response-scale vs link-scale mapping by outcome type — new table (continuous/identity, count/log,
  binary/logit) doubling as the three-links roadmap with trial examples.
- Model-term clinical translation table after `@def-individual-model`.
- Reference-constraint note ($\beta_{2,1}=0$, $\gamma_1=0$ are identifiability conventions, not claims).
- Leading-order lemma given its own subsection `### The leading-order bias {#sec-agg-leading-bias}` with a
  one-sentence takeaway (pacing fix both reviewers raised).
- Exercises: added the `$\star$` = Appendix F convention line and a grading note; added two unstarred
  warm-ups (`exr-agg-same-mean-different-prediction` interpretation; `exr-agg-mini-arithmetic` computation)
  before the proof-heavy set.

## Deliberately not done (with reason)
- Did **not** physically relocate the heat-flow section. Both reviewers offered "move OR label optional";
  moving it after the link sections would create forward references (the log/probit/logit results cite
  `@lem-agg-heat-flow`), which Section 10 forbids. Labeled it clearly optional instead.
- NMA reduction added as a `.remark`, not a new `#thm-`/`#prp-`, to avoid duplicating the result Chapter 23
  formally owns while still giving the Chapter-15 reader the bridge inline.
- Probit substitution non-elementarity discussion kept (reviewers found part (d) heavy) but front-loaded a
  plain "practical bottom line" so the applied message leads.

## Preserved (hard constraints)
- All 20 original labeled environments (`def-`, `thm-`, `lem-`, `prp-`, `exm-`, `exr-`) intact, each once.
- All 14 original `#eq-agg-*` labels intact, each once.
- All 8 proofs preserved verbatim and un-shortened (only surrounding scaffolding/gloss added; two glosses
  added *inside* proofs — Jensen functional-equation explanation, tower-property naming — without altering
  any mathematics).
- `:::` fences balanced 50/50. No dash punctuation; ASCII-only math; `$\star$` marker used.
- Labels I was tempted to change but preserved: `#sec-agg-heat` (tempted to move/rename per reviewers —
  kept in place, only added optional signpost); no existing `#thm-`/`#def-`/`#eq-`/`#exr-` renamed.

## New labeled ids added (all verified unique across `chapters/` + `appendices/`)
`#sec-agg-running`, `#sec-agg-leading-bias`, `#sec-agg-noncollapse`,
`#exr-agg-same-mean-different-prediction`, `#exr-agg-mini-arithmetic`.
New tables (3): clinical model-term translation; response-scale-by-outcome-type; logit curvature/bias-sign.

## Notes for orchestrator
- No new `@bibkey` citations introduced; only existing keys used (`@phillippo2020mlnmr`,
  `@phillippo2019thesis`, `@owen1956`, `@sklar1959`, `@sobol1967`). Chapter does not cite
  `@phillippo2016tsd`, so no `...18` fix was needed.
- Cross-refs to `@def-sema`, `@def-poisson-binomial`, `@def-non-collapsibility`, `@def-link-function` reuse
  labels already referenced by the original chapter; assumed resolvable (owned by Chs 7, 11, 17, 21).
- No machine-checked tag added (chapter has none; consistent with existing Notes section).
