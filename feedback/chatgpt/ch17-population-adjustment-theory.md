# Chapter 17 Feedback: Population Adjustment Theory
## Overall reaction

This chapter has a strong conceptual backbone: population adjustment is presented as the response to the failure of Bucher when trial populations differ in effect modifiers. From the perspective of a novice health researcher, the chapter is serious, coherent, and often reassuringly explicit about what each assumption buys. The anchored versus unanchored distinction is especially important, and the chapter repeats it often enough that the reader can eventually see why unanchored comparisons require much stronger assumptions.

The main weakness is that the chapter often moves from an intuitive sentence directly into dense theorem language. A mathematically stronger reader will appreciate this, but a novice health researcher may not yet have enough scaffolding to connect the symbols to a trial appraisal task. The chapter would be easier to learn from if it paused more often to say, in ordinary health research terms, what is being estimated, whose population it applies to, what data are available, and why the assumption is plausible or implausible.

The introduction is accurate but overloaded. It names Bucher, effect modification, IPD, AgD, MAIC, STC, ML-NMR, scale alignment, non-collapsibility, anchored comparisons, unanchored comparisons, SEMA, testability, and the proof catalogue before the reader has worked through one concrete population-adjusted example. For a motivated novice, the central story is visible, but it is buried under many forward references and technical caveats.

## What was clear

The operational contrast between IPD and AgD is clear in `Data structures, models, and estimands`. The sentence explaining that IPD lets the analyst recompute an effect under a new covariate distribution, while AgD only gives an already averaged effect, is one of the most helpful novice-facing sentences in the chapter.

The anchored versus unanchored setup is also clear at the broad level. The text repeatedly explains that a common comparator can cancel baseline differences in the anchored case, while the unanchored case has no comparator and therefore must transport absolute outcomes. This is likely to stick with a health researcher because it maps directly to a recognizable trial network problem.

The distinction between effect modifiers and prognostic variables is useful and well motivated. The purely prognostic covariate example makes the key point: a variable can change outcomes without changing a treatment contrast, so it matters much more in unanchored comparisons than in anchored ones.

The worked anchored comparison is the chapter's best learning device. The binary covariate, explicit risks, unadjusted Bucher estimate, adjusted estimate, weights, effective sample size, and odds-ratio contrast give the reader concrete numbers to check. Step 6 is especially useful because it shows that the estimand and scale are not cosmetic choices.

The short methods preview at the end helps connect theory to MAIC, STC, and ML-NMR. It gives the reader a reason to care about the abstract formulas before moving into the method chapters.

## What was unclear

The target population concept needs more intuitive framing. The chapter defines $\mathcal P^{*}$ formally, but a novice may still ask: is the target the population in the comparator trial, the reimbursement population, a trial-eligible population, or something chosen for convenience? The text mentions that in the two-study MAIC case $\mathcal P^{*}=\mathcal P_{BC}$, but the practical consequences of choosing one target rather than another are not explained enough.

The marginal versus population-average conditional estimand distinction is formally stated but still hard to internalize. Both quantities are averages over a population, and both use similar notation. A novice may not immediately grasp why "average the stratum-specific effects" and "contrast the marginal means" are different questions. The chapter should add a plain-language comparison before equations @eq-pat-marg and @eq-pat-cond, perhaps with one small binary-risk example.

The model-link versus reporting-scale distinction is introduced early, but the reader is not given enough concrete anchors before seeing $h\circ g^{-1}$. A novice health researcher may know risk difference, risk ratio, odds ratio, hazard ratio, and RMST, but not know which are model links, reporting scales, or marginal estimands. A small table would help a lot.

SEMA is mathematically defined, but its health-research meaning is underdeveloped. "The treatment-by-covariate interactions are the same" is clear algebraically, but a novice needs a clinical example: for instance, disease severity modifies both active treatments versus placebo by the same amount, so severity cancels in the active-versus-active contrast. The chapter should also give a counterexample where SEMA is implausible.

The phrase "conditional recovery, any scale" in the anchored theorem could be misread. A novice might think this means the method recovers any clinically reported effect measure, but part (c) then says it does not generally recover a non-collapsible marginal odds ratio or hazard ratio. The distinction between recovering a conditional contrast on a named scale and recovering a marginal policy estimand needs to be stated in plainer terms before the theorem.

## Under-explained details

The chapter uses the reference-second convention several times, where $\tau^g_{kC}(x)=g(\mu_C(x))-g(\mu_k(x))$ and a positive value means the active treatment improves an unfavorable outcome. This is easy to miss and can reverse the reader's interpretation of the worked example. A small sign-convention callout before the example would prevent confusion.

The role of AgD covariate summaries is not fully unpacked. The theory often writes integrals over the target density $f_{*}$, but in practice the AgD trial may report only means, standard deviations, or selected proportions. A novice may not understand when matching means is enough and when the full covariate distribution is needed. This is particularly important because MAIC is previewed as entropy balancing on moments, while the theory is written as exact density reweighting.

Overlap is listed as an assumption, but the practical meaning deserves more explanation. A health researcher needs to know that if the target population includes patients unlike any in the IPD trial, the model is extrapolating rather than transporting. This would connect the positivity condition to trial eligibility criteria and baseline characteristics tables.

The chapter says unanchored comparisons require adjustment for prognostic variables as well as effect modifiers. That is clear mathematically, but the practical burden could be made more vivid. The reader should be told that this often means measuring every important predictor of outcome, including variables that do not modify treatment benefit, which is why unanchored comparisons are fragile.

The testability section is elegant but abstract. "Over-identifying restriction" and "node-splitting" may be too compressed for a novice. The section would benefit from a paragraph saying: with only one AgD contrast, many different combinations of the B main effect and B interaction can produce the same observed summary, so the data cannot tell whether SEMA is true.

## Where a novice may get lost

The introduction may overwhelm the reader before they know the chapter's basic problem. It might work better to start with a single clinical network: trial AC has younger patients, trial BC has older patients, age modifies A versus C, and the analyst wants A versus B in the BC or decision population. Then the chapter can name that as population adjustment.

The anchored consistency theorem is a likely stopping point. It contains multiple assumptions, five conclusions, collapsibility, scale alignment, non-collapsibility, scale misalignment, and class-wise necessity. The theorem may be correct and important, but a novice needs a "reader translation" immediately before or after it: "If this is an anchored comparison, adjust for imbalanced effect modifiers on the scale you plan to analyze. Do not expect this to give a marginal odds ratio unless the estimand and scale conditions also line up."

The notation load is high in the first half: $\mathcal P_{AC}$, $\mathcal P_{BC}$, $\mathcal P^{*}$, $f_{*}$, $g$, $h$, $\tau$, $\Delta^{\mathrm{Marg}}$, $\Delta^{\mathrm{Cond}}$, $\theta^{\mathrm{anch}}$, and $\tilde d$ appear before the worked example. A compact symbol table for this chapter only would make the text much more approachable.

The target-population estimand theorem appears late, after the anchored and unanchored consistency theorems. For learning, the reader may need the estimand definitions earlier. Otherwise the chapter proves consistency for objects that the novice has not yet fully understood.

The scale-dependence example is good, but it appears after SEMA and the main theorems even though the phrase "on scale $g$" is already doing heavy work throughout. Moving a simpler version earlier, or previewing it near the first definition of effect modification on scale $g$, would make later caveats less surprising.

Some exercises are quite demanding for the intended novice. The first three exercises are accessible and useful. The reverse scale-dependence construction and the starred non-collapsibility exercise are valuable, but they may need hints or a graduated warm-up version so readers do not confuse algebraic difficulty with conceptual failure.

## Suggested improvements

Add a short clinical vignette before the formal setup. It should name treatments A, B, and C, describe the AC and BC trials, identify a plausible effect modifier such as baseline risk or disease severity, and state the target population in words.

Add a "what changes by architecture" table with columns for anchored and unanchored comparisons. Rows could include available data, target quantity, assumption needed, covariates that must be adjusted, what the comparator cancels, and why the method can fail.

Move or preview the target estimand definitions earlier. A novice should know the difference between the target marginal effect and target population-average conditional effect before reading the consistency theorems.

Add a scale cheat sheet. Include examples such as identity link and risk difference, log link and risk ratio, logit link and odds ratio, log-hazard and hazard ratio, and hazard model with RMST target. For each, state whether the chapter's caveats about non-collapsibility or scale misalignment are likely to matter.

Insert plain-English interpretations after the key formal results. The most important places are @prp-pat-conditional-transport, @thm-anchored-paic-consistency, @thm-unanchored-paic-consistency, @def-sema, and @prp-testable-untestable-constancy.

Clarify when exact theory differs from reported trial summaries. The chapter sometimes speaks as if AgD gives an average conditional contrast, but many trial reports give marginal arm summaries or model-based adjusted estimates. A note distinguishing the idealized theorem from common reporting practice would help.

Expand the SEMA explanation with one plausible example and one implausible example. The current algebra is concise, but the health-research intuition is not yet strong enough for a new learner.

Add small visual or tabular summaries for effect modifiers versus prognostic variables. A two-by-two table with "affects outcome" and "affects treatment contrast" would reinforce why anchored and unanchored comparisons need different adjustment sets.

## Highest-priority fixes

1. Put the target population and target estimand story earlier, with a concrete health-research example.

2. Add a plain-language guide to the anchored consistency theorem, especially the difference between conditional recovery and marginal recovery.

3. Add a scale table explaining $g$, $h$, collapsibility, non-collapsibility, and scale misalignment with common measures.

4. Strengthen the clinical intuition for SEMA and for why it is often untestable in the smallest network.

5. Add novice-friendly bridge text around AgD limitations, overlap, and why unanchored comparisons require prognostic variables, not just effect modifiers.
