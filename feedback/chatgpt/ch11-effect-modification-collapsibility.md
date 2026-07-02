# Chapter 11 Feedback: Effect Modification, Interaction, and Collapsibility

## Overall reaction

The chapter has a strong core message: effect modification and non-collapsibility are different reasons why trial results can appear to disagree, and a reader must keep conditional and marginal effects separate. The opening is especially helpful because it starts with a recognizable trial-comparison problem rather than with notation.

From the perspective of a novice health researcher, however, the chapter becomes mathematically dense very quickly. It often explains the correct formal distinction before giving enough practical intuition for why a health researcher would care, how the distinction would show up in an evidence synthesis, or what decision the reader should make differently. I could follow the broad story, but I would not always know how to diagnose the situation in my own indirect treatment comparison.

The chapter is strongest as a rigorous reference for a reader who already knows potential outcomes, link functions, odds ratios, hazard ratios, and transportability. It is less secure as a teaching chapter for someone who is just learning ITCs and is weak in abstract mathematics. The main concepts are distinguishable by the end, but the path there is steep, and several bridge sentences or small examples would make the distinction much more usable.

## What was clear

The introductory contrast between effect modification and non-collapsibility is very effective. The two-trial story makes the reader understand that one phenomenon is about real variation in effects across patient types, while the other is about the effect measure changing when one averages. That framing should be preserved.

The definitions of conditional effect and marginal effect are conceptually clear once the reader slows down. The sentence explaining the order of operations, "transforms first, then averages" versus "averages first, then transforms," is one of the most useful teaching moments in the chapter. This should probably be repeated later, especially before the odds ratio and hazard ratio material.

The worked example is the most valuable part for a novice. It gives actual risks, computes risk differences, risk ratios, odds ratios, and then changes the covariate mix in a second trial. This is exactly the kind of example that lets a health researcher see why a marginal effect can move between trials. The comparison between $0.35$ as a true average and $4.5$ as a marginal odds ratio not equal to the constant conditional odds ratio $6$ is memorable.

The distinction between effect modifiers and prognostic variables is also useful. The four-cell table helps, and the anchored versus unanchored explanation gives the idea a clear role in ITCs. The chapter does a good job stating that anchored comparisons mainly need effect modifiers, while unanchored comparisons may need prognostic variables too.

The warning that non-collapsibility is not confounding is important and well placed. A novice could easily assume that any adjusted versus unadjusted discrepancy means bias. The chapter explicitly says that the discrepancy can occur inside a randomized trial, which is a strong corrective.

## What was unclear

The biggest unresolved difficulty is that the chapter asks the novice to track several distinctions at once: conditional versus marginal effects, effect modification versus interaction, effect modifiers versus prognostic variables, collapsibility versus direct collapsibility, and scale dependence. Each distinction is individually explained, but the cumulative load is high. A reader may understand one distinction locally and then lose it when the next one is introduced.

The term "scale" needs more concrete motivation before it becomes central. The chapter says identity, log, logit, and log-hazard scales, but a novice health researcher may not immediately connect these to risk difference, risk ratio, odds ratio, and hazard ratio as reporting choices. The chapter could state earlier that "scale" here means the mathematical form of the effect measure, not just the units of the outcome.

The transition from conditional and marginal effects to Jensen's inequality is abrupt. The marginal-conditional gap lemma is mathematically elegant, but for a novice it may feel like the chapter has suddenly switched from health research reasoning to abstract function behavior. The reader needs one small numerical preview before the lemma, or immediately after it, showing that averaging risks and then taking a logit differs from taking logits and then averaging.

The relationship between statistical interaction and effect modification is partly clear but still likely confusing. The chapter says interaction is model-bound and symmetric, while effect modification is causal and asymmetric. That is useful, but the health researcher may still wonder what to do with a regression output. If I fit a treatment by covariate interaction and it is nonzero, when should I call that effect modification, and when should I be cautious? The chapter could use a small paragraph translating this into applied language.

The hazard ratio section is mathematically correct in spirit, but pedagogically difficult. The closed-form survival example uses averaged survival functions, marginal hazards, and time-varying hazard ratios in quick succession. A novice who has only used hazard ratios as single Cox model summaries may not understand why the marginal hazard ratio can vary over time or why this is still not confounding.

## Under-explained details

The notation $\mu_t(x)$ is defined, but it carries a lot of work. A novice may need a plain-language reminder that $\mu_0(x)$ is the expected outcome risk under control among people with covariate value $x$, and $\mu_1(x)$ is the same under treatment. This should be repeated before the first numerical example, not only in the notation-heavy opening.

The link function $g$ is introduced as strictly increasing and twice differentiable, but the reader does not yet get enough intuition for why the chapter uses links rather than simply naming effect measures. A short table near the first definition could help:

| effect measure | link $g$ | what the contrast means |
|---|---|---|
| risk difference | identity | subtract risks |
| risk ratio | log | subtract log risks, equivalent to log risk ratio |
| odds ratio | logit | subtract logits, equivalent to log odds ratio |

Direct collapsibility is under-explained relative to how important it becomes. The definition says it is a weighting-respecting average of conditional effects, but a novice needs a more concrete paraphrase: if the effect varies across patient types, does the marginal effect still equal the patient-mix-weighted average of those stratum effects? That sentence would make the risk difference versus risk ratio contrast much easier to remember.

The phrase "baseline-risk distribution" appears in the odds ratio discussion and the worked example, but the reader may need help connecting it to prognostic variables. The chapter should explicitly say that even when the conditional odds ratio is constant, different mixes of patients with different control risks will change the marginal odds ratio.

The anchored cancellation lemma is important, but it is introduced in a way that may be hard to map onto actual trial networks. A novice may need a simple $A$ versus $C$ and $B$ versus $C$ diagram or paragraph before the lemma: the shared comparator creates subtraction of contrasts, so purely prognostic effects can cancel. Without that concrete anchor, the $(X,W)$ notation feels abstract.

The exercises are mostly demanding. They are appropriate for a mathematical textbook, but several assume the reader can construct counterexamples, prove monotone attenuation, or reason about limiting survival behavior. For a novice health researcher, there should also be one or two lower-entry exercises that ask for interpretation rather than construction.

## Where a novice may get lost

A novice may get lost in the first section when the chapter invokes several prior definitions by cross-reference: potential outcomes, SUTVA, consistency, ignorability, positivity, g-formula, and no confounding. Even if those were covered earlier, the opening of this chapter would benefit from a short plain-language recap: in this chapter, treatment assignment is randomized, so the differences shown are not caused by confounding.

The marginal-conditional gap lemma is a likely stumbling point. The notation $J_g(\mu_t)$ is efficient, but it hides the simple idea that a nonlinear transformation does not usually commute with averaging. Without a concrete risk or odds example, the reader may memorize the formula without understanding the problem it diagnoses.

The scale-dependence proposition may surprise readers in a good way, but the explanation could be more applied. A novice health researcher might ask whether it is "wrong" to call age an effect modifier if it modifies the risk difference but not the odds ratio. The chapter should answer directly: it is not wrong, but it is incomplete unless the effect measure is named.

The prognostic variable section has a subtle trap. The table says "effect modifier and not prognostic" is impossible, but the next theorem says an effect modifier need not be prognostic for a specified treatment. This is logically consistent because it must be prognostic for at least one treatment, but a novice may see it as a contradiction. The text should add a bridge sentence before the theorem to explain that "not prognostic" in the table means not prognostic for either arm.

The odds ratio proof will be difficult for the target reader. The change-of-measure argument with $Q$, $Q_\omega$, Radon-Nikodym derivatives, likelihood ratios, and covariance inequalities is far beyond what many health researchers need to understand the applied point. It is fine for rigor, but it needs a preceding intuitive explanation and maybe a boxed takeaway before the proof.

The synthesis table says "EM-status scale dependent" in the preceding text, but the table only lists collapsibility and direct collapsibility. If the chapter intends to summarize two axes, the table should include whether no-effect-modification on that scale is enough for marginal transportability, or it should explicitly say the table is only about collapsibility.

## Suggested improvements

Add an early "reader map" that uses plain applied language. For example: first decide whether the covariate changes the conditional treatment contrast on the effect scale you plan to report. That is effect modification. Then decide whether your effect measure remains the same after averaging over the patient mix. That is collapsibility. These are separate checks.

Add a small running two-stratum example before the formal definitions, then reuse it throughout. The final worked example is excellent, but it arrives late. A smaller teaser example near the start would make the definitions feel less abstract and would help the reader see why order of operations matters.

Insert a short table immediately after the conditional and marginal effect definitions that translates notation into health research language:

| notation | plain meaning |
|---|---|
| $\mu_0(x)$ | expected outcome under control for patients with covariate value $x$ |
| $\mu_1(x)$ | expected outcome under treatment for patients with covariate value $x$ |
| $\tau^g_{01}(x)$ | treatment effect within that covariate stratum on scale $g$ |
| $\Delta^{\mathrm{Marg},g}$ | effect after averaging outcomes over the target population |

Give more explicit "do not confuse" statements. The most important ones are: effect modification is not the same as having a prognostic variable; statistical interaction is not automatically a causal effect modifier unless the model and scale are meaningful; non-collapsibility is not confounding; a marginal odds ratio is not just the average of stratum odds ratios.

Move some of the advanced proof machinery behind a clearer teaching layer. For the odds ratio and hazard ratio, the chapter could first give a numerical demonstration and applied interpretation, then present the proof. That would let novice readers understand the result even if they cannot follow every algebraic step.

Add one accessible exercise that asks the reader to classify scenarios rather than prove a theorem. For example: given four small tables of stratum risks, identify whether there is effect modification on the risk-difference scale, whether there is effect modification on the odds-ratio scale, and whether the marginal odds ratio equals the conditional odds ratio.

Strengthen the ITC motivation at the points where the chapter becomes abstract. The opening and worked example clearly connect to trial comparisons, but several middle sections read as general causal inference theory. Short bridge sentences could repeatedly answer: why does this matter for Bucher, MAIC, STC, or ML-NMR?

## Highest-priority fixes

1. Add a plain-language bridge after the definitions of conditional and marginal effects, with one small numerical example showing "average then transform" versus "transform then average."

2. Clarify the scale concept early with a table linking identity, log, logit, and log-hazard scales to risk difference, risk ratio, odds ratio, and hazard ratio.

3. Add a novice-facing summary box distinguishing effect modification, statistical interaction, prognostic variables, collapsibility, and non-collapsibility in one place.

4. Make the prognostic-variable table less ambiguous by clarifying that "not prognostic" means not prognostic for either treatment, while an effect modifier may be prognostic for only one arm.

5. Put an intuitive numerical odds-ratio non-collapsibility example before the change-of-measure proof, so readers grasp the phenomenon before the proof details.

6. Add at least one low-entry exercise focused on interpretation and classification, not proof construction.
