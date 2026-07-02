# Chapter 27 Feedback: Aggregate-Level Covariate-Distance Matching

## Overall reaction

This is a strong and unusually honest chapter. The main message is valuable for a novice health researcher: aggregate covariate-distance matching can help choose among external comparator studies, but it cannot prove that an unanchored comparison is valid. The chapter is mathematically careful, and the final caveat about zero mean distance not guaranteeing zero bias is exactly the kind of warning a beginner needs.

The main weakness is that the chapter often explains the mathematics before giving the reader enough practical footing. A motivated health researcher who is weak in abstract mathematics may understand the broad warning, but may struggle to answer basic applied questions: What data do I need from each candidate study? Which covariates should go into the distance? Which scale should I use? How do I explain a Mahalanobis ranking to an HTA reviewer? What do I do if one metric picks Study A and another picks Study D? The chapter has pieces of those answers, but they are scattered across remarks, the worked example, and the exercises.

## What was clear

The introduction clearly motivates why comparator selection matters in disconnected networks and single-arm settings. The contrast with anchored evidence is helpful because it explains why the comparator is sometimes forced by the network and sometimes becomes a design choice.

The definition of aggregate-level comparator selection is clean. The notation $\bar{\mathbf{x}}_0$, $\bar{\mathbf{x}}_j$, and $\boldsymbol{\delta}_j$ gives the reader a simple object to hold onto: each candidate has a covariate gap from the index population.

The explanation of raw versus standardized Euclidean distance is one of the most accessible parts of the chapter. The age in years versus proportion male example makes the scale problem concrete.

The Mahalanobis section gives a useful verbal intuition after the theorem. The idea that some directions are "cheap" because they follow the usual covariance pattern, while discordant directions are "expensive," is much more beginner-friendly than the quadratic form itself.

The scale-invariance section has a clear practical moral. A novice may not follow every algebraic step, but the conclusion is easy to grasp: raw Euclidean distance can choose a comparator for arbitrary unit reasons, so it is a weak basis for an HTA decision.

The worked example is useful because it shows that different reasonable distances can pick different studies. That is a very important lesson. It also shows why reporting only one distance can create false confidence.

## What was unclear

The chapter would benefit from a slower explanation of what "aggregate-level covariate distance" means in real review work. It says candidate studies report vectors of covariate summaries, typically means, but a novice may not know whether these are baseline means across all randomized patients, arm-specific means, target-population means, or summaries after applying eligibility restrictions.

The practical role of comparator selection is still a little abstract. The chapter says the selected study is fed into unanchored MAIC, STC, or ML-UMR, but it does not fully spell out the workflow from systematic review to candidate filtering to covariate table to distance ranking to sensitivity analysis.

The choice of reference scales is under-explained. The definition lists index IPD standard deviations, reported comparator standard deviations, and Bernoulli standard deviations, but it does not give enough guidance on when each is appropriate. This matters because the exercises later show that changing reference scales can change the winner.

The chapter does not fully explain how to choose the covariates included in the distance. A novice may include every reported baseline variable, even if some are weakly prognostic, or may omit a key effect modifier because it is missing from one candidate study. The text should connect covariate selection more explicitly to prognostic variables, effect modifiers, clinical relevance, and availability across studies.

Weighted distances are not clearly separated from standardized or Mahalanobis distances. Mahalanobis distance implicitly weights gaps by the inverse covariance structure, but a health researcher may also expect clinically weighted distances that give more importance to known effect modifiers. If arbitrary clinical or model-based weights are intentionally excluded, that should be stated. If they are allowed, they need their own short definition and caution.

The Wasserstein section is mathematically elegant but likely too abrupt for the target reader. Terms such as coupling, finite first moment, infimum, and Kantorovich-Rubinstein duality arrive before the reader has a plain mental picture of "how much mass must be moved to turn one covariate distribution into another."

The ESS tradeoff is mentioned, but not developed enough in the main text. The reader is told that smaller gaps usually mean less reweighting and higher effective sample size, but the worked example does not compute or illustrate ESS. Since ESS is one of the most practical diagnostics in MAIC, this deserves more than a remark and an exercise.

## Under-explained details

The chapter needs a more explicit distinction between clinical comparability and covariate-summary comparability. A study can be close on age, sex, and biomarker means but still differ in line of therapy, outcome definition, follow-up time, country, standard of care, or measurement practice. A novice HTA researcher needs to hear that distance matching happens after basic clinical and design comparability have been assessed.

The Gower distance needs more intuition. The formula handles mixed continuous and binary covariates, but the range scaling and truncation at 1 are not explained in applied terms. A small example with one continuous covariate and one binary covariate would help.

The mean-SMD discussion invokes the familiar $0.1$ threshold from balance diagnostics, but the chapter should be careful about how this carries over to study-level means. A novice may read $0.1$ as a formal decision threshold for comparator selection, which the chapter otherwise avoids.

The bias-bound section should say more plainly what $\boldsymbol{\beta}$ represents in a health example. For instance, if age and biomarker modify absolute response, then $\boldsymbol{\beta}$ tells us how much the treatment contrast changes per unit of each covariate. Without that bridge, the phrase "contrast direction" may feel disconnected from clinical modeling.

The practical HTA use case is present but thin. The chapter should tell the reader what a transparent submission or evidence dossier would report: the candidate set, covariates used, missing covariates, scale choices, distance rankings under several metrics, covariates driving disagreement, ESS after adjustment, and sensitivity analyses for unmeasured bias.

The worked example computes exact bias using a hypothetical affine contrast, but it does not explain how such a contrast would be obtained or elicited in practice. A novice may wonder whether $\boldsymbol{\beta}=(0.1,2,0.5)$ is estimated, assumed, borrowed from prior evidence, or used only as a teaching device.

## Where a novice may get lost

The introduction is conceptually rich but dense. It names MAIC, STC, ML-NMR, ML-UMR, disconnected networks, single-arm studies, transportability, Wasserstein distance, and bias bounds before the reader has done a single comparator-selection calculation. A short running example before the theorem roadmap would lower the entry barrier.

The metric-properties proposition may feel like a detour. A mathematically strong reader may appreciate proving which functions are genuine metrics, but a novice health researcher may lose sight of why this matters for choosing an external comparator.

The whitening theorem is likely to be difficult. The verbal explanation is good, but it comes after notation involving $B^{-1}$, matrix square roots, Cholesky factors, and covariance transformations. A simple two-covariate picture or numeric ellipse example should come before the theorem.

The Wasserstein argument is probably the steepest part of the chapter. The proof is self-contained mathematically, but the concept is not self-contained pedagogically. The reader needs a pre-proof paragraph that says, in plain language, that Wasserstein distance compares full distributions by asking how far patients would need to be moved in covariate space.

The worked example is informative but numerically heavy. It would be easier to learn from if it had a short interpretation table after the calculations: why raw picks C, why standardized picks A, why Mahalanobis picks D, and what each choice would mean for an HTA analyst.

The exercises are weighted toward proof work. Exercises on Minkowski's inequality, affine invariance, and second-moment counterexamples are mathematically appropriate for the book, but the novice health researcher also needs applied exercises that ask them to interpret a covariate table, justify a distance choice, and write a comparator-selection rationale.

## Suggested improvements

Add a short practical workflow near the start: define the target population, screen candidate studies for clinical and design comparability, choose covariates based on effect modification and prognosis, harmonize definitions, choose reference scales, compute several distances, inspect covariate drivers and ESS, then carry uncertainty into sensitivity analysis.

Introduce a small two-covariate toy example before the formal definitions. For example, compare three external studies using age and biomarker means, first in raw units and then in standardized units. This would make the later four-study worked example feel like an extension rather than the first concrete contact.

Add a boxed explanation of reference-scale choices. Cover index IPD standard deviations, pooled or comparator-reported standard deviations, binary covariate scaling, missing standard deviations, and why changing scales without changing units is a modeling choice rather than a harmless re-expression.

Give a beginner explanation of Mahalanobis distance before the theorem. A sentence such as "Mahalanobis distance asks whether the whole pattern of covariate differences looks unusual relative to the index trial covariance cloud" would help.

Add an intuitive paragraph and a tiny discrete example before Wasserstein notation. The current proof can stay, but it needs an applied bridge that contrasts "same means" with "same distribution shape."

Move more of the ESS tradeoff into the main text. A small table showing candidate distance, possible weight extremity, and ESS would help the reader understand why the closest comparator by means is not automatically the best analysis choice.

Expand the HTA reporting guidance. The chapter should explicitly recommend reporting several distance rankings, explaining disagreements, showing which covariates drive each distance, and stating that distance matching is a screening and sensitivity tool rather than evidence of exchangeability.

Add one or two applied exercises. For example, ask the reader to write a short decision memo from the worked example, or to decide what to do when the Mahalanobis winner has poor clinical comparability but the standardized Euclidean winner has better trial design similarity.

## Highest-priority fixes

1. Add a novice-facing practical workflow before the formal distance definitions.

2. Add clear guidance on reference scales, covariate selection, and missing or inconsistently reported baseline summaries.

3. Give Wasserstein distance a plain-language explanation before the theorem, or move the theorem after a more intuitive distributional counterexample.

4. Bring the ESS and bias tradeoff into the main chapter rather than leaving it mostly to remarks and exercises.

5. Strengthen the worked example with interpretation, not just calculation, especially for why each metric chooses a different comparator and how an HTA analyst should report that disagreement.

6. State more explicitly that aggregate covariate-distance matching does not replace clinical comparability assessment, effect-modifier adjustment, or quantitative bias analysis for unmeasured differences.
