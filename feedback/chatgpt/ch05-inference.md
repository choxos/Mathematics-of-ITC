# Chapter 5 Feedback: Statistical Inference

## Overall reaction

This chapter is rigorous, organized, and clearly important for the rest of the book. As a novice health researcher, I can see why inference matters for indirect treatment comparisons: every treatment effect estimate has uncertainty, and later methods such as network meta-analysis, MAIC, and ML-NMR depend on standard errors, likelihoods, and asymptotic approximations. The opening paragraphs are one of the strongest parts of the chapter because they name those later applications directly.

The main comprehension problem is pacing. The chapter begins with a useful ITC motivation, but then spends a long stretch in abstract estimation theory before returning to recognizable health research situations. The reader gets definitions, proofs, and conditions in a mathematically coherent order, but not always in a learning order for someone weak in abstract mathematics. A novice may understand individual sentences and still lose the larger story of why the score, Hessian, Fisher information, Cramer Rao bound, delta method, and sandwich variance are all parts of one practical workflow.

The chapter would be easier to learn from if it carried one simple clinical example throughout. For example, a binary response in a two arm trial could be used to introduce likelihood, score, Fisher information, Wald intervals, the delta method for log odds, and the idea of transforming estimates. A second small example involving a misspecified outcome model or weighting equation could then motivate the sandwich variance. The current Bernoulli and sandwich examples are useful, but they arrive late, after the most difficult theoretical sections.

## What was clear

The opening motivation is strong. It tells the reader that network meta-analysis uses nonlinear functions of fitted model parameters, MAIC needs robust standard errors, and ML-NMR depends on likelihoods and Fisher information. That framing is exactly what a health researcher needs before seeing abstract inference machinery.

The definition of an estimator, bias, variance, and mean squared error is clear. The bias variance decomposition is one of the most accessible proofs in the chapter, and the remark explaining that unbiasedness and consistency are logically independent is very helpful. The examples of $T_n = X_1$ and the shrunken mean make the point concrete.

The likelihood section explains the basic reversal well: a density treats the parameter as fixed and data as varying, while the likelihood treats the observed data as fixed and varies the parameter. That is an important conceptual hurdle for health researchers, and the chapter handles it clearly.

The mean zero score identity and information equality are developed carefully. The sequence from score, to expected score zero, to Fisher information, to information additivity gives a coherent mathematical story. The explanation that information additivity is why precision scales with sample size is especially useful.

The MLE invariance proposition is practically valuable. A novice may not yet know why it matters, but the statement that one can estimate a function of a parameter by plugging in the MLE is a useful bridge to odds ratios, risk ratios, hazard ratios, and marginal effects later.

The M-estimation section is one of the most relevant parts for the book. The explicit connection to MAIC is helpful, and the bread, meat, bread structure of the sandwich variance is memorable. The final misspecified normal mean example is simple enough to compute and does a good job showing why the naive model based standard error can be wrong.

The Bernoulli worked example is very useful. It shows likelihood, score, MLE, Fisher information, a Wald interval, the delta method for log odds, and all three classical tests with real numbers. This is the kind of example a novice reader can check by hand.

## What was unclear

The first major transition after the introduction is abrupt. The chapter moves from ITC applications into a formal definition of a parametric statistical model using a sample space, a sigma finite dominating measure, densities with respect to a measure, injectivity, and positive measure sets. Those are precise terms, but a novice health researcher may not know what practical problem this definition is solving. A brief patient level data table before the definition would help.

The regularity conditions are important but intimidating. Common support, smoothness, differentiation under the integral, envelopes, dominated convergence, and positive definite information are all introduced in one definition. A novice may not know which conditions are technical conveniences and which ones correspond to practical warnings. The Uniform$(0,\theta)$ exercise later shows why support matters, but that lesson would help much earlier, near the regularity definition.

The asymptotic tools section is mathematically careful but difficult as a learning entry point. Continuous mapping, Slutsky, and the delta method are introduced before the reader has seen a concrete inference problem that requires them. The delta method motivation is clear in words, but it would be more effective if the chapter first showed a small practical problem such as moving from an estimated probability to a log odds, then stated the theorem.

The proof of the continuous mapping theorem is probably too abstract for the target novice reader on first pass. It relies on Portmanteau, discontinuity sets, bounded continuous functions, and subsequences with almost sure convergence. These are valid tools, but the reader may not know what to retain. A short "what you should remember" sentence after the proof would help: if an estimate converges, then a continuous transformation of it converges too, provided the transformation behaves well at the limit.

The consistency proof of the MLE is conceptually important, but the three pieces may not be intuitive enough. The population criterion, uniform law of large numbers, and argmax consistency are described correctly, yet a health researcher may not understand the practical meaning of "the sample log-likelihood uniformly approaches its population version." A small plot or verbal picture of random likelihood curves settling around a population curve would help.

The Cramer Rao lower bound section is elegant, but its practical role is underexplained. A novice may not know whether this bound is something they will calculate, something software uses, or mainly a theoretical benchmark. The chapter should say more plainly that the bound explains why inverse Fisher information is the natural ideal variance under a regular correctly specified model.

The tests and confidence intervals section is concise but dense. Wald, score, and likelihood ratio tests are defined in quick succession, followed by a proof of Wilks' theorem. A novice may need a more applied distinction: Wald asks how far the estimate is from the null using the estimate's curvature, score asks whether the likelihood slope at the null is too steep, and likelihood ratio asks how much better the best fit is than the null. That intuition appears only indirectly.

## Under-explained details

The notation $X_1,\dots,X_n$ switches between abstract draws from a distribution and recognizable patient data. A novice may need explicit reminders that one $X_i$ can be an outcome, a covariate vector, or a full patient record depending on the model.

The term "true parameter" $\boldsymbol\theta_0$ deserves more explanation. In health research, many models are simplified or misspecified. The chapter later handles misspecification through M-estimation, but early sections can sound as if the model is literally true. It would help to distinguish "true parameter under a correctly specified parametric model" from "target parameter under an estimating equation."

"Identifiable" is defined formally as an injective map from parameters to densities, but the practical meaning is thin. A novice would benefit from a sentence such as: if two different parameter values imply the same distribution of observable data, no amount of data can tell them apart.

The distinction between per observation information and sample information needs more emphasis. The chapter defines $\mathcal I(\boldsymbol\theta)$ and $\mathcal I_n(\boldsymbol\theta)$, but later formulas require the reader to track when a factor of $n$ is inside the information matrix and when it appears outside as $1/n$. This matters for standard errors, and it is a common novice mistake.

The observed information versus expected information remark is useful but compressed. The chapter should say more directly what most software is doing: it estimates curvature at the fitted value, inverts that curvature, and reports square roots of diagonal entries as standard errors.

The notation $O_p(1)$ and $o_p(1)$ appears in the delta method and Wilks proofs. These are listed in the notation chapter, but a novice reader may still need a short reminder in context. Otherwise, the proof can feel like it switches to a private shorthand at a key step.

The Loewner order in the matrix Cramer Rao bound is likely unfamiliar. The chapter defines it parenthetically as positive semidefinite difference, but the applied meaning could be added: every linear combination of the estimator has variance at least as large as the corresponding linear combination under the inverse information.

The "bread" and "meat" terminology is memorable, but the shapes and roles of $\mathbf A$ and $\mathbf B$ could be translated more. $\mathbf A$ is about sensitivity of the estimating equation to the parameter, while $\mathbf B$ is about variability of the estimating equation itself. That sentence would make the sandwich formula less like matrix decoration.

The confidence interval by inversion remark assumes the reader knows how a test becomes an interval. The sentence is correct, but a novice would benefit from a small scalar example: try different null values, keep the ones not rejected, and the kept values form the interval.

## Where a novice may get lost

A novice may get lost in the asymptotic tools section because it arrives before the worked example. Continuous mapping, Slutsky, and the delta method are essential, but the reader has not yet been shown enough concrete inference problems to know why these tools are needed.

The proof of MLE asymptotic normality is another likely loss point. The five step structure is helpful, but the algebra moves quickly from the score equation to the averaged Hessian system. A novice may not see the main idea: at the maximum the slope is zero, near the truth the slope is approximately a straight line, and solving that linear approximation turns score noise into estimator noise.

The regularity and compactness assumptions may make the chapter feel more fragile than intended. A health researcher may wonder whether real logistic regression, Cox models, or network meta-analysis models satisfy these conditions. The chapter does not need to answer every case, but it should reassure the reader that the assumptions are a clean foundation and later models will check or adapt them.

The Cramer Rao proof may be hard to connect to later practice. The covariance inner product and block covariance argument are mathematically economical, but a novice may not understand why this theorem belongs before M-estimation and tests. A short bridge to inverse information standard errors would help.

The Wilks theorem proof is compact but symbol heavy. A novice may understand the final result that all three tests approach chi square, but miss why the three statistics are similar. The proof would be easier to absorb if preceded by a one paragraph picture of the log-likelihood as a parabola near its maximum.

The worked example is helpful, but it arrives after nearly all the abstract material. By then, many novice readers may have already lost confidence. The chapter would be more approachable if pieces of the Bernoulli example were threaded earlier: likelihood and score in the likelihood section, information in the Fisher information section, log odds in the delta method section, and tests in the test section.

The exercises are mathematically appropriate but mixed in accessibility. The Poisson, exponential, shrinkage, and score versus Wald exercises are approachable. The Uniform$(0,\theta)$ exercise is conceptually valuable but asks for a nonstandard limiting distribution, which may be a large jump. The multivariate delta method ratio exercise is useful, but a health researcher may need a treatment effect or risk ratio framing to see its relevance.

## Suggested improvements

Add a running health research example near the start. A binary response trial with $n$ patients, $x$ responders, and parameter $p$ could carry likelihood, score, MLE, Fisher information, Wald interval, log odds transformation, and score versus Wald versus likelihood ratio tests.

Move at least one small numerical example earlier. The Bernoulli worked example does not need to wait until the end. Even a short preview calculation after the likelihood definition would anchor the score and Fisher information sections.

Add plain language summaries after the major theorem proofs. For example, after the delta method: "This is why a standard error for a log odds ratio can be obtained by multiplying the variance of the fitted parameter by the squared derivative of the transformation." After MLE asymptotic normality: "This is the source of the usual estimate plus or minus 1.96 standard errors formula."

Create a short table comparing the three tests. Columns could include what is evaluated, whether the unrestricted MLE is needed, whether the null fit is needed, and the intuitive question each test asks. This would make Wald, score, and likelihood ratio tests much more memorable.

Add a paragraph explaining per observation versus sample information. Use the Bernoulli example to show $\mathcal I(p)=1/[p(1-p)]$, $\mathcal I_n(p)=n/[p(1-p)]$, and $\mathrm{Var}(\hat p)\approx 1/\mathcal I_n(p)$.

Strengthen the ITC motivation inside the chapter, not only at the beginning and end. The delta method section could mention log odds ratios and log hazard ratios with a toy calculation. The M-estimation section could give a schematic MAIC estimating equation or at least a two covariate balancing equation. The tests section could mention comparing a treatment effect to zero on the log odds ratio scale.

Add reader guidance around technical assumptions. A small "why these assumptions are here" paragraph after regularity conditions and after MLE consistency would help novices separate the main statistical idea from the analytic machinery that makes the proof legal.

Make the exercises more health flavored. Add one exercise where the reader computes an approximate confidence interval for a log odds ratio from a simple two by two table. Add one exercise where the reader applies the delta method to transform a log odds ratio interval to an odds ratio interval. Add one exercise where a working model underestimates uncertainty and the sandwich correction changes the conclusion.

## Highest-priority fixes

1. Thread the Bernoulli or binary trial example through the chapter instead of saving nearly all numerical work for the end.

2. Add plain language intuition for the score, Hessian, Fisher information, and inverse information standard error before the formal proofs.

3. Add bridge paragraphs after continuous mapping, Slutsky, delta method, MLE asymptotic normality, and Wilks' theorem explaining what a health researcher should retain.

4. Clarify per observation information versus sample information because this is central to standard errors and easy to confuse.

5. Strengthen the health and ITC examples in the delta method, M-estimation, sandwich variance, tests, and exercises so the chapter feels less like generic asymptotic statistics and more like the foundation for indirect treatment comparisons.
