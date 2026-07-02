# Chapter 4 Feedback: Probability and Distributions

## Overall reaction

This chapter is mathematically serious and clearly written for someone who already accepts that probability is the foundation of indirect treatment comparisons. From the perspective of a novice health researcher, though, it often becomes abstract before the reader has a concrete object to hold onto. The introduction does a good job naming expectation, Jensen's inequality, and the multivariate normal as the three tools that matter later, but the rest of the chapter quickly shifts into measure theory, proof grammar, and matrix formulas. A motivated reader can see that the material is important, but may not always see what each definition is buying them for ITC, MAIC, STC, or NMA.

The main issue is not correctness. It is pacing and translation. The chapter often gives a formal definition, proves it, and only afterward gives a short applied sentence. A reader who is weak in abstract mathematics will need the applied picture first, then the formal definition, then the proof. The chapter would be much more accessible if it carried one small clinical-trial example throughout: treatment, baseline covariate, binary response, and possibly a second trial population.

## What was clear

The opening motivation is strong. It correctly tells the reader that transportability, weighted averages, marginal effects, and nonlinear links are all probability statements. That is exactly the bridge a health researcher needs before accepting a measure-theoretic chapter.

The discrete versus continuous explanation before conditional expectation is one of the clearest pedagogical moments. Saying that the familiar ratio for $P(X=x)>0$ becomes $0/0$ for continuous $X$ gives a real reason for the abstract definition.

The variance, covariance, and covariance-matrix material is relatively readable because it connects formulas to familiar second-moment quantities. The identity
$\mathrm{Var}(\mathbf{a}^{\top}\mathbf{X})=\mathbf{a}^{\top}\boldsymbol{\Sigma}\mathbf{a}$
is a good bridge from probability back to the linear algebra chapters.

The core distributions section is useful. The Bernoulli, binomial, Poisson, Poisson binomial, normal, and multivariate normal entries give means, variances, and MGFs in a consistent format. The Poisson binomial is especially relevant because it connects heterogeneous individual risks to aggregate event counts.

The worked bivariate normal example is valuable because the arithmetic is checkable. The conditional normal example at $X_2=4$ makes the abstract formula more tangible. The Poisson binomial calculation is also helpful because it shows all subset terms explicitly.

## What was unclear

The patient-record interpretation of $\omega$ may confuse a novice. The text says an outcome $\omega$ is the entire record of one patient, but later ITC arguments often concern a full trial, an aggregate count, or a target population. A reader may wonder whether $\Omega$ contains patients, possible trial datasets, or possible worlds. This needs an explicit distinction between patient-level and study-level probability spaces.

The introduction to $\sigma$-algebras is too quick. "Allowed questions" is intuitive, but the reader never gets a small example of a collection of allowed events, nor a reason why all subsets may be too much. Without that, closure under complements and countable unions feels like formal bookkeeping.

The expectation-as-Lebesgue-integral section is likely to feel like a cliff. It jumps from simple random variables to supremums over simple functions to positive and negative parts. A novice health researcher probably knows expectation as a weighted average. The chapter should explicitly show how a finite trial average, a discrete expectation, and an integral are the same idea at different levels of generality.

The conditional expectation definition uses several terms that need more reader support: sub-$\sigma$-algebra, version, almost surely, $\sigma(X)$, Radon-Nikodym theorem, and measurable function $m$. The text is precise, but a novice may not understand what information is being conditioned on. The section needs a finite-strata example before the formal definition, such as expected response within baseline-risk strata.

The graphoid axioms section is especially difficult. The axioms are important later, but the proof is long and abstract, and the health motivation is thin. The sentence about propensity-score reduction is not enough. A novice reader needs one small conditional-independence story, for example treatment assignment independent of potential outcomes after conditioning on covariates, before seeing symbolic rules.

Jensen's inequality is motivated well in the introduction, but the actual section does not yet deliver the ITC payoff. The reader is told that Jensen explains aggregation bias and non-collapsibility, but there is no simple health example with numbers. A small logistic-risk example would help: compare the average of two predicted risks with the inverse-logit of the average linear predictor.

MGFs are introduced as transforms that turn convolution into multiplication, but the reader may not know why they should care. The chapter should say plainly that MGFs are a calculation device used here to avoid repeated density integrations and to prove normal and Poisson facts efficiently.

## Under-explained details

Several recurring mathematical terms need plain-language support on first use: law, pushforward, measurable, Borel set, almost surely, integrable, $L^1$, $L^2$, version, product law, and $\sigma(X)$. Each is defined or used precisely, but not always translated into the kind of language a novice can retain.

The difference between a density, a distribution, a law, a probability measure, and a CDF could use a short comparison table. These words appear close together, and a health researcher may treat them as interchangeable unless the chapter explains the distinction.

The use of "conditional distribution given $\mathbf{X}_2=\mathbf{x}_2$" after saying continuous singletons have probability zero needs an explicit bridge. The chapter has the machinery to justify it, but the novice reader needs reassurance that this is not the forbidden $0/0$ ratio from earlier.

The independence section says that product law and factorization of expectations are equivalent. That is compact but not intuitive. A tiny binary example would help show how independence lets joint probabilities multiply.

The Fubini-Tonelli theorem appears as a cited result with little applied context. Since the text says it licenses aggregate likelihoods in Part V, it would help to show a simple nested average: first average over patients within a covariate distribution, then average over studies or arms.

The multivariate normal conditional formula uses block matrix notation heavily. A novice may not be comfortable with $\boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}$ as a regression coefficient. The chapter hints at the regression interpretation afterward, but that interpretation should come before or alongside the formula.

The exercises are mathematically appropriate, but several are not accessible as learning exercises for the stated reader. The Borel-Cantelli exercise, the covariance square-root construction, and especially the graphoid counterexample require proof maturity that many health researchers will not have after a first pass through the chapter.

## Where a novice may get lost

A novice may get lost immediately after the motivating introduction, when the chapter moves into $\sigma$-algebras without a running data example. The reader has just been promised ITC relevance, but then sees set closure rules before seeing a trial table or patient-level variables.

The expectation construction is another likely loss point. Supremums over simple functions and positive and negative parts are standard, but the reader needs a sentence explaining that this machinery exists so expectation still works for continuous and unbounded outcomes.

The tower property proof may be hard to follow because it is stated in terms of nested sub-$\sigma$-algebras rather than nested information sets. The health-research version, "average the subgroup means and you recover the overall mean," should be made explicit before the theorem.

The graphoid proof is probably beyond the novice reader's useful comprehension at this point. It may signal rigor, but it risks making conditional independence feel like symbolic manipulation rather than a tool for causal reasoning and adjustment.

The transition from scalar distributions to MGFs to the multivariate normal is efficient but fast. The reader may not see why the MGF definition of the multivariate normal is preferable to the density. This is particularly true because the density appears immediately afterward for the nonsingular case.

The worked example is useful, but it arrives late. By the time the reader reaches it, they have already passed through the hardest parts of the chapter. Earlier mini-examples would reduce the cognitive load.

## Suggested improvements

Add a running clinical-trial example near the start and reuse it throughout. For example: $T$ is treatment, $X$ is baseline severity, $Y$ is response, and $S$ is study membership. Use it to illustrate $\Omega$, events, random variables, distributions, expectations, conditioning, and independence.

Add short intuition paragraphs before the formal definitions of probability space, random variable, expectation, conditional expectation, and conditional independence. The pattern should be: clinical question, informal meaning, formal definition.

Add a table comparing "event," "random variable," "law," "CDF," "density," and "expectation." This would prevent a lot of terminology overload.

Add a finite-strata worked example for the tower property before the measure-theoretic proof. For instance, compute the overall event risk by averaging age-stratum risks with age-stratum proportions.

Add a numerical Jensen example tied to ITC. A simple two-subgroup logistic example would show why $\mathrm{logit}^{-1}(\mathbb{E}\eta)$ differs from $\mathbb{E}[\mathrm{logit}^{-1}(\eta)]$ and why this matters for marginal versus conditional effects.

Consider shortening the graphoid proof in the main chapter or moving some proof detail to an appendix or technical note. Keep the statement, give a simple causal example, and explain which later result will need the axioms.

Introduce MGFs with a concrete calculation problem: "How do we find the distribution of a sum without doing a difficult convolution?" Then the factorization theorem has a clear purpose.

Add more applied exercises. Examples: compute a target-population mean by reweighting two covariate strata, compare average predicted probabilities under two populations, compute a Poisson binomial event-count distribution for heterogeneous patient risks, and identify which conditional-independence statement corresponds to exchangeability.

## Highest-priority fixes

1. Add a running patient-level and study-level clinical example before the measure-theoretic definitions.
2. Add a plain-language bridge for conditional expectation and the tower property, with a finite-strata health example.
3. Add a concrete Jensen example showing aggregation bias or non-collapsibility on a logistic scale.
4. Reduce the main-text burden of the graphoid proof and replace some of it with causal intuition.
5. Add one or two early worked mini-examples before the final worked example section.
