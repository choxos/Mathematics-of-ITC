# Chapter 21 Feedback: Multilevel Network Meta-Regression II: Discrete Outcomes and Approximation Theory

## Overall reaction

This is a strong mathematical chapter, but for a novice health researcher it is still more like a proof chapter than a learning chapter. The introduction gives a useful promise: binary and count outcomes are common in health technology assessment, and the chapter will explain what happens when we aggregate unequal individual risks. The chapter then delivers the mathematics carefully, especially for the Poisson binomial, Le Cam bound, and adjusted binomial. The main weakness is that the reader is often asked to follow abstract probability machinery before they have a clear health-research picture of what decision the machinery supports.

The chapter would be much more accessible if it repeatedly answered this practical question: "I have an aggregate arm with an event count, covariate summaries, and an ML-NMR model. Which likelihood am I using, why, and what mistake am I avoiding?" Right now the answer is present, but spread across the introduction, the conditional versus marginal remark, the adjusted-binomial section, the worked example, and the final "Which likelihood to report" remark.

## What was clear

The opening contrast between continuous outcomes, count outcomes, and binary outcomes is helpful. It makes clear why Chapter 20 was easier and why Chapter 21 exists: aggregation is simple when averaging and the link function cooperate, but discrete event counts are sums of patient-level random variables.

The conditional versus marginal remark in the setup section is one of the clearest teaching moments. It tells the reader that fixing the actual patient covariates is not the same as integrating over a study population. That distinction is central for ML-NMR, and it is good that the chapter flags it before the technical results begin.

The Poisson section explains the count-outcome contrast well. The closure of independent Poisson variables under addition is easy to follow, and the later warning that the marginal count is mixed Poisson, not plain Poisson, is useful. The phrase that overdispersion is the count-data fingerprint of within-study covariate variation is memorable and gives the reader an intuition to hold onto.

The Poisson binomial generating-function section is mathematically clean. A motivated reader can see why unequal binary risks do not collapse to an ordinary binomial, and the binomial special-case remark helps prevent a common misconception.

The worked example is the most useful part for a novice. The risk vector, the integrated binomial, the exact Poisson binomial, the adjusted binomial, and the Le Cam Poisson are concrete enough to compare. Step 7 is especially helpful because it finally reconciles why two binomials can both be legitimate answers to different questions.

## What was unclear

The chapter sends mixed signals about the "default" or "practice" likelihood for binary ML-NMR. Early on, the integrated binomial is described as exact and as the default ML-NMR likelihood. The introduction also says the adjusted two-parameter binomial is the surrogate used in practice for binary ML-NMR. Later, the "Which likelihood to report" remark explains that the integrated binomial targets an exchangeable patient sample, while the adjusted binomial targets fixed representative profiles or integration nodes. A novice is likely to read these as competing recommendations rather than as different likelihoods for different data representations.

The role of integration nodes needs more plain-language setup. In the worked example, the five equally weighted profiles are introduced as representing the study covariate distribution, but the example also says the arm reports responders out of five patients. That makes it easy to confuse actual patients with numerical integration profiles. A novice needs a direct sentence such as: "These five profiles are not necessarily five real patients; they are a numerical summary of the covariate distribution. If they are treated as fixed profiles, the conditional Poisson binomial is the target. If real patients are treated as exchangeable draws, the integrated binomial is the target."

The health meaning of total-variation distance is underdeveloped. The definition is precise, but the reader may not know what it means for an event-count likelihood. It would help to say that total variation is the largest possible absolute difference in probability assigned to any collection of counts. Then the Le Cam bound could be read as a worst-case probability error, not just an abstract norm.

The adjusted binomial needs a stronger warning about what kind of object it is. The chapter says it matches the first two moments and may use a non-integer $N^{*}$ through Gamma functions. A novice health researcher may reasonably ask: if $N^{*}<n$, can the model assign zero or awkward likelihood to event counts that are possible in the real trial? The section should explain how this is handled in actual ML-NMR software or clearly state the practical restriction. The phrase "bounded support $\{0,\dots,N^{*}\}$" is intuitive when $N^{*}$ is an integer, but confusing when $N^{*}$ is not.

## Under-explained details

Binomial aggregation is introduced in a mathematically correct way, but the practical interpretation could be stronger. The integrated binomial says that after integrating over the covariate distribution, every patient has the same marginal event probability $\theta_\bullet$. A novice may need the health interpretation: this is like saying each future patient drawn from that arm's target population has the same average event chance, even though their individual risk would differ if we observed their covariates.

The Poisson binomial idea would benefit from a short verbal example before the generating function. For instance, in a responder endpoint, one patient may have a 10 percent response probability and another a 70 percent probability because of baseline severity or prior therapy. The total number of responders is then not "five trials with probability 40 percent"; it is five different Bernoulli trials added together.

The approximation-error discussion is mathematically careful but not fully translated into modeling consequences. Le Cam gives a distance guarantee but can have the wrong variance for moderate clinical risks. The adjusted binomial matches mean and variance but has no distance guarantee. The chapter should explicitly connect these to inference: using the wrong approximation can overstate or understate how surprising an observed aggregate count is, which can change the contribution of an AgD arm to treatment-effect estimation.

Overdispersion is explained well for count outcomes, but the negative-binomial remedy is too brief for a novice. It says a negative binomial calibrated to the first two moments restores correct dispersion, but it does not show what the analyst would do with that statement. A small worked count example, even shorter than the binary example, would help readers see how $n\theta_\bullet+n\sigma_W^2$ changes the likelihood compared with $\mathrm{Poi}(n\theta_\bullet)$.

The phrase "effective sample size of the risk vector" is clever, but it may be too clever without more explanation. In MAIC, effective sample size reflects how much information remains after weighting. Here, $N^{*}$ reflects how many equal-risk Bernoulli trials would have the same mean and variance as the unequal-risk trials. That analogy should be stated slowly before invoking Cauchy-Schwarz.

## Where a novice may get lost

The first major danger point is the transition from the exact marginal binomial to the conditional Poisson binomial. The chapter says the marginal law is immediate and exact, then spends many pages on the conditional law and approximations. A novice may wonder why the chapter is not finished after Proposition @prp-marginal-binomial. The "Why this is not the end of the story" remark helps, but it should include a concrete ML-NMR workflow example.

The second danger point is the probability generating function. The chapter defines it and uses it correctly, but a novice may not yet understand why coefficients of a polynomial are probabilities. A miniature expansion with two Bernoulli risks before the theorem would make the later five-risk expansion easier.

The third danger point is the Le Cam proof. The coupling construction is elegant, but it is a long detour from the health-research problem. The reader may lose the point of the proof before reaching the practical message that the Poisson approximation is only good for rare events. A preview sentence before the proof and a "what this means for event rates of 5 percent, 20 percent, and 50 percent" paragraph after it would help.

The fourth danger point is the contrast between overdispersion for counts and reduced variance for unequal binary risks. The chapter notes that spreading binary risks apart reduces the Poisson-binomial variance, which is the opposite of the Poisson-rate intuition. This is important and surprising enough to deserve a more intuitive explanation, perhaps using the idea that risks near 0 or 1 are more predictable than risks near 0.5.

The exercises may be too hard for the stated novice reader without intermediate scaffolding. The Le Cam exercise essentially asks the reader to reproduce the proof. The adjusted-binomial exercise asks for Gamma-function likelihood evaluation and total-variation distance. Those are valuable, but the chapter also needs easier exercises that ask readers to choose the appropriate likelihood, interpret overdispersion, or explain in words why unequal risks are not binomial.

## Suggested improvements

Add a short decision table near the start or end of the chapter. The rows could be: count outcome with fixed covariates, count outcome marginalized over covariates, binary outcome with exchangeable patients, binary outcome with fixed integration nodes, and rare binary events. The columns could name the target law, approximation if any, what it matches, and when it is appropriate.

Add one bridge paragraph after Proposition @prp-marginal-binomial that states the practical problem plainly: original ML-NMR often integrates over a population to get $\theta_\bullet$, but numerical integration also creates fixed nodes with unequal risks, and those two viewpoints produce different aggregate laws.

Add a health-oriented example before the Poisson binomial theorem. Use a responder or adverse-event endpoint and two or three patient profiles. Show that unequal probabilities create terms like $p_1(1-p_2)p_3$, so the subset formula is not just notation.

Add a short interpretation box for total variation. It should say what a value like 0.17 means for event-count probabilities and why a bound of 1.00 is technically correct but practically uninformative.

Add a count-outcome mini-example for overdispersion. A simple two-profile hospitalization or exacerbation-rate example would make the mixed-Poisson variance formula feel less abstract.

Clarify the non-integer adjusted-binomial likelihood. State whether the Gamma-function form is used only as a computational approximation, how support is handled, and what happens if the observed event count exceeds the effective size $N^{*}$.

Revise the worked binary example to separate "five real patients" from "five integration profiles." If the goal is to teach fixed nodes, call them profiles or nodes throughout. If the goal is to teach actual patients, then explain why the integrated binomial is the marginal answer.

Add easier exercises before the proof-heavy ones. For example: "Given three scenarios, choose integrated binomial, adjusted binomial, Le Cam Poisson, or negative binomial, and justify the choice in one sentence."

## Highest-priority fixes

1. Resolve the apparent tension between integrated binomial as the default ML-NMR likelihood and adjusted binomial as the practical binary ML-NMR surrogate. This is the most important comprehension issue.

2. Clarify the patient-versus-integration-node distinction in the setup and worked example. Without that, the conditional and marginal laws feel like a technical subtlety rather than a modeling choice.

3. Add health-research interpretations of approximation error, total variation, moment matching, and overdispersion. The mathematics is present, but the novice needs to know what each quantity means for an aggregate event count.

4. Explain the practical status of non-integer $N^{*}$ in the adjusted binomial, including support and observed counts. This is likely to be a major sticking point for readers.

5. Add one smaller count-outcome example and one easier likelihood-selection exercise so that readers can practice the ideas before facing the more abstract proofs.
