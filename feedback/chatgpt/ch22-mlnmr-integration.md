# Chapter 22 Feedback: Multilevel Network Meta-Regression III: Numerical Integration Theory

## Overall reaction

This chapter is technically impressive and has a clear purpose: explain how ML-NMR turns an aggregate-data likelihood into a numerical integration problem, then justify the Sobol' plus copula machinery used to evaluate it. As a novice health researcher, I can see why the topic matters. The introduction does a good job connecting the integral to the logit link, aggregate likelihoods, and the practical need for numerical evaluation.

The main problem is pacing. The chapter often moves from a useful health-research intuition into a full mathematical theorem before I have had enough time to understand the object being introduced. Quadrature, Monte Carlo, quasi-Monte Carlo, copulas, probability integral transforms, and Gaussian copulas are all new for many health researchers. Each is introduced correctly, but several are explained at a level where I understand the formal statement before I understand why I personally need the idea.

For the target reader, the chapter would be much stronger if it repeatedly returned to the same concrete ML-NMR task: "We need the average event probability in an aggregate study arm when only covariate summaries are available." The chapter says this, but the mathematical sections sometimes drift away from that anchor.

## What was clear

The opening motivation is one of the strongest parts. The link from Chapter 20 to the aggregation integral, the warning that plugging in the covariate mean is not valid for nonlinear links, and the special difficulty of the logit link are all clear and directly relevant to health technology assessment.

The contrast between product quadrature, Monte Carlo, and quasi-Monte Carlo is helpful. The simple cost message, $k$ nodes per axis means $k^d$ total nodes, is easy to grasp and gives a concrete reason why standard quadrature becomes unrealistic with several covariates.

The Monte Carlo section is accessible. The variance of a sample mean is familiar enough that the $N^{-1/2}$ rate feels believable, and the bounded-link remark for logit probabilities gives a useful probability-scale interpretation.

The fixed-node explanation in the ML-NMR integration pipeline is very useful. The point that Sobol' nodes are computed once and then reused at every likelihood evaluation is the clearest practical bridge between numerical integration and Bayesian computation. This is exactly the kind of detail a health researcher needs to understand why QMC is not just a faster random simulation trick.

The one-covariate worked logit example is valuable. The symmetric $\mu=0$ case is especially good because it gives the reader a known answer and a visible reason why the estimate is exactly 0.5. The comparison with five ordinary Monte Carlo seeds also makes reproducibility and stochastic noise tangible.

## What was unclear

The chapter says product quadrature is "out" for $d=3$ to $10$, but the practical threshold is not fully explained. A novice may ask: if I have three covariates and use five nodes per covariate, is $125$ nodes really too many? The current argument becomes convincing at ten covariates, but it would help to discuss typical ML-NMR workloads: number of studies, number of arms, number of posterior evaluations, and why even moderate node counts multiply quickly.

The term "transport map" appears early and is mathematically precise, but it may be too abstract on first contact. I would have benefited from a plain-language sentence such as: "The map $T$ is just the recipe that turns uniform numbers between 0 and 1 into plausible covariate profiles for the aggregate study."

The QMC section defines star discrepancy and Hardy-Krause variation formally, but a novice may not understand what kind of "bad behavior" these quantities measure. Discrepancy is somewhat intuitive because of corner boxes. Hardy-Krause variation is much harder. The definition may be correct, but the reader needs more interpretation before the theorem: high variation means the integrand changes sharply or jumps over the cube, so evenly spread points may still miss important changes.

The Gaussian copula section clearly defines the model, but the assumption itself needs more health-research discussion. The chapter states that the Gaussian copula has zero tail dependence and is usually acceptable for central HTA inference. That claim may feel too quick. A novice reader needs to know when this assumption could matter clinically, for example when severe baseline risk factors cluster together, or when two biomarkers are more likely to be jointly extreme than a Gaussian copula would imply.

The chapter is not always clear about which correlations are observed, assumed, latent, or borrowed. It says $\boldsymbol{\Omega}$ is the correlation of latent normals, not generally of the covariates themselves. That is important, but it deserves more emphasis because a health researcher may otherwise think they can directly insert the reported Pearson correlation from a trial table.

## Under-explained details

The probability integral transform needs a more concrete opening example before the generalized inverse theorem. A simple example using age modeled as normal, or a binary covariate such as sex or biomarker-positive status, would make the role of $F^{-1}(u)$ much easier to understand. The Bernoulli discussion appears later as a caveat, but it could also be used pedagogically when the transform is introduced.

The copula idea would benefit from a small health-data example before Sklar's theorem. For instance: an aggregate psoriasis trial reports mean age and mean weight, but not how age and weight are paired within patients. The marginals describe each variable separately; the copula describes which ages tend to go with which weights. That framing would make Sklar's theorem feel necessary rather than abstract.

The relation between marginal summaries and assumed marginal distributions is under-explained. The chapter says AgD studies report means, standard deviations, or proportions, and that margins such as normal or beta margins can be calibrated. A novice needs more guidance on how this calibration happens and what is assumed. If a study reports mean age and standard deviation, are we assuming normal age? If a covariate is bounded or skewed, what should be done? This is not just technical detail, because the integration result depends on the assumed margin.

The numerical integration error discussion gives rates and bounds, but the practical interpretation is still thin. The chapter mentions comparing $N$ with $N/2$, but a novice needs a clearer answer to: how small is small enough? Is an error of 0.005 on the probability scale acceptable? Does that depend on posterior uncertainty, treatment ranking, or decision thresholds?

The worked example gives a "high-accuracy reference value" of 0.6020, but it does not say how that value was obtained. A reader trying to reproduce the example may wonder whether it came from a very large Sobol' rule, adaptive quadrature, simulation, or software. A sentence naming the method would improve trust.

The two-covariate trace is helpful but too short to fully teach the copula step. It traces one Sobol' point, but it does not show how a set of points becomes a joint covariate cloud with the intended dependence. A small two-dimensional table with several Sobol' points before and after Cholesky transformation would make the dependence mechanism much more visible.

## Where a novice may get lost

A novice may get lost at the first theorem. Gauss-Legendre quadrature is introduced as the one-dimensional gold standard, but the theorem and proof immediately require Legendre polynomials, Hermite interpolation, polynomial exactness, and a derivative error formula. For a reader focused on ITCs, the important message is that one-dimensional quadrature is excellent but tensor-product quadrature scales badly. The proof may be mathematically appropriate for the book, but it needs a gentler entry point.

The move from Monte Carlo to QMC may also be hard. The chapter says fixing random Monte Carlo points removes noise but forfeits the independence behind the RMSE proof, then introduces deterministic low-discrepancy points. That is conceptually important, but a novice may not understand why "fixed random points" are not already enough. A short comparison of three choices would help: fresh random points, fixed pseudorandom points, and Sobol' points.

Hardy-Krause variation is likely the hardest definition for the target reader. The phrase "sums the Vitali variations of $f$ restricted to every face of the cube" is precise, but it will not be intuitive unless the reader already has multivariable analysis background. A novice may leave this section understanding only that $V_{\mathrm{HK}}$ is a mysterious penalty term.

The Sobol' sequence construction may be more detailed than a novice needs at first. Primitive polynomials over $\mathbb{F}_2$, direction numbers, and bitwise exclusive-or are interesting, but they may distract from the central idea that Sobol' points fill the cube evenly and are nested as $N$ grows. The current worked example later rescues the intuition, but the construction may lose some readers before they reach it.

The Gaussian copula pipeline uses several transformations in sequence: Sobol' uniforms, inverse normal, Cholesky, normal CDF, target inverse CDF. This is logically clear after careful reading, but it is a lot to hold in working memory. A novice may not know why the pipeline goes from uniform to normal to uniform to covariate, especially when the one-covariate normal example collapses some of the steps.

The exercises are mathematically strong but may be intimidating. Several require comfort with discrepancy, quantile functions, and copula correlations. For a health researcher just learning ITCs, there should be at least one lower-barrier applied exercise, such as interpreting what happens to an aggregate event probability when the correlation between two effect modifiers is changed.

## Suggested improvements

Add a short "running health example" near the start and reuse it throughout. For example, a binary outcome AgD arm with age, baseline severity, and biomarker status as covariates would give every abstract object a concrete role: margins, copula, Sobol' nodes, transformed covariate profiles, conditional event probabilities, and aggregate mean.

Before each major mathematical tool, add a plain-language "why this tool appears here" paragraph. Quadrature answers "why not a grid"; Monte Carlo answers "why random sampling helps but is noisy"; QMC answers "why deterministic evenly spread points are better for HMC"; copulas answer "how to invent a joint covariate distribution from marginal summaries"; the probability integral transform answers "how unit-cube points become covariate values."

Add a diagram or numbered algorithm for the ML-NMR pipeline. The current theorem gives the pipeline in equations, but a novice would benefit from a recipe:

1. Choose Sobol' points in $[0,1]^d$.
2. Convert them to independent normal scores.
3. Correlate the normal scores using $L$.
4. Convert correlated normal scores back to uniforms.
5. Convert those uniforms to covariate values using each marginal distribution.
6. Evaluate the individual outcome model at each covariate profile.
7. Average the response-scale predictions.

Clarify the Gaussian copula assumption in applied terms. State what is preserved, what is assumed, and what is not guaranteed. In particular, emphasize that the marginal distributions are preserved exactly, the dependence structure is imposed through latent normal correlation, and the resulting Pearson correlations of nonnormal covariates may not equal the latent correlations.

Give more practical guidance on integration error. The chapter should explain how a researcher would decide whether $N$ is adequate in a real analysis, how the $N$ compared with $N/2$ check is interpreted, and how integration error should be judged relative to posterior uncertainty or decision-relevant effect sizes.

Move some of the detailed Sobol' digital-net construction into a remark or optional box, and foreground the usable intuition first. The novice needs to know that Sobol' points are deterministic, evenly spread, nested, and reproducible before learning how direction numbers generate them.

Expand the two-covariate copula example into a small table with multiple points. Showing only one point proves the mechanics, but showing several points would help the reader see dependence appear across the transformed covariate profiles.

Add an applied exercise that does not require new proof skills. For example: given two alternative correlations, compute or inspect how the aggregate event probability changes, then explain why dependence among effect modifiers can affect an AgD likelihood even when the marginal summaries are unchanged.

## Highest-priority fixes

1. Add a plain-language bridge before the transport-map and unit-cube formulation, explaining that $T$ is the recipe for turning uniform Sobol' points into plausible aggregate-study covariate profiles.

2. Add applied intuition before Hardy-Krause variation and Koksma-Hlawka. The reader needs to understand discrepancy as point-set evenness and variation as integrand roughness before seeing the formal bound.

3. Clarify the Gaussian copula assumption much more explicitly, especially the difference between latent normal correlation, observed covariate correlation, rank dependence, and tail dependence.

4. Expand the numerical integration error discussion into practical guidance: how to choose $N$, how to interpret the $N$ compared with $N/2$ diagnostic, and when remaining error matters for health technology assessment conclusions.

5. Strengthen the worked example by saying how the reference value 0.6020 was obtained and by adding a multi-point two-covariate table that makes the copula step visible.
