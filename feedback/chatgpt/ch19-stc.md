# Chapter 19 Feedback: Simulated Treatment Comparison

## Overall reaction

From the perspective of a motivated novice health researcher, the chapter has a strong core idea: STC is the outcome-model route to the same target-population problem that MAIC addresses by weighting. The opening contrast, "MAIC bends the sample, STC bends a model," is memorable and gives the reader a useful mental handle.

The chapter is also much harder than it needs to be at first contact. It often moves from a clinical motivation to formal notation, asymptotic theory, and proof language before the practical workflow is fully anchored. A novice can see that STC fits a regression in the index trial and predicts into the comparator population, but may not yet understand exactly what is being predicted, what is being simulated, why the target covariate distribution matters, and how this creates an A versus B estimate. The chapter would be much more teachable if it first gave a plain workflow, then returned to the theorems.

## What was clear

- The introduction clearly explains the basic contrast between MAIC and STC. The idea that MAIC leaves outcomes untouched and changes the sample, while STC leaves the sample untouched and changes the model, is one of the clearest parts of the chapter.
- The anchored triangle is well motivated. The reader is told that the immediate job is to estimate the A versus C effect in the BC population, then use Bucher's subtraction with the published B versus C effect.
- The conditional versus marginal distinction is conceptually important and the chapter identifies it correctly. The phrase "the outcome of the average" versus "the average of outcomes" is the right intuition for a novice, even if it could be foregrounded more.
- The worked logistic example is helpful because it computes three different values: conditional plug-in, target marginal STC, and source marginal. That makes the estimand problem visible.
- The remarks after the worked example are useful. "What population adjustment moves" and "Closing the triangle" are exactly the kind of interpretive paragraphs a health researcher needs.
- The comparison with MAIC near the end gives a useful practical message: MAIC depends on overlap and weights, while STC depends on a correctly specified model and extrapolation.

## What was unclear

- The word "simulated" is not explained operationally enough. A novice may ask: are we simulating outcomes, patients, covariates, missing treatment arms, or only averaging fitted predictions over a target covariate distribution? The chapter eventually says that covariate vectors are sampled from \(f_{BC}\), but the reader needs this much earlier.
- The sign convention is a serious comprehension obstacle. The chapter introduces \(\Lambda=\eta_A-\eta_C\), then \(d_{AC}=\eta_C-\eta_A\), then uses \(\ell_{AC}\) for active versus reference log odds ratios. The orientation remark is honest, but a novice will likely keep wondering whether positive means A is better, A is worse, or only "A versus C" in a model convention.
- Conditional transportability, conditional constancy of relative effects, and correctness of the outcome surface are all used, but their relationship is not intuitive. A novice needs a bridge sentence such as: "For STC, we assume that once we condition on the selected covariates, the fitted A and C outcome curves from the AC trial can be used for patients like those in the BC trial."
- The "no overlap required" message could be misunderstood. Mathematically, STC does not require MAIC-style positivity for weights, but practically it may extrapolate into covariate regions where the index trial has no patients. A novice health researcher should be warned that this is not a free advantage.
- Covariate simulation from aggregate data is underdeveloped. The chapter mentions Gaussian copulas and Chapter 22, but a reader may not understand what to do when the BC publication reports only means, standard deviations, proportions, or no correlations.
- The uncertainty discussion is mathematically sophisticated but not practically separated into sources. A novice needs to distinguish outcome-model parameter uncertainty, Monte Carlo simulation uncertainty, uncertainty in the reconstructed BC covariate distribution, and uncertainty in the published B versus C estimate.
- There is a small numerical consistency issue that may confuse readers: the closing-triangle remark reports \(-1.44270\), while Step 2 reports \(1.44261\) on the active-versus-reference scale. Even a tiny mismatch can make a novice suspect that the sign convention or arithmetic has changed.

## Under-explained details

- STC model building needs more practical explanation. The chapter defines the GLM, prognostic effects, and treatment-by-covariate interactions, but it does not slow down enough to explain how a health researcher decides which covariates are prognostic variables, which are effect modifiers, and which interactions must be included.
- G-computation is referenced often, but the STC version needs a boxed recipe. For example: fit \(\mu_A(x)\) and \(\mu_C(x)\) in the AC IPD, create or obtain covariates from the BC population, predict both treatment outcomes for each target covariate profile, average those predictions on the outcome scale, then take the contrast.
- Target-population prediction needs a more concrete interpretation. The reader should be told that STC is asking: "What would the outcomes have looked like if patients with the BC trial's covariate distribution had received A and C, using the response model learned from the AC trial?"
- Non-collapsibility is central, but the chapter still leans heavily on link-scale algebra. A novice may not yet feel why an odds ratio changes after averaging even when the treatment effect is constant within covariate strata. A small two-stratum table before the theorem would help.
- The conditional plug-in bias theorem is mathematically precise, but the Taylor expansion and Jensen gap arrive before enough plain intuition. The reader needs a short warning first: "A nonlinear curve makes the prediction at the mean covariate different from the mean of the predictions."
- Covariate simulation deserves its own explanation. The chapter should say what happens with binary covariates, continuous covariates, correlations, impossible combinations, and missing covariance information.
- Variance is under-explained for applied use. The Bayesian g-computation section explains pushforwards and Bernstein-von Mises, but a novice needs to know what uncertainty should appear in a confidence or credible interval for the final A versus B comparison.
- The exercises are good but steep. The delta-method variance and log-link cancellation exercises are valuable, but the chapter also needs at least one low-barrier implementation exercise that walks through a full STC table with supplied synthetic target covariates.

## Where a novice may get lost

- The first major technical section begins with the outcome model, likelihood, score, information, and MLE asymptotics. A novice health researcher may not yet know why these are needed for using STC. This proof-heavy opening risks hiding the practical STC workflow.
- The notation load is high: \(\mathcal P_{AC}\), \(\mathcal P_{BC}\), \(f_{BC}\), \(\eta_k\), \(\mu_k\), \(\bar\mu_{k(\mathcal P)}\), \(d_{AC}^{\mathrm{cond}}\), \(d_{AC}^{\mathrm{marg}}\), and \(\Lambda\) all appear early. A symbol table specific to STC would reduce friction.
- The transition from conditional STC to marginal STC is the chapter's most important learning point, but it is embedded in formal estimand definitions. A novice may not realize that conditional STC is not "slightly approximate STC," but a different estimand for nonlinear links.
- The non-collapsibility counterexample is useful, but it appears after several abstract statements. A reader weak in mathematics may benefit from seeing the same idea first as a simple clinical probability table with two risk strata.
- The Bayesian g-computation section will likely be difficult for the target novice. Terms like pushforward, weak convergence, Bernstein-von Mises, and total variation distance are mathematically appropriate, but the section needs a plain-language paragraph saying what posterior simulation is doing in applied STC.
- The final MAIC and STC equivalence theorem is conceptually useful but dense. A novice may miss the practical takeaway: if the outcome model is linear and MAIC balances the covariate means that matter, both methods are estimating the same target contrast.

## Suggested improvements

- Add an "STC in five steps" box immediately after the introduction. It should state the applied workflow before the formal model.
- Add a small STC-specific notation table before the outcome model. Include source population, target population, conditional mean, marginal mean, conditional effect, marginal effect, and final Bucher contrast.
- Add a sign-convention table. Show active-versus-reference \(\eta_A-\eta_C\), reference-first \(d_{AC}=\eta_C-\eta_A\), and how each enters the worked example and Bucher subtraction.
- Add one short clinical motivation paragraph before the formulas. For example, describe a comparator trial that enrolled older or higher-risk patients, then explain why predicting A and C outcomes for those patients is the target.
- Move a very small numerical example earlier, before the MLE theorem. Even two covariate strata and two fitted probabilities would help the reader understand why marginalization must happen on the response scale.
- Expand the explanation of covariate simulation from aggregate data. Include what is assumed when only means are available, what extra information correlations provide, and why a wrong reconstructed \(f_{BC}\) can bias STC.
- Rephrase the "no overlap required" remark to distinguish mathematical definability from scientific credibility. STC can extrapolate without weights, but extrapolation should be diagnosed and reported.
- Add a practical variance paragraph before or after Bayesian g-computation. Separate model-parameter uncertainty, target-covariate simulation uncertainty, reconstructed-distribution uncertainty, and comparator-trial uncertainty.
- Add bridge sentences after each theorem that translate the result into applied language. For example: "This theorem says that if the model is right and the target covariate distribution is right, marginal STC estimates the trial result we would expect in the BC population."
- Add one easier exercise that provides fitted coefficients and a small table of target patients, then asks the reader to compute predicted probabilities, average them, apply the link, and close the triangle.

## Highest-priority fixes

1. Add a plain STC workflow box near the start: fit the AC outcome model, generate or obtain BC covariates, predict A and C outcomes for the BC population, average on the outcome scale, apply the link, then combine with the published BC contrast.
2. Clarify conditional versus marginal STC before the formal bias theorem. This is the central novice learning hurdle.
3. Simplify and tabulate the sign conventions. The current \(\Lambda\), \(d_{AC}\), and \(\ell_{AC}\) switching is likely to confuse readers.
4. Add a concrete explanation of covariate simulation from aggregate data, including the limitations when only marginal summaries are published.
5. Temper the "no overlap required" language with an explicit warning about extrapolation and model dependence outside the index trial support.
6. Make the non-collapsibility explanation more intuitive with a small two-stratum probability table before the algebra.
7. Add a practical uncertainty checklist so readers know what variance components matter in a real STC analysis and in the final A versus B indirect comparison.
