# Chapter 20 Feedback: Multilevel Network Meta-Regression I: The Aggregation Principle

## Overall reaction

This chapter has a strong central idea: aggregate data should be modeled by averaging individual-level predictions over the study covariate distribution, not by plugging the mean covariate into the model. That idea is important, and the chapter states it early and repeatedly. As a motivated health researcher, I could see why ML-NMR is being introduced after MAIC and STC, and I understood that the chapter is trying to explain why ML-NMR is the coherent way to combine IPD and AgD.

The main problem is that the chapter often explains the idea in mathematically correct but very compressed language. It assumes that the reader already feels comfortable moving among individual likelihoods, marginal likelihoods, covariate distributions, link functions, Jensen gaps, ecological bias, and marginal odds ratios. A novice can follow the broad story, but many passages move too quickly from health-research motivation to formal notation. The reader may understand the slogan, "integrate, do not plug in," without fully understanding what is being integrated, over whom, on what scale, and how that changes an indirect treatment comparison.

The best parts are the opening motivation, the response-scale versus link-scale warning, and the discrete logit worked example. The hardest parts are the transition from population adjustment to a joint ML-NMR likelihood, the IPD versus AgD likelihood distinction, the heat-flow section, and the no-closed-form logit discussion. These sections are not necessarily wrong, but they are likely too abstract for a novice health researcher unless more clinical intuition and intermediate bridge sentences are added.

## What was clear

The introduction gives a useful contrast between MAIC, STC, and ML-NMR. The explanation that MAIC and STC are pairwise repairs, while ML-NMR fits one individual-level outcome model for the whole network, is a helpful framing. It also helps that the chapter identifies the three limitations being addressed: one triangle at a time, a single comparator population, and nonlinear-link aggregation bias.

The sentence-level distinction between the "inverse link of the average" and the "average of the inverse link" is one of the clearest teaching moments in the chapter. This is exactly the kind of phrase a novice can remember. It should be treated as the pedagogical anchor of the chapter.

The aggregate-level model section makes the key rule reasonably clear: apply the inverse link at each covariate value, then average over the covariate distribution. The remark "Integrate the response scale, not the link scale" is especially useful. It directly addresses a common applied mistake.

The identity-link and log-link sections are easier to understand than the logit section. The identity-link message is clear: if the outcome scale is linear, the study mean covariate is enough. The log-link closed form is also understandable because the multiplicative correction factor has a simple interpretation.

The logit worked example is the most accessible part of the chapter. The table of conditional risks at $x=0$ and $x=1$, followed by the integrated risks and plug-in risks, gives the reader a concrete handle on what aggregation means. The sign reversal between arms is a good demonstration of why a naive analysis can distort a treatment contrast even when the arm-level biases look modest.

The exercises are mostly well aligned with the chapter. They ask the reader to recompute the worked example, inspect variance-driven bias, and connect the special cases back to standard NMA. These are useful practice tasks for a motivated reader.

## What was unclear

The chapter does not fully slow down at the moment when "population adjustment" becomes "ML-NMR." The introduction says ML-NMR writes one individual-level outcome model for the whole network and then integrates for AgD studies. That is the correct high-level statement, but a novice may still wonder: what exactly is shared across studies, what is study-specific, and what information can an AgD study actually contribute to estimating effect modification? The chapter mentions that identifiability is taken up in Chapter 23, but the reader needs a short informal preview here.

The distinction between IPD and AgD likelihood contributions is under-explained for the intended reader. The chapter says IPD studies contribute patients one by one and AgD studies contribute through the integral, but the likelihood discussion quickly becomes formal. A novice may not know whether the AgD integral is replacing missing individual covariates, replacing missing individual outcomes, or both. The chapter should explicitly say that for AgD we do not observe each patient's covariate vector, so the likelihood averages over the plausible covariate values that could have generated the reported arm summary.

The role of $f_j$ is clear mathematically but not yet intuitive clinically. The chapter says an AgD study has a covariate distribution reconstructed from reported means, standard deviations, and possibly correlations. A novice health researcher may not appreciate how much modeling is hidden inside that phrase. If a trial reports only mean age and percentage female, what does it mean to have a joint distribution over covariates? How uncertain is that distribution? Why is that uncertainty postponed to Chapter 22 rather than treated as part of the current model? Even a short warning would help.

The Jensen gap is introduced correctly, but the novice reader may not yet connect it to actual treatment-effect distortion. The chapter proves that the plug-in arm mean can be above or below the integrated arm mean, then later the example shows a contrast bias. The bridge between those two ideas could be stronger: arm-level aggregation bias matters for ITC because treatment effects are contrasts of arm means, and the biases need not cancel across arms or across studies.

The logit section says the bias has no fixed sign because expit is convex below zero and concave above zero. That is clear for a mathematical reader, but a health researcher needs the risk interpretation stated directly: below 50 percent risk, heterogeneity tends to pull the average risk upward relative to the plug-in value; above 50 percent risk, it tends to pull it downward. The chapter eventually shows this in the example, but it would be easier if that intuition appeared before the theorem.

The heat-flow section is elegant but likely opaque for the target novice. Phrases such as "heat semigroup," "Gaussian convolution," "eigen-type orbit," and "inverse link diffused for time $\tau$" are not necessary for understanding ML-NMR aggregation. Unless this chapter is also meant to teach the mathematical structure for later numerical analysis, this section risks making the chapter feel much harder than the core method actually is.

The no-elementary-closed-form statement for the logit-normal integral may confuse the reader because the proof admits it is more of an argument than a formal impossibility proof. For a novice, the important message is practical: unlike the identity and log cases, the logit aggregate mean usually has to be computed numerically. The current discussion of elementary functions, error functions, softplus, and Liouville-type impossibility may distract from that applied message.

## Under-explained details

The notation $\theta_{\bullet jk}$ needs more explanation. The bullet subscript is defined as an average over individuals, but a novice may not internalize it. It would help to say in ordinary language that $\theta_{\bullet jk}$ is the model-predicted arm-level event risk, mean outcome, or rate for study $j$ and treatment arm $k$ after averaging over that study's case mix.

The linear predictor in @def-individual-model has several moving pieces, and the chapter explains them in a remark, but the causal and clinical roles could be clearer. For example, $\boldsymbol\beta_1$ is prognostic because it changes outcomes similarly across arms, while $\boldsymbol\beta_{2,k}$ is effect modification because it changes treatment differences. That is stated, but it would be useful to add a small one-covariate example such as age raising baseline risk in both arms versus age making treatment $B$ work better or worse.

The reference-treatment constraints $\boldsymbol\beta_{2,1}=\mathbf 0$ and $\gamma_1=0$ may feel arbitrary to a novice. A brief sentence should say these are identifiability conventions, not substantive claims that the reference treatment has no biological effect or no effect modification.

The chapter uses "marginal" in several ways that could be confusing: marginal individual likelihood, marginal mean outcome, marginal odds ratio, and marginal versus conditional effects. A novice health researcher may know marginal effects from trial reports but not from probability theory. The chapter should explicitly distinguish "marginal over the covariate distribution" from "conditional on a covariate value."

The aggregate likelihood part of @thm-aggregation is too fast for the reader stance. The theorem moves from individual marginal likelihoods to the likelihood of a summary statistic through $\pi_{\mathrm{Agg}}$. A novice may need an example immediately after the theorem: if an AgD binary arm reports 37 events among 100 patients, ML-NMR models that count using the arm-level risk $\theta_{\bullet jk}$, while that risk itself came from averaging individual risks over $f_j$.

The statement that the exact binary event-count law is Poisson binomial rather than binomial is important but not unpacked. A novice may not understand why event probabilities differ across patients after conditioning on covariates, or why a binomial model is therefore approximate. Even though Chapter 21 handles this, one or two sentences here would prevent confusion.

The link-scale versus response-scale distinction should be tied more explicitly to familiar outcome types. For binary outcomes, the response scale is risk and the link scale is log odds. For count outcomes, the response scale is rate and the link scale is log rate. For continuous identity-link outcomes, the response scale and link scale coincide. This concrete mapping would make the abstraction less intimidating.

The example's marginal odds ratio calculation is valuable, but the wording "reported estimand" may be slightly abrupt. It would help to remind the reader that trial reports usually summarize arm-level risks or counts, so the treatment comparison implied by those aggregate summaries is a marginal comparison in the study population, not the conditional effect at a fictional patient with mean covariates.

The exercises assume comfort with algebra, Taylor expansion, heat equations, and second-derivative bounds. Some are appropriate for the book's mathematical goal, but for this chapter's key applied learning objective, there should also be at least one more interpretation-heavy exercise that asks the reader to explain in words why two studies with the same mean covariate can still require different aggregate predictions.

## Where a novice may get lost

A novice may get lost in the first formal definition because the chapter moves from "ML-NMR fixes MAIC and STC limitations" to a full network predictor with $\mu_j$, $\boldsymbol\beta_1$, $\boldsymbol\beta_{2,k}$, $\gamma_k$, $\boldsymbol\phi$, and reference constraints. The reader may need a simple diagram or a two-treatment, one-covariate version before the general notation.

The aggregation theorem may be hard because it combines several concepts at once: unobserved covariates, conditional outcome models, integration over $f_j$, marginal likelihoods, and summary-statistic likelihoods. A novice could understand each piece separately but lose the thread when they are presented in one theorem. The proof is mathematically clean, but the teaching would benefit from a short plain-language "what this theorem says" paragraph before the theorem and a binary-event example after it.

The reader may lose the health-research motivation during the heat-flow section. At that point the chapter shifts from ML-NMR as a way to analyze mixed IPD and AgD networks to ML-NMR aggregation as a partial differential equation. This may be beautiful for mathematically advanced readers, but a novice health researcher may wonder whether they need heat equations to understand indirect treatment comparisons. If the section stays, it needs a clearer signpost explaining that it is optional structural insight and not required to fit or interpret ML-NMR.

The logit no-closed-form theorem is likely too heavy for the payoff. The reader needs to know that binary-outcome ML-NMR must integrate numerically, and that plug-in methods can overestimate or underestimate depending on baseline risk. The detailed comparison with probit, the elementary-function discussion, and the heat-flow proof may obscure those practical lessons.

The worked example is accessible but appears after a long sequence of formal material. A novice may benefit from seeing a mini-version of the example much earlier, perhaps immediately after @def-aggregate-model. Even two lines showing $0.5\mathrm{expit}(-1)+0.5\mathrm{expit}(1)\ne \mathrm{expit}(0)$ would make the aggregation principle tangible before the main theorems.

The transition from arm-level aggregation to treatment contrasts is still a possible stumbling block. The chapter shows that $\theta_{\bullet C}$ and $\theta_{\bullet B}$ are biased differently, then computes the marginal odds ratio. But a reader who is just learning ITCs may need a stronger reminder that indirect comparisons ultimately compare treatment effects across studies, so a small aggregation mistake in each arm can become a systematic error in the network contrast.

The future-chapter dependencies are sometimes used as placeholders where a novice needs local intuition. The chapter postpones covariate distribution reconstruction to Chapter 22, identifiability to Chapter 23, discrete likelihood approximations to Chapter 21, and computation to Chapter 24. That is reasonable structurally, but the reader still needs minimal local answers to "what does ML-NMR use from an AgD study?" and "why is this estimable at all?"

## Suggested improvements

Add a short clinical motivating example before the first formal definition. For instance: an AB trial has IPD with age and baseline severity, a BC trial reports only mean age, severity summaries, and arm event counts, and the analyst wants a coherent estimate of B versus C in a chosen population. Then explain that ML-NMR uses the IPD to learn the individual outcome model and uses the AgD covariate distribution to average predicted individual risks in the AgD trial.

Insert a small "translation table" near @def-individual-model. It could map the model terms to applied meanings: $\mu_j$ as study baseline risk, $\gamma_k$ as treatment effect at the reference covariate value, $\boldsymbol\beta_1$ as prognostic covariate effect, $\boldsymbol\beta_{2,k}$ as effect modification, and $f_j$ as the case-mix distribution of study $j$.

Add a bridge paragraph before @thm-aggregation that says, in words, what will be proved. A possible message is: if we could see every patient in an AgD trial, we would evaluate their conditional risk and multiply their likelihood contributions. Because we cannot see those covariates, we average over their distribution. That averaging produces both the arm mean and the aggregate likelihood.

After @thm-aggregation, add a concrete binary AgD likelihood example. Use a simple event count such as 37 events out of 100 and say how $\theta_{\bullet jk}$ enters the aggregate model. This would make the IPD versus AgD likelihood contrast much more intuitive.

Move a very small discrete logit calculation earlier, or preview the worked example before the Jensen theorem. The chapter currently asks the reader to absorb the formal theory before seeing the simple arithmetic that makes the idea obvious. A tiny early example would reduce cognitive load.

Strengthen the Jensen-gap interpretation. After @thm-aggregation-bias, add a paragraph that states why this matters for ITC: each arm can have a different slope, covariate distribution, and curvature region, so the plug-in biases need not cancel when forming a treatment contrast.

Clarify the risk interpretation of logit curvature before the theorem. Say explicitly that when the mean linear predictor is below zero, the mean risk is below 50 percent and the logistic curve is convex, so heterogeneity pulls the average risk upward. When it is above zero, mean risk is above 50 percent and the curve is concave, so heterogeneity pulls the average risk downward.

Consider shortening or demoting the heat-flow section. It could be labeled as optional mathematical insight, moved after the main link-specific results, or reduced to a remark. The current placement interrupts the applied learning path from aggregation to identity, log, and logit examples.

Reframe the no-closed-form logit result around practical consequences. The proof can remain, but the main teaching message should be stated first: for binary outcomes with continuous covariates, ML-NMR usually cannot compute the aggregate risk by algebra, so it needs numerical integration. The formal non-elementarity discussion can then be treated as supporting context.

Add one more health-facing exercise. For example: "Two trials have the same mean age but different age variability. Explain why a nonlinear outcome model may predict different aggregate risks, and why matching only mean age may not remove ecological bias." This would test conceptual understanding without requiring heat equations.

## Highest-priority fixes

1. Add a simple running health-research example before the formal model. The chapter needs an AB and BC mixed IPD and AgD story that follows the reader through the aggregation principle.

2. Make the IPD versus AgD likelihood distinction more concrete. The reader should see exactly how an observed patient contributes in IPD and how an event count or arm mean contributes in AgD.

3. Add bridge sentences around the aggregation theorem and Jensen theorem. These are the chapter's core ideas, and the current transitions are too abrupt for a novice.

4. Explain $f_j$ as study case mix, including what is known, what is reconstructed, and why this matters for AgD trials.

5. Move or clearly label the heat-flow material as optional advanced structure. It is likely to distract novice health researchers from the main ML-NMR intuition.

6. Bring a tiny numeric aggregation example earlier. The later worked example is good, but the reader needs a quick arithmetic demonstration before the long formal development.

7. State the treatment-contrast consequence of arm-level aggregation bias more directly: ML-NMR matters because aggregation errors can differ by arm and therefore distort indirect comparisons, not merely because arm means are individually misestimated.
