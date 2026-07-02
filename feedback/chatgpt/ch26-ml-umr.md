# Chapter 26 Feedback: Multilevel Unanchored Meta-Regression

## Overall reaction

This is a strong and unusually honest chapter. It repeatedly tells the reader that ML-UMR buys target-population flexibility only by paying for SPFA, an assumption the available Type 1 data cannot test. That message is exactly what a novice health researcher needs to hear.

The main weakness is that the chapter often teaches by theorem cascade rather than by reader orientation. A motivated health researcher can probably follow the broad story, but only with effort: no shared comparator, borrow the prognostic slope from the index IPD, use the comparator aggregate outcome to locate the comparator intercept, then integrate both arms over a chosen target population. That story is present, but it is buried under many symbols, cross-references, and proof dependencies.

For this audience, the chapter needs more plain-language bridges before the formal results. The formal material is valuable, but a novice reader may not yet know which mathematical objects correspond to the clinical data they recognize: an index single-arm trial, an external comparator, a Kaplan-Meier curve, subgroup response rates, covariate summaries, and a requested HTA population.

## What was clear

The opening motivation is clinically recognizable. The examples of single-arm oncology trials, rare-disease registries, and real-world cohorts make the unanchored setting feel real rather than artificial.

The single-arm conflation result is helpful. The idea that a single-arm source identifies an absolute arm level, not a separable study baseline and treatment effect, is one of the clearest pieces of teaching in the chapter.

The SPFA message is candid. The chapter states that SPFA is stronger than SEMA, is untestable from two single-arm sources, and has to be defended externally. That is a crucial point for health researchers who may otherwise treat ML-UMR as a more advanced method that automatically solves unanchored comparison.

The comparison with unanchored STC is one of the most useful parts. The statement that ML-UMR agrees with unanchored STC in the comparator population, and only extends beyond it by assuming SPFA, is a clear practical takeaway.

The worked binary example is valuable. The two-point sums, the calibration of $\alpha_B$, and the SPFA-violation calculation make the abstract identifiability argument much easier to see. Step 6 is especially useful because it shows why comparator-population estimates can look stable while transported target-population estimates become fragile.

The final limits remarks are strong. The chapter clearly names untestable SPFA, unmeasured prognostic factors, reconstructed covariate distributions, Kaplan-Meier digitization noise, weak relaxed-model identification, and hazard-ratio non-collapsibility as real limitations.

## What was unclear

The phrase "absolute effects" is likely to confuse novices. Many health researchers read "absolute effect" as a risk difference or difference in mean outcomes. Here it means something closer to transportability of absolute outcome surfaces or conditional outcomes, contrasted with relative-effect transport in anchored comparisons. The chapter should pause and explain that distinction in ordinary language before using "conditional constancy of absolute effects" as a central concept.

The SPFA versus SEMA distinction is correct but too fast for a weak mathematical reader. The move from equal total slopes, to equal treatment-by-covariate interactions, to "no effect modification at all" depends on the reference-arm parameterization. A novice may think SEMA already says the slopes are equal, so why is SPFA stronger? This needs a small table that separates prognostic slope, treatment interaction slope, total arm slope, anchored cancellation, and unanchored projection.

The target population idea needs more operational explanation. The chapter says ML-UMR can report a contrast in any $\mathcal{P}^{*}$, but a health researcher will ask where $f_{*}$ comes from, what covariate moments are needed, whether correlations must be assumed, and what happens if only means are available. This is especially important because target flexibility is the advertised advantage over STC.

The relaxed model is hard to translate into practice. The theorem says subgroup outcomes can identify $\alpha_B$ and $\boldsymbol\beta_B$, but it is not immediately clear what a real paper would need to report. Is it response rates by biomarker subgroup, Kaplan-Meier curves by risk stratum, subgroup sample sizes plus covariate summaries, or all of these? The phrase "subgroup outcomes" needs concrete HTA examples.

The QMC section is mathematically clean but reader-hostile for a novice. Hardy-Krause variation, Sobol' nets, Gaussian copulas, and inverse-CDF transport arrive before the reader has a simple picture of why binary and survival outcomes need the full covariate distribution, while identity-link continuous outcomes may need only means.

The survival section is dense. PH, AFT, integrated censored likelihoods, pseudo-IPD reconstruction, marginal hazards, RMST, non-collapsibility, and scale misalignment are all introduced quickly. The individual ideas are important, but the reader needs a workflow: published Kaplan-Meier curve to pseudo event times, pseudo event times plus unknown covariates to integrated likelihood, posterior draws to target survival and RMST.

The outcome-direction conventions could be clearer. In the binary example, the outcome is a good response, so positive $\Delta_{AB}$ favors $A$. In survival, hazard ratios and RMST contrasts can point in opposite practical directions depending on which arm is in the numerator and whether higher is better. A novice reader needs explicit reminders at the survival transition.

## Under-explained details

The notation $\alpha_A$ and $\alpha_B$ deserves more interpretation. The chapter defines them as conflated intercepts, but a novice would benefit from a sentence saying that each is the fitted absolute arm level after study baseline and treatment main effect have become inseparable.

The chapter should explain earlier why $g(\bar\theta)$ is used rather than $\int g(\theta(x))f(x)\,dx$. The worked example eventually demonstrates non-collapsibility, but the estimand definition appears before the reader has been prepared for link of the marginal mean versus mean of the link-scale conditional effect.

The comparator covariate distribution $f_B$ is treated as known or reconstructed, but its uncertainty is not made very tangible. The chapter notes misspecification risk later, but the model-building sections would be clearer if they said which data are observed, which are reconstructed, and which are assumed.

The "automatic information weighting" remark is useful but could be misread as saying the joint likelihood makes the comparison robust. It should say plainly that more comparator events sharpen $\alpha_B$, but they do not validate the borrowed slope in the Type 1 model.

The relaxed model needs a distinction between identifiability and stability. The chapter mentions weak identification, but a novice may not understand that $Z\ge d+1$ is only a counting requirement. The subgroup covariate patterns must also be sufficiently different, and even then priors may dominate if the subgroup outcome summaries are noisy.

The pseudo-IPD reconstruction explanation should emphasize that pseudo patients do not have real covariates. A novice might otherwise imagine that the Kaplan-Meier reconstruction has recovered individual histories. The chapter says this, but it should be made more prominent because the survival model then integrates over a covariate distribution that is separate from the reconstructed times.

The worked example calls $X=1$ a high-risk indicator, but $X=1$ has a higher probability of a good outcome under the fitted index model. That may distract health researchers. Either rename the covariate to something like biomarker-positive or explain that "high-risk" here means a risk stratum with higher modeled response, not worse prognosis.

## Where a novice may get lost

A novice may get lost in the introduction because it relies on many prior chapter names and theorem labels before giving a simple data picture. The chapter would be easier to enter if it first showed one index trial, one external comparator, no common arm, and one target population, then named the formal methods.

The first estimand definition is mathematically precise but abrupt. A reader who is just learning ITCs may not yet understand why both arms are evaluated in the same target population, why the conditional model is integrated before taking the contrast, or why the contrast is on the link scale.

The proof of identifiability invokes full column rank, monotone aggregate maps, and a unique root. The health-researcher version is simpler: the IPD can estimate one slope and one intercept for arm $A$; SPFA lets that slope be reused for arm $B$; the comparator aggregate outcome then estimates the one remaining arm-$B$ intercept. That sentence should appear before the theorem.

The relaxed-model theorem is likely the hardest non-survival part. The weighted-moment matrix $M$ and inverse-function theorem will be opaque unless the reader first sees a simple example such as one binary effect modifier with two subgroup response rates, or two binary modifiers with four cells.

The QMC theorem may feel like a detour. The novice needs to know the practical reason for the machinery: aggregate papers usually report margins, not individual covariate rows, so the model fabricates integration points consistent with the reported margins and assumed correlations.

The survival material may overwhelm readers because it changes both the outcome type and the estimand scale. A novice can easily mix up conditional log hazard ratio, marginal hazard ratio, survival curve, RMST, RMST contrast, and median survival. A small estimand map would help.

The exercises are mathematically meaningful, but several assume comfort with bracketing, closed-form hazard derivations, and non-collapsibility arguments. More conceptual warmups would help novices check their understanding before moving into derivations.

## Suggested improvements

Add a short running example before the first definition. For example: trial A has IPD on a new therapy; study B has only an aggregate response rate and baseline age or biomarker summaries; there is no common comparator; the HTA question asks for $A$ versus $B$ in a reimbursement population. Reuse this example when introducing $\alpha_A$, $\alpha_B$, $\boldsymbol\beta_{\mathrm{PF}}$, $f_B$, and $f_{*}$.

Add a side-by-side comparison table for unanchored STC, ML-NMR, and ML-UMR. Useful columns would be data structure, need for a connected network, target population, key assumption, what is estimated from IPD, what is estimated from AgD, and main limitation.

Add a plain-language SPFA box. It should answer: what clinical belief does SPFA encode, what would violate it, why the data cannot test it in the Type 1 setting, and why it is stronger than SEMA. Include one plausible example and one implausible example.

Add a "what identifies what" table. Rows could be index IPD, comparator aggregate outcome, comparator covariate distribution, comparator subgroup outcomes, target population distribution, and external clinical knowledge. Columns could state the parameter or assumption each row informs.

Add a bridge before QMC. Explain that with an identity link the mean covariate value may be enough, but with logit, hazard, and other nonlinear links the average outcome depends on the full distribution of covariates, not just their means. Then the QMC machinery will feel motivated.

Add a relaxed-model mini-example. One binary covariate and two subgroup response rates would show why two equations can identify an intercept and slope. A second example with two subgroups that have nearly identical covariate profiles would show why counting alone is not enough.

Add a survival workflow figure or numbered recipe in prose. The recipe should be: digitize or reconstruct the comparator Kaplan-Meier curve, form pseudo event and censoring times, combine those with an assumed comparator covariate distribution, integrate the censored likelihood over unobserved covariates, fit the posterior, then compute target survival, marginal hazard, RMST, and median survival.

Make the worked example more visual. A small table with rows for $x=0$ and $x=1$, population weights, $p_A(x)$, fitted $p_B(x)$, and true $p_B(x)$ under SPFA violation would help the reader see why the comparator-population mean is calibrated while another target population is biased.

Add a few conceptual exercises. For example: explain in words why ML-UMR cannot test SPFA in the Type 1 model; decide whether a published evidence set supports SPFA, relaxed ML-UMR, or only STC; identify which target distribution information is missing from a mock HTA report.

## Highest-priority fixes

1. Add a novice-oriented roadmap near the start that explains the ML-UMR data flow in words before the first formal estimand.

2. Clarify SPFA, absolute-effect constancy, and the difference from SEMA with a concrete clinical example and a small notation table.

3. Add a side-by-side comparison of ML-UMR, unanchored STC, and ML-NMR so the reader can see exactly what ML-UMR adds and what assumption pays for it.

4. Add a practical identifiability table showing which data source identifies $\alpha_A$, $\boldsymbol\beta_{\mathrm{PF}}$, $\alpha_B$, $\boldsymbol\beta_B$, $f_B$, and $f_{*}$.

5. Expand the survival bridge, especially the path from Kaplan-Meier reconstruction to integrated likelihood and then to RMST or marginal hazard outputs.

6. Revise the worked example labels and presentation so the clinical meaning of the covariate, outcome direction, calibration at $\mathcal{P}_B$, and bias away from $\mathcal{P}_B$ are immediately visible.
