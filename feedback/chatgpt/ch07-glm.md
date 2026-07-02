# Chapter 7 Feedback: Generalized Linear Models
## Overall reaction

This chapter is strong as a rigorous mathematical bridge from linear regression to the outcome models used in indirect treatment comparisons. As a novice health researcher, I found the opening clinical motivation genuinely helpful: binary response, adverse event counts, person-time, and survival outcomes make it clear why ordinary linear regression is not enough.

The main weakness is that the chapter often moves from a helpful health research motivation into a high-density formal proof before the reader has a stable mental picture of the objects. The exposition is mathematically careful, but it sometimes expects the reader to hold too many scales at once: observed outcome, mean, natural parameter, linear predictor, link scale, treatment contrast, conditional effect, and marginal effect. A motivated novice could follow parts of the chapter, especially the logistic and Poisson interpretations, but may lose the thread in the exponential dispersion family, score equations, Fisher information, and deviance sections.

The chapter would work better pedagogically if it repeatedly returned to one simple trial example and used it to label every symbol before proving the general result.

## What was clear

The introduction explains the need for GLMs well. The examples of response counts, adverse event counts, and fitted probabilities outside $[0,1]$ give a concrete reason why the normal linear model is structurally wrong for common health outcomes.

The explanation of logistic regression is one of the clearest parts. The movement from probability to odds to log odds to odds ratio is readable, and the statement that a treatment coefficient is a conditional log odds ratio is exactly the kind of interpretation a health researcher needs.

The Poisson regression section also gives a useful practical interpretation, especially the offset explanation for person-time. This is a good health research bridge because rates and incidence rate ratios are familiar targets.

The remark "IRLS in words" is very helpful. It gives the reader a plain-language version of an otherwise intimidating algorithm and ties the procedure back to weighted linear regression.

The two-stratum odds ratio example is valuable. It is concrete, numerical, and directly connected to the later ITC problem of conditional versus marginal estimands. This is probably the most important conceptual example in the chapter.

The worked logistic regression example is useful because it gives actual data, actual coefficients, one IRLS step, and a deviance test. The fact that all numbers can be checked with a calculator fits the stated audience well.

## What was unclear

The exponential dispersion family definition is too abrupt for a novice. Terms such as reference measure, natural parameter space, cumulant function, dispersion parameter, prior weight, and $c(y,\phi)$ arrive together. The text says this is the random component of a GLM, but it does not first give the reader a simple mental model like: "this is a template that lets Bernoulli, binomial, Poisson, normal, and gamma distributions share the same estimation machinery."

The role of the prior weight $w$ is especially unclear. The binomial proportion example later says $w=n$, but a novice may not understand why the response is $Y=R/n$ rather than $R$, why the denominator becomes a weight, or how this relates to a trial arm with $R$ responders out of $n$ randomized patients.

The chapter asks the reader to distinguish $\theta$, $\eta$, $\mu$, $g(\mu)$, $g^{-1}(\eta)$, $b'(\theta)$, and $\boldsymbol\beta$ before giving a simple symbol map. The "note on three reused symbols" is helpful, but it also signals that the notation is fragile. A novice could still confuse the natural parameter $\theta$ with the mean $\mu$ and the network-model mean symbol from the notation chapter.

The transition from canonical links to non-canonical links needs more motivation. The text says the canonical link gives analytic and computational simplifications, but the practical reason for using or not using canonical links is not fully explained. For example, the reader may wonder why anyone would use probit or complementary log-log if logit is canonical and interpretable.

The maximum likelihood section is mathematically coherent, but the reader may not know what problem is being solved in practical terms. The score equations, information matrix, and IRLS proof would benefit from a short preface saying what software is trying to do when it fits a logistic regression model.

The deviance section introduces saturated models, scaled deviance, deviance, residual deviance, deviance residuals, and Bregman divergence in quick succession. The practical message, "this is how we measure lack of fit and compare nested GLMs," is present, but it comes after a lot of abstraction.

The hazard ratio discussion is too compressed for this point in the book. The formula involving population-averaged survival functions and integrated hazards uses survival notation that has not yet been developed. The qualitative message is important, but the mathematical statement may feel premature.

## Under-explained details

The chapter needs a clearer explanation of scale. A novice health researcher needs repeated reminders of which scale each quantity lives on: probability scale, count scale, mean scale, linear predictor scale, log odds scale, log rate scale, and ratio scale after exponentiation.

The variance function $V(\mu)$ is important but under-motivated. The Bernoulli and Poisson examples help, but the chapter could state more explicitly why this matters for trial data: the uncertainty in a 50 percent response rate is not the same as the uncertainty near 0 percent or 100 percent, and the uncertainty in a count often grows with the expected count.

The grouped binomial setup deserves more explanation. Many health researchers think in tables with responders and nonresponders, not in proportions with prior weights. A short worked mini-example before the formal table would help: $R=18$ of $n=60$, so $y=0.30$, $w=60$, $\mu=p$, and $\mathrm{Var}(Y)=p(1-p)/60$.

The difference between conditional and marginal effects should be prepared earlier. The chapter states that GLMs combine effects on the link scale, then later shows non-collapsibility. The bridge could be stronger: "a coefficient from logistic regression is conditional on the covariates in the model; an ITC decision problem may require a population average."

The statement that the odds ratio is universally attenuated toward the null appears in the non-collapsibility example, but the proof is left to a difficult starred exercise. As a novice, I would either want the statement softened in the example or given a short intuitive justification there.

Overdispersion is not sufficiently discussed. The chapter says the dispersion does not affect $\hat{\boldsymbol\beta}$ for the score equations and notes known versus unknown $\phi$, but health researchers often encounter extra-binomial or extra-Poisson variation. Even a short remark explaining where overdispersion does and does not fit would prevent confusion.

Separation is mentioned clearly, but it would benefit from a tiny health example, such as a subgroup table where all treated patients respond and no controls respond. That would make the failure of a finite logistic maximum likelihood estimate less abstract.

## Where a novice may get lost

A novice may get lost at the first theorem on EDF mean and variance. The proof relies on moment generating functions, normalization, cumulant generating functions, and inverse functions. The result is important, but the payoff should be stated before the proof in simple terms: once you know $b$, you know the mean and variance.

The chain rule derivation of the score equations is another likely stumbling point. It is correct and detailed, but the chain $\boldsymbol\beta\mapsto\eta_i\mapsto\mu_i\mapsto\theta_i$ is abstract. A small logistic-only derivation next to the general derivation would help the reader see what the pieces mean.

The Fisher information section may feel like a wall of matrices. The reader has just learned that GLMs are about valid means and link functions, then suddenly must parse $\mathbf D$, $\boldsymbol\Sigma$, $\mathbf W$, positive definiteness, and full column rank. A bridge sentence explaining why information becomes the standard error formula would help.

The IRLS theorem is hard before the worked example. The later example makes it much clearer, so the chapter might preview that example before the theorem or insert a one-row intuition for the working response $z_i$.

The non-collapsibility definition is formal before it is intuitive. The two-stratum example is easier to understand than the definition. A novice may benefit from seeing the example first, then returning to the formal definition once the problem is visible.

The exercises are mostly appropriate for a mathematically ambitious reader, but several are demanding for the stated novice health researcher. The starred probit IRLS and non-collapsible odds ratio exercises are advanced. The set could use more entry-level exercises that ask for interpretation of coefficients, construction of a simple trial arm likelihood, and explanation of conditional versus marginal effects in words.

## Suggested improvements

Add a short "GLM ingredients in one trial arm" subsection before the exponential dispersion family. Use one binary trial arm and one count outcome to show the response, mean, variance, link, linear predictor, and treatment coefficient before introducing the EDF template.

Add a symbol table inside the chapter for $\theta$, $\eta$, $\mu$, $g$, $g^{-1}$, $b$, $V(\mu)$, $w_i$, $\phi$, and $\boldsymbol\beta$. The notation chapter is useful, but Chapter 7 needs a local map because the same few symbols drive the whole argument.

Give the grouped binomial case more space. This is central for ITC trial data, and the proportion plus weight formulation will not be obvious to many readers.

Add short "why this matters for ITC" bridge paragraphs after the link function section, after the estimation section, and before deviance. The introduction does this well, but the middle of the chapter becomes mostly general GLM theory.

Put a small logistic regression calculation before or inside the score equation section. For example, show that with logit link the score has the familiar form $\sum_i n_i(y_i-p_i)x_{ij}=0$. This would make the general score formula feel less mysterious.

Expand the deviance intuition before the Bregman divergence proof. A novice needs to know that deviance compares the fitted model to a perfect fit, then uses likelihood differences to test whether added covariates improve fit.

Move some of the hazard ratio detail to a later chapter or add a clear warning that this is only a conceptual preview. The current paragraph is important but mathematically too compressed for a first GLM chapter.

Add a few lower-barrier exercises. Examples: interpret a logistic treatment coefficient from a small table, compute a fitted probability from a linear predictor, identify the link and variance function for a trial outcome, and explain in words why marginal and conditional odds ratios can differ without confounding.

## Highest-priority fixes

1. Add a novice-friendly map of the GLM objects and scales before the EDF definition.
2. Expand the grouped binomial explanation because it is the main bridge from trial response data to GLMs for ITCs.
3. Add a simple logistic-specific derivation beside the general score and IRLS formulas.
4. Strengthen the bridge between conditional link-scale coefficients and marginal population estimands before the non-collapsibility section.
5. Make the deviance section more intuitive before introducing saturated models and Bregman divergence.
6. Either soften the universal attenuation claim for odds ratios or provide a short explanation before leaving the proof to an exercise.
