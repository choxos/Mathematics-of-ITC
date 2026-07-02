# Revision log: Chapter 25 — General Likelihoods (Survival and Ordered Categorical)

File: `chapters/part5/25-general-likelihoods.qmd`. Catalogue J.1 to J.8.
Before: 1080 lines. After: 1497 lines (+417).

Revised to address both reviewers (`feedback/chatgpt/ch25-general-likelihoods.md` and
`feedback/glm/ch25-general-likelihoods.md`), prioritizing their highest-priority fixes, under the
Section 10 accessibility contract and the Section 11 PDF-build rules. No existing `#thm-/#lem-/#def-/#eq-/
#prp-/#sec-` label removed or renamed; every existing theorem and full proof preserved (only expanded with
clarifying prose). American English, no dash punctuation, ASCII-only math verified programmatically.

## Running example introduced (single highest-value addition)

A **running two-arm myeloma progression-free-survival trial** (`#exm-genlik-running`), introduced right
after the intro in a new section `#sec-genlik-core-idea`: one binary high-risk covariate $X$ with
$P(X=1)=1/2$, exponential control hazards $\lambda_0=1,\lambda_1=3$/year, treatment $A$ with constant
conditional hazard ratio $\psi=1/2$. These are exactly the numbers of the end-of-chapter worked example
`#exm-genlik-survival`, so the early box now sets up the trial and the late example completes it. The trial
is reused at each transition: survival/hazard definitions, the $S=e^{-H}$ identity, a pulled-forward
numeric marginal-hazard snapshot at $s=0.5$, a risk-set-drift table, the two-population RMST contrast, the
event/censoring pseudo-patients, and the aggregate likelihood. A parallel ECOG three-band ordinal running
example (`#exm-genlik-ordinal`) mirrors it on the categorical side.

## ChatGPT highest-priority fixes (all addressed)

1. Plain-language conditional-vs-marginal hazard-ratio bridge added as a `.remark` before
   `#lem-survivor-weighted-hazard` (adjusted vs unadjusted Cox, survivor selection).
2. AgD-to-pseudo-IPD bridge paragraph added at the head of `#sec-genlik-aggregation`, with the explicit
   split that even after event *times* are reconstructed the *covariates* stay unobserved (so the $f_j$
   integral remains). Plus a one-paragraph Guyot-style reconstruction sketch after
   `#thm-aggregate-marginal-likelihood`.
3. Ordinal section expanded: clinical anchor (ECOG/PASI), a full `def`-level reader translation of the
   $\alpha_k-\eta$ sign convention (larger $\eta$ = worse category), and a new in-text worked example
   `#exm-genlik-ordinal` ($K=3$, binary covariate, conditional and marginal category probabilities,
   proportional-odds check).
4. RMST warning made concrete: new two-population `.remark` (contrast $0.350$ vs $0.375$ years at
   $q=1/2$ vs $q^*=1/4$) plus a three-row decision table (log-hazard effects transport; marginal HR does
   not; RMST is a population-specific read-out).
5. Step 5 exponent bug fixed: `e^{-3\lambda_1/2}` was wrong; corrected to `e^{-\lambda_1/2}` (the
   observed time is $t_1=1/2$), with an inline note explaining the reparameterization
   ($e^{-\lambda_x t_1}=e^{-\lambda_x/2}$, $e^{-\lambda_x t_2}=e^{-2\lambda_x}$).

Other ChatGPT points addressed: 4-step conceptual recipe box; survival glossary table; "mechanism in
words" now appears before the theorem (drift remark) as well as after; risk-set-drift table as the verbal
substitute for a figure; hazard-is-a-rate numeric ("$0.2$/year is not $20\%$"); baseline-hazard analogy to
study intercepts (`.remark` after the PH model); independent-censoring health examples (administrative /
loss-to-follow-up / informative dropout); object-map glossary table for
$\pi_{\mathrm{Ind}},\theta,\theta_{jk},\xi,\eta_{jk},f_j$; mixed-likelihood clarification (one family per
network vs a joint model sharing the linear-predictor effects); exercise labels and hints.

## GLM reviewer suggestions (all ten addressed)

1. Plain-English roadmap paragraph before `#def-survival-function`.
2. `#thm-survival-hazard-relation` forward proof expanded: inline reminders of absolute continuity,
   Lipschitz composition, and the explicit $S'=-F_T'=-f$ derivative.
3. Verbal/tabular substitute for the survivor-selection figure (risk-set-drift table at $s=0,0.5,2$).
4. Exponential-family score-variance identity named and cross-referenced (Chapter 5) in the tilt proof.
5. In-text ordinal example (`#exm-genlik-ordinal`).
6. Mini-version of the worked example pulled forward: numeric $h_C^{\mathcal P}(0.5)=1.538$ snapshot right
   after `#lem-survivor-weighted-hazard`.
7. `#thm-general-likelihood-mlnmr` Part 3 overgeneralization softened: affine-in-$\theta$ tied explicitly
   to Bernoulli/identity-link, with Poisson/survival/ordinal flagged as retaining the full integral.
8. Pseudo-IPD reconstruction paragraph (digitize KM, recover $(t_i,\delta_i)$ from numbers at risk).
9. "Frailty," "exponential tilt," "natural parameter" defined inline; `expit` reminded in the ordinal
   section; the survivor covariate density is now named in the lemma statement.
10. Outcome-family reduction table `#tbl-genlik-reduction` (reduces to mean aggregation? yes/no).

Plus GLM's smaller asks: why-log-hazard motivation (Cox as HTA lingua franca); conditional-loghr payoff
("one transportable number per comparison"); marginal-HR practical-consequence lead-in; ordinal clinical
anchor; general-theorem structural-advantage framing; simple computational picture before the cost remark.

## New labeled environments and tables added

- Section `#sec-genlik-core-idea`.
- Examples `#exm-genlik-running`, `#exm-genlik-ordinal`.
- Exercises `#exr-genlik-hazard-not-probability` (warm-up), `#exr-genlik-cond-vs-marg-interpretation`
  (interpretation).
- Captioned/labeled table `#tbl-genlik-reduction`.
- Four unlabeled plain tables: survival glossary, risk-set-drift, object-map glossary, RMST decision rule.
- Exercises section now opens with the `$\star$` = Appendix-F-solution convention; two warm-up/
  interpretation exercises precede the proof-heavy ones; existing exercises tagged
  (Computation/Proof/Challenge) and the two starred exercises given hints. Exercise slugs unchanged.

## Counts

Intuition additions (reader translations / plain-language after definitions and lemmas): ~11.
"Why this matters" additions: ~8.

## Labels I was tempted by but preserved

Preserved every existing label unchanged, including `#eq-genlik-S-exp-H` (mixed-case; still declared once,
referenced 4x) and all six exercise slugs. Did not rename `#thm-general-likelihood-mlnmr` Part 3 despite
the overgeneralization; instead added a clarifying sentence and the reduction table. Kept the end-of-chapter
`#exm-genlik-survival` as the full payoff rather than relocating it, and linked it bidirectionally with the
new early `#exm-genlik-running`.

## Deliberately not done

No raster/vector figures were generated (cannot produce images here); both reviewers explicitly accepted a
verbal or tabular substitute, delivered as the risk-set-drift table and the $s=0.5$ numeric snapshot. No
new `@bibkey` citations introduced (none needed; `@phillippo2016tsd` does not appear in this chapter, so no
`...18` fix was required). Klein-Moeschberger and Guyot-et-al remain proposed bib entries flagged in the
Notes section, unchanged from the prior draft.

## Build safety verified

Even `$$` count (98); no bare `align`/`equation`/`gather` inside `$$`; `aligned`/`cases` used where needed;
no `\not` on extensible arrows; ASCII-only in math; no em/en dash, double hyphen, or spaced-hyphen
connector; inline `$` parity even; new tables have consistent column counts; every `#sec-` id unique
across the chapter; no duplicate labels; no dangling local cross-references.
