# Work log: Chapter 23 — ML-NMR IV: Estimands, Identifiability, and Generality

File authored: `chapters/part5/23-mlnmr-estimands.qmd` (overwrote stub; kept YAML title).

## Sources consulted
- `ITC_Coq/proofs/H_ml_nmr.md`, results H.20 (target-population estimand integral), H.21
  (two-study identifiability under SEMA), H.22 (larger-network identifiability), H.23 (ML-NMR
  generalizes NMA / IPD-NMR / MAIC / STC). These are the catalogue results this chapter owns.
- `ITC_Coq/manuscript/10_ml_nmr.md`, sections 10.20–10.23 (the base draft for the four owned results)
  and 10.24 (confirms there is **no** Coq counterpart for ML-NMR).
- `ITC_Coq/proofs/D_network_meta_analysis.md`, D.8 (graph-incidence-rank NMA identifiability) and
  D.12 (IPD-NMR identifiability), used as the identified building blocks for H.21/H.22.
- Sibling chapters for exact cross-reference slugs and voice:
  - Ch4 `@thm-jensen`; Ch7 `@def-non-collapsibility`; Ch8 `@def-exchangeability`,
    `@def-random-effects`, `@thm-conjugate-normal`; Ch11 `@def-effect-modifier`,
    `@def-prognostic-variable`; Ch14 `@thm-bucher-unbiased`; Ch15 `@thm-fe-nma-identifiability`,
    `@thm-ipd-nmr-identifiability`; Ch16 `@def-ecological-bias`;
    Ch17 `@thm-target-population-estimand` (E.12), `@def-sema` (E.8),
    `@def-conditional-constancy-relative`, `@def-conditional-constancy-absolute`,
    `@thm-shared-em-identifiability`, `@prp-testable-untestable-constancy`;
    Ch18 `@thm-anchored-maic-consistency`, `@thm-unanchored-maic-consistency`;
    Ch19 `@thm-stc-consistency`, `@thm-marginal-stc-unbiased`, `@thm-maic-stc-equivalence`.
  - Same-wave Part V siblings referenced by their assigned slugs: Ch20 `@def-individual-model`,
    `@def-aggregate-model`, `@thm-aggregation`, `@thm-aggregation-bias`, `@thm-identity-link-exact`;
    Ch22 `@thm-hypercube-integration`.
- Primary citation `@phillippo2020mlnmr` and `@phillippo2019thesis` (thesis §4.4–4.7); `@dias2018nma`
  for the NMA reductions.

## Catalogue identifiers covered
- H.20 → `@thm-target-population-integral` (owned)
- H.21 → `@thm-mlnmr-identifiability-2study` (owned)
- H.22 → `@thm-mlnmr-identifiability-large` (owned)
- H.23 → `@thm-mlnmr-generalizes-nma` (owned)

Each owned theorem carries an explicit "(corresponds to H.xx in the proof catalogue)" line.

## Slugs defined in this chapter
Owned theorems:
- `thm-target-population-integral`
- `thm-mlnmr-identifiability-2study`
- `thm-mlnmr-identifiability-large`
- `thm-mlnmr-generalizes-nma`

Supporting (new, topic-namespaced `mlnmr-…`; checked against the slug map for collisions, none found):
- `def-mlnmr-target-contrast` (marginal and conditional target-population contrasts)
- `lem-mlnmr-surface-transport` (network-level surface is population-free; relative-effect surface is
  baseline-free)
- `lem-mlnmr-aggregate-monotone` (strict monotonicity of an aggregate mean in a scalar shift; the
  workhorse for AgD identification)
- `prp-mlnmr-sema-necessary` (without SEMA the two-study target contrast is non-identified off the
  comparator population)
- `cor-mlnmr-exchangeable` (exchangeable / treatment-class EM as extensions of the shared-EM theorem)
- `exm-mlnmr-new-target` (worked example: population-adjusted estimate in a new target)
- Equation labels namespaced `eq-mlnmr-est-…`.
- Exercises `exr-mlnmr-…`; starred for Appendix F: `exr-mlnmr-sema-gap` and `exr-mlnmr-stc-reduction`.

## Machine-checked tags
None. Confirmed `ITC_Coq/theories/` has no `ML_NMR.v` (or any aggregation/NMR file); manuscript
§10.24 states ML-NMR is deliberately not formalized in the Coq tree. Per the authoring brief
("Part V results are mostly computational; tag only if present"), no `[machine-checked: …]` tags were
added.

## Proposed notation / bibliography additions
- No new bibliography entries required; all citations (`@phillippo2020mlnmr`, `@phillippo2019thesis`,
  `@dias2018nma`) are present in `references.bib`.
- No new notation symbols beyond what `notation.qmd` already fixes. I reuse `\bar\theta_t(\mathcal P^*)`
  as the target arm mean (an instance of the aggregate mean `\theta_{\bullet jk}` already in the
  outcome-models table) and `f_*` as shorthand for `f_{\mathcal P^*}`; both are defined inline on first
  use, so no global addition is strictly needed. If the orchestrator prefers a global symbol for the
  target arm mean, suggest adding `\bar\theta_{t}(\mathcal P)` to the "Outcome models and likelihoods"
  table; left out of scope here per file discipline.

## Decisions
- Sign convention: I use the book/Notation convention `d_{ab(\mathcal P)}` = marginal effect of `b`
  versus `a` = `g(\bar\theta_b) - g(\bar\theta_a)`, matching Ch17 `@eq-pat-target-marg`. The catalogue
  H.20 display writes the same difference; I flagged the convention explicitly so the worked-example
  signs are unambiguous, and verified the anchored identity `d_{BA} = d_{CA} - d_{CB}` numerically.
- H.20 is stated as a theorem (identification + integral form + collapsibility dichotomy + computation),
  realized as the ML-NMR instance of E.12 (`@thm-target-population-estimand`), rather than as a bare
  definition, to honor "prove everything."
- H.21: expanded the catalogue's one-line "AgD identifies `\gamma_B`" into a full argument via the new
  monotonicity lemma `lem-mlnmr-aggregate-monotone`, plus a rigorous non-identification proposition
  for the no-SEMA case (explicit binary-X two-point construction).
- H.22: gave a complete identification proof for the shared-EM case (three identified blocks:
  IPD→`beta1,beta2`; monotone aggregate/individual→per-arm intercepts; connectivity→treatment effects),
  then handled exchangeable EM by Bayesian identifiability (proper posterior; partial pooling via
  `@thm-conjugate-normal`) and treatment-class EM as a block version.
- H.23: split into exact reductions (NMA, IPD-NMR — model/likelihood collapse) and estimand/limit
  reductions (MAIC, STC), proving the STC reduction as an exact functional identity (the ML-NMR
  aggregate mean *is* the marginal STC predicted mean) and the MAIC reduction as estimand coincidence
  with exact estimator coincidence under a linear surface.
- Worked example: logit link, single binary effect modifier, SEMA; computed three targets to exhibit
  (i) integrating over a target covariate distribution, (ii) the conditional A-vs-B contrast pinned at
  `\gamma_A-\gamma_B` by SEMA while the marginal drifts via non-collapsibility, (iii) genuine
  population dependence of the A-vs-C estimate. All numbers verified by a Python script
  (`scratchpad/ex.py`) to six decimals.

## Gaps / for review
- The exchangeable-EM identifiability is stated in the Bayesian (proper-posterior) sense, which is the
  honest level; a frequentist rank statement is not available when AgD-only treatments carry single
  aggregate equations. Flagged in the text.
- Cross-references to Ch20/Ch22 use the assigned slugs of stubs being authored in parallel; if any
  sibling renames a slug, the consistency pass should reconcile (`@def-individual-model`,
  `@def-aggregate-model`, `@thm-aggregation`, `@thm-aggregation-bias`, `@thm-identity-link-exact`,
  `@thm-hypercube-integration`).
