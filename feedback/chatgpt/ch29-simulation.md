# Chapter 29 Feedback: Simulation Study Theory

## Overall reaction

This is a strong chapter with a clear mathematical spine. The opening motivation is especially helpful: it explains why consistency theorems are not enough for health technology assessment decisions, and the distinction between the per-replication sample size $n$ and the number of simulation replications $R$ is one of the clearest ideas in the chapter.

For a novice health researcher, though, the chapter often succeeds more as an advanced mathematical treatment than as a learning bridge into simulation studies. The practical question, "How would I design and read a simulation study for an indirect treatment comparison?", is present, but it is frequently buried under functional notation, asymptotic statements, and theorem language. The reader who is weak in abstract mathematics will understand the purpose early on, then may start losing the thread once $F_n$, performance functionals, $\theta_0$, $\sigma_n$, and standardized bias enter.

The chapter would be much more accessible if it added more plain-language translation around the formal definitions, especially for data-generating mechanisms, estimands, Monte Carlo standard error, coverage, and replication planning. The mathematical material does not need to be removed, but it needs more stepping stones.

## What was clear

- The introduction gives a persuasive health-research reason for simulation studies: finite trial sizes, imperfect overlap, omitted effect modifiers, and variance approximations matter in ways that asymptotic consistency alone cannot answer.
- The distinction between $n$ and $R$ is clear and important. Calling this the "cardinal sin" of simulation practice is memorable and useful.
- The ADEMP framework is a good organizing device. The example aim about MAIC bias under an omitted binary effect modifier is concrete enough to show what a simulation question can look like.
- The bias section explains the basic idea well: bias is the average estimate minus the known truth, and its Monte Carlo standard error shrinks like $1/\sqrt{R}$.
- The empirical standard error versus model-based standard error diagnostic is highly useful for an applied reader. The three regimes, $\mathrm{ModSE}\approx\mathrm{EmpSE}$, $\mathrm{ModSE}<\mathrm{EmpSE}$, and $\mathrm{ModSE}>\mathrm{EmpSE}$, are explained in a way that connects directly to interval reliability.
- The coverage-collapse idea is conceptually powerful. The message that more data can make a biased method's intervals worse is exactly the kind of lesson a novice health researcher needs to internalize.
- The worked miniature simulation is valuable because it computes bias, empirical standard error, Monte Carlo standard error, mean squared error, and coverage by hand.
- The empirical robustness proposition is careful about its status. It is helpful that the chapter explicitly says this is an empirical finding, not a theorem.

## What was unclear

- The data-generating mechanism is defined formally, but a novice may still not know what they would actually need to specify for an ITC simulation. The chapter should say more explicitly which pieces come from real trials, which pieces are chosen by the analyst, and which pieces are varied across scenarios.
- The estimand is too compressed. The definition says $\theta$ is a functional of the DGM and can be known by analytic calculation or a large auxiliary simulation, but a novice health researcher may not understand how the "known truth" is obtained, especially for marginal log-odds ratios, risk differences, survival estimands, or non-collapsible scales.
- The jump from ADEMP as a practical checklist to "performance measures as functionals" of $F_n$ is abrupt. A reader may understand "repeat the simulation and summarize estimates" but not immediately understand why this becomes a functional of a sampling distribution.
- The phrase "methods are measurable maps from a dataset to a triple" is mathematically precise but pedagogically cold. It could be followed by a plain version: each method takes one simulated trial dataset and returns an estimate, a standard error, and an interval.
- The notation in the coverage section is likely to confuse novices. In particular, $\theta$ is the true estimand, $\theta_0$ is the working-model target in the misspecification section, and then $\theta_0$ is also used as the null value in the power section. That reuse is mathematically manageable but pedagogically risky.
- Monte Carlo standard error is central, but the chapter could distinguish it more repeatedly from the standard error reported by a statistical method. A novice may confuse the uncertainty in the simulation summary with the uncertainty in each individual simulated analysis.
- Replication planning is underdeveloped as a workflow. The formulas are present, but the reader is not walked through a practical sequence such as run pilot simulations, estimate the relevant variance or coverage, choose a target MCSE, then solve for $R$.
- The model-based standard error definition averages reported standard errors, while the prose says the target includes the average reported variance. That may be technically defensible depending on the intended summary, but for a novice it needs an explanatory note because average SE and square root of average variance are not the same object.

## Under-explained details

- The chapter needs more intuition for why simulation studies have a "known truth." In real data, the truth is unknown; in a simulation, the analyst creates a world where the truth is known. That contrast should be made explicit before the formal estimand definition.
- The DGM should be unpacked in health-research terms: patient covariates, trial membership, treatment assignment, baseline risk, treatment effect modification, outcome noise, missing aggregate information, and overlap between populations.
- Coverage needs a plain definition before the indicator formula. A novice-friendly version would be: if we could repeat the entire study many times, coverage is the fraction of reported intervals that include the true effect.
- The distinction between bias and variance is clear mathematically, but the decision implications could be stronger. For example, bias threatens validity, variance threatens precision, mean squared error combines both, and coverage tells whether uncertainty statements are trustworthy.
- The Cramér-Rao efficiency baseline is probably too abstract for the target novice reader. It needs a short applied motivation before the proposition: "This tells us whether a method is merely better than another method, or close to the best precision any regular estimator could achieve."
- The robustness proposition would be easier to absorb with a small table listing methods, required assumptions, expected bias, expected variance, and expected coverage behavior under good and poor overlap.
- The exercises are mathematically appropriate but uneven for a novice health researcher. The first two are accessible. The coverage curve exercise needs a hint for solving the inverse problem. The power and mean-squared-error-optimal moment set exercises are useful but may need intermediate prompts or a small template.

## Where a novice may get lost

- Immediately after the ADEMP definition, when the chapter shifts from practical design language into $F_n$, deterministic functionals, iid replicate triples, and two asymptotic regimes.
- In the proof of the empirical variance result. The algebra is correct in spirit for a mathematical text, but the long parenthetical expansion may be hard to follow. A novice may need the key idea first: the sample mean is estimated from the same replications, so one degree of freedom is lost.
- In the coverage theorem. Conditions C1 to C3 are dense, and the reader has to understand asymptotic normality, ratio-consistent standard errors, working-model targets, and standardized bias before seeing the result. A plain-language preview would help a lot.
- In the transition from misspecification coverage to power. The same machinery is being reused, but the notation shift makes it feel like a new topic rather than an application of interval-test duality.
- In the efficiency baseline section. Uniform integrability, regular parametric models, local-asymptotic-minimax theory, and the Cramér-Rao floor are likely beyond what a novice health researcher can process without a conceptual map.
- In the worked example's DGM. The example says each replication draws $n$ patients per arm, but the table immediately presents five estimates. A novice may not see the missing layer: each row is the result of simulating a full dataset and applying the method.
- In the naive-method coverage table. The conclusion is excellent, but the reader may need a sentence explaining why $\sigma_n$ shrinks as $n$ grows before the table.

## Suggested improvements

- Add a short "simulation study in one ITC example" box before the ADEMP definition. Use a concrete anchored comparison with AC individual patient data, BC aggregate data, an effect modifier, and a target population. Show the DGM, estimand, methods, and performance measures in one compact table.
- Add a plain-language translation after @def-sim-performance-functional. For example: "At fixed $n$, there is a true bias and true coverage for the method in this artificial world. We do not know those numbers exactly, so we estimate them by repeating the artificial world $R$ times."
- Add a small glossary or summary table for $n$, $R$, $\widehat{\mathrm{SE}}$, MCSE, EmpSE, ModSE, coverage, bias, variance, and MSE.
- Expand the estimand discussion with at least one extra health-scale example. The current identity-scale worked example is useful, but novices also need to know what changes when the target is a marginal log-odds ratio or another common ITC scale.
- Insert a practical replication-planning paragraph after the coverage replication corollary. Include a small table such as $R=500$, $1000$, $2000$, $5000$ with approximate MCSE for coverage near $0.95$.
- Add "how to read this theorem" paragraphs before @thm-coverage-misspecification and @thm-sim-power. These should define $\theta$, $\theta_0$, $\sigma_n$, and $b$ in words before the formal statement.
- Use different notation for the null value in the power section, such as $\theta_{\mathrm{null}}$, to avoid confusion with the working-model target $\theta_0$ from the misspecification section.
- Strengthen the worked example by explicitly saying that each row in the replication table is the output from a complete simulated dataset. If space allows, show one miniature simulated dataset or a schematic of one replication.
- Add one paragraph after the worked example translating the performance results into an applied decision: which method would look valid, which would look overconfident, and what additional scenario would be run next.
- Add hints to the more advanced exercises, especially the coverage curve inverse problem and the power calculation.

## Highest-priority fixes

1. Add a concrete ADEMP table for an anchored ITC simulation before or immediately after @def-ademp.
2. Add a plain-language bridge from the DGM to the known estimand, including how the truth is calculated in a simulated ITC.
3. Add a short glossary separating statistical standard error from Monte Carlo standard error.
4. Unpack the coverage-collapse theorem in words before the formal conditions, especially $\theta$, $\theta_0$, $\sigma_n$, and standardized bias $b$.
5. Clarify replication planning as a practical workflow, not only as formulas.
6. Make the worked example more explicit about what one replication contains and why $R=5$ is pedagogical rather than realistic.
7. Change or clearly distinguish the power-section null notation so it does not collide with the working-model target notation.
