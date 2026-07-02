# Chapter 25 Feedback: General Likelihoods: Survival and Ordered Categorical Outcomes
## Overall reaction

This chapter has a strong and useful message: ML-NMR is not just a binary, normal, or count-outcome method, because the deeper operation is to average an individual-level likelihood over the covariate distribution. That is exactly the right conceptual point for a health researcher who wants to understand how time-to-event and ordinal endpoints enter population-adjusted comparisons.

The main problem is that the chapter often explains the mathematics after the formal theorem, not before it. A novice health researcher can follow pieces of the story, especially the survival definitions and the worked exponential example, but may not have enough intuitive scaffolding to understand why the same integral solves censored survival data, ordered categories, and aggregate-data arms. The chapter feels rigorous, but it sometimes assumes the reader already thinks like a mathematical statistician.

## What was clear

The opening motivation is effective. It names endpoints health researchers actually see, including time to event, progression-free survival style endpoints, performance status, pain scales, and ordered response bands. The contrast with one-parameter GLM outcomes helps explain why the chapter is needed.

The statement that general-likelihood ML-NMR averages a conditional likelihood over the study covariate distribution is the clearest organizing idea in the chapter. The sentence-level distinction between aggregating a mean and aggregating a likelihood is especially helpful, even though it needs more examples.

The definitions of survival function, hazard, cumulative hazard, and right-censored likelihood are mostly readable. The event branch versus censoring branch in the censored likelihood is concrete: an observed event uses density, while a censored observation uses survival probability. That is a good novice bridge.

The RMST section makes the key point cleanly: RMST is the area under the survival curve, and the marginal RMST equals the average conditional RMST. The proof is formal, but the idea is accessible.

The fully worked exponential-hazard example is the most novice-friendly part of the chapter. The binary covariate keeps the integration visible as a two-point average, and the table showing the marginal hazard ratio changing over time makes non-collapsibility much easier to believe.

## What was unclear

The conditional versus marginal hazard ratio distinction needs more setup before the theorem. A novice may know Cox regression reports hazard ratios, but may not know whether those are conditional, marginal, model-based, covariate-adjusted, or population-specific. The phrase "the quantity a single Cox fit to a population would report" needs a slower explanation, because it is central to the chapter's claim that the marginal hazard ratio is not transportable.

The hazard is introduced as an instantaneous event rate, but the reader may still confuse it with a probability. The text says $h(t\mid x)\Delta t$ is approximately a probability, which is useful, but it would help to add a small numerical statement such as "a hazard of 0.2 per year means about 0.2 times a short interval in years, not a 20 percent probability over all follow-up."

The move from AgD to "possibly reconstructed individuals" is abrupt. The chapter says an AgD study has individual observations $y_{1jk},\dots,y_{n_{jk}jk}$ and later says these may be pseudo-IPD reconstructed from Kaplan-Meier curves. A novice may ask: if this is aggregate data, where did individual rows come from? This needs a bridge paragraph before @thm-aggregate-marginal-likelihood.

The survival aggregation result is mathematically clear, but its applied interpretation is not fully spelled out. The chapter should say explicitly that, for each reconstructed time and censoring indicator, we average the likelihood over plausible unobserved covariate values for that study, then multiply those averaged contributions across pseudo-patients.

The ordered categorical section is too short compared with the survival section. The proportional-odds model is stated correctly, but a novice health researcher may not understand what the cutpoints do, why the same slope across cutpoints is called proportional odds, or how a positive $\eta$ changes the chance of being in better or worse categories. The sign convention in $\operatorname{logit}P(Y\le k)=\alpha_k-\eta(x)$ needs a plain-language direction-of-effect explanation.

The chapter mentions mixed likelihood networks only implicitly. It is clear that the framework can accept different outcome likelihoods, but it is not clear whether one network may combine survival, ordinal, binary, and count outcomes in the same treatment-effect model. If the intent is "same machinery for different outcome families, one outcome family at a time," that should be said. If genuinely mixed outcome likelihoods can be combined, the chapter needs to explain the shared parameter or estimand that makes the combination meaningful.

## Under-explained details

The baseline hazard $h_{0j}(s)$ deserves more explanation. The remark says the scalar study intercept $\mu_j$ becomes a baseline log-hazard function, but a novice may not know what it means for every study to have its own baseline hazard while treatment effects are shared through the network. A short analogy to study intercepts in logistic or normal models would help.

Independent censoring is defined formally, but the health-research interpretation is thin. The chapter should explain common examples: administrative censoring at data cutoff, loss to follow-up unrelated to prognosis after conditioning on covariates, and informative dropout that would violate the assumption.

RMST is described as collapsible but not automatically transportable. That is an important warning, but it is too compressed. A novice may hear "collapsible" and assume "safe to compare across populations." The chapter should add a simple two-population example before pointing forward to Chapter 26.

The relationship between PH, RMST, and ML-NMR estimands needs a clearer decision rule. If the model is fitted on the log-hazard scale but RMST is a read-out, the reader needs to know what should be reported, what is transported, and what target population the reported RMST contrast belongs to.

The general-likelihood theorem uses $\pi_{\mathrm{Ind}}$, $\boldsymbol\theta$, $\boldsymbol\xi$, $\eta_{jk}(x)$, $f_j$, IPD arms, and AgD arms all at once. A novice would benefit from a small table mapping each object to a practical item: patient outcome model, patient covariates, study covariate distribution, treatment-effect parameters, and observed arm data.

The final formula in Step 5 of the worked example may confuse readers. The earlier event contribution for high-risk patients is $\lambda_1 e^{-\lambda_1 t_1}$ with $t_1=0.5$, which suggests $\lambda_1 e^{-\lambda_1/2}$ when written as a function of $\lambda_1$. The displayed function uses $e^{-3\lambda_1/2}$. If that is intentional, it needs explanation; if not, it will make novices doubt their arithmetic.

## Where a novice may get lost

The introduction has many cross-references to Chapters 20 through 24 before the new idea is made concrete. A novice who does not remember moment generating functions, Sobol' nets, Gaussian copulas, or non-collapsibility may feel behind before the chapter begins. A one-paragraph "you only need this idea" bridge would reduce that burden.

The proof of the hazard-survival identity uses absolute continuity, almost-everywhere derivatives, local integrability, and one-to-one correspondence. This is mathematically appropriate, but the reader needs a prior intuitive version: hazard accumulates over time into cumulative hazard, and survival is the exponential of the negative accumulated risk.

The marginal hazard ratio theorem is likely the hardest conceptual jump. The survivor-weighted density $\tilde f_t(x\mid s)$ is the right object, but it arrives as a formula before the risk-set intuition is fully developed. The "mechanism, in words" remark is excellent and should appear before, or both before and after, the theorem.

The term "frailty" appears in the theorem, but a novice health researcher may know frailty as a random-effects survival concept, not just as a high-risk prognostic covariate. The chapter should say that here it means an unobserved or observed risk multiplier, not necessarily a full shared-frailty model.

The ordered-categorical material may feel like an appendix rather than a second main endpoint. There is no worked ordered-categorical example in the chapter body, so the reader may not see how ordinal aggregation is practically different from binary aggregation.

The computational-cost remark may overwhelm the intended reader. HMC leapfrog steps, time quadrature, QMC truncation, $\widehat R$, PSIS-LOO, and model comparison appear together. These are useful, but the chapter should first give a simple computational picture before listing diagnostics.

## Suggested improvements

Add a short conceptual workflow box near the beginning:

1. Write the likelihood for one patient if their covariates were known.
2. For an AgD patient, average that likelihood over the study covariate distribution.
3. Multiply those averaged likelihoods across patients or pseudo-patients in the arm.
4. Share treatment-effect parameters across the network.

Add a small glossary table for the survival part: $S(t)$, $h(t)$, $H(t)$, $f(t)$, $G(t)$, $\delta$, pseudo-IPD, conditional hazard ratio, marginal hazard ratio, and RMST. The notation is standard, but the chapter introduces many survival-specific symbols quickly.

Move or duplicate the "mechanism, in words" explanation before @thm-marginal-hr-time-varying. The reader should understand survivor selection before reading the exponential-tilt proof.

Add a diagram or verbal substitute for risk-set drift: at baseline both arms have the same covariate mix; later, control has lost more high-risk patients; treated survivors still include more high-risk patients; the marginal hazards now compare different covariate mixes.

Expand the pseudo-IPD explanation. State what is reconstructed from a Kaplan-Meier curve, what is still unobserved, why the covariate distribution $f_j$ is used for each pseudo-patient, and how this differs from true IPD.

Give the ordered-categorical model a miniature worked example in the main text, not only in the exercises. A three-category severity outcome with two cutpoints and one binary covariate would make the cutpoints, sign convention, and integrated category probability much clearer.

Clarify the scope of "mixed likelihood" use. Say whether the chapter means one general framework that can be applied separately to many outcome families, or a single joint network that combines multiple outcome families. If the latter, explain the common estimand or shared latent treatment effect.

Add hints or labels to the exercises. For a novice, the Weibull and binary-reduction exercises are reasonable practice, the ordinal exercise is useful but calculator-heavy, and the starred marginal-hazard attenuation exercise is advanced. A short hint for the starred exercises would make them less discouraging.

## Highest-priority fixes

First, add a plain-language bridge for conditional versus marginal hazard ratios before the survivor-weighted theorem. This is the conceptual hinge of the survival part.

Second, clarify how AgD survival data become pseudo-individual likelihood contributions, especially the distinction between reconstructed event or censoring times and still-unobserved covariates.

Third, expand the ordered categorical section with an in-text numerical example and a direction-of-effect explanation for the proportional-odds sign convention.

Fourth, make the RMST warning more concrete: collapsible within a population does not mean transportable across populations.

Fifth, check the final likelihood formula in the worked example, because the apparent exponent mismatch will trip up exactly the readers who try to verify the arithmetic.
