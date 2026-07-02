# Appendix C Feedback: Probability Distributions

## Overall reaction

Appendix C is useful as a compact formula reference, but it is not yet fully usable for a novice health researcher trying to learn the mathematics of indirect treatment comparisons. The tables are tidy and the definitions are mathematically disciplined, but the appendix often reads as if the reader already knows why each distribution matters. A motivated beginner can look up a density or variance, but may still not know whether a distribution is being used for an outcome likelihood, a prior, a covariate model, a survival baseline, a discrete aggregation argument, or ML-NMR integration.

The biggest missing layer is practical orientation. A health researcher needs a bridge from familiar data structures, such as responders out of randomized patients, events per person-time, survival times, study-level treatment effects, baseline covariates, and prior information, to the distributions in the catalogue. The appendix says where some distributions appear later, but it does not make the distribution-to-role mapping easy to scan.

## What was clear

The opening paragraph clearly states that the appendix is a reference catalogue rather than a proof chapter. That helps set expectations.

The table format is helpful. Listing support, mass or density, mean, variance, and moment generating function in the same order makes the appendix consistent and easy to compare across families.

The rate convention for exponential and gamma distributions is important and well placed. Many applied readers have seen both rate and scale versions, so explicitly saying that this book uses shape-rate for gamma and rate for exponential prevents a common source of errors.

The discrete distributions section gives a helpful nesting story: Bernoulli as binomial with one trial, binomial as a special Poisson binomial, and Poisson as a rare-event limit. This is a good conceptual path for aggregate binary outcomes.

The Weibull hazard parametrization remark is valuable because it connects the table's shape-scale form to the proportional-hazards form used later. That kind of bridge is exactly what a novice needs more often.

The conjugate pairs table is one of the most reader-friendly parts of the appendix. It directly connects priors, likelihoods, and posteriors, which is closer to how a health researcher will encounter these distributions in Bayesian evidence synthesis.

## What was unclear

The appendix gives moment generating functions a central role before explaining why a health researcher should care about them. A reader who is trying to understand likelihoods and priors may wonder why MGF is one of the main table columns while cumulative distribution functions, survival functions, hazard functions, or link-function roles are mostly absent.

The distinction between mass function, density, distribution function, survival function, and hazard is not made explicit. This matters because the appendix mixes binary outcomes, count outcomes, continuous outcomes, multivariate covariates, and survival times. A novice may not understand why a density value is not a probability, or why the survival function is the natural object for Weibull but not for binomial data.

The phrase "support" is used correctly, but it may be too terse for the target reader. A short explanation that support means the values the random variable can take would help, especially before the simplex in the Dirichlet section.

The beta MGF entry, with a confluent hypergeometric function, is mathematically accurate but likely distracting. For this reader, the important beta facts are that it lives on probabilities, its parameters behave like prior successes and failures in the beta-binomial setting, and its mean and variance are easy to interpret. The hypergeometric MGF may make the distribution look harder than it needs to be.

The Dirichlet section becomes abstract quickly. "Lebesgue measure on the $(K-1)$-dimensional simplex" and "joint moment generating function on $\mathbb{R}^K$ is degenerate" are likely to lose a novice before they understand the main idea: the Dirichlet is a prior for several probabilities that must add to one.

The multivariate normal section is mathematically important, but the clinical or ITC motivation is thin. A novice may not recognize that this family can describe correlated baseline covariates, random effects, approximate sampling distributions, and Gaussian copula constructions.

## Under-explained details

The appendix needs a clearer map from distributions to modeling roles. For example, Bernoulli and binomial usually appear as likelihoods for binary outcomes; Poisson appears for event counts or rates; Poisson binomial appears when individual risks differ before aggregation; normal and multivariate normal appear in priors, random effects, approximate sampling distributions, and covariate models; beta and Dirichlet appear as priors for probabilities; gamma appears as a prior for rates or precisions; exponential and Weibull appear as survival time models; and standard normal functions appear in probit links and Gaussian copulas.

The Poisson distribution would benefit from a sentence about exposure time or person-time. Health researchers often meet Poisson models as event rates rather than just counts, so $\lambda$ should be linked to a rate times exposure when appropriate.

The Poisson binomial row is important for ML-NMR and covariate-adjusted risks, but the subset formula is hard to parse. A concrete example with three patients and three different event probabilities would make the distribution recognizable.

The normal distribution could use a clearer separation of roles: outcome model for continuous endpoints, prior on treatment effects, approximate likelihood for estimated effects, and building block for multivariate covariates. Without this, the normal row looks generic rather than central to ITC.

The standard normal section mentions the probit model and Gaussian copula, but it does not explain enough for a novice to see why $\Phi^{-1}$ transforms uniform variables into normal scores for ML-NMR integration. A two-sentence bridge to the integration chapters would help.

The conjugacy section would be stronger if it explicitly framed conjugacy as an algebraic convenience for Bayesian updating, not as a general requirement for Bayesian modeling. A novice might otherwise infer that priors must be conjugate.

## Where a novice may get lost

A novice may get lost immediately in the conventions section because MGF, gamma function, beta function, and parametrization conventions appear before any health-data example. The material is correct, but it starts with abstract tools rather than the question "what kind of data am I modeling?"

The discrete distribution table is compact but dense. The Bernoulli and binomial rows are likely familiar, but the Poisson binomial mass function over subsets is a big jump. The remark about heterogeneous individual risks being less dispersed is useful, but it needs a plain-language lead-in: if predicted risks differ across patients, the aggregate number of events is no longer exactly binomial.

The continuous table mixes very different objects. Normal, exponential, gamma, beta, and Weibull have different modeling jobs, but the table makes them look like peers in a formula sheet. A novice may not know that beta is usually about probabilities, gamma about positive rates or precisions, and Weibull about time-to-event outcomes.

The multivariate normal conditioning formula is likely too advanced without an applied anchor. The Schur complement expression is not the problem by itself; the problem is that the reader may not know what question it answers. An example such as predicting the distribution of missing covariates from observed covariates would make the formula more meaningful.

The Mills ratio bound in the standard normal section feels like a sudden increase in mathematical intensity. It may be useful later, but a novice may not know whether it is essential for ITC or optional technical reference material.

The appendix relies on cross-references such as @sec-genlik-survival, @sec-conjugacy, and @sec-mvn. Those are useful, but a novice browsing the appendix needs more local guidance about what they will find there and why they should click through.

## Suggested improvements

Add a short "How to use this appendix" paragraph near the start. It should say that the reader should first identify the modeling role: outcome likelihood, prior, covariate distribution, survival baseline, aggregation approximation, or numerical integration device.

Add a compact role map before the formula tables. Suggested columns: distribution, common health-data object, ITC role, later chapters. This would directly answer the novice question "which distribution am I seeing, and why is it here?"

Add a "where this appears in the book" column or short note for each distribution. For example: Bernoulli and binomial for binary responders; Poisson for counts and rates; Poisson binomial for aggregated individual risks; normal for continuous outcomes, treatment-effect approximations, and priors; multivariate normal for correlated covariates and Gaussian copulas; beta and Dirichlet for probability priors; gamma for rates or precisions; Weibull and exponential for survival.

Add one or two miniature numerical examples. Good candidates are a beta-binomial update with a small responder count, a Poisson binomial example with three unequal risks, and a Weibull survival example showing how shape affects increasing or decreasing hazard.

Move the most technical MGF details into an "advanced reference" paragraph or explain that readers can skip them on first pass. The MGF column is helpful for proofs and moment calculations, but it should not compete with likelihood and prior interpretation for this audience.

Add more intuition for parameters. For beta, explain $a$ and $b$ as controlling prior mass near 0 or 1 and as pseudo-counts in the conjugate update. For Dirichlet, explain $\alpha_k$ as category-specific pseudo-counts and $\alpha_0$ as concentration. For Weibull, explain how $k<1$, $k=1$, and $k>1$ change the hazard over time.

Add explicit bridge text to ML-NMR integration. The appendix should explain that ML-NMR often needs both outcome distributions and a model for the covariate distribution, and that the multivariate normal and Gaussian copula are used to integrate individual-level likelihood contributions over aggregate covariate information.

## Highest-priority fixes

1. Add a distribution-to-modeling-role table that distinguishes likelihoods, priors, covariate models, discrete outcome aggregation, survival baselines, and ML-NMR integration.

2. Add novice-level worked examples for Poisson binomial aggregation, beta-binomial updating, and Weibull survival interpretation.

3. Add plain-language explanations for support, density versus probability, rate versus scale, concentration, pseudo-counts, and simplex before the more technical formulas.

4. Make the ML-NMR connection explicit. The current appendix mentions Gaussian copulas and covariate-adjusted risks, but it does not yet help a novice see how distributions support likelihood integration over patient covariates.

5. Mark hypergeometric MGFs, Dirichlet measure details, Schur complements, and Mills ratio bounds as advanced reference material so first-time readers know they can keep going without mastering those pieces immediately.
