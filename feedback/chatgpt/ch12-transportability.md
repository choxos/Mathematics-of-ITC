# Chapter 12 Feedback: Transportability: The Estimand-Based Theory

## Overall reaction

This chapter has a strong and important message for a health researcher learning indirect treatment comparisons: an effect estimate is not automatically portable just because it came from a valid trial, and the population attached to the estimand matters. The introduction is compelling, especially the contrast between the trial population and the reimbursement decision population. The chapter also makes the key warning memorable: odds ratios and hazard ratios are often the measures decision makers see, but they are also the measures that resist marginal transport.

From a novice reader's perspective, though, the chapter becomes abstract very quickly. The prose often assumes the reader can already move comfortably among conditional means, marginal effects, links, transforms, covariate distributions, and estimands as functionals of populations. A motivated health researcher can follow the practical concern, but may not yet have enough mathematical fluency to see why the formulas answer that concern. The chapter would be more teachable if it gave the reader a concrete HTA story, then kept returning to that story whenever a new formal object is introduced.

The most valuable parts are the two-step PAIC decomposition, the sponsor disagreement remark, the transportability table, and the worked examples. Those are the parts where the chapter feels closest to the novice's real question: "What population does this comparison actually apply to?" The main weakness is that the bridge between that practical question and the formal machinery is sometimes too thin.

## What was clear

The opening motivation is clear and clinically relevant. The sentence that a randomized trial answers a question about enrolled patients while a reimbursement decision asks about future treated patients gives the reader a concrete reason to care about transportability.

The distinction between generalizability and transportability is helpful. Defining generalizability as a within-population sampling issue and transportability as a between-population movement issue is likely to stick, especially because the text immediately explains why HTA lives in the gap between them.

The paragraph after the transport g-formula that maps the formula to STC, MAIC, ML-NMR, and doubly robust methods is very useful. A novice may not absorb every formula in @thm-conditional-transportability, but they can understand that outcome regression predicts into the target population, weighting rebalances the source population, and doubly robust methods combine those routes.

The two-step decomposition of PAIC is one of the clearest conceptual contributions. The idea that the explicit step standardizes the index trial to the comparator population, while the implicit step carries the comparator-population effect to the decision population, is exactly the kind of insight a novice needs before using MAIC or STC mechanically.

The "Why two sponsors can disagree" remark is excellent. It turns an abstract estimand issue into a realistic applied scenario and makes the point that different answers can be different estimands rather than mistakes.

The worked binary example is especially effective. Seeing the same conditional odds ratio of 7.389 become marginal odds ratios of 3.24 and 1.86 in two populations makes non-collapsibility much more understandable than the theorem alone.

## What was unclear

The phrase "a population is a probability distribution over the covariate space" is mathematically precise, but it is not yet intuitive for the intended novice. A health researcher may think of a target population as "adults with moderate to severe disease eligible for reimbursement in Canada" or "patients matching the label indication." The chapter should explicitly connect that real-world population to the density $f_{\mathcal P}$ and explain that the density is the mathematical representation of how age, severity, prior treatment, biomarkers, and other baseline variables are distributed in that group.

The definition of structural invariance is central but may feel too strong or too hidden. The text says the conditional model is biology rather than population, but a health researcher may immediately wonder about health systems, adherence, follow-up schedules, background therapy, diagnostic criteria, or outcome measurement. The chapter should say more plainly that those features either need to be included in $X$, held comparable, or treated as reasons invariance may fail.

The difference between a marginal relative effect and a population-average conditional effect is easy to miss, even though it drives much of the chapter. The formulas in @eq-transport-marg-effect and @eq-transport-cond-effect are precise, but a novice may not understand why "transform after averaging" differs from "average after transforming." This distinction should receive a small numerical demonstration before it becomes the basis for non-collapsibility and transport failure.

Direct transportability and conditional transportability are defined correctly, but the labels could use more plain-language reinforcement. Direct transportability means "carry the number over unchanged." Conditional transportability means "carry the conditional response relationship over, then recompute the population average in the target population." That wording should appear close to the formal definition.

Scale alignment is probably the hardest new idea for a novice. The chapter introduces $g$, $h$, and $\psi=h\circ g^{-1}$ in a mathematically elegant way, but the health researcher first needs the practical question: "Did we model the outcome on the same scale on which we plan to report the treatment effect?" The logistic model with risk difference and the proportional hazards model with RMST are good examples, but they arrive after the formal definition. They should be previewed before the notation.

The sponsor-specific decision context is underdeveloped. The chapter says two sponsors can disagree because they standardize to different comparator populations, but it should spell out a concrete version: Sponsor 1 has AB IPD and standardizes to its AC trial; Sponsor 2 has BC or AC evidence with a different comparator population; a regulator or HTA body may need a third population defined by the label or reimbursement criteria. Without that, the phrase "decision population" may remain abstract.

## Under-explained details

The support and overlap conditions need more applied explanation. The theorem states that the target covariate support must be contained in the source support, but a novice needs an example such as: if the decision population contains older patients with renal impairment and the source trial excluded them, the source model cannot validly predict their outcomes without extrapolation.

The covariate set $X$ needs a practical checklist. The text says $X$ must be rich enough to capture every variable that modifies the treatment effect, but does not give much help for deciding what that means. A novice would benefit from a distinction between prognostic variables, effect modifiers, variables that affect trial inclusion, and variables that are merely imbalanced but irrelevant to transport.

The role of the comparator population $f_{AC}$ should be emphasized earlier. In @thm-two-step-transport, the reader learns that PAIC estimates $d_{BC(AC)}$, not $d_{BC(\mathcal P^{*})}$. That is crucial enough to deserve a simple table with rows for index trial AB, comparator trial AC, and decision population $\mathcal P^{*}$, showing which outcomes and covariates are observed and which estimand each step targets.

The effect scale examples need more clinical interpretation. The chapter lists mean difference, risk ratio, odds ratio, hazard ratio, RMST difference, and rate ratio, but a novice may not know which are conditional by default in a regression model and which are marginal by default in a decision analysis. The text should explicitly say why HTA often wants marginal effects for population-level decisions, and why a conditional odds ratio answers a different question.

The "if and only if" result in @thm-sema-insufficient is mathematically powerful, but the proof is too dense for the first pass. Terms like strict concavity, Jensen gap, non-degenerate, and mixture-of-survival argument may be familiar from earlier chapters but still cognitively heavy here. A short intuition paragraph before the proof would help: the odds ratio is nonlinear, so averaging risks changes the contrast even when the conditional odds ratio is constant.

The survival example could use more context. RMST is introduced as a reported effect, but the reader may need a sentence explaining that RMST is the expected event-free time up to a chosen horizon $\tau$, and that reporting an RMST difference is often more directly interpretable than reporting a hazard ratio.

The exercises are valuable but skew difficult. Several exercises require comfort with proofs, Jensen's inequality, and scale transformations. For a novice health researcher, there should be at least one lower-barrier exercise that asks them to identify source, comparator, and decision populations in a realistic HTA vignette before doing algebra.

## Where a novice may get lost

A novice may get lost when the chapter moves from the introduction into the formal setup. The practical claim is clear, but the first formal section immediately uses population distributions, densities, potential outcomes, structural invariance, marginal means, links, and conditional effects. The reader needs a local glossary or a slower bridge before those objects are used together.

The notation $d_{ab(\mathcal P)}$, $d_{ab}(x)$, $m_t(\mathcal P)$, $f_{AB}$, $f_{AC}$, and $\mathcal P^{*}$ is manageable one symbol at a time, but demanding in combination. In the two-step PAIC section, the reader must track treatments, trials, populations, scales, and estimands simultaneously. A diagram would reduce a lot of that burden.

The cancellation argument under SEMA is likely to be hard on first reading. The model in @eq-transport-nmr is compact, but a novice may not see why subtracting the B and C linear predictors cancels the baseline, prognostic term, and shared interaction. This deserves a small worked algebra line before the theorem, possibly with scalar $x$ and one effect modifier.

The phrase "scale misalignment manufactures effect modification" is memorable, but it may be puzzling until the reader has seen the logistic risk-difference example. The chapter should consider placing a tiny example before @thm-scale-alignment, then returning to the general theorem.

The transition from conditional transportability to direct transportability in PAIC is conceptually subtle. The reader may think: if I have standardized B to the AC population and C was measured in AC, then I am done. The chapter does say this is not enough for the decision population, but it should pause longer on the question "What if AC is not the population the decision maker cares about?"

The table in @prp-transport-table is very useful, but it arrives after several difficult theorems. A simplified preview table earlier in the chapter could orient the reader before the proofs, with columns such as "Can carry the marginal effect unchanged?" and "Why or why not?"

## Suggested improvements

Add a running HTA example and keep it alive throughout the chapter. For example: Trial AB enrolled younger biologic-naive patients, Trial AC enrolled older biologic-experienced patients, and the decision population includes all reimbursement-eligible patients in a national HTA submission. Use this example when defining $\mathcal P$, $f_{AB}$, $f_{AC}$, and $\mathcal P^{*}$.

Add a figure for the two transports in PAIC. It should show AB IPD moving conditionally to AC, then AC moving directly to the decision population. Label Step 1 as "model or weight to comparator population" and Step 2 as "assume comparator-population effect applies to decision population." This would make @eq-two-step-bias much easier to understand.

Before the formal definition of scale alignment, add a short plain-language subsection: "Model scale versus reporting scale." Give two aligned examples and two misaligned examples, then introduce $g$, $h$, and $h\circ g^{-1}$ as the notation for that idea.

Add a local "what to remember" paragraph after the major theorems. For @thm-conditional-transportability, say that we can identify target outcomes if the source conditional outcome model is valid in the target and the target contains no covariate patterns absent from the source. For @thm-two-step-transport, say that standard PAIC usually targets the comparator trial population. For @thm-sema-insufficient, say that SEMA makes the conditional odds ratio portable, not the marginal odds ratio.

Strengthen the explanation of target population and sponsor-specific decision contexts. The text should explicitly separate the trial source population, the comparator trial population, the sponsor's estimand, and the HTA decision population. A novice should come away knowing that the "target" is not automatically "the comparator trial" and not automatically "whoever was in the IPD."

Move one simple numerical contrast earlier. Even a two-line example showing that the same conditional odds ratio can produce different marginal odds ratios would motivate the later proof and make the chapter's central warning easier to accept.

Make the exercises more tiered. Start with applied identification and interpretation questions, then move to computations, then proofs. The starred proof exercises are appropriate, but the unstarred set should include more tasks a novice health researcher can complete without advanced mathematical maturity.

## Highest-priority fixes

1. Add a concrete running HTA example that defines the source, comparator, and decision populations and returns in each major section.

2. Add a diagram or table for the two-step PAIC transport, especially the fact that the usual PAIC estimand is $d_{BC(AC)}$ unless the decision population is actually the comparator population.

3. Add more intuition before scale alignment and non-collapsibility. A novice needs to understand the practical idea before seeing $h\circ g^{-1}$, strict concavity, or Jensen's inequality.

4. Clarify the difference between marginal effects and population-average conditional effects, since this is the point on which the odds-ratio and hazard-ratio conclusions turn.

5. Make the decision-context language more explicit. Explain why a regulator, payer, or sponsor may care about $\mathcal P^{*}$ rather than $f_{AC}$, and what information is needed to define that population.

6. Add applied interpretation to the worked examples. After each calculation, state in plain language what a researcher would report, what population it applies to, and what would go wrong if they carried it to another population.

7. Add at least two novice-accessible exercises based on realistic HTA vignettes before the proof-heavy exercises.
