# Revision log: Chapter 08, Hierarchical Models, Shrinkage, and Bayesian Inference

Reviewers: `feedback/chatgpt/ch08-hierarchical-bayes.md`, `feedback/glm/ch08-hierarchical-bayes.md`
(both read as a novice health researcher with weak mathematics). This chapter had already been partially
revised in an interrupted earlier pass (reader map, early running example `@exm-three-trials-early`, cast
table, measure-theory primer, terminology-reconciliation table, discrete Bayes example, several reader
translations). This pass added only what the feedback still asked for and was missing. No existing
theorem, proof, or label was removed or renamed; every addition is net-new. Verified: 74 unique labels,
no duplicates; `$$` count even (166); pure ASCII, no Unicode star (only `$\star$`); fenced divs balanced
95/95; no em/en/double-hyphen dash punctuation; no bare `align`/`equation`/`gather`.

## Highest-priority fixes addressed

### ChatGPT reviewer
1. **Bridges keeping ITC/health motivation visible after each hard section.** Added a "Why this matters"
   ITC line after normal-normal conjugacy (`@thm-conjugate-normal`); a numeric shrinkage table plus a
   "Why this matters" remark after `@thm-shrinkage-posterior-mean`; a "Why this matters" after
   James-Stein; a reader translation, a worked REML instantiation, and a "Why this matters" in the REML
   section; a practical "what draws mean / what to check" remark closing MCMC; and a physical-picture
   paragraph plus ITC touchstone opening HMC. (Exchangeability and de Finetti bridges were already
   present.)
2. **Fixed vs random vs fixed-effect vs complete-pooling terminology.** Already handled by the
   pre-existing terminology-reconciliation table after `@def-random-effects`; left as is.
3. **Simple applied Bayes example before the measure-theoretic proof.** Pre-existing
   `@exm-bayes-discrete` already does this; additionally added a beta-binomial event-count example
   `@exm-beta-binomial-early` immediately after `@thm-conjugate-beta-binomial` (also GLM suggestion 1).
4. **Expand de Finetti finite discussion.** Pre-existing intuition/finite paragraphs kept; added a
   martingale gloss inside the converse ("a running average that neither drifts up nor down") and the
   explicit reading that the latent parameter is the long-run success frequency.
5. **Clinically interpretable worked example.** Added an "on the odds-ratio scale" block to
   `@exm-three-study-shrinkage`: trial 3's raw OR 3.32 shrinks to 2.46, trial 1's credible interval
   converted to OR (0.67, 2.70), with a clinical sentence that shrinkage moved the point estimate without
   manufacturing certainty.
6. **Novice-friendly tau^2, Q, DerSimonian-Laird before the formula.** tau^2 intuition pre-existing;
   added a plain-language description of Cochran's Q and a full method-of-moments derivation as a new
   proposition `@prp-dl-moment` (proving E[Q] = (J-1) + tau^2 (sum w - sum w^2 / sum w)), with the
   truncation-at-zero consequence spelled out.
7. **Reframe MCMC/HMC around the practitioner's question.** Added the MCMC practical remark (posterior
   draws = jointly plausible parameter settings; trace = grassy caterpillar; check R-hat, effective
   sample size / Monte Carlo error, divergent transitions, prior sensitivity; theory vs run distinction)
   and the HMC landscape/momentum picture, plus an expanded funnel-geometry and divergent-transition
   explanation with the non-centered fix.

### GLM reviewer (its numbered suggestions)
1. Interleave numbers with theory: added the shrinkage taste table after the shrinkage theorem and the
   beta-binomial example after the conjugacy theorem (early example already threaded from the top).
2. Intuition + binary example before de Finetti: already present; kept.
3. Define or defer measure theory: primer + skim signposts already present; kept, and added the
   noncentral chi-square gloss where it was previously named but undefined.
4. ITC touchstones throughout: added "this is the update a Bayesian NMA performs" (conjugacy), "this is
   what metafor / multinma / Stan estimate for tau^2" (REML), "this is what runs when you call Stan"
   (HMC).
5. Expand DL derivation: `@prp-dl-moment` (see above).
6. Figures: real figures are out of scope for this text pipeline; substituted textual/tabular
   equivalents (raw-vs-shrunk OR table as a "forest plot in words," trace as a "grassy caterpillar,"
   funnel as a "trumpet bell," HMC as a puck rolling on the log-posterior landscape). Flagged as a
   deliberate limitation below.
7. Unify notation / gloss jargon: phi-vs-xi clarification pre-existing; added noncentral chi-square gloss
   inline; stackrel{d}{=}, kernel, delta_x, martingale already glossed inline. Remaining symbols flagged
   for notation.qmd below.
8. Soften James-Stein: proof preserved in full (hard constraint); foregrounded intuition via a "Why this
   matters" (frequentist license to pool with J >= 3, no prior needed) and clarified the coordinate
   conditioning step (fix the other coordinates, apply Stein's lemma in one variable, remove the
   conditioning by the tower property). The SURE alternative route already exists as `@exr-james-stein-sure`.
9. Posterior-predictive ITC example: expanded the remark after `@def-posterior-predictive` into a reader
   translation plus explicit ITC reading (a population-adjusted target-population effect is a posterior
   predictive quantity: draw parameters, push through the target covariate distribution).

## Task deliverables
- Early concrete example: pre-existing `@exm-three-trials-early`; now explicitly reused at the shrinkage
  transition (raw-vs-shrunk OR table referencing it).
- Reader translations added after definitions that lacked them: `@def-reml` (error contrast = residual
  space), `@def-detailed-balance` (flow x->y equals flow y->x), and an expanded reader translation for
  `@def-posterior-predictive`.
- "Why this matters" lines added after `@thm-conjugate-normal`, `@thm-shrinkage-posterior-mean`,
  `@thm-james-stein`, the REML development, and `@thm-mh-stationarity` (practical remark).
- Tables: added the raw-vs-shrunk odds-ratio shrinkage table. (Cast, health-object, terminology, and
  five-distributions tables were already present.)
- Exercises: added the one-line starred-exercise convention ("a starred exercise ($\star$) has a full
  worked solution in Appendix F") and two accessible warm-ups before the computational block,
  `@exr-interpret-shrinkage` (interpret shrinkage in words) and `@exr-or-interpretation` (log OR to a
  clinical odds-ratio statement).

## New labeled environments (all additive)
- `@prp-dl-moment` — DerSimonian-Laird as a method-of-moments estimator, with full proof of E[Q].
- `@exm-beta-binomial-early` — event-count beta-binomial update placed right after the conjugacy theorem.
- `@exr-interpret-shrinkage`, `@exr-or-interpretation` — two unstarred interpretation warm-ups (no
  Appendix F solution needed).
Also added several unlabeled `.remark` blocks (reader translations, "Why this matters," practical MCMC,
DL truncation note) and inline glosses; these are not cross-referenced.

## Notation to fold into notation.qmd (I must not edit notation.qmd; flagged for the orchestrator)
GLM flagged these as used-but-absent from `notation.qmd`; all are glossed inline in the chapter:
- `\stackrel{d}{=}` "equal in distribution" (glossed at `@def-exchangeability`).
- `\delta_x` Dirac point mass (glossed at `@thm-mh-stationarity`).
- `\boldsymbol\vartheta`, `\mathbf V(\boldsymbol\vartheta)` variance-parameter vector / covariance in REML.
- noncentral chi-square (now glossed inline in the James-Stein proof).
- `\hat R` potential scale reduction factor (glossed inline in the new MCMC remark).

## New sources cited in prose (author-year only, no bibtex key yet; consistent with the chapter's
existing practice of flagging un-keyed sources for merge)
- Hartung and Knapp (small-sample variance correction for random-effects meta-analysis), named once in
  the empirical-Bayes caution. Candidate entry: Hartung, J. and Knapp, G. (2001), "On tests of the
  overall treatment effect in meta-analysis with normally distributed responses," Statistics in
  Medicine 20(12):1771-1782. All other author-year mentions (DerSimonian-Laird, Patterson-Thompson,
  Harville, Metropolis, Hastings, Tierney, Hoffman-Gelman, Neal, Betancourt, Efron-Morris,
  James-Stein) were already present and already noted in the pre-existing Notes section / work log.
No new `@key` citations were introduced into the text; every `@...` citation used
(`@dias2018nma`, `@dersimonian1986`, `@carpenter2017stan`, `@strang2016`, `@bingham2010regression`)
was verified present in `references.bib`.

## Deliberately left unchanged
- All theorem/lemma/corollary/proposition statements and their proofs (rigor preserved per the hard
  constraint). The James-Stein proof was clarified, not shortened or moved to an appendix.
- The measure-theoretic Bayes proof `@thm-bayes` (kept; the pre-existing primer and skim signpost, plus
  `@exm-bayes-discrete`, already make it optional for the novice).
- The overall section order. GLM suggested physically relocating the consolidated worked example earlier;
  instead I interleaved short numeric illustrations (shrinkage table, early beta-binomial example) at the
  transitions and kept `@sec-hb-worked` as the consolidated "putting it together" section, which
  satisfies "numbers should appear before the end" without disturbing cross-references into that section.
- Real figures (shrinkage plot, funnel sketch, HMC trajectory, MCMC trace) were not added; the pipeline
  is text/LaTeX and the reviewers' figure requests were met with textual/tabular equivalents. Flagged
  here so a later illustration pass can add true figures if desired.
- `_quarto.yml`, `notation.qmd`, `references.bib`, and all other chapters: untouched.
