# Polish: notation mirroring and bibliography folding

Deferred consistency-pass items, applied on branch `add-notation-and-bibliography-entries`.
Scope was limited to `notation.qmd` and `references.bib`; no chapter or appendix prose was edited and no
new `@citekey` was inserted into prose, so the render stays clean.

## notation.qmd

Two additive blocks, both taken from proposals in the per-chapter and appendix work logs and from
Appendix A:

1. Linear algebra and matrices table: added seven rows proposed by the foundations chapters (orthogonal
   complement of a subspace; weighted inner product and its induced norm; negative definiteness; the
   symmetric positive semidefinite square root; the characteristic polynomial; the spectrum and
   eigenspace; the Frobenius inner product with the operator and Frobenius norms).
2. New subsection "Bayesian computation and model comparison", mirroring the symbols catalogued in
   Appendix A (`@tbl-gloss-bayes`) that had no home in the Notation chapter: prior and posterior density,
   likelihood, prior probability measure, between-study heterogeneity variance, the Gelman-Rubin
   statistic, the MCMC effective sample size, the DIC deviance pieces, lppd and elpd-hat, WAIC and LOO,
   and PSIS with its tail-index diagnostic.

No existing symbol row was removed or renamed. All new math is ASCII and balanced.

## references.bib

Added the six matrix-calculus references that Appendix B currently attributes by author name only
(proposed in `logs/log-appB.md`): `magnus2019matrix`, `petersen2012cookbook`, `harville1997matrix`,
`sherman1950adjustment`, `woodbury1950inverting`, `horn2012matrix`. These are canonical texts with
verifiable bibliographic data. Entry count 35 to 41; no duplicate keys.

The entries are available for future `@key` citation; the Appendix B Notes prose still attributes them by
name, so nothing is cited-but-undefined and the build stays clean. Converting that prose to `@key` form
is left as an optional follow-up.

## Deliberately deferred

The two Appendix E "in preparation" sources (`logs/log-appE.md`: a Remiro-Azocar doubly-robust method and
a Ren NORTA copula method) were NOT added. Both are described as in preparation, so a full BibTeX entry
would require guessing a venue and year; the honest by-name attribution already in the appendix is better
than an invented citation. Add these once their primary sources are finalized.
