# Work log: Chapter 08, Hierarchical Models, Shrinkage, and Bayesian Inference

Author pass by the Ch08 agent. File written: `chapters/part1/08-hierarchical-bayes.qmd`
(1383 lines, stub removed, YAML title preserved).

## Sources consulted

- `~/Documents/GitHub/ITC_Coq/proofs/L_bayesian.md` (catalogue items L.1 to L.5: Bayes' theorem,
  conjugate families, HMC/NUTS detailed balance, posterior predictive, marginal likelihood and Bayes
  factors). Statements and the dependency notes were used to align this chapter; the catalogue's
  one-line sketches were expanded into full proofs.
- `~/Documents/GitHub/ITC_Coq/manuscript/03_bayesian.md` (companion prose). Confirms the scope decision
  that the Coq development does not formalize Bayesian inference, so no machine-checked tags are used.
- `~/Documents/GitHub/ITC_Coq/theories/` grep: confirmed no `Theorem` named for Bayes, shrinkage,
  conjugacy, Metropolis, REML, or posterior exists. The single "shrink" hit (`Comparison.v:432`) refers
  to ESS shrinking and is unrelated. Hence no `[machine-checked: ...]` tags in this chapter.
- Sibling chapters read for notation and house style: `04-probability.qmd`, `05-inference.qmd`,
  `06-linear-regression.qmd` (Ch07 is still a stub). Confirmed exact sibling slugs in Ch03 and Ch04.
- `notation.qmd` for symbols ($\boldsymbol\xi$, $\pi$, $p(\mathbf y\mid\boldsymbol\xi)$, $\theta_j$,
  $\mu$, $\tau^2$, $s_j^2$, $J_n$, $\mathrm{ESS}$, $\delta_{j,1k}$, $d_{1k}$).
- Cited in text (keys present in `references.bib`): `@dias2018nma` (random-effects NMA, Bayesian
  estimation, the bridge), `@dersimonian1986` (method-of-moments heterogeneity), `@carpenter2017stan`
  (HMC/NUTS, dual averaging, centered vs non-centered), `@strang2016` (linear-algebra prerequisites),
  `@bingham2010regression` (GLS/variance-component background).

## Slugs defined (owned, all 11 present)

`def-exchangeability`, `def-hierarchical-model`, `thm-shrinkage-posterior-mean`, `def-random-effects`,
`def-reml`, `thm-bayes`, `thm-conjugate-normal`, `thm-conjugate-beta-binomial`,
`def-posterior-predictive`, `thm-mh-stationarity`, `def-hmc`.

## Helper slugs introduced (new, globally unique, not in any cross-chapter map)

- `lem-iid-mixture-exchangeable` (mixtures of conditionally iid are exchangeable; proved)
- `thm-de-finetti` (binary de Finetti representation; easy direction proved, converse cited)
- `cor-conjugate-normal-mv` (multivariate normal-normal conjugacy; proved, ties to Ch04 MVN)
- `prp-conjugate-gamma-poisson` (gamma-Poisson conjugacy; proved)
- `lem-stein` (Stein's lemma; proved)
- `thm-james-stein` (James-Stein dominance via SURE; full proof)
- `thm-reml-invariance` (REML invariant to contrast choice; proved)
- `thm-reml-one-sample` (REML one-sample normal gives the $n-1$ denominator; proved)
- `prp-normal-marginal` (marginal model $y_j\sim N(\mu,\tau^2+s_j^2)$; proved)
- `def-credible-interval`, `prp-hpd-shortest` (HPD has minimal volume; proved)
- `def-markov-kernel`, `def-detailed-balance`, `lem-detailed-balance-stationary` (detailed balance
  implies stationarity; full proof, the requested result)
- `lem-hamiltonian-conservation`, `lem-leapfrog-volume`, `prp-hmc-invariance` (HMC correctness; proved)
- `def-marginal-likelihood`, `prp-posterior-odds` (Bayes factor and posterior odds; proved)
- Equation labels: `eq-definetti`, `eq-hier-factor`, `eq-normal-normal-model`, `eq-bayes`,
  `eq-conjugate-normal`, `eq-conjugate-beta`, `eq-shrinkage`, `eq-dersimonian-laird`,
  `eq-posterior-predictive`, `eq-detailed-balance`, `eq-mh-acceptance`, `eq-hamiltonian`.
- Section slugs: `sec-exchangeability`, `sec-normal-hierarchical`, `sec-bayes`, `sec-conjugacy`,
  `sec-shrinkage`, `sec-reml-eb`, `sec-predictive`, `sec-mcmc`, `sec-hmc`, `sec-marginal-likelihood`,
  `sec-hb-worked`, `sec-hb-bridge`, `sec-hb-notes`, `sec-hb-exercises`.
- Worked examples: `exm-three-study-shrinkage`, `exm-beta-binomial-shrinkage`.
- Exercises: `exr-shrinkage-unequal`, `exr-conjugate-n-sample`, `exr-gamma-poisson-mean`,
  `exr-mh-detailed-balance-discrete`, `exr-hpd-vs-equal-tailed`, `exr-leapfrog-jacobian`,
  `exr-empirical-bayes-recompute`, `exr-james-stein-sure` (starred, Appendix F),
  `exr-reml-one-way` (starred, Appendix F).

## Cross-references to siblings (all resolve to existing slugs)

- Ch01: `@thm-rank-nullity`, `@thm-four-subspaces`.
- Ch02: `@def-projection-matrix`, `@thm-gram-schmidt`.
- Ch03: `@thm-pd-characterization`, `@def-quadratic-form`.
- Ch04: `@def-probability-space`, `@def-conditional-expectation`, `@def-conditional-independence`,
  `@thm-mvn-linear`, `@thm-mvn-conditional`, `@prp-mvn-density` (all verified to exist in
  `04-probability.qmd`).
- Ch07: `@def-non-collapsibility` (in the cross-chapter map; Ch07 is still a stub, reference will
  resolve once Ch07 defines it).

## Catalogue coverage

L.1 (`thm-bayes`), L.2 (`thm-conjugate-normal`, `thm-conjugate-beta-binomial`,
`prp-conjugate-gamma-poisson`), L.3 (`thm-mh-stationarity` with `lem-detailed-balance-stationary`,
`def-hmc`, `prp-hmc-invariance`, `lem-hamiltonian-conservation`, `lem-leapfrog-volume`),
L.4 (`def-posterior-predictive`), L.5 (`def-marginal-likelihood`, `prp-posterior-odds`), plus the
chapter's assigned random-effects and REML content (`def-random-effects`, `def-reml`,
`thm-reml-invariance`, `thm-reml-one-sample`, `prp-normal-marginal`, DerSimonian-Laird).

## Proposed bibliography additions (NOT added to references.bib; for the orchestrator to merge)

These are attributed by author and year in the chapter prose. Full entries:

```bibtex
@article{definetti1937,
  author = {de Finetti, Bruno},
  title = {La pr\'evision: ses lois logiques, ses sources subjectives},
  journal = {Annales de l'Institut Henri Poincar\'e},
  volume = {7}, number = {1}, pages = {1--68}, year = {1937}}

@article{hewitt1955symmetric,
  author = {Hewitt, Edwin and Savage, Leonard J.},
  title = {Symmetric measures on {C}artesian products},
  journal = {Transactions of the American Mathematical Society},
  volume = {80}, number = {2}, pages = {470--501}, year = {1955}}

@inproceedings{james1961estimation,
  author = {James, W. and Stein, Charles},
  title = {Estimation with quadratic loss},
  booktitle = {Proceedings of the Fourth Berkeley Symposium on Mathematical Statistics and Probability},
  volume = {1}, pages = {361--379}, year = {1961}, publisher = {University of California Press}}

@article{efron1975steinparadox,
  author = {Efron, Bradley and Morris, Carl},
  title = {Data analysis using {S}tein's estimator and its generalizations},
  journal = {Journal of the American Statistical Association},
  volume = {70}, number = {350}, pages = {311--319}, year = {1975}}

@article{patterson1971reml,
  author = {Patterson, H. D. and Thompson, R.},
  title = {Recovery of inter-block information when block sizes are unequal},
  journal = {Biometrika}, volume = {58}, number = {3}, pages = {545--554}, year = {1971}}

@article{harville1977reml,
  author = {Harville, David A.},
  title = {Maximum likelihood approaches to variance component estimation and to related problems},
  journal = {Journal of the American Statistical Association},
  volume = {72}, number = {358}, pages = {320--338}, year = {1977}}

@article{metropolis1953,
  author = {Metropolis, Nicholas and Rosenbluth, Arianna W. and Rosenbluth, Marshall N. and Teller, Augusta H. and Teller, Edward},
  title = {Equation of state calculations by fast computing machines},
  journal = {The Journal of Chemical Physics},
  volume = {21}, number = {6}, pages = {1087--1092}, year = {1953}}

@article{hastings1970,
  author = {Hastings, W. K.},
  title = {Monte {C}arlo sampling methods using {M}arkov chains and their applications},
  journal = {Biometrika}, volume = {57}, number = {1}, pages = {97--109}, year = {1970}}

@article{tierney1994,
  author = {Tierney, Luke},
  title = {Markov chains for exploring posterior distributions},
  journal = {The Annals of Statistics},
  volume = {22}, number = {4}, pages = {1701--1728}, year = {1994}}

@incollection{neal2011hmc,
  author = {Neal, Radford M.},
  title = {{MCMC} using {H}amiltonian dynamics},
  booktitle = {Handbook of Markov Chain Monte Carlo},
  editor = {Brooks, Steve and Gelman, Andrew and Jones, Galin and Meng, Xiao-Li},
  pages = {113--162}, year = {2011}, publisher = {Chapman and Hall/CRC}}

@article{hoffman2014nuts,
  author = {Hoffman, Matthew D. and Gelman, Andrew},
  title = {The {N}o-{U}-{T}urn {S}ampler: adaptively setting path lengths in {H}amiltonian {M}onte {C}arlo},
  journal = {Journal of Machine Learning Research},
  volume = {15}, number = {1}, pages = {1593--1623}, year = {2014}}

@article{betancourt2017hmc,
  author = {Betancourt, Michael},
  title = {A conceptual introduction to {H}amiltonian {M}onte {C}arlo},
  journal = {arXiv preprint arXiv:1701.02434}, year = {2017}}

@book{gelman2013bda,
  author = {Gelman, Andrew and Carlin, John B. and Stern, Hal S. and Dunson, David B. and Vehtari, Aki and Rubin, Donald B.},
  title = {Bayesian Data Analysis}, edition = {3rd}, year = {2013}, publisher = {Chapman and Hall/CRC}}
```

If the orchestrator prefers to avoid adding all of these, the chapter's mathematics is self-contained
(every load-bearing result is proved); the names appear only as historical attribution in prose and in
the two cited statements (the de Finetti converse and the MCMC ergodic theorem), so the citations can be
softened to prose-only without breaking any argument.

## Notation: no new symbols proposed

All symbols are from `notation.qmd`. The chapter uses $\theta_j$ for the study-specific random effect
(the unit parameter of the hierarchical model), $\mu$ and $\tau^2$ for the population mean and
between-study variance, $\boldsymbol\phi$ for a generic hyperparameter, and $s_j^2$ for the known
within-study sampling variance. These are consistent with the existing scheme and with the
random-effects NMA notation ($\delta_{j,1k}$, $d_{1k}$) used in the bridge section. The mass matrix $M$
and momentum $\mathbf r$ in HMC are standard and local to `def-hmc`.

## Decisions and ordering

- The requested content flow places shrinkage before the formal Bayesian section, but the shrinkage
  estimator is a posterior mean and therefore needs Bayes' theorem and normal-normal conjugacy first.
  Resolved by ordering: exchangeability and hierarchical model (motivation), then Bayes' theorem, then
  conjugacy, then shrinkage, then REML and empirical Bayes, then posterior predictive and credible
  intervals, then MCMC, HMC, and Bayes factors. The narrative signals this dependency explicitly at the
  end of `sec-normal-hierarchical`.
- James-Stein is included with full proofs (`lem-stein`, `thm-james-stein` via the unbiased risk
  estimate) rather than only remarked on, because it is the rigorous frequentist justification of
  partial pooling and the empirical-Bayes shrinkage factor; the SURE generalization is set as starred
  exercise `exr-james-stein-sure`.
- REML "balanced normal case" is realized as the one-sample normal model (`thm-reml-one-sample`), which
  cleanly exhibits the restored $n-1$ denominator; the general restricted log-likelihood and the
  balanced one-way layout are stated in a remark and set as starred exercise `exr-reml-one-way`.
- MCMC convergence diagnostics ($\hat R$, ESS) are deliberately NOT developed here; they are forward
  referenced to the Bayesian-computation chapter (catalogue Part I, I.1 to I.6) to avoid stepping on
  that chapter's assignment. Likewise WAIC/LOO are forward referenced from the Bayes-factor remark.

## Gaps left for review

1. The de Finetti converse and the MCMC ergodic theorem (LLN/CLT for Harris-recurrent chains) are
   stated and cited, not proved; their proofs require martingale convergence and general state-space
   Markov-chain theory beyond a foundations chapter. Flagged as cited prerequisites per STYLE rule 6.
2. The general REML restricted log-likelihood determinant identity (`prp`-style remark in `sec-reml-eb`)
   is stated without the matrix-determinant-lemma derivation; the one-sample case is fully derived and
   the general case is exercised. A reviewer may wish to promote the identity to a full proposition.
3. The reference to `@def-non-collapsibility` (Ch07) will only resolve once Ch07 is authored; the slug
   is from the cross-chapter map, so this is expected, not an error.
4. No machine-checked tags, consistent with the manuscript's statement that the Coq tree omits Bayesian
   inference. Candidate future formalizations noted in the chapter's Notes section
   (`lem-detailed-balance-stationary`, `thm-shrinkage-posterior-mean`, `lem-leapfrog-volume`).

## Self-checks run

- Div fences balanced (76 openers, 76 closers); 21 proofs each ending in `$\square$`; 26
  `$\blacktriangleleft$` closers on definitions, examples, and remarks.
- No dash punctuation as a connector in prose (only math-mode minus signs); American spelling
  throughout; no em dash, en dash, figure dash, or double hyphen anywhere.
- All in-text `@` citations resolve to keys present in `references.bib`; all cross-reference slugs
  resolve to owned slugs or verified sibling slugs.
- Two worked examples with hand-verifiable arithmetic; two starred exercises with Appendix F markers.
