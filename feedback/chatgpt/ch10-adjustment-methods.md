# Chapter 10 Feedback: Adjustment Methods

## Overall reaction

This is a strong mathematically organized chapter, but from the perspective of a novice health researcher it often reads more like a proof chapter than a teaching chapter. The main conceptual arc is valuable: the chapter takes the identification result from Chapter 9 and turns it into propensity-score methods, inverse probability weighting, standardization, augmented inverse probability weighting, and efficiency. That is the right sequence for learning how adjustment methods sit underneath indirect treatment comparisons.

The main weakness is that the chapter often asks the reader to absorb abstract probability machinery before the health-research meaning has landed. A motivated reader can probably follow the opening motivation, the broad contrast between treatment-mechanism and outcome-surface modeling, and much of the worked example. But the balancing-score proof, the conditional-independence criterion, the sigma-algebra language, and the efficient influence function section are likely to feel like a sudden climb. The chapter bridges mathematical foundations to causal health-research concepts in intention, but not always in pacing. It needs more intuition, clinical framing, and concrete observed-data anchors before the proofs.

## What was clear

The opening distinction between modeling the treatment mechanism, $e(x)=P(T=1\mid X=x)$, and modeling the outcome surface, $m_t(x)=\mathbb{E}[Y\mid T=t,X=x]$, is very helpful. A novice can understand that one strategy reweights patients so treatment groups look comparable, while the other predicts outcomes under each treatment and averages. This is one of the clearest explanatory moves in the chapter.

The separate notation for $\mu_t(x)$ as the counterfactual mean and $m_t(x)$ as the observed outcome regression is also useful. Many beginners blur these together. The regression identity makes explicit that the equality between them is earned by assumptions rather than assumed by notation.

The proof of Horvitz-Thompson identification is unusually readable because it is broken into named steps: consistency, tower and pull-out, ignorability factorizes, and cancel and average. That structure helps a reader see what each assumption does. The later remark comparing IPW and standardization is also clear: IPW avoids extrapolation but can have high variance, while standardization can be biased if the model extrapolates poorly.

The worked example is the strongest novice-facing part of the chapter. The two-stratum setup, the naive contrast, the IPW cancellation, the g-computation calculation, the double-robustness scenarios, and the efficiency-bound calculation all give the reader numbers to hold onto. The explanation that the treated arm is overweighted toward the high-outcome stratum is exactly the kind of causal-health interpretation the chapter needs more often.

## What was unclear

The definition of a balancing score is mathematically compact but pedagogically thin. The sentence about level sets and conditional laws may be correct, but a novice health researcher may not know what it means for the conditional law of $X$ to be the same for treated and control units. This needs a plain-language translation, for example: within each value of the score, treated and control patients have the same distribution of measured baseline characteristics.

The statement that the propensity score is the "coarsest" balancing score may confuse readers. In ordinary language, "coarsest" sounds like it uses the least information, but the theorem then uses sigma-algebra refinement language that reverses the intuitive direction for many readers. A short example with two covariates collapsed into a single probability would make this less abstract.

The two measure-theoretic lemmas before the propensity-score theorem are likely to stop many novice readers. The conditional-independence criterion with $\sigma(W)\vee\mathcal{G}$ and the factorization lemma are not given enough motivation before they appear. A reader who wants to understand causal adjustment may feel that the chapter has moved from health research into graduate probability without warning.

The sentence saying "There are exactly two surfaces one can model" is memorable but a little too categorical for a novice. Matching, stratification, doubly robust methods, targeted learning, and machine-learning nuisance estimation will look like more than two methods to many health researchers. The intended point is probably that all these methods ultimately model or estimate the treatment mechanism, the outcome surface, or both. That should be stated more carefully.

The line connecting ML-NMR to a "combined, doubly robust estimator" is not yet explained enough. A reader new to ITCs may not know what it means for ML-NMR to play that role, especially because double robustness in this chapter is defined for AIPW under individual-level causal inference. The book may justify this later, but here the connection needs to be framed as a preview rather than as something already established.

## Under-explained details

The chapter needs more practical explanation of what is being estimated from observed data. It gives sample analogues for IPW and g-computation, but it does not show what a small observed dataset would look like, how a fitted logistic propensity model produces $\hat e(X_i)$, or how an outcome regression produces $\hat m_1(X_i)$ and $\hat m_0(X_i)$. A novice health researcher would benefit from seeing one table of patients with $X$, $T$, $Y$, $\hat e(X)$, weights, and predicted outcomes.

Strict positivity and practical overlap need more separation. The chapter defines strict positivity as a mathematical condition and later discusses poor overlap through variance, but a health researcher also needs the operational interpretation: if some patients in the target population almost never receive treatment A or B, the comparison depends on unstable weights or extrapolation. The connection to trial eligibility, prescribing practice, and sparse patient subgroups should be made explicit.

Stabilized weights, normalized weights, and Hájek estimators are introduced quickly. The chapter says the estimand is unchanged and finite-sample variance improves, but it does not slow down enough to explain why analysts often prefer the normalized form, what the denominator is doing in a real dataset, and how this relates to weight diagnostics typically reported in applied studies.

The ATE, treatment effect in the treated, and target population distinctions need more novice scaffolding. The matching remark notes that one-to-one propensity matching targets the treatment effect on the treated, but this is a major conceptual issue for ITCs and population adjustment. A novice may not yet appreciate that changing the covariate distribution being averaged over changes the estimand.

The efficient influence function section is mathematically careful but under-explained from a health-research point of view. The chapter says the efficient influence function gives the smallest achievable asymptotic variance, but it does not explain enough why an applied reader should care, how this affects confidence intervals, why AIPW is attractive in practice, or when the efficiency claim is less relevant than model misspecification and poor overlap.

## Where a novice may get lost

A novice is likely to get lost immediately after the balancing-score definition, when the chapter shifts into conditional-independence criteria using sub-sigma-algebras. The reader has just learned that propensity scores balance covariates, but before seeing a simple applied example, they are asked to follow abstract conditional-expectation machinery. That is a difficult transition.

The Rosenbaum-Rubin theorem proof is another likely stumbling point. The core idea is simple and important: among patients with the same propensity score, treatment assignment is as good as random with respect to measured covariates. But the proof emphasizes $\sigma(e(X))$, $\sigma(b(X))$, and measurable functions of $b(X)$. The reader may understand the algebraic steps without understanding the causal intuition.

The proof of propensity-score sufficiency may also be hard to connect to applied adjustment. It shows that ignorability given $X$ transfers to ignorability given $b(X)$, but the health-research implication should be highlighted before and after the proof: if all confounding is captured by measured covariates, then balancing the propensity score is enough to remove measured confounding.

AIPW is introduced with a pointwise cancellation identity involving the unobserved $Y(1)$. This is elegant, but a beginner may wonder why an estimator that uses unobserved potential outcomes in its proof can be computed from observed data. A bridge sentence should explicitly say that $Y(1)$ appears only in the algebraic proof of bias cancellation, while the actual estimator uses only $X$, $T$, $Y$, $\hat e$, and $\hat m_1$.

The efficient influence function and variance-bound section may be too compressed for the stated novice reader. Terms such as asymptotically linear, regular estimator, tangent space, Donsker condition, and sample splitting appear with limited interpretation. Even if the theorem is needed for rigor, the reader needs a labeled "advanced" framing and a plain-language summary of what to retain before moving on.

## Suggested improvements

Add a small clinical or health-technology-assessment motivating example at the start and reuse it throughout. For example, compare two diabetes drugs or oncology treatments where age and baseline severity influence both treatment choice and outcome. Use that example to explain why the naive contrast is biased, why a propensity score summarizes treatment selection, why poor overlap is dangerous, and why ITCs care about the population being averaged over.

Before the balancing-score proof, add an intuitive subsection explaining balance with a small table or histogram: before weighting, treated patients are older and sicker; after conditioning on or weighting by the propensity score, age and severity distributions align. This would help the theorem feel like a formal version of a familiar applied diagnostic.

Move the two measure-theoretic conditional-independence lemmas into a clearly marked technical interlude, or add a short reader guide before them. The guide could say: the next two lemmas are proof tools, not new causal ideas; the causal idea is that a binary treatment is fully described by its conditional probability of treatment.

Add a recipe box for each estimator. For IPW, list: estimate $\hat e(X_i)$, compute treated and control weights, check overlap and effective sample size, compute the weighted mean contrast. For g-computation, list: fit outcome models, predict each patient's outcome under each treatment, average predictions over the target covariate distribution. For AIPW, list: fit both models, combine weighted residuals with predictions, interpret double robustness carefully.

Expand the bridge to indirect treatment comparisons. The introduction mentions MAIC, STC, and ML-NMR, but a novice would benefit from a more concrete explanation: in ITCs, the target covariate distribution may come from another trial or a decision population, so adjustment methods are not just for confounding inside one observational study. They are also tools for transporting or standardizing treatment effects across populations.

Make the worked example even more useful by adding an observed-data version. The current population-level example is excellent for identities, but an applied reader also needs to see what happens with finite data: estimated propensities, actual weights, normalized weights, predicted outcomes, and a simple effective-sample-size calculation.

Revise the exercises for accessibility. Several exercises are proof-heavy and depend on advanced material. Add at least two lower-barrier applied exercises: one where the reader calculates IPW and g-computation from a small table, and one where the reader interprets poor overlap and target-population choice in words. Label exercises by difficulty so novices know which ones are conceptual foundations and which are advanced proof practice.

## Highest-priority fixes

1. Add more plain-language intuition before the balancing-score and Rosenbaum-Rubin material. This is the conceptual hinge of the chapter, and currently it becomes abstract too quickly.

2. Add a concrete observed-data example with patient rows, estimated propensity scores, weights, predictions, and an effective-sample-size calculation.

3. Clarify the practical meaning of positivity, overlap, and extrapolation in health-research terms, especially for subgroups and target populations.

4. Strengthen the connection to ITCs by explaining how IPW, standardization, and AIPW become the logic behind MAIC, STC, and later population-adjusted comparisons.

5. Reframe the efficient influence function section as advanced material with a clearer applied takeaway: what it says about variance, confidence intervals, and why AIPW is attractive when both nuisance models are well estimated.

6. Add estimator recipe boxes and difficulty labels for exercises so a novice can separate "what I need to use the method" from "what I need to prove the theorem."
