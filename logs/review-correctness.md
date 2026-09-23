# Correctness pass (mathematical and methodological)

One pass, chapter by chapter, checking every statement against its proof, every worked example by
recomputation, and every vague claim. Each entry: location, what was wrong, what was done.

## Front matter

- `notation.qmd`: replaced two en dash glyphs (Moore-Penrose, Hardy-Krause); hat matrix now states the
  full-column-rank condition and the pseudoinverse form; total variation fixed to the supremum convention
  (matches Ch 21's Le Cam bound); MAIC weight `beta` and heterogeneity `tau^2` disambiguated.
- `index.qmd`: Part I claim "proved from the basics" aligned with the rigor policy (routine facts cited);
  appendix list now includes Appendix G.
- Machine-checked tags: all 33 distinct tags resolve to a real declaration in `ITC_Coq/theories/`.
- Book-wide: removed 16 doubled prefixes such as "Exercise @exr-..." (Quarto already prints the word).

## Ch 1

- All proofs and the elimination and Gram-matrix arithmetic verified. Fixed: intro claimed the rank
  "drops" when a redundant column is added (it stays at two; the column count rises); a self-reference
  "@sec-la1-intro's promise" replaced by "Chapter 6"; vague "stealing a direction" sentence replaced by
  the exact rank-nullity statement; "This proposition" now names @prp-system-solvability.

## Ch 2

- Proofs and all worked arithmetic (two-arm fit, QR example, leverages 0.7/0.3/0.3/0.7, exercise
  answers) verified.
- Removed false methodological claims: MAIC is not "constrained least squares", does not use Mahalanobis
  distance, and does not solve normal equations; ML-NMR does not fit by normal equations. Reworded to
  generalized least squares and Chapter 27 distance matching, which is where these tools are used.
- Hint to @exr-oblique-vs-orthogonal said "as t tends to infinity" (the inequality is vacuous there);
  now "small t of either sign", matching the Appendix F solution.
- QR remark: "preserves twice as many digits" replaced by the accurate "loses roughly half as many digits",
  with the condition-number convention stated. Dropped unverifiable claims about Stata and Stan internals.
- "Reverse triangle inequality is a corollary of homogeneity" corrected to "of the triangle inequality";
  existence of a basis now cites @lem-reduction-to-basis.

## Ch 3

- All proofs and the worked numbers (eigenpairs of [[2,1],[1,2]], square root, SVD and pseudoinverse
  of the rank-one C) verified.
- Running example: the contrast y_AB - y_AC was labeled d_BC ("C versus B"); under the book's
  convention d_ab = eta_b - eta_a it is d_CB (B versus C). Relabeled throughout. The example also claimed
  correlated estimates from "two trials" and called the contrast a Bucher comparison; reframed as a
  three-arm trial, where the shared A arm is the actual source of the positive correlation.
- Generalized variance is proportional to (not equal to) the squared ellipsoid volume.
- Wrong internal citations: the "dimension formula" dim(U cap V) >= dim U + dim V - n is the starred
  exercise @exr-la1-dim-sum, not rank-nullity (Sylvester and Courant-Fischer proofs); the orthonormal
  projection formula is @prp-projection-from-onb, not @def-projection-matrix; basis extension is
  @lem-basis-extension.
- Distance matching is Part VI (Ch 27), not Part V (five places).

## Ch 4

- Proofs checked; worked bivariate normal and Poisson binomial numbers recomputed.
- Law-of-total-variance remark claimed the Part V count likelihoods avoid "the too-small variance a
  single binomial would suggest". Backwards: with fixed individual risks the Poisson binomial variance is
  smaller than the binomial one by the between-patient term. Rewritten as the exact binary identity.
- Overlap direction was reversed (twice): transport needs the source density positive wherever the
  target density is. The claim that (G5)'s positivity "is exactly" the overlap condition was removed.
- (G5) hypothesis "density strictly positive on its support" is vacuous; now "on the product of the
  marginal supports". Unsourced citation of "Pearl's development" and an incorrect attribution to
  @hernan2020whatif replaced by @pearl1988 (added to `references.bib`).
- @exr-graphoid-counterexample hint ("X = Y, W degenerate") cannot work: with W constant the premises
  imply the conclusion. Hint now matches the Appendix F witness (X = Y = W one fair coin, Z constant).

## Ch 5

- All proofs checked (delta method, Slutsky, consistency, asymptotic normality, Cramer-Rao with its
  regularity hypotheses stated, sandwich). All worked numbers recomputed; one wrong digit fixed
  (e^0.3947 = 1.4839, not 1.4830) and "odds-ratio-scale" corrected to "odds-scale" for a single arm.
- The Bernoulli consistency remark claimed Theta = [0,1] satisfies the envelope condition (C4); it does
  not (log p is unbounded). Now uses Theta = [eps, 1 - eps] with the explicit envelope -log eps.
- @exm-indirect-bucher used d_BA for "B versus A", reversing the book convention d_ab = eta_b - eta_a.
  Relabeled to d_AB, d_AC and the indirect contrast d_CB (B versus C); numbers unchanged.
- Delta-method remark referred to "the hypothesis g'(theta) != 0", which the theorem does not assume;
  restated as the condition for a nondegenerate limit.
- Asymptotic-theory citations pointed to the regression text @bingham2010regression; now
  @billingsley1995 and @vandervaart1998 (uniform LLN, convolution theorem).

## Ch 6

- Proofs checked; worked example recomputed in R (t = 2.309, p = 0.104; T0 p = 0.638; t_{3,.975} =
  3.182; F_{1,3,.95} = 10.13) and the running example fit (1, -1, 1) verified.
- Methodological error, also in Appendix F: the text claimed MAIC "is a weighted least squares of exactly
  this kind" and that generalized Gauss-Markov makes it "optimal under its own assumptions". GLS is
  optimal only when weights invert the error covariance; MAIC weights balance covariates, change the
  estimand, and inflate variance. Replaced in the Gauss-Markov "why this matters", in
  @exr-lr-gm-weighted, and in its Appendix F solution.
- "Every population-adjustment method ... fits a regression" is false for MAIC; restricted to STC and
  ML-NMR. Population adjustment is Part IV, not Part III.
- Garbled sentence in @lem-hat-properties (4) rewritten; projection-characterization citation corrected.

## Ch 7

- Proofs checked; IRLS step, MLE, deviance 5.300 (p = 0.0213), and the 22/7 marginal odds ratio verified.
- Gamma EDF exponent had the wrong sign on log(mu) (must be y(-1/mu) - log mu over 1/nu).
- Canonical link was claimed C^2 "because b' is C^2", but b was only assumed C^2. Now derived: b is
  infinitely differentiable on int Theta via the cumulant generating function, so theta(.) is C^inf.
- Saturated model: added the boundary convention (proportion 0 or 1, count 0; 0 log 0 = 0).
- Non-collapsibility hint and text credited "the convexity of the logit" and Jensen; the logit is not
  convex on (0,1), and the Appendix F proof is a monotonicity argument on A(a). Hint rewritten to match.
- Hazard-ratio preview: "cause-specific" removed (not a competing-risks setting); strictness of Jensen now
  conditioned on nondegenerate H; forward reference now points to the actual proof in Ch 11
  (@sec-emcoll-noncollapse) instead of "later chapters".

## Ch 8

- Proofs checked; worked example recomputed (credible interval, DL tau^2 = 0.11, EB estimates, MH
  acceptance 0.5273, Beta(10,4) sd 0.1167).
- Stein's lemma: the proof justified dropping the boundary term by "E|h'| < infinity forces h to grow
  slower than the Gaussian tail", which is not a valid argument. Replaced by the standard Fubini proof,
  which also shows (Z - theta) h(Z) is integrable.
- Funnel remark said missed small tau biases tau^2 upward "and understates heterogeneity"; upward bias
  overstates it. Fixed.
- James-Stein remark: "||Y||^2/(J-2) is (almost) unbiased for sigma^2 + tau^2" replaced by the exact fact
  that B-hat is unbiased for B (E[1/chi^2_J] = 1/(J-2)).
- de Finetti converse sketch: the empirical frequency is a reverse martingale, not a forward one; the
  primer's martingale gloss ("neither grows nor shrinks") replaced by the definition.
- Posterior predictive remark called the ML-NMR population effect "a posterior predictive quantity"; it
  is the posterior of a derived quantity (no new-outcome noise). Reworded.
- DL truncation: B_j = 1 exactly (not "tends to 1") when tau-hat^2 = 0. Table said "five objects" for six.
- Bayes' theorem used mu for the dominating measure, clashing with the population mean mu of this
  chapter; renamed kappa inside that theorem.
- Book text cited "see the work log" and said sources were "not yet in the bibliography ... for the
  orchestrator to merge". Added 13 bib entries (de Finetti 1937, Hewitt-Savage 1955, Stein 1956,
  James-Stein 1961, Efron-Morris 1975, Patterson-Thompson 1971, Harville 1977, Metropolis 1953, Hastings
  1970, Tierney 1994, Hoffman-Gelman 2014, Neal 2011, Betancourt 2017) and cited them properly. Ergodic
  CLT now notes it needs conditions beyond irreducibility and aperiodicity.

## Ch 9

- Proofs checked (fundamental problem, consistency, ignorability hierarchy, identification, selection
  bias); worked example recomputed (naive 9 = ATT 4 + bias 5).
- Sign error: the bridge table and text wrote d_BC = d_AB - d_AC. Under d_ab = eta_b - eta_a the
  indirect C-versus-B effect is d_BC = d_AC - d_AB (as in Ch 14). Fixed.
- Worked example called the favorable stratum X = 1 "high-risk" and said the treated would have had
  "worse" untreated outcomes (17.5 vs 12.5 on a higher-is-better scale). Both reversed; fixed.
- "Most methods target a marginal effect" softened to the accurate statement, with pointers to Ch 17/19.
- Collapsibility is in Chapter 11, not "the next chapter".
- Notes: garbled attribution sentence and a "work log for the orchestrator" leak replaced by proper
  citations (added Neyman 1923/1990, Rubin 1974, Holland 1986 to the bibliography).

## Ch 10

- Proofs checked (criterion lemma, Rosenbaum-Rubin both parts, sufficiency, Horvitz-Thompson, Hajek,
  variance/ESS, g-computation, AIPW identity and double robustness, EIF variance). All numbers recomputed:
  naive 1.833, overlap table (ESS fractions 0.48/0.30/0.17/0.09; V* for psi_1 9.33/14.33/24.33/44.33),
  ten-patient table (Hajek 2.0 and 1.0, ESS 3.0), AIPW misspecification cases (2, 2, 3).
- Methodological errors corrected: ML-NMR was called "the combined, doubly robust estimator" and
  "AIPW's network descendant" that "inherits double robustness"; it is an outcome-regression method and
  is not doubly robust. MAIC was said to "never balance covariates one at a time" (its estimating
  equations balance each covariate mean) and to inherit IPW results "verbatim" (its weight is the odds
  of target-population membership, not an inverse treatment propensity).
- The ATE-versus-ATT choice was twice equated with "anchored versus unanchored"; they are different
  distinctions (target population versus presence of a common comparator). Fixed in three places.
- The claim that MAIC, STC, and ML-NMR "each face the same variance floor" is false for parametric outcome
  models, which can undercut the nonparametric bound by extrapolating; replaced by the accurate caution.
  Cross-fitting answer no longer invokes Neyman orthogonality for non-orthogonal estimators.
- ESS "three out of the ten" clarified (three of four treated; 30% of the full sample, the same base as
  the population fraction).

## Ch 11

- Proofs checked (gap lemma, interaction lemma, EM implies prognostic, distinctness, anchored
  cancellation, RD direct collapsibility, RR, OR attenuation via tilted measures, HR example). Numbers
  recomputed: OR 6 vs 4.5, log gap -0.288, RR example 1.0397 vs 0.8755, HR(1) = 0.6773, second-trial
  marginal OR 594/119 = 4.992.
- The logit was called "strictly convex-then-concave"; it is concave on (0, 1/2) and convex on (1/2, 1).
- Interaction lemma: "X_j is an EM iff beta_2j != 0" needs X_j to vary with the other components held
  fixed (collinear covariates can cancel); hypothesis stated.
- "Anchored comparisons are unbiased only when balanced on EMs" overstated a sufficient condition.
- Saturated-model exercise claim now conditioned on beta_3 = 0 and beta_2 != 0.
- Work-log leak replaced by proper citations (added Greenland-Robins-Pearl 1999 and Gail et al. 1984).

## Ch 12

- Proofs checked; all three worked examples recomputed (mean difference 3 and 3; marginal log OR 1.17534
  and 0.62173; RMST differences 0.316055 and 0.367404) and the 0.074 logit gap.
- Sign convention: the chapter defines d_ab = g(mu_b) - g(mu_a) (b versus a) and uses
  d_BC = d_1C - d_1B in the two-step theorem, but from the SEMA section onward wrote d_BC for the
  B-minus-C contrast gamma_B - gamma_C. Relabeled those 33 occurrences to d_CB and made the link to the
  Step 2 gap explicit (d_BC = -d_CB).
- @thm-direct-transportability(b) described collapsibility as "the marginal effect is a weighted average
  of the conditional effects", which is not @def-collapsibility; the proof now uses the definition
  directly, with the weights of @lem-collapsible-scales as the explicit instance. A vague support
  hypothesis that neither proof used was removed.
- @thm-sema-insufficient claimed an iff for any scale but proved necessity only for the OR; added the
  general two-population argument from @def-collapsibility.
- "Step 1 error vanishes in expectation" corrected to convergence in probability (MAIC and STC are not
  finite-sample unbiased). Exercise referred to "the last row" of the transport table for a row that is
  not last. The claim that TSD 18 documents "EU joint guidance" (which postdates it) removed.

## Ch 13

- Proofs checked (IVW BLUE and efficiency, projector lemma, Q distribution, E[Q], I^2 ratio,
  identifiability, DL unbiasedness, REML score and fixed point, HK exactness, conjugacy, Egger identity).
  Every number in the running trio and the five-study example recomputed in R (FE 0.2663, Q 5.714,
  p 0.222, I^2 30.0%, tau^2_DL 0.01211, RE 0.3036, Wald and HK intervals, Egger 2.634 / -0.116,
  trio REML 0.045).
- The "why the log scale" paragraph claimed averaging ratios "does not even estimate a well-defined
  effect" because of non-collapsibility; that conflates two issues. Replaced by the correct reasons
  (approximate normality; additivity of log contrasts along a chain of comparisons).
- Fixed-versus-random table said a fixed-effect model "licenses transitivity"; it does not (transitivity
  is a between-comparison assumption).
- Egger remark: "large, imprecise studies ... small, precise ones" reversed; fixed.
- HK "recommended whenever k <= 10 (@dias2018nma)" was an unverified attribution; replaced by
  @inthout2014. Work-log leak replaced by 12 new bibliography entries with citations.

## Ch 14

- Proofs checked; worked example recomputed (d_AC = log 2, d_BC = log 1.5, variances 0.071667 and
  0.054167, SE 0.35473, OR 4/3 with CI 0.665 to 2.672, p 0.42; baselines 33% vs 27%).
- The introduction said "the effect of A relative to C is d_AC", contradicting the chapter's own
  orientation table (d_AC = eta_C - eta_A is C relative to A). Fixed.
- Transitivity-failure example computed marginal log odds ratios as prevalence-weighted averages of
  conditional ones, which is false on a non-collapsible scale. The collapsible simplification is now
  stated explicitly (as the matching exercise already did), and the general text says the average is
  exact only on the risk-difference scale.
- The one-half correlation remark conflated the within-trial sampling correlation of contrasts sharing an
  arm with the random-effects heterogeneity correlation; now separated and each pointed to its source.
- @exr-bucher-scales had a meaningless formula ("something additive"); restated as multiplicativity of
  ratios along a path.

## Ch 15

- Worked example rechecked by hand (A, A^-1, fitted 0.60/0.90, node-split 0.1 vs 0.4, Var 0.30,
  D_res 0.40, OR interval 0.81 to 2.24). Proofs of closure, incidence rank, equivalence,
  identifiability, one-half lemma, IPD-NMR identifiability, p_D trace identity all correct.
- False claim fixed: the surplus C-(K-1) was said to be positive whenever a multi-arm study is present and
  zero for "two-arm studies without repeated comparisons". It is the cycle rank of G: positive iff G has a
  cycle (parallel edges or a loop); a lone multi-arm study adds none. Remark, table row, and notes fixed.
- Sampling versus heterogeneity correlation were conflated in four places (intro, arm-model remarks,
  section opener, example header); references now point to the sampling remark or @sec-nma-random.
- Condition (i) of the IPD-NMR theorem (interactions shared across studies) was called "the shared effect
  modifier assumption"; that name (@def-sema) means equality across treatments. Remark and notes fixed.
- Sign wording of the running example ("second-named treatment") fixed; multi-arm subtraction written with
  indices. "Large drop in fit" for the UME comparison replaced by "markedly lower DIC". Unanchored bridging
  is Parts IV and V, not Part V only.
- Citations added: lu2004, dias2010, spiegelhalter2002.

## Ch 16

- All worked numbers rechecked (RD bias -0.06; probit b2 0.18903, contrasts 0.33231 and 0.52134, EB
  -0.03957; OR surcharge 7/3). Logit compounding exercise recomputed in R: total -0.197 = EM bias -0.217 +
  non-collapsibility +0.021.
- Conditional constancy was identified with SEMA ("the two say the same thing"), contradicting
  @def-sema in Ch 17. Now: TSD 18 calls it conditional constancy of relative effects; SEMA is distinct.
  Fixed in the text, the table, and the notes.
- False: "B versus C is the more imbalanced contrast". Both trials are 0.3 from the target.
- The log risk ratio was listed as directly collapsible (Ch 11 proves it is not); prp-limits-collapse-link
  (3) now covers every scale that is not directly collapsible.
- lem-limits-conditional-additivity restricted the averaged identity to collapsible scales; it holds on
  every scale by linearity. Continuous-case proofs relied on unstated boundedness and continuity; they now
  use point masses, with continuity stated where densities are insisted on. Fubini justified by integrability.
- STC was described as integrating over the target; Ch 19 distinguishes plug-in (original) from marginal
  STC. MAIC "performs the integration" softened to what moment matching actually guarantees.
- Exercises: logit exercise had the contrast sign reversed and compared log-odds with a risk difference;
  the zero-bias exercise asked for something impossible (binary covariate) with a self-contradicting hint;
  the log-link exercise asked a vague relation and now shows the log link does not attenuate the slope
  (hence "cannot in general be recovered" in the gap section). Appendix F general-attenuation solution
  cites this.
- Glossary convention clarified against Notation (subscript naming). Leaked process paragraph in the notes
  ("owns the slugs", "proposed additions to the notation chapter") removed; the two symbols were added to
  notation.qmd instead. Citation: robinson1950.

## Ch 17

- Sign error: eq-pat-tau-linear gave tau_kC = g(mu_C) - g(mu_k) = gamma_k + beta_2k'x, but in the model
  eq-pat-nmr gamma_k is k relative to C, so tau_kC = -(gamma_k + beta_2k'x) (Ch 11 lemma has tau_01 =
  +gamma). Propagated: SEMA constant is gamma_B - gamma_A (was gamma_A - gamma_B), identification solves
  gamma_B = -d_BC - beta_2'x_BC, the over-identifying restriction carries a minus sign, hyperplane and SEMA
  point corrected, exercise asks for gamma_B - gamma_A. Now agrees with Ch 23 (Delta_BA = gamma_A - gamma_B).
- "Conditional constancy is weaker than marginal constancy" (three places) is false: the two are logically
  independent. Rewritten.
- MAIC, marginal STC and ML-NMR were all said to target the conditional-average estimand; weighting
  delivers a marginal contrast. Fixed in the estimand paragraph, the two-faces paragraph, the method bullets,
  the closing summary, and Step 6 of the worked example ("no amount of covariate balancing closes it"
  replaced by the actual obstruction: the AgD marginal odds ratio cannot be re-standardized).
- Part (d) misalignment needs h o g^-1 not affine (an affine map is a rescaling). Unadjusted W "balanced"
  now defined conditionally on X, which the proof of part (a) uses. SEMA identifiability theorem notes that
  a real AgD trial reports a marginal contrast (Ch 23 case). ESS cited to @def-maic-ess, not
  @def-balancing-score.
- Exercises: the "numerical coincidence" in exr-pat-bias-recompute is in fact structural (p* = p_AC);
  exr-pat-scale-status constraint named; exr-pat-noncollapsible-target claimed a "pure non-collapsibility
  effect" though X modifies A versus B. Appendix F solution had the log odds ratio sign reversed relative to
  the book convention and Step 6; all signs flipped and rechecked in R.
- Worked example numbers verified (bias 0.075, ESS 150, marginal log OR -0.2283, conditional -0.1542).

## Ch 18

- Anchored MAIC theorem assumed SEMA and said SEMA makes the published BC contrast consistent; with the
  target equal to P_BC, SEMA is unnecessary and the BC contrast is consistent by randomization. Removed
  SEMA from the theorem, the intro, both tables, and the hypotheses remark.
- Step 2 of the proof transported the absolute mean mu_A under only relative constancy. Now (ii) is scale
  split: relative constancy on the identity scale (baseline cancels, direct collapsibility), transport of
  the arm means on other scales. The old "non-collapsible scales" paragraph (Step 4 needs scale alignment,
  "SEMA supplies the common baseline") was wrong: Step 4 is algebra within one population; the real issue
  is the AC trial's baseline in Step 3. Remark rewritten accordingly (matches Ch 17(c)).
- Unanchored MAIC had the contrast sign reversed (g(mu_A) - g(mu_B)) and reweighted an AgD arm; fixed to
  g(mu_B) - g(mu_A^MAIC) with mu_B the reported arm mean when P* is the B population.
- Sandwich remark and Appendix F solution claimed fixed-weight SEs are "typically anticonservative"; the
  derivation shows the correction is B11 c (c - 2 c2)/(n a22^2), approximately -B11 c^2 when weights are
  moderate (calibration effect), so fixed-weight SEs are often conservative; sign not universal. Solution
  also equated B22/(n a22^2) with sigma^2/ESS, true only for a constant conditional mean.
- Exercises: exr-maic-secondmoment asked for a variance constraint that is infeasible (x1 = +-1) and a
  false monotonicity of ESS; rewritten. exr-maic-interpret-weights (d) claimed a guaranteed ESS direction.
- Smaller: CATE sign aligned with tau_AC; "exponential form appears on its own" (automatic for two
  values); "infinite family whenever feasible" needs a positive solution; unverified R package names;
  balancing-score wording; MoM-vs-ML remark now states the double robustness of entropy balancing
  (@zhao2017entropy); Donsker wording in the bootstrap proof; O(1/n) bias claim softened.
- All example numbers verified (weights 1.5/0.5, ESS 3.2 and 2.56, alpha 0.2616, adjusted 4.5, bias 0.5,
  logit example 0.731/0.690/0.407).
- Citations: zhao2017entropy, hainmueller2012, deville1992.

## Ch 19

- Sign error: eq-stc-contrastbias (statement and proof) gave d_cond - d_marg = [eta_A(xbar) - eta_A(P)] -
  [eta_C(xbar) - eta_C(P)]; the regrouping of [eta_C(xbar) - eta_A(xbar)] - [eta_C(P) - eta_A(P)] gives
  the negative. The log-link example's final formula was already right; now consistent.
- Anchored STC consistency claimed that relative constancy plus effect-modifier inclusion makes the arm
  surfaces transport; off the identity link the baseline does not cancel. Theorem and proof now split by
  scale (as for MAIC in Ch 18). Unanchored STC was written with arms A and C; it is g(mu_B) - g(mu_A^STC)
  with mu_B the reported arm mean.
- "Biased under any nonlinear link" false for the log link without effect modification (the chapter's own
  example); fixed in intro, table, and "why this matters". "Average-patient effect is not the average
  effect" is false under a linear predictor; reworded. Arm gap nonzero needs constant-sign curvature.
- MAIC described as "indifferent to functional form"; replaced by what Ch 18 proves (correct weight model
  or arm means linear in the matched moments).
- Numbers recomputed in R: counterexample log(3.41113) = 1.22704 (was 1.22707), gap 0.27296; worked example
  1.44262 and 1.41516 (last digit), OR 4.2318, plug-in excess 0.05738.
- Appendix F log-link solution relabeled in the l = -d orientation it actually used.

## Ch 20

- The SEMA preview said SEMA means interactions "are the same across studies"; that is conditional
  constancy, already built into the model. SEMA equates interactions across active treatments; in the
  running example it supplies beta_2C, which no study reveals. Rewritten.
- The "resolution of the failure of Bucher" remark conflated effect-modifier imbalance with ecological bias;
  now separates the two failures of Ch 16. Intro likewise cited the wrong theorem and said MAIC/STC are
  "exact only on a linear scale"; "everyone before us was biased" removed.
- Probit heat-flow check had (1+tau)^2 for (1+tau)^(3/2). Equality clause of thm-aggregation-bias restated
  (affine gives equality always; strict convexity gives equality iff degenerate), leading-order lemma needs
  the third-derivative bound on the support, identity-link converse needs a nonzero slope.
- "On the log link this gap does not arise" false with effect modification (Ch 19 example); fixed.
- Worked example recomputed: marginal log OR 1.21999 (was 1.22000), bias 0.08001; J(1,1) = 0.6967 and probit
  0.7602 confirmed; log-link example exact. Appendix F prevalence solution: 1.04424, bias 0.05576.
- Notes leaked "we note this gap in the work log" and an unverifiable claim about Coq libraries; removed.
  Jensen-gap-bound exercise wrongly assumed expit'' >= 0.

## Ch 21

- All worked numbers verified (PoBin polynomial, variance 1.00, third moment 0.12, TV 0.0200 and 0.1707,
  Poisson tail 0.0166, count overdispersion 80/120). Le Cam coupling proof correct.
- Checked against multinma (R/nma.R, inst/stan/binomial_2par.stan) and the thesis (Section 4.2.1): the
  default AgD likelihood is the one-parameter binomial; the two-parameter binomial (N' = n pbar^2 / p2bar,
  p' = p2bar / pbar, identical to the adjusted binomial here) is an option. "The surrogate used in practice"
  and "used in phillippo2020mlnmr (psoriasis case study)" replaced by what the sources support; the thesis
  attributes both surrogates to Le Cam, now noted.
- Barbour-Hall bound: the refined bound is the risk-weighted average risk, not p-bar; the Poisson regime
  needs small p_i only, not small lambda.
- Notes leaked "recorded in the work log as proposed additions"; added barbour1984, chen1975, barbour1992
  and cited them. "the author's own lemma" wording removed.

## Ch 22

- False claim (theorem, proof, and remark): "for continuous margins and a bounded smooth link such as the
  logit, V_HK(psi) is finite". With normal margins and d >= 2 the mixed derivative is not integrable; e.g.
  two independent normals and eta = a + b z1 + c z2 give Vitali variation
  integral |bc expit''(eta)| dz1 dz2 = infinity. Now: finite for d = 1 (V <= 1), possibly infinite for d >= 2,
  where the near-1/N behavior rests on boundary-growth analysis (@owen2006halton) or scrambling. Also
  corrected: an axis-aligned jump has finite variation; the infinite case is the copula-tilted jump.
- Stirling asymptotic of the Gauss constant was pi/(4^{2k}(2k)!); it is pi/(4^k (2k)!) (k = 1 gives 1/3).
- The product-rule corollary mixed k and N (N = k^d with error O(k^-2k) "= O(N^-2k/d)"); restated for the
  composite tensor rule, N = (mk)^d, with a telescoping proof.
- Checked against multinma: points come from randtoolbox (not Stan or qrng), the default is 64 nodes (not
  "hundreds to low thousands"), and correlations are converted to latent copula correlations; the Spearman
  conversion 2 sin(pi rho_S / 6) is now stated. Joe-Kuo tables cover 21,201 dimensions.
- The N-versus-N/2 gap was called conservative; in the chapter's own table it slightly understates the
  error (0.0054 vs 0.0062 at N = 64). Reworded.
- All example numbers recomputed in R (reference 0.60203, seven-point 0.6091, refinement table n = 1..N,
  copula traces, Appendix F four-point estimates 0.54019 and 0.56015).

## Ch 23

- prp-mlnmr-sema-necessary claimed the two observationally identical parameter pairs give the same
  conditional contrast exactly at xbar* = q; the root of the difference is q g1'/((1-q) g0' + q g1') in the
  infinitesimal limit, equal to q only on the identity link. The chapter's own example contradicted it
  (0.500 vs 0.528 at q = 0.6; they meet at 0.543). Restated: the identified quantity is the marginal contrast
  in P_BC; the conditional contrast is unidentified everywhere except at most one mean.
- Collapsibility dichotomy needs direct collapsibility. The scale table said the log link needs the target
  baseline; e^mu* cancels (it needs the full f* only under effect modification). Fixed.
- Generality theorem (c): MAIC hypotheses listed SEMA (removed, per Ch 18); MAIC reports d_AB = -d_BA;
  the "same limit" argument equated absolute arm means with different trial baselines; now argued on the
  contrast, where the baseline cancels, on the identity link.
- Monotonicity lemma: finiteness for every c was claimed from finiteness at one c0 for any link (false in
  general); integrability is now a hypothesis, with the cases where it is automatic.
- ICH E9(R1) claims softened to what the guideline asks. Notes: authoring-history phrasing ("base draft",
  "upgraded from a remark", "the manuscript records") removed.
- Worked example, both targets, the high-baseline remark, and the SEMA-failure pairs recomputed in R.

## Ch 24

- Leapfrog stability is bounded iff eps*omega < 2 (at = 2 the proof itself shows linear growth); statement,
  proof, and notes said <= 2.
- WAIC-DIC penalty equality was justified by "the score vanishes at the mode"; it rests on the
  information-matrix equality, i.e. correct specification. Under misspecification p_WAIC estimates the
  robust trace penalty. Stated.
- Running example: with one study per contrast the likelihood carries essentially no information on tau
  (posterior close to prior), not "weakly identified from a pair of contrasts". The influential-study remark
  recommended refitting without BC, which would make d_AC unidentifiable; replaced by a sensitivity analysis
  of that study's inputs.
- Garbled expression in the Gelman-Rubin proof fixed; rank-normalized R-hat cited (@vehtari2021rhat).
  Checked against multinma: non-centered random effects by default (confirmed); baselines are fixed effects.
- Summary table labeled d_AC "A vs C" against the notation (effect of C versus A). "Gabra" -> "Gabry".
- All worked numbers recomputed (R-hat 1.025, WAIC 4.012, LOO 3.956, QMC sequence to 0.5868).

## Ch 25

- tbl-genlik-reduction and Part 3 of the general-likelihood theorem claimed the Gaussian likelihood is
  affine in its mean, so the integrated likelihood equals the kernel at the aggregate mean. False: the
  integrated Gaussian likelihood is a normal mixture. Only the Bernoulli kernel is affine; the identity
  link still makes the arm mean exact. Fixed.
- SEMA misused for "effects shared across populations" (remark, table, notes, exercise, Appendix F
  solution); replaced by conditional constancy of relative effects. RMST transport also needs the target
  baseline hazard.
- RMST contrast subscript order was Delta_ba = RMST_b - RMST_a, against the book convention; now
  Delta_ab, and the example and exercise use Delta_CA = RMST_A - RMST_C.
- Overclaims that MAIC and STC cannot handle survival or ordinal outcomes (intro, two remarks) replaced by
  the accurate contrast (per-outcome estimators, pairwise, comparator population only).
- Notes leaked "proposed bibliography entry in the work log" and a local file path; added klein2003,
  cited guyot2012, removed unverifiable multinma specifics.
- All numbers checked (marginal hazards and mHR table, survivor fractions, RMSTs 0.5986/0.9489/0.3503,
  L1 0.6380, L2 0.06891, product 0.04396, ordinal probabilities).
- Related SEMA conflations fixed elsewhere: Ch 11 (two places) called the "balance only effect modifiers"
  rule SEMA; Appendix E defined SEMA as sharing across studies.

## Ch 26

- Reframed SPFA versus SEMA. def-spfa (beta_A = beta_B) is, in the beta_1 + beta_2k parametrization, the
  same equation as SEMA; the old prp-spfa-vs-sema switched reference arm between parts and its strictness
  witness (beta_2A = beta_2B = c != 0) satisfies def-spfa. Rewritten (label kept) as "SPFA is SEMA without
  an anchor": same slope restriction; the strict gap is absolute versus relative constancy
  (@prp-pat-absolute-implies-relative). Ripple fixes: intro, tbl-mlumr-methods, def-spfa wording,
  plain-language remark, tbl-spfa-sema (testability, methods), lem-spfa-absolute-constancy (retitled; it
  is a constant-contrast result, not absolute constancy), "why this is a transportability problem" remark,
  notes, exercise; Ch 11, Ch 17 remark, Appendix A glossary, Appendix E.
- STC equivalence: Chapter 19's unanchored contrast is g(mu_B) - g(mu_A^STC) = -Delta_AB; orientation stated
  and the citation moved to @thm-stc-consistency(2). SPFA is not used at P_B (calibration makes the arm-B
  mean the observed one), so "the extension uses a stronger assumption than STC" now says why: STC needs no
  arm-B slope. Calibration proof made precise (alpha_B absorbs the comparator factor for any other values).
- thm-mlumr-tte(e): non-constancy of the RMST contrast needs alpha_A != alpha_B and a covariate range;
  proof now uses analyticity (identity theorem) instead of a limit argument; "differs across targets"
  qualified. Worked remark: conditional log HR is log(lambda_A/lambda_B); "gap grows with tau" replaced by
  the tau -> infinity limit.
- QMC theorem: margins need not be continuous; V_HK finiteness claim for normal margins removed (Ch 22
  caveat). owen1956 (bivariate normal tables) was cited for scrambling and Sobol' QMC; fixed here and in
  Ch 25 (inverse CDF).
- Pseudo-IPD: the KM curve (not the distribution) is reproduced; statistics using exact censoring times
  are not. KM example uses approx for rounded inputs. set_agd_surv() takes pseudo-IPD, does not run Guyot.
- Joint likelihood: binomial collapse is exact; the normal sample-mean model is a large-sample
  approximation (normal mixture). Median survival is not collapsible (theorem, proof, table caption).
  Estimand table: log hazard ratio, not log risk ratio.
- Checked against mlumr: n_int = 64, check_integration(), predict(type = "loghr"), t -> 0 scalar HR,
  distributions, no random effects. All numbers recomputed in R (alpha_B -0.998, 0.4706, 0.4745, Step 6
  bias -0.18, marginal HR 1.438/1.398/1.491, RMST 5.32/4.17, exercise alpha_B -1.197, LOR 0.961).
  Appendix F: interpolation bracket typo and log HR orientation fixed.

## Ch 27

- Work-log leaks ("citation forthcoming", "proposed in the work log") replaced by real entries:
  perren2024compass (as cited in the uitc vignette), uitc, mahalanobis1936, gower1971, villani2009.
- Claims that Mahalanobis becomes faithful when beta points "along the high-variance axis" were false (in
  the two-trial example beta along the principal axis still favors Q). Replaced by a verified flip,
  beta = (-0.1, 0.5) giving B_P = 1.0, B_Q = -2.6, and by the exact characterization: d_SE and d_M rank by
  worst-case bias over ||S beta|| <= 1 and beta' Sigma beta <= 1.
- ESS remark mixed the unadjusted bias B_j with post-adjustment variance; now bias comes from the part of the
  gap left unadjusted and variance from the part matched. Exercise wording aligned.
- Cited a nonexistent "affine-mu_t hypothesis" of thm-unanchored-paic-consistency; fixed. Conditional
  constancy of a contrast cited to the relative definition. Whitening part 2 stated for B^{-1}X, not the gap.
- Raw-Euclidean explanation said the biomarker dominates; age does. "l1 and l2 must often agree" fixed.
- All numbers recomputed in R (d_E, d_SE, d_M, mean-SMD, biases 1.8/3.2/3.6/4.0, both equality cases,
  exercise values). uitc facts checked: standardized_euclidean default, Minkowski order p >= 1, omitted
  distances, Gower truncation.

## Ch 28

- Indirect-comparison E-value used RR_UD = exp(|beta_U|), the per-unit risk ratio, for a continuous
  covariate. RR_UD in the sharp bound is max/min risk over the support of U, so the running example's
  E_ITC = +infinity "certificate" was false; the chapter's own tipping point (a 1.4 L shift) overturns the
  result. Definition now states RR_UD per covariate type (binary, bounded, unbounded -> E_ITC = BF_obs);
  example part (c), the three-cases remark, caveats, workflow, intro, dossier exercise, starred exercise and
  its Appendix F solution rewritten (E_ITC = 2.014 and 3.019; certificate illustrated with a binary
  covariate). Note: the uitc function itc_evalue_from_parts / ipd_u_association has the same issue.
- Exercise: E-value of HR limit 0.85 is 1.63, not 1.7.
- Unreported covariate in the unanchored setting is prognostic (or modifier), not only an effect modifier;
  thm-sema-insufficient (non-collapsibility) was cited for omitted-covariate bias; replaced by
  thm-unanchored-paic-consistency. Scale sentence (log OR "lives on the RR scale") fixed. Bucher condition
  stated as balance of effect modifiers. "Nearest correlation matrix" wording fixed (eigenvalue clipping is
  not the nearest). E-value "routinely" softened; plug-in RR is 0.497 (E = 3.443).
- Citations added: ren2025qba (from the uitc bibliography), ding2016sensitivity, schlesselman1978,
  cario1997, kruskal1958, nelsen2006; unverifiable attribution of the ITC E-value to Ren et al. and to mlumr
  (which has no E-value code) removed.
- Numbers verified: K = 0.300, Delta(2) = -0.700, E = 3.443, E(1.3) = 1.925, E_ITC(3.0) = 4.085, NORTA
  rho_N = -0.313, Var 0.3526, RR 0.512, PBA intervals and P_ben 0.992; starred exercise K = 0.495,
  BF = 3.019, m_dagger = 0.619.

## Ch 29

- Running example described the outcome as a PASI *reduction* (higher is better) while using the MAIC
  example's contrast mu_C - mu_A = 4 + x1 as "the benefit of A"; that holds only for a lower-is-better
  score. Outcome restated as week-16 PASI (lower is better); theta = d_AB = mu_B - mu_A made explicit.
- Robustness proposition overstated the thesis: ML-NMR "most robust" and "lowest variance" (thesis: ML-NMR
  and STC perform very similarly); MAIC "low bias with adequate overlap" (thesis: bias removed only when the
  AgD population is inside the IPD support, sometimes worse than Bucher, unstable bootstrap SEs); Bucher
  "largest bias" (MAIC sometimes larger); STC "can interpolate" (it extrapolates). Table and items fixed
  against thesis Section 8.3.
- Unanchored items cited @def-sema for SPFA and claimed residual bias "under a correct SPFA"; now @def-spfa
  with absolute constancy, comparator-population versus transported estimands separated, "any strength"
  softened. thm-sema-insufficient (non-collapsibility) replaced by prp-spfa-vs-sema where the claim is
  about unanchored demands.
- Fixed-bias corollary claimed monotone worsening in n; now stated for the approximate coverage h(b_n).
- Appendix F: adding a balance constraint does not provably lower ESS; stated as the exercise's assumption.
- Numbers verified: h(b) table, coverage MCSE table, R = 1090, example bias/EmpSE/MSE identity, power
  n = 197, ModSE/EmpSE exercise (predicted 0.85 vs 0.86 observed).

## Ch 30

- Running example read d_AC = -0.80 as "A lowers the odds", against the book convention d_ac = eta_c - eta_a
  (and against Bucher.v, which defines d_AB as the effect of B vs A). Numbers restated as d_AC = 0.80,
  d_BC = 0.50, d_AB = 0.30 (A better, OR A vs B 0.74); sign-slip illustration and exm-coq-bucher-numeric
  follow.
- The example's MAIC weight of exactly 0 contradicts maic_weight_pos; now a rounded near-zero weight.
- ESS_upper_bound proves only the inequality; the map table now says the equality case is paper-only.
- Appendix F faithfulness solution claimed an abstract premise makes a vacuous proof impossible; restated
  (an opaque premise cannot be unfolded to True).
- Verified against ITC_Coq: 15 files, every Coq identifier in the chapter exists, quoted statements are
  verbatim, no Admitted/Axiom/admit, all 33 machine-checked tags in the book resolve, and
  Print Assumptions on ESS_upper_bound, bucher_unbiased, not_EM_does_not_imply_not_PV,
  propensity_score_is_balancing, double_robustness returns exactly the three boolp axioms (run locally).

## Appendices

- A: glossary fixes (exponential weights come from the entropy objective, not the balance constraints;
  active axioms are the three boolp axioms, excluded middle derived; doubling diagnostic is a proxy, not a
  bound; ITC E-value, QBA, tipping point, direct collapsibility, marginal versus average-conditional, and
  the unanchored network entries restated to match their definitions).
- B: compound symmetry was called the marginal covariance of a random-effects meta-analysis (that
  covariance is diagonal); now the one-way within-group covariance. Woodbury no longer claimed for ML-NMR
  (which integrates numerically); MAIC not described as likelihood-based; Fisher scoring not attributed to
  ML-NMR.
- C: Weibull example claimed all shapes have h(1) = 1; they share H(lambda) = 1 instead.
- D: one-probit max error is near |z| = 2.8; two-probit example value 0.6021 (error 0.0001) and
  Phi(0.34015); discrepancy proof's limit direction and the seven-point maximizer (k = 1) fixed; QMC rate
  caveats added; Page (1977) citation for 1/1.702 replaced by the IRT attribution (Haley, 1952); software
  claims about erf-inverse softened. Verified T(0.3536, 0.5774) = 0.0778, E[Phi^2] = 0.4826, two-probit
  coefficients and max error 0.0040 by numerical solution.
- E: multinma call used `(age + sex):.trt`, which omits prognostic main effects (checked against nma()
  docs); now `*`. Adjusted binomial said to widen the variance; it shrinks it to the Poisson-binomial
  value. mlumr Stan snippet replaced by the actual code (integrated_binomial_lpmf). set_agd_surv() takes
  reconstructed pseudo-IPD (Guyot reconstruction happens upstream). RMST no longer "transports cleanly".
  E-value function mapping corrected; the uitc ITC E-value's per-unit RR_UD limitation noted.
- F: solutions for Ch 1 to 13 reviewed: DL constant 8.3572 / 13.0039; stabilized weights do not reduce
  the Hajek estimator's variance (Ch 10 text, table, exercise, and solution fixed); James-Stein toward a
  data-estimated center needs J >= 4 (Ch 8 remark and solution); Bucher correlated-contrast orientation
  and the reason for the value 1/2; REML algebra step; Jensen side remark removed from the OR solution;
  "more dispersed" replaced by mean-preserving spread.
- G: claimed the MAIC exponential tilt is machine-checked (only the weight form and positivity are; the
  duality derivation is paper-only) and that Coq checks "absence of effect modification" for unanchored
  comparisons; both restated. Bucher symbol table now states the book's d_ab orientation (d_AB is the
  effect of B relative to A, as in Bucher.v). All Coq identifiers and quoted code verified against
  ITC_Coq.
