# Chapter 18 Feedback: Matching-Adjusted Indirect Comparison
## Overall reaction

This is a strong chapter for a mathematically prepared reader, but it is probably too compressed for a novice health researcher who is just learning indirect treatment comparisons. The chapter does explain why matching-adjusted indirect comparison matters: the reader is told that a naive Bucher comparison mixes the $AC$ and $BC$ populations, and that reweighting the $AC$ individual patient data is meant to make the $AC$ estimate live in the $BC$ population. That motivation is valuable and mostly comes through.

The main difficulty is that the chapter quickly shifts from the health research problem to convex optimization, entropy, Kullback-Leibler divergence, Karush-Kuhn-Tucker conditions, convex hulls, relative interiors, M-estimation, Hadamard differentiability, and bootstrap theory. Those sections are rigorous, but the novice reader may lose the practical thread: "What am I doing to the patients, why do these weights solve my trial comparison problem, and how would I recognize a bad MAIC in a published paper?"

The chapter would work better for the stated audience if each major mathematical object were paired with a plain health-research interpretation before the proof begins. At present, the explanations are often present but placed after the formal statement, or they require the reader to already understand the mathematical language.

## What was clear

The opening setup is clear and useful. The asymmetric triangle with $AC$ supplying individual patient data and $BC$ supplying only aggregate data gives the reader a concrete reason for MAIC. The sentence explaining that we cannot move the $BC$ patients into the analysis but can move the analysis into the $BC$ population is one of the most helpful intuitive lines in the chapter.

The distinction between anchored and unanchored MAIC is also clearly stated at a high level. The chapter repeatedly emphasizes that anchored MAIC needs effect modifiers, while unanchored MAIC also needs prognostic variables. That is an important practical message for health technology assessment readers.

The effective sample size section is one of the more accessible parts of the chapter. The bound $\mathrm{ESS}\le n$, the variance inflation factor $n/\mathrm{ESS}$, and the worked example's calculation of ESS make the precision cost of weighting concrete.

The two-covariate worked example is valuable. It shows actual weights, balance checks, ESS, adjusted arm means, and the final anchored indirect comparison. The example also usefully separates an effect modifier from a purely prognostic covariate, which is exactly the distinction a novice needs to internalize.

The remarks after the main theorems are often more reader-friendly than the theorem statements. In particular, "The fundamental MAIC trade-off," "Reweighting interpolates, it does not extrapolate," and "What the prognostic covariate cost" are strong explanatory anchors.

## What was unclear

The chapter does not fully explain what a MAIC weight means in patient terms before giving the entropy program. A novice may need a simple sentence such as: "A patient with a high weight represents many similar target-population patients, while a patient with a low weight contributes little because their covariate profile is less common in the target population." Without that bridge, $w_i=\exp(\alpha+\boldsymbol{\beta}^\top\boldsymbol{\Delta}_i)$ feels like an optimization artifact rather than a representation of the target population.

The transition from moment balance to entropy balance is abrupt. The text says infinitely many weight vectors can achieve balance, then immediately introduces KL divergence from uniform weights. A novice health researcher may not understand why "closest to uniform" is a desirable scientific choice. The chapter would benefit from a small clinical analogy: among all ways to make the $AC$ sample look like $BC$, choose the one that changes the original trial as little as possible.

The Kullback-Leibler and entropy discussion is mathematically correct but not intuitive enough for the target reader. The notation $\mathrm{KL}(\mathbf{p}\,\|\,\mathbf{u})$ and the derivation from $p_i=w_i/\sum_j w_j$ appear before the reader has been given a simple sense of KL as a penalty for unequal weights. A small numeric comparison, for example weights $(1,1,1,1)$ versus $(2.25,0.75,0.75,0.25)$, would make the entropy idea easier to absorb.

The convex hull and relative interior condition is precise, but the practical implication could be clearer. A novice may understand "target mean must lie inside the IPD covariate cloud" but may not understand what to do with that in real study reports. The chapter should explicitly connect this to checking whether each reported $BC$ mean, range, and standard deviation is plausible relative to the $AC$ individual data.

The anchored estimator sign convention may confuse readers. In some places the chapter describes an $A$ versus $C$ benefit as $\mu_C-\mu_A$, while the notation for $d_{AC}$ and the formula $g(\hat\mu_C)-g(\hat\mu_A)$ require the reader to track whether a positive value favors $A$ or $C$. The worked example is understandable, but a novice would benefit from one explicit sentence defining the direction of a positive effect in this chapter.

The sandwich variance section is likely too abstract for the novice stance. The block estimating function is introduced correctly, but the reader may not understand why uncertainty in weights changes uncertainty in treatment effects. The later remark helps, but it comes after a theorem full of asymptotic notation. A brief practical warning before the equations would help: "Do not compute standard errors as if the weights were known before seeing the data."

## Under-explained details

The chapter should say more plainly what information is available from the comparator trial. It mentions the mean covariate vector, possible standard deviations, and a published relative effect with standard error. A novice may not realize that MAIC usually cannot use the full $BC$ covariate distribution, only the summaries reported in a paper or submission. This limitation matters because it explains why balance is only on selected moments.

The phrase "balanced effect modifiers" needs more applied interpretation. The chapter defines the formal balance equations, but a novice health researcher may need a more direct explanation that balancing only matters for covariates that change relative treatment effects in anchored MAIC. The worked example eventually shows this, but the conceptual explanation should appear earlier, before the consistency theorem.

The distinction between effect modifiers and prognostic variables is central, but it relies heavily on previous chapters. Chapter 18 should briefly restate the difference in applied language: an effect modifier changes the treatment contrast, while a prognostic variable changes outcomes regardless of treatment. That reminder would make anchored versus unanchored MAIC much easier to follow.

The "link scale decides" remark is important but dense. It says first-moment balance suffices when the averaged quantity is affine in the matched features, but on nonlinear links higher moments or the joint distribution may matter. This is a key practical warning. It should be unpacked with a small example, such as two populations with the same mean age but different age spread giving different average risks under a logistic model.

The logistic inverse-probability weighting equivalence is potentially illuminating, but it assumes comfort with selection models and density ratios. The chapter should first give the intuitive version: MAIC acts as if it had fit a model predicting whether a patient belongs to the $AC$ or $BC$ population, then upweights $AC$ patients who look more like $BC$ patients. That would make the formal density-ratio proof less intimidating.

The finite-sample bias point is stated but could be better motivated. The chapter says MAIC is consistent rather than finite-sample unbiased because the weights are estimated. A novice may not know why estimated weights create bias. A short explanation that the same data are used to choose weights and estimate outcomes would make the warning clearer.

The bootstrap section is mathematically sophisticated, but the practical instruction is only in the remark. For this audience, the most important point is operational: when bootstrapping MAIC, resample patients and refit the weights in every bootstrap sample. That sentence should appear before the theorem, not only after it.

## Where a novice may get lost

The first major loss point is @sec-maic-weights. The chapter moves from a comprehensible balancing problem to KKT conditions and a dual log-partition function. A novice may not know whether the goal is still to match trial populations or now to solve an abstract optimization problem. Adding a pre-proof roadmap would help: the Lagrangian is only a tool for proving that the least-distorting balanced weights must be exponential.

The second loss point is @sec-maic-existence. "Relative interior," "affine hull," "coercive," and "convex duality" are all introduced in close succession. The geometry is important, but the novice takeaway should be stated first: if the $BC$ population is too different from the $AC$ trial, MAIC either fails or produces extreme weights. The formal theorem can then justify that message.

The third loss point is the anchored consistency theorem. The assumptions are accurate but numerous, and several are named by cross-reference. A novice reader may not be able to separate testable requirements from untestable assumptions. The later remark does this partly, but the theorem would be more readable if preceded by a short checklist: randomized $AC$ trial, common comparator, all imbalanced effect modifiers measured and balanced, enough overlap, and an appropriate link-scale model.

The fourth loss point is non-collapsibility. The chapter mentions that log odds ratios and log hazard ratios require scale-alignment conditions, but a novice may not understand why this changes MAIC. Because many health researchers work with odds ratios and hazard ratios, this needs more intuition. The text should explicitly say that matching mean covariates does not automatically make marginal odds ratios comparable.

The fifth loss point is @sec-maic-sandwich and @sec-maic-bootstrap. These sections are rigorous but may feel disconnected from applied MAIC reporting. A novice reader likely needs to know what variance approach to use, what not to use, and why. The current text gives the mathematical foundation, but it could better separate the applied instruction from the proof.

The exercises may also be difficult for the intended novice. The first exercise is accessible, but the majorization exercise and the starred sandwich exercise are quite advanced. They are useful for a mathematical textbook, but the chapter should include at least one applied interpretation exercise, such as diagnosing whether a published MAIC is credible from reported covariate balance, ESS, and anchored or unanchored status.

## Suggested improvements

Add a short "MAIC in plain language" paragraph near the beginning of @sec-maic-setup. It should explain that the method gives each $AC$ patient a multiplier so the weighted $AC$ sample resembles the $BC$ sample on reported effect modifiers, then recomputes the $A$ versus $C$ effect in that weighted sample.

Add a tiny one-covariate visual or table before the entropy section. For example, show four $AC$ patients with ages or baseline risks, a higher $BC$ mean, and the qualitative result that older or higher-risk $AC$ patients get larger weights. This would prepare the reader for the exponential formula.

Move some intuition before the formal theorem statements. The chapter has good remarks, but many arrive after difficult proofs. For novice comprehension, each theorem should start with a one or two sentence "why this matters" bridge.

Clarify the scale and sign convention for effects in the worked example and near @eq-maic-anchored-est. State whether positive values represent benefit of the first treatment, benefit of the second treatment, or improvement because lower outcomes are better.

Expand the explanation of entropy and KL with a small numeric demonstration. The reader does not need a long information-theory detour, but they need to see that entropy penalizes highly unequal weights and therefore protects against letting one or two patients dominate the pseudo-population.

Add a practical overlap diagnostic paragraph after @thm-maic-existence-uniqueness. It should tell the reader to inspect covariate ranges, standardized differences before and after weighting, extreme weights, and ESS, and to treat failed convergence as a warning about overlap rather than merely a software problem.

Strengthen the anchored versus unanchored warning with a direct health-research example. For instance, in an anchored comparison, baseline severity that affects both $A$ and $C$ equally cancels from the relative effect, but in an unanchored comparison it changes the absolute outcome under $A$ and must be adjusted for.

Make the variance guidance more operational. Include a short paragraph stating that reported MAIC uncertainty should account for weight estimation, the uncertainty in the published $BC$ effect, and the independence of the two trial sources. Then present the sandwich and bootstrap as two ways to do that.

Add at least one applied exercise. A useful exercise would ask the reader to evaluate a mock MAIC report with covariate balance, ESS, a published $BC$ standard error, and a statement that the comparison is unanchored. The task would be to identify the main credibility concerns.

## Highest-priority fixes

First, add more pre-proof intuition for the weights. The reader needs to understand what high and low weights mean before seeing entropy balancing, exponential weights, and KL divergence.

Second, make anchored versus unanchored MAIC more concrete. This is the most important applied distinction in the chapter, and the current formal assumptions may not be enough for a novice to understand why unanchored MAIC is so fragile.

Third, unpack ESS and variance uncertainty as reporting diagnostics. The ESS material is good, but the chapter should more explicitly connect low ESS, extreme weights, overlap failure, and unreliable standard errors.

Fourth, add a bridge for nonlinear link scales and non-collapsibility. Many applied readers will care about odds ratios and hazard ratios, and the current warnings may be too terse for them to know when first-moment matching is insufficient.

Fifth, revise the exercises so at least one or two are accessible applied-comprehension checks rather than only mathematical derivations. The current exercises fit the book's proof-oriented ambition, but they do not fully serve a health researcher trying to learn how to judge or perform a MAIC.
