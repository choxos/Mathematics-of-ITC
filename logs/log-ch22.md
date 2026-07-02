# Work log: Chapter 22, ML-NMR III: Numerical Integration Theory

File authored: `chapters/part5/22-mlnmr-integration.qmd` (stub overwritten with full chapter).
Catalogue coverage: **H.12 to H.19** of `proofs/H_ml_nmr.md`, plus the integration-error material I.4 of
`proofs/I_computation.md` (cross-referenced forward to Chapter 24, not owned here).

## Sources consulted

- `proofs/H_ml_nmr.md`, sections H.12 (Gauss quadrature), H.13 (Monte Carlo), H.14 (Koksma-Hlawka),
  H.15 (Sobol' nets), H.16 (Sklar), H.17 (Gaussian copula), H.18 (inverse-CDF), H.19 (pipeline).
  Every sketch in these sections was expanded into a complete proof in the book's notation.
- `proofs/I_computation.md`, section I.4 (integration-error monitoring), used for the `N`-vs-`N/2`
  diagnostic remark and the forward link to Chapter 24.
- `chapters/part4/18-maic.qmd` for voice, div grammar, worked-example style, and notes/exercises layout.
- `logs/STYLE.md` and `notation.qmd` (authoring contract and symbol table).
- `ITC_Coq/manuscript/10_ml_nmr.md` (prose companion) skimmed for narrative alignment.

## Catalogue identifiers and the slugs that realize them

| Catalogue | Owned slug | What was proved |
|---|---|---|
| H.12 | `thm-quadrature-error` | Gauss-Legendre error; full proof via Legendre orthogonality + Hermite remainder, exact constant derived; composite `O(h^{2k})` proved by panel scaling. |
| H.13 | `thm-mc-rmse` | Monte Carlo RMSE `O(N^{-1/2})`; full proof (unbiasedness, variance, CLT), dimension-free; bounded-integrand variance ceiling 1/4. |
| H.14 | `thm-koksma-hlawka` | Koksma-Hlawka; **1D case proved in full** (FTC + Fubini identity `eq-qmc-koksma-identity`), multi-d stated and cited (Niederreiter 1992). |
| H.15 | `def-sobol-net` | Digital `(t,m,s)`-net + Sobol' construction over F_2; van der Corput first coordinate shown. |
| H.16 | `thm-sklar` | Sklar; **existence + uniqueness proved in the continuous case** (assigned direction). |
| H.17 | `def-gaussian-copula` | Gaussian copula defined; `prp-gaussian-copula-is-copula` proves it is a copula and gives the Cholesky sampler. |
| H.18 | `thm-inverse-cdf` | Inverse-CDF / PIT both directions proved; `lem-quantile-galois` (coupling inequality) proved. |
| H.19 | `thm-hypercube-integration` | Pipeline assembled; pushforward correctness + Koksma-Hlawka error bound proved. |

## Supporting slugs defined (globally unique, topic-namespaced; record for harmony pass)

Definitions/lemmas/cor/prp not in the assigned cross-ref list but needed for self-contained proofs:
`def-copula`, `def-star-discrepancy`, `def-hardy-krause-variation`, `lem-quantile-galois`,
`lem-copula-lipschitz`, `cor-tensor-quadrature-curse` (the curse of dimensionality),
`prp-gaussian-copula-is-copula`.
Examples: `exm-qmc-logit` (1D logit aggregate mean by QMC), `exm-qmc-copula-trace` (2D pipeline trace).
Exercises: `exr-qmc-gauss-two-node`, `exr-qmc-mc-variance`, `exr-qmc-discrepancy`, `exr-qmc-pit-discrete`,
`exr-qmc-gaussian-copula-cov` (★), `exr-qmc-logit-pipeline` (★).

**Starred for Appendix F:** `exr-qmc-gaussian-copula-cov` and `exr-qmc-logit-pipeline`.

Equation labels are all namespaced `eq-qmc-*` (no collision risk).

## Cross-references out (verified against the slug map)

- Written chapters (resolve now): `@def-mgf`, `@thm-cov-psd` (Ch4); `@def-link-function` (Ch7);
  `@def-hmc`, `@thm-mh-stationarity` (Ch8); `@def-ecological-bias` (Ch16).
- Sibling stubs (resolve once authored): Ch20 `@def-individual-model`, `@def-aggregate-model`,
  `@thm-aggregation`, `@thm-aggregation-bias`, `@thm-identity-link-exact`, `@thm-log-link-mgf`,
  `@thm-logit-no-closed-form`; Ch21 `@thm-poisson-aggregate`, `@thm-poisson-binomial-pgf`,
  `@thm-le-cam-tv`, `@thm-adjusted-binomial`; Ch23 `@thm-target-population-integral`,
  `@thm-mlnmr-identifiability-2study`, `@thm-mlnmr-generalizes-nma`; Ch24 `@def-centered-noncentered`,
  `@def-integration-error-monitoring`, `@def-mcmc-ess`.
  These are the only render warnings (expected; not errors).

## Machine-checked tags

**None.** Confirmed by grep over `ITC_Coq/theories/*.v`: no files mention sobol/copula/quadrature/
koksma/hlawka/discrepancy/sklar/hypercube/QMC. Part V numerical-integration results are pen-and-paper,
consistent with the assignment note ("tag only if present"). No `[machine-checked: ...]` tags added.

## Worked example (numbers verified by script, scrapped after use)

- 1D, `X ~ N(0,1)`, logit link. Part A (`mu=0`): exact truth 0.5 by symmetry; 7-point Sobol' set
  `{1/8,...,7/8}` recovers 0.5 exactly. Part B (`mu=0.5`): truth 0.6020 (no closed form); 7-point
  estimate 0.6091; sequential van der Corput convergence table N=4..128 with errors and the N-vs-N/2
  diagnostic; MC comparison across 5 seeds shows the QMC advantage. All quantile/expit/average arithmetic
  reproduced to the displayed precision with scipy.
- 2D trace: `u=(1/2,1/4)`, `rho=0.5`, normal margins, Cholesky `L=[[1,0],[0.5,0.8660]]` ->
  `x=(0,-0.5841)`, `expit(eta)=0.4275`. Verified.

## Proposed bibliography additions (relied on by author-year in prose; add for harmony pass)

These back named results not currently keyed in `references.bib`. Cited in prose as "Author (year)" so the
chapter renders cleanly; promote to `@key` once added.

```bibtex
@book{niederreiter1992, author={Niederreiter, Harald},
  title={Random Number Generation and Quasi-Monte Carlo Methods},
  series={CBMS-NSF Regional Conference Series in Applied Mathematics}, volume={63},
  publisher={SIAM}, year={1992}}
@article{koksma1943, author={Koksma, Jurjen F.},
  title={Een algemeene stelling uit de theorie der gelijkmatige verdeeling modulo 1},
  journal={Mathematica B (Zutphen)}, volume={11}, pages={7--11}, year={1942/43}}
@article{hlawka1961, author={Hlawka, Edmund},
  title={Funktionen von beschr{\"a}nkter Variation in der Theorie der Gleichverteilung},
  journal={Annali di Matematica Pura ed Applicata}, volume={54}, pages={325--333}, year={1961}}
@article{joekuo2008, author={Joe, Stephen and Kuo, Frances Y.},
  title={Constructing Sobol sequences with better two-dimensional projections},
  journal={SIAM Journal on Scientific Computing}, volume={30}, number={5}, pages={2635--2654}, year={2008}}
@book{stoerbulirsch2002, author={Stoer, Josef and Bulirsch, Roland},
  title={Introduction to Numerical Analysis}, edition={3}, publisher={Springer}, year={2002}}
@article{owen1998scrambling, author={Owen, Art B.},
  title={Scrambling Sobol' and Niederreiter--Xing points},
  journal={Journal of Complexity}, volume={14}, number={4}, pages={466--489}, year={1998}}
@book{nelsen2006, author={Nelsen, Roger B.},
  title={An Introduction to Copulas}, edition={2}, publisher={Springer}, year={2006}}
```

Note: `@owen1956` (Donald B. Owen, bivariate normal tables) is in the bib and is used correctly for
evaluating the Gaussian copula's bivariate normal probabilities; the scrambling reference is the distinct
Art B. Owen (1998) proposed above. Do not conflate.

## Notation

No additions to `notation.qmd` needed. All symbols used are already in the table: `C`, `C_Omega`,
`V_HK(f)`, `D_N^*(P)`, `Phi`, `phi`, `F^{-1}`, `Omega`, `f_j`, `F_j`. Local-only symbols introduced and
defined in-text: `T` (transport map `[0,1]^d -> X`), `psi = g^{-1} o eta o T` (cube-pullback integrand),
`varphi = g^{-1} o eta` (covariate-space integrand), `Delta_N` (local discrepancy). These are scoped to the
chapter and need not enter the global table.

## Gaps / decisions left for review

1. Multi-d Koksma-Hlawka identity and the Sobol' rate `D_N^* = O((log N)^d / N)` are stated and cited
   (Niederreiter 1992), not reproved; the 1D case is proved in full, per the assignment.
2. Gauss-Legendre proof cites two classical facts (Legendre orthogonality; Hermite remainder formula);
   everything else, including the exact error constant, is derived.
3. Sklar proved only in the continuous-margin case (assigned); the discontinuous-margin uniqueness
   subtlety is noted in prose but not formalized.
4. `def-copula` placed here as the canonical home (this is the copula chapter). If Ch26/Ch27 also need a
   copula definition they should cross-reference `@def-copula` rather than redefine; flag in harmony pass.
5. Render check: `quarto render` (v1.8.26) of the file succeeds (HTML produced); only warnings are the
   sibling-stub cross-refs listed above.
