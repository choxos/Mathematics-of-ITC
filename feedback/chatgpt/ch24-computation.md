# Chapter 24 Feedback: Bayesian Computation and Diagnostics

## Overall reaction

This is a rigorous and useful chapter, but for a novice health researcher it often reads more like a mathematical diagnostic reference than a guide to deciding whether an indirect treatment comparison fit can be trusted. The opening motivation is strong: it clearly separates Monte Carlo error from numerical integration error, and it explains why ML-NMR has both. That framing is exactly what a reader new to Bayesian ITC needs.

The main weakness is that the chapter moves very quickly from practical worries to formal derivations. A motivated reader who knows health research but is weak in abstract mathematics may understand that R-hat, effective sample size, divergences, LOO, WAIC, and Pareto k matter, yet still not know what to do when one of them is bad. The chapter proves why the diagnostics work, but it gives less help with the decision process: when to rerun, when to reparameterize, when to increase integration points, when to distrust model comparison, and when a problem is a statistical modeling issue rather than a computational one.

## What was clear

The introduction gives a clear reason for the chapter. The distinction between finite-chain Monte Carlo error and nested QMC integration error is especially helpful because it ties the computation directly to ML-NMR rather than presenting generic Bayesian software advice.

The centered versus non-centered parameterization section has a clear conceptual target. The chapter explains that the two parameterizations are the same statistical model but different coordinate systems for HMC. That is an important point for a novice because it prevents the common misunderstanding that non-centering changes the estimand or the likelihood.

The warning about two meanings of effective sample size is well placed. A reader who has just learned MAIC could easily confuse weighting ESS with MCMC ESS, so the early remark helps.

The AR(1) effective sample size example is one of the most accessible parts of the chapter. It gives a concrete feel for autocorrelation: 4000 draws can behave like 2000 draws or only about 210 draws, depending on stickiness.

The integration doubling rule is practically valuable. The reader gets a simple operational check, a tolerance, and an explanation that QMC error is deterministic conditional on the point set. This is a good bridge from Chapter 22 to actual ML-NMR fitting.

The Pareto k thresholds are mostly clear once reached. The chapter explains why k below 0.5, between 0.5 and 1, near 0.7, and above 1 imply different levels of trust in PSIS-LOO. The final remark usefully frames high k as both a reliability warning and a substantive signal of an influential or poorly fit aggregate cell or study.

## What was unclear

HMC and NUTS are introduced as the engines of Stan, but the chapter does not give enough of a refresher for a reader who only vaguely remembers Chapter 8. The reader is told that HMC simulates Hamiltonian trajectories and that NUTS is adaptive, but not what NUTS actually changes in practice. A novice will not know whether a bad fit should be addressed through more iterations, higher `adapt_delta`, more warmup, a different mass matrix, non-centering, stronger priors, or a model change.

The discussion of divergences is too brief relative to its importance. Divergent transitions appear in the parameterization section as the symptom of the funnel, but the chapter never gives a practical definition in health research language. A novice needs a sentence such as: a divergence means Stan could not accurately follow the posterior geometry in part of the space, so some posterior regions may be under-sampled and the reported treatment effect may be biased. The chapter should also explain why even a small number of divergences after warmup is not something to ignore.

The centered versus non-centered practical rule is helpful but too abstract. "Use NCP when tau is weakly identified and CP when it is strongly identified" is mathematically accurate, but a novice may not know how to diagnose weak identification in an HTA evidence network. The section would benefit from concrete cues: few studies per contrast, sparse aggregate cells, wide posterior for tau, divergences near small tau, and strong shrinkage of study effects.

The R-hat section proves the statistic carefully, but the practical interpretation is thin. The chapter gives the 1.01 threshold, but it does not explain what quantities should be checked in ML-NMR: treatment contrasts, heterogeneity tau, study baselines, effect modifiers, transformed marginal probabilities, generated quantities, and log likelihood contributions. A novice may wrongly check only the headline contrast.

The information criteria section assumes a factorized likelihood over observations. For ML-NMR, the novice reader needs help identifying what an "observation" is. Is the pointwise unit an individual patient, an aggregate arm, an aggregate contrast, a study arm cell, or a study? This matters directly for WAIC, LOO, Pareto k, and standard errors of model-comparison differences.

The chapter uses "model comparison" more than "model checking." A health researcher may infer that WAIC or PSIS-LOO is the main way to decide whether a model is acceptable. The chapter should more clearly separate computational diagnostics, posterior predictive checks, prior sensitivity, covariate overlap or transportability checks, and predictive criteria. A model can have good LOO and still answer the wrong ITC question if the target population, effect modification structure, or exchangeability assumptions are wrong.

## Under-explained details

Warmup, adaptation, and post-warmup draws need a short explanation. The worked example starts with post-warmup draws, but a novice may not know that warmup draws are discarded because Stan is tuning the sampler and moving toward the typical set.

The "typical set" is absent. Since HMC diagnostics are really about whether the sampler explores the posterior geometry, a brief intuitive account of the typical set would help readers understand why posterior mode finding and posterior sampling are different tasks.

Mass matrix adaptation is mentioned only in the notes. For a novice, this is a missing bridge because parameterization, curvature, and step size are all tied to how Stan rescales the posterior. The chapter does not need a full derivation, but it should say that Stan learns a metric during warmup and that non-centering helps when rescaling alone cannot remove a funnel.

The leapfrog stability proof is mathematically clear but under-motivated for the target reader. Before the matrix calculation, the chapter could give a health research analogy: if one direction in the posterior is extremely narrow, the sampler must take tiny steps there, which makes exploration of wider directions painfully slow.

The relative doubling rule uses `|theta_hat_N|` in the denominator. The chapter should mention what to do when the aggregate-cell quantity is near zero or when the scale is log odds, log hazard, or another transformed quantity. A novice might apply the relative tolerance mechanically where an absolute tolerance would be safer.

The thresholds need more practical context. R-hat below 1.01, bulk and tail ESS above 400, integration tolerance 0.005, and Pareto k around 0.7 are all given, but the reader needs a compact explanation of which thresholds are hard failures, which are warnings, and which depend on the precision needed for the reimbursement or comparative-effect decision.

The DIC discussion explains why DIC is inferior, but a novice may still wonder whether to report it because older NMA literature often does. A short note could say: report WAIC or PSIS-LOO for modern Bayesian model comparison, and report DIC only when required for comparison with older analyses, with caveats.

## Where a novice may get lost

The first likely loss point is the move from the intuitive funnel story to Hessians, eigenvalues, and leapfrog stability. The reader may understand that small tau causes trouble but not why curvature equals `1/tau^2` or why this forces the step size toward zero. A short visual or verbal bridge before the theorem would help.

The R-hat derivation is long and formal. A novice can follow the definitions of W and B, but the expectation identities and the role of autocorrelation may obscure the core message: R-hat asks whether independent chains are telling the same posterior story. The proof should be followed by a plain-language box that explains common failure patterns, such as chains stuck in different modes, slow drift, and one chain with a different mean.

The ESS section uses autocorrelation in a way that may be unfamiliar. The AR(1) example helps, but the earlier formula with the infinite sum may be intimidating. A small table showing phi, integrated autocorrelation time, and effective sample size would make the idea more usable.

The information-criteria section is probably the hardest part for the intended reader. Cumulant generating functions, harmonic means, elpd, lppd, DIC, WAIC, and LOO all arrive close together. The reader needs a stronger bridge sentence: all of these are attempts to estimate how well the model would predict data not used to fit it, and the penalties correct for the fact that in-sample prediction is too optimistic.

PSIS smoothing is under-explained algorithmically. Fitting a generalized Pareto distribution to the largest ratios and replacing them with expected order statistics is technically accurate, but a novice will not understand what is being smoothed. A small numeric or graphical example showing one extreme weight before and after smoothing would make Pareto k much more concrete.

The worked example is useful for arithmetic but not fully useful for ITC judgment. It uses tiny artificial chains, two observations, and no real ML-NMR data structure. It proves the calculations are checkable, but it does not show what a diagnostic report for an actual treatment network would look like.

## Suggested improvements

Add a short "How to use this chapter in practice" subsection before the final example. It should give the sequence a health researcher should follow: check divergences and treedepth, check R-hat, check bulk and tail ESS, inspect problematic parameters and pairs plots, check QMC doubling for aggregate cells, run posterior predictive checks, then use PSIS-LOO or WAIC only after the fit is computationally trustworthy.

Add a stoplight table for diagnostics. Rows could include divergences, R-hat, bulk ESS, tail ESS, QMC doubling, Pareto k, and large model-comparison standard errors. Columns could be "what it means," "why it matters for an ITC," and "what to try next."

Give one ML-NMR-specific example of pointwise log likelihood. For example, show whether the pointwise units are aggregate arms, aggregate contrasts, or individual observations when both IPD and AgD are present. This would make WAIC, LOO, and Pareto k far easier to apply correctly.

Expand the divergence discussion into a practical diagnostic subsection. Include what divergences mean, why they often indicate geometry rather than too few iterations, and typical remedies: non-centered parameterization, stronger priors on tau, rescaling covariates, increasing `adapt_delta`, and checking whether the model is overcomplicated for the evidence network.

Add one concrete HTA interpretation after each major diagnostic. For R-hat: different chains imply the treatment contrast estimate is not stable. For ESS: the credible interval endpoints may be noisy. For integration error: the aggregate likelihood itself is approximate. For Pareto k: one study or arm may be dominating model comparison. For LOO and WAIC: predictive fit is not the same as validity of the transportability assumptions.

Strengthen the worked example by adding a miniature evidence network. Even a two-study AB and BC example with one aggregate arm and one treatment contrast would help the reader connect diagnostics to ITC reporting. The current example is good for arithmetic, but it does not yet teach what to write in a methods or results section.

Make the exercises more scaffolded. Several are accessible, especially the R-hat, ESS, and doubling exercises. The starred exercises on R-hat bounds and Pareto tails are much harder. Consider adding a first exercise that asks the reader to interpret a Stan diagnostic table in words before doing algebra.

## Highest-priority fixes

1. Add practical guidance for HMC, NUTS, divergences, warmup, and common remedies. This is the biggest gap for a novice who must decide whether a Bayesian ITC fit is trustworthy.

2. Clarify what the pointwise likelihood unit is in ML-NMR and mixed IPD plus AgD settings. Without that, WAIC, LOO, PSIS, and Pareto k are mathematically defined but hard to apply correctly.

3. Add a diagnostic decision workflow that says what must be checked before model comparison is meaningful. R-hat, ESS, divergences, QMC error, posterior predictive checks, and Pareto k need to be ordered into a practical sequence.

4. Turn the worked diagnostic example into a small ML-NMR-style report, or add a second example that looks like one. The arithmetic example is clear, but it does not yet show how these diagnostics protect a real indirect comparison.

5. Add plain-language bridge paragraphs after the most formal derivations. The chapter is mathematically strong, but the intended novice reader needs more statements of the form: "In practice, this means..."
