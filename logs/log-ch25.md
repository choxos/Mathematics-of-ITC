# Work log: Chapter 25, General Likelihoods (Survival and Ordered Categorical Outcomes)

Author pass: Opus 4.8. File written: `chapters/part5/25-general-likelihoods.qmd` (overwrote the stub,
kept YAML title). Catalogue coverage: J.1 to J.8 (Part J).

## Sources consulted

- `proofs/J_general_likelihoods.md` (base draft; J.1 to J.8, including sub-results J.4a, J.4b, J.4c).
- `manuscript/14_general_likelihoods.md` (companion prose chapter; sections 14.2 to 14.14, including the
  note in 14.13 that survival is not formalized in Coq).
- `chapters/part4/18-maic.qmd` (voice, structure, depth target; worked-example and notes/exercises style).
- `logs/STYLE.md`, `notation.qmd` (authoring contract and notation).
- `references.bib` (verified keys: phillippo2025general, phillippo2020mlnmr, phillippo2019thesis,
  chandler2025mlumr, mccullagh1989glm, sobol1967, sklar1959, owen1956, carpenter2017stan, dias2018nma).
- `~/Documents/GitHub/multinma/vignettes/example_ndmm.Rmd` and `data/` (newly diagnosed multiple myeloma
  PFS survival example: M-spline baseline hazard, 4 covariates, 64 Sobol' integration points, gamma age +
  Bernoulli binaries, Gaussian copula). Used to frame the worked example as a stylized analogue; the book
  example itself is a self-contained exponential-hazard binary-covariate model checkable by hand.
- `~/Documents/GitHub/ITC_Coq/theories/*.v` (confirmed: no Survival.v; only a prose comment in STC.v
  mentions hazard/non-collapsibility). Hence no machine-checked tags in this chapter.

## Catalogue results expanded (sketch -> full proof in book notation)

- J.1 -> `@def-survival-function`; J.2 -> `@def-hazard` (with a short proof of the f/S limit form);
  J.3 -> `@thm-survival-hazard-relation` (full proof via absolute continuity + FTC, plus a converse
  establishing the hazard<->distribution bijection, which the base draft did not state).
- J.4 -> `@def-censored-likelihood` plus `@prp-censored-likelihood-density` (the base draft gave a
  one-line "combining" argument; expanded to a rigorous independent-censoring joint-density factorization
  with the non-informative-censoring assumption stated and the parameter-free factors identified).
- J.4a -> `@thm-conditional-loghr-ph` (full cancellation proof).
- J.4b -> `@lem-survivor-weighted-hazard` (representation, with the differentiate-under-integral step
  justified by dominated convergence) + `@thm-marginal-hr-time-varying`. The base draft asserted
  time-variation; I gave a complete proof under the standard frailty/PH structure via an exponential-tilt
  covariance (variance-of-the-natural-parameter) argument, proving strict attenuation toward the null and
  mHR(0)=psi.
- J.4c -> `@def-rmst` + `@thm-rmst-collapsible` (Fubini/Tonelli proof) with the scale-misalignment
  transportability caveat as a remark forward-referencing Ch26.
- J.5 -> `@thm-marginal-individual-likelihood` (marginalization proof + finiteness + relation to
  mean-aggregation and to QMC).
- J.6 -> `@thm-aggregate-marginal-likelihood` (product justified from conditional independence + iid
  covariate draws via Tonelli; built on `@thm-aggregation`). Pseudo-IPD remark forward-references Ch26.
- J.7 -> `@def-proportional-odds` + `@lem-ordinal-valid-probabilities` (nonnegativity, sum-to-one via
  telescoping, and the proportional-odds property, all proved).
- J.8 -> `@thm-general-likelihood-mlnmr` (capstone: IPD/AgD arm likelihoods, GLM reduction proved for
  affine-in-mean kernels, NMA reduction, survival/ordinal instances).

## Slugs defined (globally unique, topic-namespaced)

Owned (8, all present): `def-survival-function`, `def-hazard`, `thm-survival-hazard-relation`,
`def-censored-likelihood`, `thm-marginal-individual-likelihood`, `thm-aggregate-marginal-likelihood`,
`def-proportional-odds`, `thm-general-likelihood-mlnmr`.

Additional slugs I defined to give complete proofs of catalogue sub-results J.4a/J.4b/J.4c and supporting
lemmas (all within Chapter 25's scope; recorded here for the harmony pass):
`thm-conditional-loghr-ph`, `lem-survivor-weighted-hazard`, `thm-marginal-hr-time-varying`, `def-rmst`,
`thm-rmst-collapsible`, `prp-censored-likelihood-density`, `lem-ordinal-valid-probabilities`,
`exm-genlik-survival`, and exercises `exr-genlik-weibull-hazard`, `exr-genlik-cumulative-hazard-additive`,
`exr-genlik-binary-reduction`, `exr-genlik-ordinal-network`, `exr-genlik-mhr-attenuation` (starred),
`exr-genlik-rmst-transport` (starred). Section labels: `sec-genlik-intro`, `-survival`, `-hazard-ratio`,
`-rmst`, `-likelihood`, `-aggregation`, `-ordinal`, `-general`, `-example`, `-notes`, `-exercises`.
Equation labels namespaced `eq-genlik-*` (17, no duplicates).

## Cross-references used (all resolve to approved-map slugs or confirmed written slugs)

Ch4: `@thm-fubini-tonelli`, `@thm-dominated-convergence`, `@thm-jensen` (confirmed present in
`chapters/part1/04-probability.qmd`). Ch7: `@def-link-function`, `@def-non-collapsibility`. Ch17:
`@def-sema`. Ch20: `@thm-aggregation`, `@thm-identity-link-exact`, `@thm-log-link-mgf`,
`@thm-logit-no-closed-form`. Ch22: `@thm-hypercube-integration`, `@def-sobol-net`, `@thm-sklar`,
`@def-gaussian-copula`, `@thm-inverse-cdf`. Ch23: `@thm-mlnmr-generalizes-nma`. Ch24:
`@thm-gelman-rubin`, `@def-mcmc-ess`, `@def-integration-error-monitoring`, `@thm-dic-waic-loo`,
`@def-psis-loo`. Ch26 (forward): `@thm-pseudo-ipd-reconstruction`, `@thm-mlumr-tte`.

## Machine-checked tags

None. Confirmed there is no survival/hazard/RMST/ordinal formalization in `ITC_Coq/theories/`
(no Survival.v; STC.v only mentions them in a comment). This matches manuscript section 14.13.

## Proposed bibliography additions (for the orchestrator to merge into references.bib)

Used in prose with explicit "see the work log" placeholders rather than fabricated keys:

```bibtex
@book{kleinmoeschberger2003,
  author    = {Klein, John P. and Moeschberger, Melvin L.},
  title     = {Survival Analysis: Techniques for Censored and Truncated Data},
  edition   = {2nd},
  publisher = {Springer},
  year      = {2003}
}
@article{guyot2012km,
  author  = {Guyot, Patricia and Ades, A. E. and Ouwens, Mario J. N. M. and Welton, Nicky J.},
  title   = {Enhanced secondary analysis of survival data: reconstructing the data from published
             Kaplan-Meier survival curves},
  journal = {BMC Medical Research Methodology},
  volume  = {12},
  pages   = {9},
  year    = {2012}
}
```

Optional (only if the M-spline baseline is cited elsewhere by key rather than via phillippo2025general):
a `phillippo2024mspline` entry for the flexible M-spline baseline-hazard methodology. I cited the
M-spline through `@phillippo2025general` to avoid inventing a key.

## Proposed notation additions (for notation.qmd, "Outcome models and likelihoods" / "Survival")

- $S(t\mid\mathbf{x})$ survival function, $h(t\mid\mathbf{x})$ hazard, $H(t\mid\mathbf{x})$ cumulative
  hazard; relation $S=\exp(-H)$.
- $T$ event time, $C$ censoring time, $\tilde T=\min(T,C)$ observed time, $\delta=\mathbf 1\{T\le C\}$
  event indicator; observed pair $(t,\delta)$.
- $\operatorname{RMST}_t^{\mathcal{P}}(\tau)=\int_0^{\tau}S_t^{\mathcal{P}}(s)\,ds$ restricted mean
  survival time; $\Delta\!\operatorname{RMST}$ its contrast. (RMST already in the abbreviations table; the
  symbol is new.)
- $\pi_{\mathrm{Ind}}(y\mid\boldsymbol\theta)$ individual-level conditional likelihood kernel (the generic
  integrand of general-likelihood ML-NMR); $\boldsymbol\theta_{jk}(\mathbf{x};\boldsymbol\xi)$ the
  conditional parameter map.
- $\tilde f_t(\mathbf{x}\mid s)$ survivor covariate density at time $s$ under treatment $t$.
- $\rho(\mathbf{x})$ frailty (positive prognostic multiplier of the baseline hazard).
- $\alpha_k$ proportional-odds cutpoints, $p_k(\mathbf{x})$ category probabilities, $\operatorname{expit}$
  the inverse logit (already used in Ch18).

These are introduced and used self-consistently in the chapter; none conflict with existing symbols.

## Decisions

- Included J.4a/J.4b/J.4c as full theorems (conditional HR, time-varying marginal HR, RMST), not just J.5
  to J.8, because they are the mathematically richest survival results, are in catalogue Part J and the
  source manuscript (sections 14.6 to 14.8), and the worked example demonstrates them. The chapter thus
  covers all of J.1 to J.8 including sub-results.
- Proved `@thm-marginal-hr-time-varying` under the frailty/PH structure (covariate-independent conditional
  HR, prognostic frailty). This is the standard, cleanest non-collapsibility setting and admits a complete
  proof (exponential-tilt covariance). The broader "effect-modification-present" case is discussed in
  prose; a complete proof there would need a comonotonicity hypothesis, deferred deliberately to keep
  every stated theorem fully proved rather than sketched.
- Worked example uses one binary covariate so the covariate integral is an exact two-point sum, all
  survival probabilities/hazards/RMSTs/likelihoods are closed-form and hand-checkable, and it doubles as a
  demonstration of HR non-collapsibility (table of mHR over time) and RMST collapsibility.

## Gaps / for the harmony pass

- The Ch4 references `@thm-fubini-tonelli` and `@thm-dominated-convergence` were verified to exist; if they
  are renamed in the consistency pass, update three citations (RMST collapsibility, the aggregate-product
  Tonelli step, and the differentiate-under-integral step).
- Forward references to Ch26 (`@thm-pseudo-ipd-reconstruction`, `@thm-mlumr-tte`) assume those slugs are
  defined as listed in the wave map; verify after Ch26 is authored.
- Klein-Moeschberger and Guyot et al. are referenced in prose pending the bibliography merge above; until
  merged, those two sentences name the authors without a live `@key`.
- No `quarto render` performed (single-chapter agent); cross-reference resolution to sibling Part V
  chapters (still stubs at author time) will be confirmed at the book-level render.
