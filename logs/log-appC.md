# Work log: Appendix C, Probability Distributions

File authored: `appendices/C-distributions.qmd` (stub overwritten; YAML title kept, stub callout dropped).

## Scope and classification

Per the STYLE.md rule set, Appendix C is a *reference* appendix (precise reference material, not a
proof catalogue). It therefore owns no proof-catalogue identifiers; it restates results that are derived
and owned by Chapters 4 and 8 and adds the further families used later in the book. Every formula was
checked for correctness; nothing is asserted without either a derivation in a referenced chapter or a
one-line elementary calculation, and the catalogue means/variances were numerically sanity-checked.

## Sections written

- `sec-dist-conventions`: MGF recap (refs `def-mgf`, `thm-mgf-moments`, `thm-mgf-uniqueness`), gamma
  function `eq-dist-gamma-function`, beta function `eq-dist-beta-function`, parametrization conventions.
- `sec-dist-discrete`: table `tbl-dist-discrete` (Bernoulli, binomial, Poisson binomial, Poisson).
- `sec-dist-continuous`: table `tbl-dist-continuous` (normal, exponential, gamma, beta, Weibull), plus
  beta MGF `eq-dist-beta-mgf` and the Weibull hazard-parametrization remark.
- `sec-dist-mvn`: table `tbl-dist-mvn` and closure properties, all referencing Chapter 4 by slug.
- `sec-dist-dirichlet`: `def-dist-dirichlet`, density `eq-dist-dirichlet-density`, moments
  `eq-dist-dirichlet-moments`, table `tbl-dist-dirichlet`.
- `sec-dist-standard-normal`: phi/Phi `eq-dist-phi`, identities `eq-dist-phi-derivs`, moments
  `eq-dist-normal-moments`, erf form `eq-dist-Phi-erf`, Mills bound `eq-dist-mills`.
- `sec-dist-conjugacy`: table `tbl-dist-conjugacy` (the three Chapter 8 pairs plus Dirichlet-multinomial).
- `sec-dist-notes`.

## References and sections consulted

- `@billingsley1995` (Probability and Measure, 3rd ed.), cited for the measure-theoretic foundations and
  for §29 to §30 (MGF / characteristic-function inversion and uniqueness). Already in `references.bib`.
- Chapter 4, `chapters/part1/04-probability.qmd`: `sec-distributions`, `sec-mvn`; `def-bernoulli`,
  `def-binomial`, `def-poisson-binomial`, `def-poisson`, `def-normal`, `def-mvn`, `prp-mvn-density`,
  `thm-mvn-linear`, `lem-normal-uncorrelated-independent`, `thm-mvn-conditional`, `def-mgf`,
  `thm-mgf-moments`, `thm-mgf-uniqueness`, `thm-mgf-sum`, `thm-poisson-limit`, and equations
  `eq-mvn-mgf`, `eq-mvn-density`, `eq-mvn-conditional`. All MVN results referenced by slug as instructed.
- Chapter 8, `chapters/part1/08-hierarchical-bayes.qmd`: `sec-conjugacy`; `thm-conjugate-normal`,
  `cor-conjugate-normal-mv`, `thm-conjugate-beta-binomial`, `prp-conjugate-gamma-poisson`, and equations
  `eq-conjugate-normal`, `eq-conjugate-beta`. These are the conjugacy pairings the task asked me to note.
- Chapter 25, `chapters/part5/25-general-likelihoods.qmd`: `sec-genlik-survival` (exponential and
  Weibull hazard parametrization), `@phillippo2025general` (already in `references.bib`).
- Chapter 26, `chapters/part5/26-ml-umr.qmd`: survival baseline families (exponential, Weibull, gamma).

All 35 outbound cross-references were verified to resolve against existing `{#slug}` anchors.

## Decisions

1. **Parametrizations fixed to match the chapters.** Gamma and exponential use the shape-rate
   convention so `Gamma(a,b)` has mean `a/b`, matching `prp-conjugate-gamma-poisson`. Weibull uses the
   standard shape-scale form (clean Gamma-function moments) with an explicit remark converting to
   Chapter 25's hazard form S(t)=exp(-lambda t^nu): shape k=nu, scale lambda=lambda(x)^(-1/nu).
2. **MGF "where it exists" made explicit.** Domains given for exponential (t<lambda) and gamma
   (t<beta). Beta MGF stated as the confluent hypergeometric 1F1(a;a+b;t) with the note that it has no
   elementary closed form (moments are elementary, formula given). Weibull MGF: no elementary form and
   finite near 0 only for shape k>=1 (for k<1 it does not exist, though all polynomial moments do).
   Dirichlet MGF is degenerate because the support lies in the hyperplane sum=1; characterized by the
   mixed-moment formula instead.
3. **Dirichlet-multinomial conjugacy** included as the K-category generalization of beta-binomial, but
   flagged as "generalizes `thm-conjugate-beta-binomial`" rather than attributed to Chapter 8, which
   proves only the K=2 case.
4. **Table markup safety.** Used `\lvert ... \rvert` (Poisson binomial pmf) and `\mid` (conditioning)
   inside table cells to avoid literal `|` characters that would break markdown tables. Verified every
   table row has balanced `$` and consistent column counts.
5. **Appendix D pointer** given as a plain link `[Appendix D](/appendices/D-special-functions.qmd)` for
   the numerical evaluation of Gamma, B, and erf (mirrors the recommended `[Notation](/notation.qmd)`
   pattern); avoided a `@sec-`/`@thm-` ref because Appendix D is still a stub.

## Numerical sanity checks (all passed)

Beta(2,3) mean 0.4 / var 0.04; Gamma(3,2) mean 1.5 / var 0.75; Weibull(2,1) mean 0.8862 / var 0.2146;
standard-normal even moments 1, 3, 15 = (2m-1)!!; Dirichlet(2,3,5) means, var, cov; Poisson binomial
p=(0.2,0.5,0.8) pmf sums to 1 with mean 1.5 matching both the closed form and the pmf.

## Proposed notation additions (for the orchestrator to fold into `notation.qmd`)

These distribution symbols are used by Appendix C and are not yet listed in `notation.qmd`. Several are
already used de facto in Chapters 8, 25, 26.

| Symbol | Meaning |
|---|---|
| `\mathrm{Exp}(\lambda)` | exponential, rate lambda |
| `\mathrm{Gamma}(\alpha,\beta)` | gamma, shape alpha and rate beta (already used in Ch 8) |
| `\mathrm{Beta}(a,b)` | beta on (0,1) (already used in Ch 8) |
| `\mathrm{Weib}(k,\lambda)` | Weibull, shape k and scale lambda |
| `\mathrm{Dir}(\boldsymbol{\alpha})` | Dirichlet on the simplex |
| `\mathrm{Multinomial}(N,\mathbf{p})` | multinomial (used in Dirichlet conjugacy row) |
| `\Gamma(s)`, `B(a,b)`, `B(\boldsymbol{\alpha})` | gamma function and (multivariate) beta function |
| `\mathrm{erf}`, `\mathrm{erfc}` | error function and its complement |
| `{}_1F_1(a;c;t)`, `(c)_n` | confluent hypergeometric function, Pochhammer symbol |
| `\Delta^{K-1}` | open probability simplex in R^K |
| `(2m-1)!!` | double factorial |

## Gaps left for review

- **Multinomial not formally defined.** The Dirichlet-multinomial conjugacy row references the
  multinomial, which appears only in passing in the book (Ch 8 MCMC prose). If the orchestrator wants a
  formal anchor, a one-line multinomial definition could be added to `notation.qmd` or Chapter 4; the
  appendix currently treats it as standard. No change needed for correctness.
- **Appendix D cross-references.** Once `D-special-functions.qmd` is authored, the plain links to it for
  Gamma / B / erf evaluation could be upgraded to slug cross-references.
- No new bibliography entries required: `billingsley1995` and `phillippo2025general` are both present.
