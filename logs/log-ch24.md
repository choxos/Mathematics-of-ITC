# Work log: Chapter 24, Bayesian Computation and Diagnostics

File authored: `chapters/part5/24-computation.qmd` (stub overwritten with full chapter; YAML title kept,
stub callout dropped).
Catalogue ownership: I.1 through I.6 of `proofs/I_computation.md`.

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (notation, single source of truth).
- Base draft expanded: `~/Documents/GitHub/ITC_Coq/proofs/I_computation.md` (results I.1 to I.6) and the
  companion manuscript `~/Documents/GitHub/ITC_Coq/manuscript/13_computation.md`. Every sketch in those
  files (the funnel intuition, the $\hat R$ formula, the ESS definition, the doubling diagnostic, the
  DIC/WAIC/LOO definitions, the PSIS sketch) was expanded into a complete proof in this book's notation.
- `~/Documents/GitHub/ITC_Coq/proofs/L_bayesian.md` for the Bayesian prerequisites L.1 to L.4 (Bayes,
  conjugacy, HMC detailed balance, posterior predictive) that this chapter draws on.
- `~/Documents/GitHub/ITC_Coq/proofs/00_concepts_index.md` for catalogue wording and dependency map
  (I.4 depends on H.14 = Koksma-Hlawka and I.3; I.5 on L.1, L.4; I.6 on I.5, L.4; D.14 = DIC decomposition).
- `chapters/part1/08-hierarchical-bayes.qmd` (read in full around the relevant divs) to match the exact
  statements and slugs of `@def-hmc`, `@thm-mh-stationarity`, `@thm-conjugate-normal`, `@def-random-effects`,
  `@def-exchangeability`, and to inherit the leapfrog substep convention and the funnel remark there (so I
  develop, rather than repeat, the funnel that Ch8's NUTS remark only gestures at).
- `chapters/part4/18-maic.qmd` for voice, div grammar, worked-example style, and the existing weighting
  `ESS` usage (which I deliberately keep distinct from the MCMC `N_eff`; see notation note below).
- `chapters/part3/13-pairwise-meta-analysis.qmd` to confirm the slug `@def-random-effects-ma` for the
  cross-reference to the random-effects NMA layer.
- Verified the numbers in the worked example and the QMC sequence with a short scipy/numpy script
  (Gauss-Hermite truth, van der Corput / 1-D Sobol' running estimates, Gelman-Rubin arithmetic, AR(1) ESS,
  WAIC/LOO on the 2x4 likelihood table, GPD moment thresholds). All chapter numbers are reproduced exactly.

## Catalogue results covered (I.1 to I.6)

- I.1 centered vs non-centered: `def-centered-noncentered`, plus `lem-comp-reparam` (reparameterization
  equivalence), `lem-comp-leapfrog-stability` (the $\epsilon\omega\le2$ Stormer-Verlet threshold, proved
  via the 2x2 leapfrog matrix eigenvalues), `lem-comp-funnel` (CP vs NCP curvature), and `thm-comp-param`
  (the geometry theorem). References `@def-hmc` and `@thm-mh-stationarity` as instructed.
- I.2 Gelman-Rubin: `thm-gelman-rubin`, derived in full from two exact expectation identities
  `lem-comp-within` ($\mathbb E[W]=\frac{N}{N-1}(\sigma^2-v_N)$) and `lem-comp-between`
  ($\mathbb E[B]=Nv_N$); the headline result $\mathbb E[\hat V]=\sigma^2$ exactly at stationarity, the
  one-sided bias, the $\hat R\to1$ limit, and the non-convergence inflation are all proved. Supporting
  `def-comp-rhat-pieces`.
- I.3 effective sample size: `def-mcmc-ess`, with `prp-comp-acf-variance` (the exact
  $\mathrm{Var}(\bar\theta_N)$ identity and its integrated-autocorrelation-time limit) and
  `cor-comp-ess-variance` (the variance-equalization property that names it), and `exm-comp-ar1`.
- I.4 integration-error monitoring: `def-integration-error-monitoring` (the doubling rule) and
  `prp-comp-doubling` (the increment bounds the error under geometric decay), tied to `@thm-koksma-hlawka`,
  `@thm-mc-rmse`, `@def-sobol-net`, `@thm-hypercube-integration` (Ch22) and `@thm-aggregation` (Ch20).
- I.5 DIC/WAIC/LOO: `thm-dic-waic-loo`, with `def-comp-criteria` and the engine `lem-comp-loo-identity`
  (the exact leave-one-out importance-sampling identity, harmonic-mean form). The three relationships are
  derived: WAIC = LOO to second order via a cumulant expansion of $\log\mathbb E[e^{\pm\ell_i}]$;
  $p_D=\mathrm{tr}(\mathcal J\,\mathrm{Var})\to p$ and $p_{\mathrm{WAIC}}$ obeys the same trace formula;
  WAIC/LOO parameterization-invariant, DIC not.
- I.6 PSIS-LOO: `def-psis-loo`, with `lem-comp-gpd-moments` (GPD $m$-th moment finite iff $m<1/k$) and
  `thm-comp-psis-reliability` (the $\hat k<0.5/<0.7/\ge1$ thresholds, derived).

## Slugs defined

Owned (catalogue): `def-centered-noncentered`, `thm-gelman-rubin`, `def-mcmc-ess`,
`def-integration-error-monitoring`, `thm-dic-waic-loo`, `def-psis-loo`.

Chapter-local (namespaced `*-comp-*`): lemmas `lem-comp-reparam`, `lem-comp-leapfrog-stability`,
`lem-comp-funnel`, `lem-comp-within`, `lem-comp-between`, `lem-comp-loo-identity`, `lem-comp-gpd-moments`;
propositions `prp-comp-acf-variance`, `prp-comp-doubling`; corollary `cor-comp-ess-variance`; definitions
`def-comp-rhat-pieces`, `def-comp-criteria`; examples `exm-comp-ar1`, `exm-comp-diagnostics`; theorems
`thm-comp-param`, `thm-comp-psis-reliability`; exercises `exr-comp-rhat`, `exr-comp-rhat-floor` (star),
`exr-comp-ess-acf`, `exr-comp-leapfrog`, `exr-comp-doubling`, `exr-comp-loo-identity`, `exr-comp-waic-loo`,
`exr-comp-gpd` (star). The two starred exercises (`exr-comp-rhat-floor`, `exr-comp-gpd`) are flagged for
Appendix F.

Section labels: `sec-comp-intro`, `-param`, `-rhat`, `-ess`, `-integration`, `-ic`, `-psis`, `-example`,
`-notes`, `-exercises`. Equation labels all lowercase, namespaced `eq-comp-*` (hier, ncp, leapfrog-matrix,
cp-curv, ncp-curv, wb, vhat, ew, eb, rhat, gap, var-mean, ess, kh, doubling, error-bound, lppd,
loo-identity, is, pd, waic-loo-pointwise, psis). No capitals remain in any slug or equation label.

## Machine-checked tags

None. As the companion manuscript states and the `theories/*.v` listing confirms (no computation or
diagnostics file exists; the formalized tree ends with population-adjustment algebra: Bucher, MAIC, STC,
propensity/IPW/AIPW/outcome-regression), nothing in this chapter has a Coq counterpart. A remark closing
the PSIS section and a sentence in Notes state this explicitly. No theorem carries a tag.

## Proposed notation additions (for `notation.qmd`; not edited here)

- `$N_{\mathrm{eff}}$` MCMC effective sample size, $=N/(1+2\sum_{k\ge1}\rho_k)$. **Deliberately distinct**
  from the existing weighting `$\mathrm{ESS}$` of `notation.qmd` (which is reserved for
  $(\sum w_i)^2/\sum w_i^2$). A remark in the introduction flags the distinction for the reader. Recommend
  adding `$N_{\mathrm{eff}}$` to the "Population adjustment / computation" block or a new "Diagnostics" row.
- Convergence-diagnostic symbols, all defined in-text: `$\widehat R$` (potential scale reduction),
  `$W,B,\widehat V$` (within/between/pooled variance), `$\tau_{\mathrm{int}}$` (integrated autocorrelation
  time), `$\rho_k$` (lag-$k$ autocorrelation).
- Information-criterion symbols, defined in-text: `$\mathrm{elpd}$`, `$\mathrm{lppd}$`,
  `$p_{\mathrm{WAIC}}$`, `$p_D$`, and abbreviations DIC, WAIC, LOO(-CV), PSIS, GPD; plus `$\widehat k$`
  (generalized-Pareto shape diagnostic). Recommend adding the abbreviations to the abbreviations table.

None of these conflict with existing notation; all are introduced explicitly on first use so the chapter
is self-contained if the additions are deferred.

## Proposed bibliography additions (for `references.bib`; not edited here)

Cited by bibtex key in the chapter: only `@carpenter2017stan` (already present). All other attributions are
by author name in prose (Notes section), because the keys are not yet in `references.bib`. Proposed entries
(orchestrator to merge and dedupe; some may already be proposed by the Ch8 log, which names Hoffman-Gelman,
Neal, Betancourt, Tierney, Metropolis, Hastings):

- `gelman1992` Gelman, A.; Rubin, D. B. (1992). "Inference from iterative simulation using multiple
  sequences." *Statistical Science* 7(4):457-472.
- `brooks1998` Brooks, S. P.; Gelman, A. (1998). "General methods for monitoring convergence of iterative
  simulations." *Journal of Computational and Graphical Statistics* 7(4):434-455.
- `vehtari2021rank` Vehtari, A.; Gelman, A.; Simpson, D.; Carpenter, B.; Bürkner, P.-C. (2021).
  "Rank-normalization, folding, and localization: an improved $\widehat R$ for assessing convergence of
  MCMC." *Bayesian Analysis* 16(2):667-718.
- `vehtari2017loo` Vehtari, A.; Gelman, A.; Gabry, J. (2017). "Practical Bayesian model evaluation using
  leave-one-out cross-validation and WAIC." *Statistics and Computing* 27(5):1413-1432.
- `watanabe2010waic` Watanabe, S. (2010). "Asymptotic equivalence of Bayes cross validation and widely
  applicable information criterion in singular learning theory." *JMLR* 11:3571-3594.
- `spiegelhalter2002dic` Spiegelhalter, D. J.; Best, N. G.; Carlin, B. P.; van der Linde, A. (2002).
  "Bayesian measures of model complexity and fit." *JRSS-B* 64(4):583-639.
- `geyer1992` Geyer, C. J. (1992). "Practical Markov chain Monte Carlo." *Statistical Science* 7(4):473-483.
- `hoffman2014nuts` Hoffman, M. D.; Gelman, A. (2014). "The No-U-Turn Sampler." *JMLR* 15:1593-1623.
- `neal2011hmc` Neal, R. M. (2011). "MCMC using Hamiltonian dynamics." In *Handbook of Markov Chain Monte
  Carlo*, Chapman & Hall/CRC, 113-162.

## Decisions and notes for the harmony pass

- The funnel is developed rigorously here (curvature lemmas + leapfrog linear-stability lemma giving
  $\epsilon_{\max}(\tau)=2\tau$ in CP vs $\epsilon_{\max}=2$ in NCP), rather than repeating Ch8's one-line
  NUTS remark. Ch8 owns `@def-hmc`/`@thm-mh-stationarity`; I reference them and do not redefine.
- Gelman-Rubin: I prove the simplified modern $\widehat R=\sqrt{\widehat V/W}$ (the catalogue/Vehtari-2021
  form), not the original 1992 $t$-corrected version. The exact identity $\mathbb E[\widehat V]=\sigma^2$
  is the clean center of gravity; the gap $\mathbb E[\widehat V]-\mathbb E[W]=(Nv_N-\sigma^2)/(N-1)$ ties
  directly to the $1+2\sum\rho_k$ factor of the ESS section, giving the two diagnostics a shared spine.
- The exact LOO importance identity (`lem-comp-loo-identity`) is made the engine for both the WAIC-LOO
  equivalence (I.5) and PSIS (I.6); this is cleaner than the catalogue's separate treatments and avoids
  any hand-waving about "approximately the same quantity."
- WAIC-LOO equivalence proved via a cumulant expansion under explicit posterior-concentration regularity
  ($v_i=O(1/n)$, $\kappa_{3,i}=o(v_i)$); the 0.7 PSIS alarm is given as the empirical convention beyond the
  proved 0.5 finite-variance threshold, with the reason stated.
- Worked example numbers are all hand-checkable and were script-verified: $\widehat R=\sqrt{21/20}\approx
  1.025$; AR(1) $N_{\mathrm{eff}}=N(1-\phi)/(1+\phi)$ giving $2000$ and $\approx210$; QMC logit cell
  converging to the exact $0.5868$ with the doubling test first passing at $N=128$ ($0.0045<0.005$);
  WAIC $=4.012$ vs raw-IS LOO $=3.956$ (gap $0.056$ illustrating second-order agreement).
- No gaps. All owned catalogue results (I.1-I.6) are stated and proved; all cross-references either resolve
  now (Ch8, Ch13) or are intended lateral references to this same Part-V wave (Ch20 `@thm-aggregation`,
  `@thm-log-link-mgf`, `@thm-logit-no-closed-form`; Ch22 `@thm-koksma-hlawka`, `@thm-mc-rmse`,
  `@def-sobol-net`, `@thm-inverse-cdf`, `@def-gaussian-copula`, `@thm-hypercube-integration`; Ch23
  `@thm-target-population-integral`, `@thm-mlnmr-generalizes-nma`), matching the orchestrator slug map.

## Verification performed

- Div fences balanced (54 open / 54 close). 14 `.proof` blocks, each closing with exactly one `$\square$`
  (14 `\square`). 30 cross-referenceable divs, each with a `## Name` title line.
- All 6 owned slugs present. No capital letters in any div slug or equation label (5 capitalized eq labels
  renamed to lowercase: `wb, vhat, ew, eb, pd`, with their references updated).
- No dangling `@eq-comp-*`, `@sec-comp-*`, or own-div references. No `@sec-notation`/`@sec-preface` misuse;
  `[Notation](/notation.qmd)` used twice.
- No dash-as-connector punctuation (em/en/spaced-hyphen/double-hyphen). American spelling throughout
  (British-spelling sniff clean; only false positives on "optimism/optimistic"). Two starred exercises
  present. `@carpenter2017stan` cited.
- Two `thm-dic-waic-loo` fence and one in-math `\ref` bugs found and fixed during validation.
