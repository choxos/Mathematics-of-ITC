# Chapter 23 Feedback: Multilevel Network Meta-Regression IV: Estimands, Identifiability, and Generality
## Overall reaction
This chapter has a strong mathematical spine and a genuinely useful central message: ML-NMR estimates treatment contrasts by fitting a conditional outcome surface and then integrating that surface over a chosen target population. For a novice health researcher, that idea is valuable because it connects the method directly to the decision question: "Which treatment effect, for which patients?"

The difficulty is that the chapter often reaches the formal result before the reader has a stable verbal model of the problem. A mathematically stronger reader will probably follow the chain from model surface to target-population estimand to identifiability to special cases. A motivated health researcher who is new to indirect treatment comparisons may understand the worked example, but may not yet understand why each theorem was needed, what data inputs are needed in practice, or how to tell whether an ML-NMR estimate answers their actual clinical or health technology assessment question.

The chapter is clearest when it speaks in plain terms, especially in the introduction, the "superpower and its price" remark, the "Why SEMA is doing the work" remark, and the binary worked example. It is least accessible when it moves into identifiability language, graph rank, manifolds, and Bayesian identifiability without first giving the reader a practical accounting of what is known, what is unknown, and what one aggregate trial can or cannot teach us.

## What was clear
The opening three questions are a helpful frame. "Which quantity, in which population?", "Is the quantity even identified?", and "How does ML-NMR relate to everything before it?" are exactly the right questions for this chapter. They tell the reader that the chapter is not mainly about fitting software, but about interpreting the answer that comes out of the fitted model.

The distinction between a fitted conditional surface and a single treatment contrast is well motivated. The statement that a fitted ML-NMR model is a surface over covariate space, while an indirect comparison is a single number, is one of the best pedagogical sentences in the chapter. That idea should be repeated later because it is the anchor for target populations, marginalization, and generality.

The target-population flexibility of ML-NMR is clear in broad terms. The chapter makes it clear that ML-NMR is not locked to the comparator population in the same way as MAIC or STC. The idea that one may choose the population of either trial, or a third decision-relevant population, is important and comes through.

The definition of marginal versus conditional contrasts is helpful because it names the order of operations: integrate then contrast, versus contrast then integrate. This is a good way to explain the difference to a novice. The text should lean even harder on this wording because it is more intuitive than the equations alone.

The worked target-population example is the strongest teaching device in the chapter. A binary effect modifier, logit link, two target populations, and calculator-checkable values make the abstract claims visible. The example demonstrates why the target covariate distribution changes the answer, why the conditional A-versus-B contrast is constant under SEMA, and why the marginal A-versus-B contrast still moves on a non-collapsible scale.

The comments around STC as a special case are also helpful. The statement that the ML-NMR aggregation integral is the marginal STC predicted mean is a clear conceptual bridge. The later explanation that STC fits the surface on IPD alone, while full ML-NMR lets AgD outcomes inform the fit, is a useful distinction for readers who know STC first.

## What was unclear
The chapter still needs a plainer answer to "What does ML-NMR actually estimate?" The formal answer is present, but a novice needs it stated before the theorem in ordinary language. For example: ML-NMR estimates the mean outcome each treatment would have in a named target population, then compares those target-population means on a specified scale. On the identity scale this can be a risk difference or mean difference. On the logit scale it is a marginal log odds ratio if the contrast is taken after averaging. This should be stated as a compact practical summary before `@def-mlnmr-target-contrast`.

The target baseline `mu_*` is under-explained. The chapter says a target baseline is needed on non-collapsible scales, but a health researcher will immediately ask where it comes from. Is it estimated from a trial arm, supplied by external epidemiology, inferred from the comparator, predicted from the model, or treated as a scenario input? If the target is a third decision population rather than one of the trials, this becomes especially unclear. The chapter should explain that the marginal odds ratio is not fully defined without a target absolute risk level, and should discuss practical sources and uncertainty for that input.

The notation `Delta_{ab}` is easy to misread. The definition says it is the contrast of treatment `b` versus treatment `a`, so `Delta_{BA}` means A versus B. This is mathematically consistent, but it is not intuitive for many readers because they may read the subscript left to right as B versus A. The example does label `Delta_{BA}` as A versus B, but the convention deserves a small warning or mini-table.

The phrase "population-free surface" may be too compressed for the intended novice. The conditional relative-effect part is population-free, but the absolute arm surface still needs a baseline. The lemma states this carefully, yet the title could make a novice think no population information is needed at all. A bridge sentence should say: the relative-effect formula can be transported across populations, but the absolute risks cannot be computed without a baseline risk in the target population.

SEMA is central but not sufficiently reintroduced in this chapter. The shared effect modifier assumption is cross-referenced, but a novice needs the clinical meaning restated. In the two-study triangle, SEMA means the covariate changes the A-versus-C effect by the same amount as it changes the B-versus-C effect. That is the reason the IPD trial can teach us the interaction needed for the AgD trial. Without that sentence, the identifiability proof feels like a symbol manipulation rather than a health research assumption.

The general outcome-scale message is not yet concrete enough. The theorem refers to a general link `g`, collapsible scales, logit, log-hazard, and identity, but the worked example is entirely logistic. A novice may leave thinking the chapter is mostly about odds ratios. It would help to add a short table comparing identity, log, logit, and possibly survival scales: what the arm mean is, what the marginal contrast means, whether target baseline is needed, and what information about the target population is required.

## Under-explained details
The chapter says the target density `f_*` can be described, but it does not explain what "described" means for a real evidence synthesis. Earlier chapters cover copula reconstruction, but Chapter 23 should remind the reader which target inputs are needed: covariate means, marginal distributions, correlations, and for non-collapsible scales a baseline risk or rate. A novice should not have to infer this from Chapter 22 references.

The distinction between effect modifiers and prognostic variables needs one more local reminder. The proof shows that the conditional contrast cancels the baseline and prognostic effects, while the marginal contrast on a non-collapsible scale can still depend on prognostic effects and baseline. This is a subtle point. A health researcher may wrongly think "prognostic variables do not modify relative effects, so they do not matter for the relative treatment effect." The chapter should explicitly say that this is false for marginal odds ratios because prognostic variables change the distribution of baseline risk before averaging.

The identifiability accounting needs a nontechnical version before the proofs. The key idea is simple: IPD can estimate slopes and interactions because individual covariates are observed; one AgD arm mean can identify only one scalar shift; therefore an AgD-only treatment cannot estimate a whole treatment-by-covariate interaction vector unless a structure such as SEMA, treatment classes, or a prior supplies the missing information. That explanation is present in pieces, but it should appear before `@thm-mlnmr-identifiability-2study` as a short ledger of unknowns and data constraints.

The no-SEMA proposition is mathematically useful but hard for the target reader. Terms such as "p-dimensional manifold", "implicit function theorem", and "generic target" may make a novice lose the practical message. The practical message is that many different B-treatment interaction patterns can reproduce the same aggregate B-arm mean, but they give different predictions when transported to another population. This should be stated before the formal result, perhaps with a two-row binary covariate table.

The exchangeable EM part of the large-network theorem is likely too fast. "Bayesian identifiability" and "proper posterior" are not the same kind of identifiability as the rank arguments in the earlier parts, and a novice may not see the difference. The chapter does say this is a genuine limitation, which is good, but it should define the practical interpretation: the data alone do not pin down AgD-only interactions, so the prior and partial pooling contribute real information to the estimate.

The sign convention in the worked example could be clearer. The event is unfavorable and larger logit contrasts mean worse outcomes relative to C. That sentence helps, but the example would be easier if it also translated one contrast into words, such as "A has higher odds of the bad event than C in this target population." This matters because treatment letters and contrast order are already cognitively demanding.

## Where a novice may get lost
A novice may get lost at the very beginning because the introduction refers to many prior results before giving a concrete study setup. The references to Chapters 20 to 22, aggregation bias, Sobol' sequences, Sklar's theorem, and Gaussian copula are accurate, but they create a lot of cognitive load. A small visual or verbal setup first would help: one IPD A-C trial, one AgD B-C trial, a target population, and a choice between reporting A versus B in the comparator population or in another population.

The model equation in `The fitted model and its population-free surface` contains many symbols at once: `mu_j`, `beta_1`, `gamma_k`, `beta_{2,k}`, `theta`, `eta`, `g`, `j`, `k`, and `x`. The prose defines them, but a novice reader may still need a local table with columns for parameter, plain-language meaning, whether it is study-specific or network-level, and why it matters for transport.

The jump from target-population estimands to identifiability is conceptually important but abrupt. The reader has just learned how to define an estimand in any population, then the chapter immediately asks whether the model coefficients are identified. A bridge paragraph should say that choosing any target population is only valid if the data have identified the surface being transported. Otherwise ML-NMR can write down a target contrast algebraically, but the data cannot determine it.

The two-study identifiability proof is hard because it asks the reader to track both clinical trial structure and algebraic parameter recovery. It would help to separate the story into three plain-language steps before the proof: IPD A-C estimates the shared effect modification pattern; AgD C estimates the B-C study baseline; AgD B estimates the B treatment effect; then A versus B can be transported to a target.

The larger-network theorem may be beyond the novice unless the chapter adds a diagram or a parameter-counting example before the theorem. Connectivity, incidence rank, treatment-class EM, and exchangeable EM are each understandable individually, but they arrive together. The exercise later asks for a three-study network count, which is a good idea, but a smaller version of that count should appear in the main text before the theorem.

The generality theorem is conceptually useful but dense. A novice may not see the practical difference between "exact special case", "estimand and limit", and "exact functional identity." These distinctions matter. A short comparison table would help: NMA removes covariates; IPD-NMR removes AgD integration; STC uses the same integral but fits only to IPD and fixes the target; MAIC targets the same comparator-population estimand under additional weighting conditions.

The exercises are mathematically appropriate but uneven for the stated novice. The first two exercises are accessible and reinforce the worked example. The monotonicity tilt exercise and the closed-form non-collapsibility gap are much harder. They are useful for a mathematically advanced reader, but the chapter should signal which exercises are for comprehension and which are proof-building challenges. The starred notation partly does this, but `exr-mlnmr-monotone-general` is also likely difficult even though it is not starred.

## Suggested improvements
Add a short clinical decision vignette before the formal setup. For example: Trial AC has IPD, trial BC has only aggregate outcomes and covariate summaries, and the decision maker wants A versus B in a reimbursement population that differs from both trials. Then state what ML-NMR will estimate in that target population and what inputs are needed.

Add a boxed plain-language summary after the model is recalled: ML-NMR fits a conditional outcome model, converts it to target arm means by averaging over a target covariate distribution, then forms a marginal or conditional contrast. This would give the reader a map before the theorem.

Add a small contrast notation table. It should show that `Delta_{CA}` means A versus C, `Delta_{CB}` means B versus C, and `Delta_{BA}` means A versus B. This would prevent a predictable source of confusion.

Add an "inputs required" table for target-population estimation. Suggested rows: conditional contrast on an identity-like collapsible scale, marginal contrast on identity scale, marginal odds ratio, marginal hazard ratio or survival contrast if applicable. Suggested columns: target covariate mean, full target covariate distribution, target baseline risk, fitted treatment-by-covariate interactions, and whether the baseline cancels.

Restate SEMA locally in clinical language. The chapter should say that SEMA is not merely a mathematical convenience. It is a claim that the same patient characteristic modifies the relative effects of the active treatments in the same way. Then explain that this is why IPD from the A-C trial can supply the interaction information needed for the B-C aggregate trial.

Move some of the intuition from the remarks into the main path. The remarks are often the most novice-friendly parts of the chapter, especially "The superpower and its price", "Why SEMA is doing the work", and "Where each hypothesis is spent." Consider promoting shorter versions of these points before the corresponding theorem statements.

Add a side-by-side STC comparison before the generality theorem. A novice needs to see that STC and ML-NMR share the standardization integral, but differ in fitting and targeting. One row could say: STC fits on IPD only and standardizes to the comparator. Another row could say: ML-NMR fits jointly to IPD and AgD outcomes and can standardize to any described target population.

Add one more general outcome-scale example. The current logit example is useful, but the chapter would benefit from a simple identity-link mini-example where marginal and conditional contrasts coincide, or a short log-link example where the target baseline issue differs from the odds-ratio case. This would make the general `g` notation feel less abstract.

## Highest-priority fixes
1. State earlier and more plainly what ML-NMR estimates: target arm means plus treatment contrasts in a named target population, with marginal and conditional versions depending on the order of averaging and contrasting.

2. Explain the practical role of the target baseline `mu_*`, especially for marginal odds ratios and other non-collapsible scales. The chapter should say where this input might come from and what happens if it is uncertain.

3. Clarify SEMA before the identifiability proof. The reader needs a clinical sentence, a parameter-counting sentence, and a two-study diagram or table before seeing the theorem.

4. Add a notation warning for `Delta_{ab}` so readers do not misread `Delta_{BA}` as B versus A.

5. Give novices a bridge into the generality theorem. The STC special case is important and should be presented as a practical comparison before the formal proof: same standardization integral, different data used to fit the surface, and more freedom in choosing the target population.
