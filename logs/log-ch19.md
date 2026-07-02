# Work log: Chapter 19, Simulated Treatment Comparison

Author pass by the Ch19 agent. File written: `chapters/part4/19-stc.qmd` (stub removed, YAML title
preserved). Chapter length about 8,800 words; 10 proved results, 1 fully worked numerical example plus one
in-text closed-form computation, 8 exercises (2 starred for Appendix F).

## Sources consulted

- `~/Documents/GitHub/ITC_Coq/proofs/G_stc.md` (catalogue G.1 to G.7): the base draft. Every sketch was
  expanded into a complete proof in the book's notation. The catalogue's "generic Jensen is not quite
  right" warning for G.2 was honored: the plug-in bias is proved by a second-order Taylor expansion of
  $g^{-1}\circ\eta_k$ with Lagrange remainder at the arm level, then assembled into the contrast
  decomposition `@eq-stc-contrastbias`. The log-link Gaussian closed form (catalogue G.2 Step 5) became
  `@exm-stc-loglink`, extended to show the rate-ratio contrast is collapsible iff
  $\boldsymbol\beta_1^\top\boldsymbol\Sigma\boldsymbol\beta_2+\tfrac12\boldsymbol\beta_2^\top\boldsymbol\Sigma\boldsymbol\beta_2=0$.
- `~/Documents/GitHub/ITC_Coq/manuscript/09_stc.md` (companion prose): used for narrative framing (the
  MAIC/STC duality, the conditional-vs-marginal choice, the strengths/weaknesses table) and for the
  non-collapsibility worked example structure (Section 9.6).
- `~/Documents/GitHub/ITC_Coq/theories/STC.v`: read in full. Confirmed `Theorem STC_consistent` (line 333),
  `Lemma STC_collapse_linear` (line 250), `Theorem STC_unbiased` (alias, line 348), `Lemma E2_sub`. The
  definitions `mu_A_STC`, `mu_C_STC`, `effect_AC_STC` (marginal, response scale) and
  `effect_AC_STC_conditional` (plug-in at mean) match `@def-stc-marginal` and `@def-stc-conditional`.
- `~/Documents/GitHub/ITC_Coq/theories/Comparison.v`: read in full. Confirmed
  `Theorem methods_agree_when_correct` (line 408), `Lemma MAIC_variance_inflation_ge1` (line 442),
  `Theorem MAIC_robust_to_outcome_model`, `Theorem STC_robust_to_poor_overlap`. The method-profile records
  informed the STC-vs-MAIC trade-off remark.
- `~/Documents/GitHub/ITC_Coq/theories/OutcomeRegression.v`: read for the g-computation correspondence
  (`mu1_OR`, `ATE_OR`, `Theorem mu1_OR_unbiased`, `Corollary ATE_OR_unbiased`, `Lemma ATE_as_averaged_CATE`).
  Not tagged here (these are Ch10's `@thm-g-computation-unbiased`); cited in prose as the source-population
  analogue of marginal STC.
- `~/Documents/GitHub/ITC_Coq/theories/MAIC.v`: read for the entropy-balanced exponential-weight structure
  (`maic_weight_fn`, `moment_balance`, `ESS_upper_bound`) used in `@thm-maic-stc-equivalence`.
- Sibling chapter for voice and exact slugs/equations: `chapters/part3/14-bucher.qmd` (link-position
  machinery `@eq-bucher-eta`, `@def-marginal-link-position`, Bucher unbiasedness, transitivity, constancy,
  index-order remark, the worked-example arithmetic style with five-decimal hand checks).
- `notation.qmd` and `logs/STYLE.md` for the authoring contract; `logs/log-ch16.md` for the cross-chapter
  conventions and the proposed-notation status.
- Citations used (all keys verified present in `references.bib`): `@caro2010stc`, `@phillippo2019thesis`,
  `@phillippo2016tsd18`, `@chandler2026transport`, `@phillippo2020mlnmr`, `@hernan2020whatif`,
  `@rosenbaum1983`, `@mccullagh1989glm`, `@vandervaart1998`.

## Catalogue coverage (owns G.1 to G.7)

- G.1: `@thm-stc-outcome-mle` (MLE consistency + asymptotic normality). Expanded from a one-line citation
  into a full proof that *verifies the hypotheses* of the master theorem `@thm-mle-asymptotic-normality`
  (identifiability via design rank, mean-zero score under correct specification, information equality,
  exponential-family concavity, CLT + Slutsky), then invokes it. Misspecification/sandwich remark added via
  `@def-sandwich-variance`.
- G.2: `@thm-conditional-stc-bias` (plug-in bias). Full proof: arm-level Taylor/Jensen gap `@eq-stc-taylor`,
  contrast-bias decomposition `@eq-stc-contrastbias`, identity-link exactness. Uses `@def-non-collapsibility`,
  `@def-conditional-effect`, `@def-marginal-effect`.
- G.3: `@thm-marginal-stc-unbiased` (marginal STC consistency). Full proof via uniform convergence of fitted
  means on bounded support + continuous mapping; identified as transported g-computation in `@prp-stc-gcomp`
  (links to `@thm-g-computation-unbiased`, `@thm-conditional-transportability`). MACHINE-CHECKED tag.
- G.4: `@thm-stc-noncollapsibility-counterexample` (closed-form OR counterexample). Full arithmetic proof,
  pen-and-paper; collapsible boundary isolated as `@prp-stc-linear-collapse` (MACHINE-CHECKED). Uses
  `@thm-noncollapsibility-or-hr`, `@def-collapsibility`.
- G.5: `@thm-bayesian-g-computation`. Full proof of the pushforward + Monte Carlo parts; frequentist
  calibration via Bernstein-von Mises (cited, `@vandervaart1998`) + delta method (`@thm-delta-method`).
- G.6: `@thm-stc-consistency` (anchored + unanchored). Proof combines G.3 with the Chapter 17 PAIC
  conditions `@thm-anchored-paic-consistency`, `@thm-unanchored-paic-consistency`,
  `@def-conditional-constancy-relative`, `@def-conditional-constancy-absolute`; parallels MAIC
  `@thm-anchored-maic-consistency`, `@thm-unanchored-maic-consistency`.
- G.7: `@thm-maic-stc-equivalence` (linear-model equivalence). Full proof both directions to a common limit;
  uses `@thm-maic-exponential-weights`, `@def-moment-balance`, `@def-entropy-balancing`. Abstract
  joint-validity corollary `@cor-maic-stc-agree` (MACHINE-CHECKED). Breakdown remark (nonlinear link,
  higher moments, nonlinear interactions).

## Slugs defined (owned, all 7 present and verified)

`thm-stc-outcome-mle`, `thm-conditional-stc-bias`, `thm-marginal-stc-unbiased`,
`thm-stc-noncollapsibility-counterexample`, `thm-bayesian-g-computation`, `thm-stc-consistency`,
`thm-maic-stc-equivalence`.

## Helper slugs introduced (new, globally unique, topic-namespaced; flagged for the orchestrator)

Definitions: `def-stc-outcome-model`, `def-stc-conditional`, `def-stc-estimands`, `def-stc-marginal`,
`def-stc-bayes`. Results: `prp-stc-gcomp`, `prp-stc-linear-collapse`, `cor-maic-stc-agree`. Worked items:
`exm-stc-logistic`, `exm-stc-loglink`. Exercises: `exr-stc-recompute`, `exr-stc-em-shift`,
`exr-stc-identity-exact`, `exr-stc-gcomp-positivity`, `exr-stc-noncollapsibility-sign`,
`exr-stc-loglink-cancellation` (starred, Appendix F), `exr-stc-delta` (starred, Appendix F),
`exr-stc-maic-numeric`. Section slugs: `sec-stc-intro`, `sec-stc-outcome-model`, `sec-stc-mle`,
`sec-stc-conditional`, `sec-stc-marginal`, `sec-stc-noncollapsibility`, `sec-stc-example`, `sec-stc-bayes`,
`sec-stc-consistency`, `sec-stc-maic-equivalence`, `sec-stc-notes`, `sec-stc-exercises`. Equation labels:
`eq-stc-linpred`, `eq-stc-condmean`, `eq-stc-cate-link`, `eq-stc-loglik`, `eq-stc-score`, `eq-stc-mle-an`,
`eq-stc-cond`, `eq-stc-armmean`, `eq-stc-marg-estimand`, `eq-stc-cond-estimand`, `eq-stc-armgap`,
`eq-stc-taylor`, `eq-stc-contrastbias`, `eq-stc-marg-mean`, `eq-stc-marg`, `eq-stc-mc`,
`eq-stc-marg-consistency`, `eq-stc-functional`, `eq-stc-linear-collapse`, `eq-stc-maic-equiv`.

## Machine-checked tags added (all confirmed by reading the .v files)

1. `@thm-marginal-stc-unbiased` -> `theories/STC.v`, `Theorem STC_consistent`. The Coq theorem proves the
   response-scale contrast identity `effect_AC_STC = E2 Y_A_target - E2 Y_C_target` from the two per-arm
   transported g-computation premises; the link transformation by `g` and the uniform-convergence step are
   the pen-and-paper additions. Scope explained in a remark and in Notes.
2. `@prp-stc-linear-collapse` -> `theories/STC.v`, `Lemma STC_collapse_linear`. Proves marginal STC equals
   the treatment coefficient under a linear model using only linearity of the abstract target expectation.
   This is the collapsible boundary of the non-collapsibility theorem G.4; the G.4 counterexample itself is
   left pen-and-paper (it is a numerical witness, not an algebraic identity), as is honest given the Coq
   file's scope.
3. `@cor-maic-stc-agree` -> `theories/Comparison.v`, `Theorem methods_agree_when_correct`. The logical core
   of the MAIC-STC equivalence: from the two identification premises, the two estimates coincide.

## Cross-references to siblings (all owned, verified-present, or same-wave map slugs)

- Ch5: `@thm-mle-asymptotic-normality`, `@def-sandwich-variance` (given). `@thm-delta-method` verified via
  usage in `chapters/part3/14-bucher.qmd`.
- Ch7: `@def-link-function`, `@def-non-collapsibility` (given).
- Ch10: `@thm-g-computation-unbiased` (given).
- Ch11: `@def-effect-modifier`, `@def-prognostic-variable`, `@def-collapsibility`, `@def-conditional-effect`,
  `@def-marginal-effect`, `@thm-noncollapsibility-or-hr` (given).
- Ch12: `@def-transportability`, `@thm-conditional-transportability` (given).
- Ch14: `@def-transitivity`, `@thm-bucher-unbiased`, `@def-constancy-relative-effects` (given);
  `@eq-bucher-eta` verified present in `14-bucher.qmd` (`@def-marginal-link-position`).
- Ch16: `@thm-failure-of-bucher` (given).
- Ch17 (same wave, currently stub): `@def-conditional-constancy-relative`, `@def-conditional-constancy-absolute`,
  `@thm-anchored-paic-consistency`, `@thm-unanchored-paic-consistency`. From the wave slug map; resolve once
  Ch17 is authored.
- Ch18 (same wave, currently stub): `@def-moment-balance`, `@def-entropy-balancing`,
  `@thm-maic-exponential-weights`, `@thm-anchored-maic-consistency`, `@thm-unanchored-maic-consistency`,
  `@thm-maic-ess-bound`, `@thm-maic-no-extrapolation`. From the wave slug map; resolve once Ch18 is authored.
- Chapters 20 and 26 referenced in prose only (no `@sec-` to unwritten chapters), per the dash-free,
  name-the-chapter convention.

## New notation used (NOT added to notation.qmd; for the orchestrator to fold in or confirm)

- `\eta_k(\mathbf x;\boldsymbol\xi)`, `\mu_k(\mathbf x;\boldsymbol\xi)`: the arm-$k$ linear predictor and
  fitted conditional mean as explicit functions of the parameter; consistent with the notation table's
  `\eta_{ijk}`, `\theta_{ijk}=g^{-1}(\eta_{ijk})`, with study index suppressed for a single IPD trial.
- Intercept written `\alpha` (matching the Ch11 model `@eq-emcoll-model`, per the Ch16 log) to avoid
  clashing with the conditional-mean function `\mu_k(\cdot)`; the notation table's baseline symbol `\mu_j`
  is the same object with `j` suppressed.
- `\boldsymbol\beta_{(k)}` for the arm-$k$ covariate slope (`\boldsymbol\beta_1` for $C$,
  `\boldsymbol\beta_1+\boldsymbol\beta_2` for $A$); local, used in the Taylor/Gaussian computations.
- `d^{\mathrm{marg}}_{AC(\mathcal P)}` and `d^{\mathrm{cond}}_{AC(\mathcal P)}` for the marginal and
  conditional-at-the-mean relative effects (`@def-stc-estimands`). The marginal one equals the existing
  notation-table `d_{ab(\mathcal P)}`; the conditional-at-the-mean one is the local symbol this chapter
  needs. If the orchestrator prefers the Ch16-proposed `\Delta^{\mathrm{Marg},g}` / `\tilde d` family, these
  can be aligned in the harmony pass.
- `\ell_{AC}:=\eta_A-\eta_C` for the active-versus-reference log odds-ratio, used to keep the worked
  arithmetic in positive numbers; explicitly related to the reference-first `d_{AC}=-\ell_{AC}` of Ch14.
- `\hat\mu_A^{\mathrm{STC}}`, `\hat\mu_C^{\mathrm{STC}}`: taken directly from the notation table
  (`\hat\mu_t^{\mathrm{STC}}`).
- `\Psi(\boldsymbol\xi)`: the STC functional (`@eq-stc-functional`); local.

No conflicting symbols introduced. No bibliography additions needed; all nine citation keys were already in
`references.bib`.

## Decisions and ordering

- Sign convention. The book/Ch14 uses reference-first `d_{AC(\mathcal P)}=\eta_{C}-\eta_{A}`, while the STC
  literature and the GLM treatment coefficient use active-first `\gamma+\mathbf x^\top\boldsymbol\beta_2`.
  Rather than redefine `d_{AC}` (which would break the Bucher consistency equation referenced from Ch14), I
  kept the reference-first `d` for all named relative effects and added one index-order remark (mirroring
  Ch14's) reconciling the two; the worked arithmetic is carried in the positive active-orientation `\ell`
  and the global sign is flagged as immaterial to every bias/consistency/non-collapsibility statement, each
  of which is a single-arm or contrast statement on a fixed scale.
- G.4 worked counterexample uses the catalogue's Bernoulli logistic numbers (conditional 1.5, marginal
  1.22707) to isolate non-collapsibility in a single population. The chapter's main worked example
  `@exm-stc-logistic` is a distinct, fuller STC *pipeline* (fit on source $\Pr(X{=}1){=}0.5$, transport to
  target $0.8$) producing three contrasting numbers: conditional plug-in 1.50000, target marginal 1.44261,
  source marginal 1.41515 (all recomputed to five decimals by hand; see self-checks).
- G.1 is proved by verifying the hypotheses of the Chapter 5 master theorem and invoking it, which is the
  rule-6-compliant treatment for an asymptotic result whose general form is a stated prerequisite. The
  sandwich/pseudo-true behavior under misspecification is given as a remark, since it is the load-bearing
  caveat for STC.
- Two starred exercises for Appendix F: `exr-stc-loglink-cancellation` (clean iff condition for log-link
  contrast collapsibility) and `exr-stc-delta` (delta-method variance of the STC functional, with the
  sandwich extension), both with closed-form solutions.

## Gaps left for review

1. `@def-conditional-constancy-relative`, `@def-conditional-constancy-absolute`,
   `@thm-anchored-paic-consistency`, `@thm-unanchored-paic-consistency` (Ch17) and the Ch18 MAIC slugs resolve
   only once those same-wave chapters are authored. All are taken from the wave slug map. Expected, not an
   error (mirrors the Ch15/Ch16 situation noted in `log-ch16.md`).
2. The conditional-at-the-mean estimand symbol `d^{\mathrm{cond}}` and the active-orientation `\ell` are
   local; if the orchestrator folds the Ch16-proposed `\Delta^{\mathrm{Cond},g}` / `\tilde d` family into
   `notation.qmd`, the harmony pass may wish to align this chapter's symbols with them.
3. The machine-checked tag on `@thm-marginal-stc-unbiased` covers the response-scale contrast identity, not
   the link transformation or the uniform-convergence limit; scope is stated explicitly in the proof remark
   and in Notes. A reviewer may prefer to move the tag onto a bare response-scale restatement; flagged for
   the harmony pass. The G.4 counterexample carries no tag by design (only its collapsible boundary
   `@prp-stc-linear-collapse` is machine-checked).

## Self-checks run

- Div fences balanced: 47 openers, 47 bare closers (94 `:::` lines). 10 `.proof` blocks, 10 `$\square$`
  endings. 19 `$\blacktriangleleft$` closers (5 definitions, 2 examples, 12 remarks).
- No dash punctuation as connector or parenthetical anywhere; the only `---` lines are the two YAML
  delimiters. American spelling throughout (grep for behaviour/colour/-ise/modelling/centre/etc. clean).
- Every `@`-citation resolves to a key in `references.bib` (9/9 OK). Every cross-reference resolves to an
  owned slug, a verified sibling slug, or a same-wave map slug; the five `@eq-stc-outcome-model` typos were
  corrected to `@def-stc-outcome-model`. No proof-catalogue prerequisite codes (A.x, B.x, ...) left in prose;
  only the owned `G.1`-`G.7` identifiers remain, in the roadmap and "corresponds to G.n" parentheticals.
- All three machine-checked tags re-confirmed against the `.v` files by exact theorem/lemma name.
- Worked example recomputed by hand at five decimals: `expit(-1)=0.26894`, `expit(0.5)=0.62246`,
  `expit(1.5)=0.81757`; target marginals `0.45379`, `0.77855` give `logit` `-0.18538`, `1.25723`, contrast
  `1.44261`; source marginals `0.38447`, `0.72002` give contrast `1.41515`; conditional plug-in `1.5`
  exactly; non-collapsibility gap `0.05739`; back-transformed odds ratios `4.4817`, `4.2317`, `4.1171`. G.4
  counterexample verified: `0.5` and `0.773301` give marginal log-OR `1.22707` against conditional `1.5`,
  gap `0.27293`.
