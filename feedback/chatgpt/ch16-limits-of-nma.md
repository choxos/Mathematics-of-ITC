# Chapter 16 Feedback: The Limits of Standard Network Meta-Analysis

## Overall reaction

This is an important and convincing chapter, but for a novice health researcher it is currently more rigorous than teachable. The central message is strong: standard NMA fails when trial populations differ in effect modifiers, and aggregate meta-regression cannot reliably repair that failure because it works with trial-level summaries rather than individual-level relationships. I understood that message by the end, especially after the worked examples, but the chapter asks the reader to carry too much notation before giving enough clinical intuition.

The chapter would work better if it made the practical ITC problem concrete earlier. A novice needs to picture a familiar anchored comparison: an A versus C trial in one patient population, a B versus C trial in another, and a target population for the A versus B decision. The current opening says this, but mostly in mathematical language. Before the first definition, it would help to say plainly that the common comparator C does not make the two trials comparable if the patients differ in a variable that changes the relative benefit of A or B.

The strongest parts are the exact bias formula, the remarks explaining why the Bucher standard error is silent, and the risk-difference worked example. The hardest parts are the distinction between marginal and average-conditional effects, the two meanings of constancy, the noncollapsibility discussion, and the ecological-bias section. Those are exactly the ideas a novice needs most, so they need more scaffolding.

## What was clear

The introduction does a good job identifying constancy of relative effects and transitivity as the load-bearing assumption behind Bucher and standard NMA. The statement that this chapter explains what happens when that assumption fails is motivating.

The paragraph after the failure-of-Bucher theorem is one of the clearest parts of the chapter. Explaining each bias term as the difference between the trial-population mean of a conditional contrast and the target-population mean gives the formula an interpretation rather than leaving it as an integral identity.

The distinction between effect modifiers and purely prognostic variables is useful, especially the corollary that prognostic variables cancel in anchored comparisons. This is a clinically important point because otherwise a novice might think every baseline imbalance is equally threatening.

The two remarks after the prognostic-variable corollary are helpful. "Where the standard error is silent" explains a major practical trap: a precise indirect comparison can still be precisely wrong. "What is and is not testable" helps the reader understand why transitivity is a substantive assumption, not something guaranteed by the network geometry.

The first worked example is very effective. The binary covariate, risk-difference scale, sign reversal, and explicit recomputation of the bias make the abstract theorem feel real. This example should probably be previewed earlier, because it is the first point where a novice can easily see the mechanism.

The final section connecting the gap to MAIC, STC, and ML-NMR is helpful. It clearly states that population adjustment must estimate the conditional contrast function and integrate it over the target covariate distribution.

## What was unclear

The chapter introduces several related quantities too quickly: marginal relative effect, average-conditional relative effect, target average-conditional contrast, Bucher estimand, and trial-reported contrast. A novice can easily lose track of which quantity is observed from a trial, which is estimated from IPD, which is the target estimand, and which one standard NMA implicitly subtracts.

The sign convention needs more explicit help. The notation $d_{AB}$ is described as A versus B in prose, but the definition of $\tau^g_{ab}(x)=g(\mu_b(x))-g(\mu_a(x))$ means the contrast is treatment $b$ relative to treatment $a$. In the worked example, the target risk difference is $+0.05$ and is interpreted as B raising risk relative to A. That is coherent, but a novice reader may expect "A versus B" to mean A minus B. A small sign-convention box before the theorem would prevent confusion.

The statement that a trial reports the marginal effect while an IPD regression estimates the average-conditional effect is important, but the explanation is too compressed. It would help to spell out what the trial publication gives the analyst in a real ITC: arm-level event counts, mean outcomes, odds ratios, hazard ratios, and sometimes covariate summaries. Then connect those outputs to $d_{ab(\mathcal P)}$.

The "two faces of constancy" section is conceptually important but abstract. Conditional constancy sounds stronger than marginal constancy, so it is not obvious at first why conditional constancy can hold while Bucher still fails. A clinical sentence would help: the biology of the treatment effect within age strata may transport perfectly, but the trial-level average changes if one trial has many older patients and the other has few.

The noncollapsibility surcharge remark is dense. It says the theorem is exact for the average-conditional estimand on any scale, while trial-reported marginal contrasts on a non-collapsible scale add a second discrepancy. That is a subtle and important distinction, but a novice needs a table or mini-example showing the two separate problems: population imbalance in effect modifiers and the difference between marginal and conditional odds ratios.

The ecological-bias section says aggregate meta-regression is the natural first attempted cure, but it does not show enough of what that attempted cure looks like. A novice would benefit from seeing a tiny table with trial mean age and trial log odds ratio, followed by the warning that the slope across trial means is not the same as the patient-level treatment-by-age interaction.

## Under-explained details

The target population $\mathcal P^{*}$ needs more practical motivation. The chapter says the target is where we wish to report A versus B, but it would help to give examples: the decision population for reimbursement, the population of the B versus C trial, or the population represented by an HTA submission. Different target choices matter for population adjustment.

The difference between an effect modifier and a prognostic variable should be illustrated before the corollary. For example, baseline severity can raise event risk in both arms and be prognostic, but it only threatens anchored ITC if it changes the treatment contrast. The cancellation idea is too important to leave mostly to algebra.

Direct collapsibility is treated as known from earlier chapters, but this chapter depends heavily on it. A short reminder would help: on the risk-difference scale, averaging first and contrasting second gives the same answer as contrasting first and averaging second; on odds-ratio-like scales this can fail.

The integral notation assumes comfort with densities, signed differences of densities, and support. The proof uses point masses and narrow densities, which are mathematically fine, but a novice may need a discrete binary-covariate version of the bias formula before seeing the general integral form.

The phrase "covariance-like quantity" is useful but underdeveloped. It would help to say that bias is large when high-effect strata are overrepresented or underrepresented relative to the target. That wording connects the formula to the epidemiologic idea of case mix.

The ecological-bias definition introduces $b_2$ as a slope in $\bar x$ of the aggregate marginal contrast. This is a major conceptual jump. The reader needs a clearer distinction between $\beta_2$, the within-patient interaction from an individual model, and $b_2$, the between-trial slope from aggregate summaries.

The role of within-trial variance $\sigma^2$ in the probit theorem is mathematically clear but practically under-explained. The key point is that two sets of trials can have the same covariate means but different within-trial spreads, and the aggregate contrast can change because nonlinear models average over the whole distribution, not just the mean.

## Where a novice may get lost

A novice may get lost in the first definition because "marginalizes inside the link" and "outside the link" are precise but not intuitive. This needs a plain-language translation immediately after the equations.

The proof of the collapsibility proposition references earlier results and Jensen gaps before the reader has a stable picture of the two effects being compared. A small numeric example with the identity link and the logit link would make the proposition less abstract.

The failure-of-Bucher theorem is long enough that a novice may not know what to focus on. The theorem would be easier to absorb if preceded by a one-line binary-covariate version, such as bias equals the treatment-specific effect-modification slope times the difference between trial and target prevalence, minus the analogous term for the other contrast.

The transition from Bucher bias to ecological bias is a big jump. The reader has just learned that the cure is to reweight or re-regress conditional contrasts to the target population. Then the chapter moves to aggregate meta-regression and Jensen's inequality. A bridge paragraph should explain the analyst's temptation: "I do not have IPD for the other trial, but I do have trial mean age, so maybe I can estimate effect modification from trial means."

The probit ecological theorem is likely to lose novice readers because many symbols change at once: $a_0$, $a_1$, $\rho_0$, $\rho_1$, $\beta_2$, $b_2$, $\sigma^2$, and $\bar x_j$. The result is important, but it needs a symbol map before the theorem.

The second worked example is useful but less accessible than the first. It confirms the theorem numerically, but a novice may still not understand why the aggregate slope is attenuated. A sentence comparing "patients within trials" versus "trial averages across trials" would help.

The exercises become difficult quickly. The logit compounding exercise and general attenuation exercise are valuable, but they need more hints or should be clearly marked as advanced. The first two exercises are more appropriate for the target novice audience.

## Suggested improvements

Add a short clinical running example before the first definition. For instance: A versus C was studied mostly in low-risk patients, B versus C mostly in high-risk patients, and baseline severity modifies the benefit of A but not B. Use this example to explain why subtracting the two trial effects can give the wrong A versus B answer.

Add a compact estimand table with columns for notation, plain meaning, what data estimate it, and why it matters. Include $d_{ab(\mathcal P)}$, $\tilde d_{ab(\mathcal P)}$, $\Delta^{\mathrm{Cond},g}_{AB}(\mathcal P^{*})$, and $d_{AB}^{\mathrm{Bucher}}$.

Add a sign-convention note near the start. State explicitly that $d_{AB}$ and $\tau_{AB}$ are B relative to A under the chapter's notation, and that positive risk difference means B has a higher event risk than A when the event is unfavorable.

Move a simplified version of the first worked example earlier, or give a preview before the theorem. The full example can remain later, but the reader needs a concrete binary case before the general integral formula.

Add a side-by-side explanation of effect modifier versus prognostic variable in anchored comparisons. One row should show a covariate that changes both arm risks equally and cancels. Another row should show a covariate that changes the treatment difference and does not cancel.

Before the ecological-bias proof, add a small aggregate meta-regression example with trial-level covariate means. Then state the problem in plain language: a between-trial slope based on averages is not the same as a within-patient interaction.

Add a visual or verbal explanation of the Jensen gap. For example: with a curved risk function, the average of patients' risks is not the risk of the average patient. That sentence would make the mathematics much easier to interpret.

In the final population-adjustment bridge, add one sentence for each method saying what data it needs. MAIC needs IPD in one study and aggregate target moments; STC needs an IPD-fitted outcome model plus target covariates or summaries; ML-NMR models IPD and AgD jointly by integrating over covariate distributions.

Add more exercise hints for novice readers. The first risk-difference exercise is well pitched. The noncollapsibility and general-link exercises should have intermediate steps or be marked as advanced challenge exercises.

## Highest-priority fixes

1. Add a concrete health-research example before the first definition so the reader understands why population differences can break standard NMA even with a common comparator.

2. Add an estimand and sign-convention table. This would prevent confusion about marginal versus average-conditional effects, target effects, Bucher subtraction, and whether the contrast is B relative to A or A relative to B.

3. Insert a binary-covariate version of the Bucher bias formula before the general integral theorem. This would make the theorem feel like a generalization of an understandable calculation rather than a first encounter with the idea.

4. Rebuild the ecological-bias section around the practical failed cure: aggregate meta-regression on trial-level covariate means. Explain that $b_2$ is a between-trial slope and $\beta_2$ is a within-patient interaction before proving the probit attenuation result.

5. Strengthen the bridge from failure to population adjustment. State more explicitly that standard NMA fails because it averages the wrong conditional effects over the wrong populations, and population-adjusted methods are needed because they estimate conditional effects and average them over the target population.
