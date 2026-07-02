# Work log: Chapter 7, Generalized Linear Models

Author pass over `chapters/part1/07-glm.qmd`. Full chapter written; stub removed; YAML title kept.

## Sources consulted

- `@mccullagh1989glm`, Chapters 2 and 4: exponential dispersion family, link/canonical link, score
  equations, Fisher scoring, IRLS, deviance, analysis of deviance. Every statement that the monograph
  presents as a calculation is given a full proof here.
- `@dias2018nma`, Chapter 4: GLMs as the outcome models of network meta-analysis; combination of evidence
  on the conditional log-odds and log-rate scales; motivation for the non-collapsibility section.
- Cross-chapter results imported (verified to exist in the sibling `.qmd` files):
  - Ch03 `@thm-pd-characterization` (positive definiteness of `X^T W X`).
  - Ch04 `@def-mgf`, `@thm-mgf-moments` (CGF/MGF proof of mean and variance), `@thm-jensen`
    (non-collapsibility mechanism), `@def-bernoulli`, `@def-binomial`, `@def-poisson`.
  - Ch05 `@thm-mle-asymptotic-normality` (asymptotic normality of the GLM MLE), `@def-fisher-information`,
    `@thm-information-equality`, `@def-score`, `@def-mle`, `@thm-delta-method` (OR/RR standard errors),
    `@thm-wilks` (analysis of deviance).
  - Ch06 `@def-linear-model`, `@thm-ols-normal-equations`, `@def-hat-matrix` (IRLS = weighted least
    squares; normal model as the identity-link special case; deviance = RSS).
- ITC_Coq alignment:
  - `theories/STC.v`, `Lemma STC_collapse_linear`: machine-checked counterpart for the collapsibility of
    the linear (mean-difference) effect; tagged inside `@prp-collapsibility-rd-rr`. Confirmed present and
    is a complete proof from linearity of expectation.
  - `proofs/B_causal_foundations.md` (B.13) supplied the two-stratum non-collapsible-OR numerical example;
    I reproduced and independently re-derived its numbers for `@exm-noncollapsible-or`.

## Slugs defined (globally unique, namespaced by topic)

Owned (all nine present and defined):
`def-exponential-family`, `thm-glm-mean-variance`, `def-link-function`, `def-canonical-link`,
`thm-glm-score`, `thm-irls`, `def-deviance`, `def-non-collapsibility`, `exm-noncollapsible-or`.

Additional slugs introduced this chapter (supporting results, all proved):
`def-glm`, `def-saturated-model`, `prp-canonical-eta-theta`, `cor-canonical-score`, `prp-glm-information`,
`lem-canonical-hessian`, `cor-glm-asymptotic-normality`, `prp-deviance-nonneg`, `thm-deviance-test`,
`prp-collapsibility-rd-rr`, `exm-edf-members`, `exm-deviance-forms`.

Exercise slugs: `exr-glm-edf-gamma`, `exr-glm-canonical-list`, `exr-glm-poisson-score`,
`exr-glm-irls-probit` (starred), `exr-glm-deviance-poisson`, `exr-glm-deviance-rss`,
`exr-glm-offset-rate`, `exr-glm-noncollapse` (starred), `exr-glm-wald-or`, `exr-glm-cloglog`.
Starred exercises (solutions belong in Appendix F): `exr-glm-irls-probit`, `exr-glm-noncollapse`.

Section anchors: `sec-glm-intro`, `sec-edf`, `sec-links`, `sec-logistic`, `sec-poisson`,
`sec-other-links`, `sec-glm-estimation`, `sec-deviance`, `sec-noncollapsibility`, `sec-glm-worked`,
`sec-glm-notes`, `sec-glm-exercises`.

Referenceable equations: `eq-edf-density`, `eq-edf-normalization`, `eq-glm-mean-variance`,
`eq-variance-function`, `eq-edf-cgf`, `eq-link`, `eq-logistic`, `eq-odds-ratio`, `eq-poisson`,
`eq-glm-loglik`, `eq-glm-score`, `eq-glm-score-matrix`, `eq-canonical-score`, `eq-glm-information`,
`eq-fisher-scoring`, `eq-irls`, `eq-working-response`, `eq-scaled-deviance`, `eq-deviance`,
`eq-deviance-diff`, `eq-deviance-chisq`, `eq-cond-marg-effect`, `eq-glm-asymptotic-normality`.

## Proposed notation additions (for the orchestrator to fold into `notation.qmd`)

These are the standard GLM symbols, introduced and defined locally in this chapter. They do not conflict
with existing entries but should be registered in the "Outcome models and likelihoods" block:

- `b(theta)` cumulant function of the exponential dispersion family; `b'(theta)=mu`, `b''(theta)=V(mu)`.
- `theta` natural (canonical) parameter of the EDF; `a(phi)=phi/w` with dispersion `phi` and known prior
  weight `w`; `c(y,phi)` the carrier term.
- `V(mu)` variance function, so `Var(Y)=a(phi)V(mu)`.
- `W=diag(W_i)` IRLS/Fisher working-weight matrix, `W_i=(w_i/(phi V(mu_i)))(dmu_i/deta_i)^2`;
  `z` working (adjusted) response of IRLS.
- `D`, `D*` deviance and scaled deviance; `r^D_i` deviance residual.

Three deliberate symbol reconciliations, flagged in a chapter remark so a reader is never confused:

1. `theta` here is the EDF natural parameter, a specific instance of the generic Ch05 parameter
   `boldsymbol theta`. It is distinct from the subscripted outcome-scale mean `theta_{ijk}=g^{-1}(eta_{ijk})`
   used in the network-model chapters; the bare `theta` of this chapter never denotes a mean. The GLM mean
   is always written `mu_i`.
2. `phi` here is the dispersion parameter (universal GLM usage). To avoid clashing with the
   `notation.qmd` entry where `phi` is the standard normal density, I never write the normal density as
   `phi` in this chapter: in the probit discussion the inverse-link derivative is written `Phi'`.
   Recommend the orchestrator either keep `phi` overloaded with this local convention (clearly stated) or
   adopt `varphi` for the normal density globally; I did not change `notation.qmd`.

## Bibliography

No new bib entries needed. All citations (`@mccullagh1989glm`, `@dias2018nma`, and the sibling-chapter
cross-references) use keys already present in `references.bib`.

## Decisions

- Proved `@thm-glm-mean-variance` by the cumulant-generating-function route requested in the brief:
  computed the MGF in closed form from the EDF normalization identity, obtained `K_Y(t)=[b(theta+t a(phi))-b(theta)]/a(phi)`,
  and read off `K'(0)=mu=b'(theta)`, `K''(0)=Var=a(phi)b''(theta)`. This is cleaner and more rigorous than
  the Bartlett-identity differentiation and matches the chapter's emphasis.
- Verified the regularity hypotheses (A1)-(A3) of `@thm-mle-asymptotic-normality` for the canonical-link
  GLM via `@lem-canonical-hessian` (nonrandom Hessian `-X^T W X`), so the asymptotic-normality corollary
  is fully justified rather than asserted.
- Proved deviance nonnegativity (`@prp-deviance-nonneg`) by exhibiting each contribution as a Bregman
  divergence of the convex cumulant function `b`, which also yields the equality-iff-saturated condition
  and the normal `D = RSS` specialization in one stroke.
- Worked example chosen so the MLE is available in closed form (saturated 2x2 logistic), letting the
  reader check the IRLS iterates against an exact target. All numbers re-verified computationally:
  conditional log-OR `= log 3.5 = 1.25276` in both strata; marginal OR `= 22/7 = 3.142857` (attenuated);
  MLE `(-1.38629, 2.23359)`, `exp(beta1)=9.33333`; IRLS `(0,0) -> (-1.2,2.0) -> (-1.3769,2.2238) -> (-1.3863,2.2336)`;
  null residual deviance `D0 = 5.300` on 1 df, `p = 0.0213`.

## Gaps left for review

- Non-collapsibility of the hazard ratio is stated precisely (`@sec-noncollapsibility`) but not proved in
  place; it is deferred to the survival-analysis material because it needs the survival function and a
  proportional-hazards model not yet developed. This is the only result in the chapter given as a forward
  reference rather than proved; flagged explicitly in the chapter text and in Notes and references.
- Machine-checked tags: only `@prp-collapsibility-rd-rr` carries a `[machine-checked: ...]` tag
  (`theories/STC.v`, `STC_collapse_linear`), which I confirmed exists. I did not find a standalone Coq
  theorem proving the odds-ratio non-collapsibility example, so `@exm-noncollapsible-or` is left untagged
  (it corresponds to catalogue B.13 in `proofs/`, noted in the text). The orchestrator's consistency pass
  should confirm the single tag.
- The probit normal-density symbol question (item 2 above) is the one notation decision I leave to the
  orchestrator; the chapter is internally consistent either way.
