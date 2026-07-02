# Feedback: Chapter 20 — ML-NMR Aggregation

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part5/20-mlnmr-aggregation.qmd`

## Overall impression

As a health researcher who knows what an odds ratio is and has run a logistic regression in R, I could follow the high-level story (aggregate by integrating, not plugging in the mean) but I got buried in the math very early. The biggest barrier was that the chapter front-loads an enormous amount of notation and abstract machinery (linear predictors, link functions, multivariate normals, MGFs, heat semigroups) before I ever see a concrete drug trial or a single patient. By the time the worked example finally arrives in Section @sec-agg-example (line 699, almost 700 lines in), I had already lost the thread of why any of this matters for an HTA submission. The chapter reads like it was written for someone who already knows ML-NMR, not for a naive researcher being brought to mastery.

## What was unclear

- **The aggregation theorem statement (@thm-aggregation, lines 194-222)** threw me. Part (a) introduces a conditional density $L_{i\mid x}$ with a notation I have never seen before in Part IV, and then part (c) talks about "summary statistic $T(\mathbf y_{jk})$" without telling me what $T$ is concretely. I do not understand the jump from "one AgD patient has a marginal density" to "the arm likelihood is a product" (line 218) when the whole point of AgD is that I never see individual patients. A sentence saying "we never observe the $y_{ijk}$, but the math is cleaner if we write it this way first" would help.
- **The bullet subscript $\theta_{\bullet jk}$ (line 161)** confused me for several pages. It is introduced as "denoting the average over individuals" but I kept reading it as a typo or a multiplication. A one-line gloss like "$\bullet$ = averaged over the invisible individuals" with a verbal name ("the dot-mean") would anchor it.
- **@eq-agg-individual-model (line 106)** stacks four terms ($\mu_j$, $\mathbf x^\top\boldsymbol\beta_1$, $\mathbf x^\top\boldsymbol\beta_{2,k}$, $\gamma_k$) and I could not immediately see why the prognostic slope $\boldsymbol\beta_1$ and the interaction $\boldsymbol\beta_{2,k}$ are written separately rather than combined into one slope. The remark at line 130 helps a little, but the formula itself should flag the split visually, e.g. with a brace grouping "prognostic" vs "effect modification."
- **The converse in @thm-identity-link-exact (lines 471-490)** invokes "Jensen's equation" and "midpoint-affine identity." I have basic calculus, I do not know Jensen's functional equation. The step "a measurable function satisfying midpoint-affine is affine" is stated without proof and cites nothing. This is a load-bearing step and I got stuck.
- **@lem-agg-heat-flow (lines 396-442)** is the hardest math in the chapter for me. The growth bound $|\psi(z)|\le Ce^{a|z|}$ and "differentiation under the integral justified by dominated convergence" (line 430) are beyond my training. I could not verify the heat equation calculation myself. I trust it but I do not understand it.
- **The proof of @thm-logit-no-closed-form(d) (lines 659-674)** is honestly labeled as "argued rather than invoked a Liouville-type impossibility theorem" (line 680), but as a beginner I cannot tell how strong this argument is. Is "no closed form is known" a theorem or a status report? The text oscillates between "we argue" and "is well known," and I am not sure what I am allowed to rely on.

## What wasn't elaborated enough

- **The shared effect modifier assumption (SEMA, line 140)** is mentioned in one sentence and then deferred to Chapter 23. But SEMA is what makes the whole network identifiable, and without it I cannot see why mixing IPD and AgD in one likelihood even works. This deserves at least a paragraph here, or a concrete example of what breaks if SEMA fails.
- **The reconstruction of $f_j$ from AgD summaries (line 80)** is repeatedly postponed to Chapter 22, but it is used in every formula. I kept wondering: if an AgD study reports only means and SDs, where does the correlation matrix come from? A one-paragraph aside with a real example (e.g. "study reports mean age and mean BMI and their SDs; we assume a Gaussian copula with correlation 0.3, carried in Chapter 22") would stop the reader from feeling the ground is missing.
- **The Poisson-binomial remark (line 179, @def-poisson-binomial)** is dropped in a footnote-style sentence and deferred to Chapter 21. Since most readers using ML-NMR will have binary outcomes, the fact that the "right" aggregate law is not binomial should not be buried in a remark.
- **The connection between aggregation bias and non-collapsibility (line 782)** is asserted in one sentence at the very end of the worked example. This is a deep and contested point in the epidemiology literature, and it deserves its own subsection, with the odds-ratio case worked through, since that is where the fights happen.
- **The reduction to standard NMA (line 142, and exercise @exr-agg-nma-reduction line 922)** is stated twice but never proved in the chapter body, only relegated to an exercise and to Chapter 23. A reader coming from Chapter 15 wants to see the bridge here, not be told to wait.

## Missing motivation / "why does this matter?"

- **The introduction (lines 5-62) never names a drug or a disease.** For a health researcher, the whole point of ML-NMR is that we have an IPD trial of Drug B vs placebo and an AgD trial of Drug C vs placebo, and we want B vs C for an HTA submission. A two-sentence scenario ("Suppose we have IPD from the plaque psoriasis network, and an AgD trial of a new IL-17 inhibitor...") at the top would transform the abstract setup into something I care about.
- **Why aggregate at all?** The chapter assumes I already want a population-level estimate, but it never explains why the estimand of interest is the marginal (population-averaged) effect rather than the conditional effect at the mean. In HTA, decision makers want the marginal effect in the target population; that policy motivation is absent. Line 56 mentions "target-population estimands" but defers it to Chapter 23.
- **Why prove @thm-aggregation (line 194) at all?** It is called "load-bearing" (line 192) but I did not understand *what would go wrong* if I used a different aggregation rule. A sentence like "any other average would be inconsistent with the data-generating process and would give biased treatment effects" would make the proof feel necessary.
- **The heat-flow view (@sec-agg-heat, line 388)** is beautiful but I never learned *why I should care* that aggregation is heat flow. The remark at line 444 says it "organizes the rest of the chapter," but for a health researcher this is pure math motivation. Is there a computational payoff? A way to read off bias signs? Tell me the payoff before the PDE.
- **The "three links" framing (line 42)** is presented as the organizing principle, but I never learned why these three (identity, log, logit) are the ones that matter. A table linking each link to a concrete outcome type (continuous mean, count/rate, binary) with a real trial example would motivate the taxonomy.

## Missing examples and intuition

- **No example appears until line 709 (@exm-agg-logit-discrete), roughly 700 lines in.** A short motivating example right after @thm-aggregation, even a toy one with two patients, would have let me see the integral in action before the bias theorems and heat flow.
- **The sign reversal of the logit bias (lines 745-754) is the most important qualitative fact in the chapter for practitioners**, and it gets one paragraph. I wanted a picture: a plot of $\mathrm{expit}$ with the convex region shaded for $m<0$ and the concave region for $m>0$, showing how plugging in the mean underestimates on one side and overestimates on the other. No figure is referenced.
- **The worked example (@exm-agg-logit-discrete) uses uninterpreted parameters** ($\mu_j=-1$, $\beta_1=0.5$, etc.) with no clinical meaning. What is the covariate? Age? Disease severity? What is the outcome? Mortality? Response? Giving the numbers a clinical dress would make the 1.22 vs 1.30 log odds ratio land as a real HTA finding.
- **The probit closed form (@prp-agg-probit-closed-form, line 580)** is proved but never exemplified. Since it is the "neighbor that works," a tiny numerical contrast with the logit integral (same $m,\tau$, two answers) would crystallize why logit is hard and probit is easy.
- **The exercises (@exr-agg-correlated, line 909)** nicely introduce two correlated covariates, but the chapter body never shows a multivariate example. Every formula is multivariate but every worked instance is univariate or scalar, so I never see the matrix algebra in action.

## Notation and jargon problems

- **$\boldsymbol\xi$ (line 123)** is the full parameter vector but is barely used in the chapter; most formulas use the component symbols. Its early prominence made me think I would need to track it, then it disappears.
- **$\pi_{\mathrm{Ind}}$ and $\pi_{\mathrm{Agg}}$ (lines 120, 166)** are introduced as "outcome families" but the word "family" is jargon from exponential-family theory that is not glossed. A health researcher knows "binomial," "Poisson," "normal," not "outcome family."
- **"Affine" is used throughout (e.g. line 126) but never glossed** in the chapter. I know "linear" but "affine" (linear plus a constant) is a distinction I had to look up. A parenthetical on first use would help.
- **The notation $f_j$ for covariate density (line 77) vs the empirical distribution for IPD (line 79)** is clear, but the text then writes integrals against $f_j$ for IPD studies too. I was confused whether IPD studies use the integral or not; line 33 says "no integration because each covariate vector is observed," but the formalism does not separate the two cases cleanly.
- **"Tower property" (@cor-total-expectation, line 244)** is the law of iterated expectations, a name many health researchers will not recognize. A parenthetical "(the law of iterated expectations)" on first use would bridge the jargon.
- **The heat-equation notation $e^{(\tau/2)\partial_m^2}$ (line 410)** is operator notation that assumes familiarity with semigroup language. For a beginner this is opaque; for me it read as a symbol I could not parse.

## Pacing issues

- **The chapter front-loads three heavy abstractions (individual model, aggregate model, aggregation theorem) before any concrete numerical work**, spanning lines 93-278. That is roughly 185 lines of pure formalism with no example. Splitting this with a mini-example after @def-aggregate-model would break the wall.
- **The bias section (@sec-agg-bias, lines 280-386) crams the theorem, proof, equality case, leading-order expansion, and the MAIC/STC reconciliation into one section** with no breath. The leading-order lemma @lem-agg-bias-expansion deserves its own subsection because it is the workhorse used by the logit and log results later.
- **The heat-flow section (@sec-agg-heat, lines 388-453) comes between the bias theory and the identity-link case**, but it is the hardest math in the chapter and is not needed until the log and logit sections. A beginner would be better served seeing the easy identity case first, then the log closed form, and only then the heat-flow unification. As written, the most abstract material interrupts the build-up of concrete cases.
- **The three link sections (@sec-agg-identity, @sec-agg-log, @sec-agg-logit, lines 455-697) vary wildly in length and difficulty.** The identity section is short and easy; the log section is moderate; the logit section is long and dense with a four-part theorem. The pacing acceleration is steep and I ran out of stamina before the worked example.
- **The worked example (@sec-agg-example, line 699) comes at the very end**, after all the theory. Pedagogically, I would want the discrete logit example immediately after @thm-aggregation-bias so I could feel the bias before reading about heat flow.

## What worked well

- The opening paragraph (lines 7-16) cleanly positions ML-NMR against MAIC and STC from Part IV, and the "three limitations at once" framing gave me a clear reason to keep reading.
- The sign-reversal worked example (@exm-agg-logit-discrete, lines 709-774) is genuinely illuminating once I reached it: the contrast between the 1.30 plug-in and 1.22 integrated log odds ratio is the single clearest demonstration in the chapter of why plugging in the mean is wrong.
- The "integrate the response scale, not the link scale" remark (lines 173-183) states the core design decision of ML-NMR in one crisp sentence; that sentence alone taught me more than several of the proofs.
- The closing notes (lines 812-851) honestly flag the absence of a Coq formalization and locate each result in the source literature, which gave me confidence about provenance even when the math was over my head.

## Suggestions

1. Open the chapter with a one-paragraph concrete scenario (plaque psoriasis or multiple myeloma, an IPD trial and an AgD trial, the B-vs-C question an HTA body is asking), and reference it whenever a new object ($f_j$, $\theta_{\bullet jk}$, $\boldsymbol\xi$) is introduced.
2. Insert a small numerical example (two covariate values, two patients) immediately after @thm-aggregation so the reader sees the integral evaluate to a number before the bias theory begins.
3. Add a figure showing $\mathrm{expit}$ with the convex region ($m<0$) and concave region ($m>0$) shaded, illustrating the sign reversal of the bias; reference it in @thm-aggregation-bias and again in @thm-logit-no-closed-form(c).
4. Move the heat-flow section (@sec-agg-heat) to after the three link sections, or clearly label it as an optional unifying aside, so beginners can follow the concrete cases first.
5. Gloss "affine," "tower property," "outcome family," "heat semigroup," and "Jensen's equation" on first use with a parenthetical in plain English.
6. Expand the SEMA discussion (around line 140) into a short subsection with a counterexample of what breaks when SEMA fails, since identifiability of the mixed network rests on it.
7. Give the worked-example parameters clinical meaning (name the covariate, the outcome, the treatments) so the 1.22 vs 1.30 log odds ratio reads as an HTA result rather than abstract arithmetic.
8. Promote the Poisson-binomial point (line 179) from a remark to a sentence in the main text, since most readers will hit ML-NMR through binary outcomes and need to know the binomial aggregate law is approximate.
9. Prove the NMA reduction (currently exercise @exr-agg-nma-reduction and deferred to Chapter 23) inline in one paragraph, so the reader from Chapter 15 sees the bridge immediately.
10. Add a one-paragraph subsection on the non-collapsibility connection (line 782), with the odds-ratio case spelled out, since it is the most contested link to the rest of the causal-inference literature and currently appears as an afterthought.