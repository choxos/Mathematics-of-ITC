# Work log: Chapter 05, Statistical Inference

Author pass by the Ch05 agent. File written:
`chapters/part1/05-inference.qmd` (overwrote the stub, kept YAML title "Statistical Inference").

## Sources consulted

- `logs/STYLE.md` (authoring contract: theorem-proof grammar, slug rules, cite-vs-prove rules).
- `notation.qmd` (single source of truth for symbols; used score `s`, Fisher info `I(theta)`,
  MLE `hat theta_MLE`, sandwich variance `V`, likelihood `L`/`ell`, convergence arrows, order symbols).
- `~/Documents/GitHub/ITC_Coq/manuscript/01_probability.md` (tail, sections 1.11-1.14) for alignment of
  the delta method, Slutsky, and continuous mapping theorem statements (catalogue A.11-A.13).
- `~/Documents/GitHub/ITC_Coq/proofs/A_probability_foundations.md` (A.11, A.12, A.13 full statements and
  sketch proofs; dependency table) and `proofs/00_concepts_index.md`.
- `references.bib`: cited `@bingham2010regression` (primary source for this chapter). Confirmed the key
  exists. No other key cited with `@` to avoid broken cross-references.

## Slugs defined (all the ones I own, plus supporting new ones)

Owned (all defined):
- `def-likelihood`, `def-score`, `def-fisher-information`, `thm-information-equality`, `def-mle`,
  `thm-mle-consistency`, `thm-mle-asymptotic-normality`, `thm-cramer-rao`, `thm-delta-method`,
  `thm-slutsky`, `thm-continuous-mapping`, `def-sandwich-variance`.

New supporting slugs I introduced (globally unique, topic-namespaced; none collide with the
cross-chapter slug map):
- Definitions: `def-statistical-model`, `def-estimator`, `def-consistent-estimator`,
  `def-regular-model`, `def-efficient-estimator`, `def-m-estimator`, `def-test-statistics`.
- Lemmas/cor/prp: `prp-bias-variance-decomposition`, `lem-score-mean-zero`,
  `cor-information-additivity`, `prp-mle-invariance`, `lem-kl-information-inequality`,
  `lem-uniform-lln`, `lem-argmax-consistency`, `cor-mle-efficient`, `thm-m-estimator-normal`,
  `cor-sandwich-collapse`, `thm-wilks`.
- Examples/exercises: `exm-binomial-inference`, `exm-sandwich-normal`, `exr-poisson-mle`,
  `exr-exponential-rate`, `exr-mse-shrinkage`, `exr-score-test-binomial`,
  `exr-information-equality-fail` (starred), `exr-sandwich-derivation` (starred),
  `exr-delta-multivariate`.
- Labeled equations: `eq-bias-variance`, `eq-score-def`, `eq-fisher-def`, `eq-info-equality`,
  `eq-delta-variance`, `eq-crlb-scalar`, `eq-crlb-matrix`, `eq-mle-asymptotic-normality`,
  `eq-an-system`, `eq-score-clt`, `eq-an-converges`, `eq-mle-linearization`,
  `eq-estimating-equation`, `eq-sandwich-asymptotic`, `eq-sandwich-estimator`, `eq-wald-stat`,
  `eq-score-stat`, `eq-lr-stat`.

## Cross-references to siblings (used the canonical slugs from the map)

- `@def-probability-space` (Ch04), `@thm-jensen` (Ch04), `@thm-cov-psd` (Ch04),
  `@thm-mvn-linear` (Ch04, see gap note), `@thm-cauchy-schwarz-ip` (Ch02).

## Catalogue identifiers covered

- A.11 delta method -> `thm-delta-method` (proved in full, multivariate via Cramer-Wold + Slutsky).
- A.12 Slutsky -> `thm-slutsky` (proved via joint convergence to a constant + continuous mapping).
- A.13 continuous mapping -> `thm-continuous-mapping` (proved for d/p/a.s. via Portmanteau).
- Plus chapter-owned MLE/Fisher/Cramer-Rao content per the STYLE assignment table for Ch05.

## Decisions

- Placed the asymptotic tools (CMT, Slutsky, delta) early (Section "Asymptotic tools"), before
  consistency and asymptotic normality, to respect dependency order: the MLE asymptotic-normality proof
  invokes Slutsky, CMT, and the CLT.
- Stated WLLN, the multivariate CLT, Portmanteau, and Cramer-Wold as cited prerequisites in a single
  `.remark` (they are routine probability facts per STYLE rule 6), citing `@bingham2010regression` and
  "a standard graduate probability text" in prose. The uniform law of large numbers
  (`lem-uniform-lln`) is also stated and cited, not proved, since it is a standard prerequisite; the
  load-bearing pieces of consistency (KL information inequality and the argmax lemma) are proved in full.
- Proved both the MLE asymptotic-normality theorem directly (variance = inverse Fisher information, using
  the information equality) and the general M-estimator theorem (sandwich variance), then showed the
  sandwich collapses to inverse information under correct specification via the information equality.
  This makes the MAIC reuse in Ch18 self-contained.
- Two starred exercises for Appendix F: `exr-information-equality-fail` (Uniform(0,theta), where
  regularity fails and the MLE is non-normal at rate n) and `exr-sandwich-derivation` (misspecified
  Poisson sandwich variance).

## Proposed additions for the orchestrator

- Notation: no new symbols needed; everything fit the existing table. I used `J_n(theta) = -nabla^2 ell_n`
  for the observed information and `widehat{V}` for the sandwich estimator (a hatted form of the
  existing `V` symbol). If desired, the orchestrator could add a one-line row for observed information
  `J_n` to the "Statistical inference" notation block, but it is defined inline where used.
- Bibliography: for the cited probability prerequisites (CLT, WLLN, Portmanteau, Cramer-Wold) and the
  Hajek-Le Cam convolution theorem, two specialized references would strengthen the citations if the
  orchestrator wishes to add them to `references.bib`:
  - van der Vaart, A. W. (1998). *Asymptotic Statistics*. Cambridge University Press.
    (proposed key `vandervaart1998asymptotic`)
  - Billingsley, P. (1995). *Probability and Measure*, 3rd ed. Wiley.
    (proposed key `billingsley1995probability`)
  I did not `@`-cite these (they are not yet in `references.bib`); I referenced them in prose only, so
  no cross-reference will break at render time.

## Gaps left for the consistency/harmony pass

- `@thm-mvn-linear` (affine image of a multivariate normal) is referenced per the chapter brief, but the
  Ch04 slug map in the assignment lists `thm-mvn-conditional`, `thm-jensen`, `def-mgf`, `thm-cov-psd`,
  `def-probability-space` and does NOT list `thm-mvn-linear`. The brief explicitly instructs referencing
  `@thm-mvn-linear`, so I used it. ACTION for harmony pass: confirm Ch04 defines a result with slug
  `thm-mvn-linear` (statement: if `Z ~ N_p(mu, Sigma)` then `AZ + b ~ N(A mu + b, A Sigma A^T)`); if Ch04
  names it differently, update the three references in this chapter
  (in `thm-delta-method`, `thm-mle-asymptotic-normality`, `thm-m-estimator-normal`). The surrounding
  prose states the property self-containedly so the math is correct regardless of how the ref resolves.
- No machine-checked tags added (none confirmed in `~/Documents/GitHub/ITC_Coq/theories/`). The
  information equality and the M-estimator sandwich are flagged in "Notes and references" as future
  formalization candidates.
