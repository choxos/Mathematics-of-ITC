# Chapter 9 Feedback: Potential Outcomes and Identification

## Overall reaction

This is a strong formal chapter, and the main causal story is there: define potential outcomes, explain why individual effects are unobservable, introduce SUTVA, define the main estimands, state ignorability and positivity, identify the ATE, then show why the naive contrast is biased. As a motivated health researcher, I found the chapter mathematically coherent and more readable than many causal inference texts because it keeps returning to the question of what is observed versus what is counterfactual.

The main weakness is that the chapter often moves from a helpful intuition to a very formal statement too quickly. It assumes that the reader can translate between health research language, probability notation, and ITC motivation in real time. A mathematically confident reader will be fine, but a novice health researcher may understand the individual paragraphs while losing the larger reason each assumption matters for indirect treatment comparisons. The chapter would benefit from more bridge sentences, a small clinical trial running example before the theorem sequence, and more explicit distinction between single-study confounding, between-study effect modification, and target-population transport.

## What was clear

The opening motivation is clear and useful. The statement that ITCs are ultimately counterfactual claims about what would happen under treatment B versus treatment C in a target population gives the chapter a relevant health-research purpose.

The fundamental problem section is effective. The two-world example with everyone treated is simple enough to follow, and it makes the missing-counterfactual problem feel structural rather than merely practical.

The consistency identity is well motivated. The explanation that consistency in causal inference is not the same as estimator consistency is exactly the kind of warning a novice needs.

The definitions of ATE, ATT, ATC, and CATE are concise and logically placed. The decomposition of the ATE over treated and control groups helps show that these are different questions, not just different names for the same thing.

The worked example in `Standardization undoes confounding in a two-stratum population` is the most useful part of the chapter for a novice. It makes the g-formula, naive contrast, and selection-bias decomposition concrete. The calculation that the naive contrast is 9 while the true ATE is 4 is memorable and clinically interpretable.

The selection-bias decomposition is also helpful. It gives a concrete meaning to confounding: treated patients would have had different untreated outcomes from controls even without treatment.

## What was unclear

The chapter says that every ITC is ultimately about counterfactuals, but the middle sections mostly read like a single-population causal inference chapter. The final bridge section reconnects to ITC, but by then a novice may have forgotten why the earlier assumptions matter for AB and AC trials. More ITC-facing reminders are needed throughout, especially after positivity, ignorability, and the adjustment formula.

The transition from patient-level language to the probability-space definition in `Potential outcomes` is abrupt. A novice health researcher may not know what it means for units to be points `omega` in `Omega`, or why measurability and `L^1(P)` are being mentioned. The formal definition is appropriate for the book, but it needs a short plain-language paragraph first.

SUTVA is formally defined using a full assignment vector over `Omega`. That is correct, but it is likely to be difficult for the intended novice reader. The vaccine and surgery examples help, but the reader may still not understand why SUTVA is needed before writing `Y = Y(T)`. A small table showing one patient, assigned treatment, observed outcome, and the hidden potential outcome would make the identity much easier.

The ignorability hierarchy is mathematically careful but pedagogically dense. Strong, weak, and mean ignorability appear all at once, followed by a proof using graphoid axioms, truncation, and conditional dominated convergence. A novice may leave this section unsure which version they should remember for health research practice.

The positivity section explains weak versus strict positivity, but the health-research interpretation could be stronger. The key idea is simple: we cannot learn treated outcomes for patient types who are never treated, or control outcomes for patient types who are never controls. That intuition should come before the propensity-score inequalities.

The chapter uses several forward references that may distract a novice, including non-collapsibility, collapsibility, ecological bias, transportability, and later estimators. These are important, but the current references sometimes feel like interruptions rather than signposts.

## Under-explained details

The target population is not explained enough. The ATE is defined as the expected effect if the entire population were switched from control to treatment, but the reader needs help understanding which population this is in a trial, in an observational cohort, and in an ITC target.

The statement that ignorability is untestable deserves a practical example. For instance, in rheumatoid arthritis or oncology, disease severity may influence treatment choice and also outcome. If severity is unmeasured, no amount of modeling of the recorded covariates fixes that.

The link between prognostic variables, effect modifiers, and confounders needs more care. The worked example uses a prognostic covariate that drives treatment selection, but the ITC problem usually turns on effect modification across study populations. A novice may wrongly infer that any baseline risk imbalance is automatically an ITC bias problem on every effect scale.

The notation `E_X[...]` appears in the identification result, but it may not be obvious that this means averaging over the marginal distribution of `X` in the target population, not over the treated group or control group. The worked example makes this clear later, but the theorem section should say it explicitly.

The term "observable functional of the data" is central but under-explained. A novice may need a sentence such as: this does not mean we know the answer in a finite sample, only that the answer is determined by the distribution of observable variables if the assumptions hold.

The difference between identification and estimation should be emphasized earlier. The chapter says identification is what could be computed with infinitely much data, but later references to G-computation, inverse-probability weighting, and doubly robust estimators may blur the line for a new reader.

The machine-checked tags and catalogue references are useful for the project, but they are visually noisy for a novice reader. If they remain in the chapter text, consider adding a sentence early in the book telling the reader they can skip these tags on first reading.

## Where a novice may get lost

A novice may get lost at the first formal definition because the chapter begins with intuitive patient language and then immediately switches to `Omega`, random variables, integrability, and functions of treatment labels.

The proof of the fundamental problem is short, but the final paragraph about no measurable functional recovering the individual or average effect may be too abstract. The reader may understand the two worlds but not the general conclusion.

The `Outcome swap under consistency` corollary is likely difficult. Conditional expectation locality is a subtle measure-theoretic idea, and the phrase "a.s. on `{P(T=t | X)>0}`" may feel remote from the health-research claim that observed treated outcomes represent treated potential outcomes only among people who actually received treatment.

The ignorability proof is the densest part of the chapter. Graphoid axioms, bounded measurable functions, truncation, and conditional dominated convergence are probably beyond what a novice health researcher can absorb while trying to learn causal identification.

The sentence about CATE not being confused with nonlinear conditional-versus-marginal distinctions may be too early. It tries to prevent a future misconception, but it may introduce non-collapsibility before the reader has enough context.

The final bridge to ITC is important but compressed. It names covariate overlap, transportability, ecological bias, effect scale, and non-collapsibility in one paragraph. A novice may need this unpacked into a slower explanation of how Chapter 9 becomes Bucher, MAIC, STC, and ML-NMR later.

The exercises move quickly from recomputation to proof construction. The mean-ignorability exercise and the symmetric selection-bias decomposition may be challenging for the stated novice audience unless earlier examples have shown how to construct simple joint laws and how to add and subtract counterfactual means.

## Suggested improvements

Add a small running health example before the Neyman-Rubin model. For example, define treatment `T=1` as a new anticoagulant, `T=0` as standard care, `Y` as 90-day stroke, and `X` as baseline risk. Use this same example to explain potential outcomes, SUTVA, ignorability, positivity, and standardization before generalizing.

Add a short "what to remember" paragraph after `Ignorability (strong, weak, mean)`. The practical message could be: randomized trials aim to make treatment independent of potential outcomes; observational analyses must condition on enough covariates to make treated and untreated patients comparable; the ATE proof only needs equality of conditional means.

Move some of the mathematical hierarchy proof detail into a remark or optional proof if the chapter is meant to be novice friendly on first reading. The result matters, but the proof currently interrupts the causal learning arc.

Strengthen the positivity explanation with a clinical example. For example: if no frail patients receive the active treatment, the data cannot tell us what active treatment would do in frail patients, so the population ATE cannot be recovered without extrapolation.

Clarify that `E_X` in the adjustment formula averages over the covariate distribution of the target population. This is the key bridge to population adjustment, and it should be made explicit before the worked example.

Add a second small ITC-oriented worked mini-example after the single-population example. It does not need full calculations. It could show two trials with different covariate mixes and explain why an effect identified in one population is not automatically the effect in another.

Break the final ITC bridge into two or three shorter paragraphs: one for within-study identification, one for transporting effects across populations, and one for why effect modifiers and overlap become central in later chapters.

Make the exercises more scaffolded. For `Mean ignorability is strictly weaker`, give a two-row template for conditional distributions. For `Positivity failure breaks identification`, first ask the reader to identify the empty cell in a table before asking for two compatible values of `mu_1(0)`.

## Highest-priority fixes

1. Add more plain-language bridges before the formal definitions of potential outcomes, SUTVA, ignorability, positivity, and identification.
2. Make the ITC motivation visible throughout the chapter, not only in the introduction and final bridge section.
3. Clarify target-population averaging in the adjustment formula, especially the meaning of `E_X`.
4. Reduce or quarantine the most technical proof details in the ignorability hierarchy so novice readers can retain the causal message.
5. Add one small clinical or ITC example showing positivity and overlap failure in concrete patient strata.
6. Unpack the final bridge section so the reader can see how single-population identification becomes the foundation for population-adjusted indirect comparisons.
