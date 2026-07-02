# Chapter 14 Feedback: Indirect Comparison and Bucher's Theorem

## Overall reaction

This is a strong chapter mathematically, and it gives Bucher's method more structure than a usual applied explanation. As a novice health researcher, I found the opening clinical problem, the common comparator story, and the worked log odds-ratio example helpful. The chapter makes clear that the formula is simple but the assumptions are not.

The main problem is cognitive load. The chapter begins with a very accessible health technology assessment scenario, but it quickly moves into link-scale positions, population-specific contrasts, proof labels, and sign conventions. A reader who is smart but weak in abstract mathematics may understand that "common comparator C cancels" in words, yet still lose track of what $d_{AC}$ means, which treatment is in the numerator, and when a quantity belongs to study $AC$, study $BC$, or a hypothetical target population.

The chapter would be much more usable for a beginning ITC reader if it added more bridge text before the formal definitions, more orientation checks around signs, and more concrete clinical examples of transitivity failure. The current proofs are clear once the notation is accepted, but the reader may not have accepted the notation yet.

## What was clear

- The Introduction gives a good clinical reason for indirect comparison: a decision maker needs $A$ versus $B$, but only $A$ versus $C$ and $B$ versus $C$ trials exist.

- The explanation that Bucher's estimator is simple arithmetic only when the algebra is licensed is effective. That sentence prepares the reader to care about assumptions instead of treating the formula as a trick.

- The "Where each hypothesis is spent" remark after Bucher's theorem is one of the clearest parts of the chapter. It separates trial unbiasedness, transitivity, and pure algebra in a way a novice can follow.

- The section "The common comparator cancels baseline differences" is conceptually useful. It explains that anchoring removes study-specific baselines and then removes the comparator effect. That two-level cancellation is probably the most important intuition in the chapter.

- The worked example from two-by-two tables is valuable because it starts from raw counts, computes log odds, computes direct contrasts, adds variances, and back-transforms to an odds ratio. This is exactly the kind of example a health researcher needs.

- The "price of indirectness" discussion is clear. The idea that the indirect standard error is larger because it accumulates uncertainty from both direct comparisons is intuitive and clinically important.

- The paragraph in "When transitivity fails" that distinguishes prognostic variables from effect modifiers is helpful. The claim that prognostic variables shift baselines, while effect modifiers change relative effects, is the right conceptual distinction for the reader.

## What was unclear

- The sign convention is likely to confuse applied readers. The chapter says $d_{ab}=\eta_b-\eta_a$, so $d_{AC}=\eta_C-\eta_A$, but applied language usually hears "A versus C" as $\eta_A-\eta_C$. The note on index order is useful, but it arrives after the reader has already seen the Introduction describe $A$ relative to $C$. A novice may not know whether a positive $\hat d_{AB}$ favors $A$ or $B$.

- The target contrast is not always clinically transparent. In the worked example, the final odds ratio is described as "comparing $B$ to $A$" because $d_{AB}=\eta_B-\eta_A$. A reader expecting an "A versus B" comparison may think the chapter changed direction. This needs a repeated orientation sentence every time the result is interpreted.

- Transitivity is defined rigorously, but it may feel too abstract. The definition says all three relative effects take the same value in all three populations. A health researcher needs an immediate translation: the trial populations must be sufficiently similar with respect to effect modifiers for the relevant relative effects, not necessarily similar in baseline risk.

- "Constancy of relative effects" and "transitivity" are introduced close together, and the difference between them may be hard to retain. It would help to state in plain language that constancy is the general network assumption, while transitivity is the triangle version needed for this Bucher comparison.

- The phrase "marginal link-scale position" is mathematically precise but not intuitive. A novice may not see why the chapter first creates $\eta_{k(\mathcal P)}$ and only then defines a treatment effect. A short explanation like "think of $\eta_k$ as the arm's adjusted location on the log-odds scale before subtracting two arms" would help.

- The unanchored comparison section uses the reversed orientation $\hat\eta_A-\hat\eta_B$ while the main Bucher target uses $d_{AB}=\eta_B-\eta_A$. The text notes this, but the bias formula may still be difficult to follow because the reader must track both anchoring and sign reversal at once.

- The covariance discussion in the variance section may surprise readers. The statement that positive covariance from a shared comparator arm reduces the Bucher variance is correct, but it needs a more intuitive sentence. For example, the shared comparator error is partly subtracted away rather than counted twice.

## Under-explained details

- The chapter should define "population" in a more applied way before using $\mathcal P_{AB}$, $\mathcal P_{AC}$, and $\mathcal P_{BC}$. A novice may wonder whether a population means the enrolled sample, the eligibility criteria, the real-world target population, or a mathematical distribution over baseline covariates.

- The hypothetical direct $A$-versus-$B$ population $\mathcal P_{AB}$ deserves more motivation. It is central to the target estimand, but the chapter moves quickly from the real trials to this hypothetical population.

- The randomized trial proposition uses language about unbiasedness, consistency, and first-order delta-method unbiasedness. For log odds ratios, a novice may not know that exact finite-sample unbiasedness is not really being claimed. The chapter should explicitly say that the trial estimates are treated as approximately unbiased on the large-sample scale used for Bucher calculations.

- The marginal versus conditional distinction is important but dense. The warning that nonlinear links do not commute with averaging is useful, but a small numerical example would make it much easier to understand before non-collapsibility is invoked.

- The role of the link scale needs one more practical bridge. The chapter says odds ratios multiply and log odds ratios add, but it should also state the applied rule: do Bucher subtraction on log OR, log RR, log HR, or mean difference scales, then back-transform if needed.

- The baseline decomposition $\eta_{k(\mathcal P_j)}=\mu_j+\alpha_k$ is very helpful, but it is introduced as a remark rather than slowly unpacked. A novice may need a sentence saying $\mu_j$ is "how risky the study population is under the reference treatment" and $\alpha_k$ is "how much treatment $k$ shifts that risk on the chosen link scale."

- The unanchored bias result would benefit from a small numerical example before or after the proposition. Seeing two studies with the same treatment effects but different baseline risks would make the bias concrete.

- The worked example assumes the reader is comfortable moving from counts to log odds, log odds ratios, standard errors, Wald intervals, and exponentiation. It is good, but it could use a small boxed recipe for the steps so the reader can reproduce Bucher from a paper that reports only log ORs and standard errors.

## Where a novice may get lost

- In "The relative effect and its scale," the nested expression $g(\int \mu_k(x)f_{\mathcal P}(x)\,dx)$ is a lot to absorb before the reader has seen a simple Bucher calculation. This section may feel like a detour unless the chapter first explains that the purpose is to put each arm on a common additive scale.

- In "The algebra of contrasts," the identity $d_{ac}=d_{ab}+d_{bc}$ is mathematically simple, but the treatment order is not intuitive. Because $d_{ab}$ means $b$ versus $a$, readers may misread the triangle identity unless there is a diagram or sign table.

- In "Constancy of relative effects and transitivity," the proof of the converse in @prp-transitivity-consistency may feel less relevant to a beginning applied reader than the forward direction. The reader may wonder why the chapter is proving a converse before they fully understand the assumption.

- In "Bucher's theorem: unbiasedness," the exact identity and the stochastic theorem are close together. A novice may read them as repeating the same idea. It would help to say explicitly: first we prove the arithmetic target if there were no sampling error, then we add sampling error and expectations.

- In "The Bucher variance," the formula is clear, but the clinical implication may need to come earlier: the standard error grows because the indirect estimate depends on two uncertain estimates. The algebra proof can follow after that intuition.

- In "The variance of an empirical log-odds," the proof may be too much before the example. A novice who just wants to know why the inverse cell counts appear may get lost in the delta method. Consider presenting the applied formula first, then keeping the proof as a justification.

- In "When transitivity fails," the mechanism is important but still abstract. The age example is helpful, but the chapter should show a tiny table where the prevalence of an effect modifier differs between trials and therefore changes a marginal treatment effect.

- The exercises are useful but several are demanding for the intended novice. The scale-additivity exercise and the longer-chain exercise require proof confidence. It would help to add at least one very guided exercise that only asks the reader to identify the anchor, choose the right sign, compute the Bucher estimate, and state transitivity in plain language.

## Suggested improvements

- Add a small orientation box near the start with three rows: applied phrase, chapter notation, and interpretation. For example, "A versus C as usually reported" equals $\eta_A-\eta_C=-d_{AC}$, while $d_{AC}$ in this chapter equals $\eta_C-\eta_A$.

- Add a triangle diagram or text diagram before @lem-relative-effect-algebra. The diagram should show $A$, $B$, and $C$, the direction of each $d_{ab}$, and the formula $d_{AB}=d_{AC}-d_{BC}$.

- Add a plain-language transitivity box: "What must be similar?" effect modifiers of the relative treatment effects. "What may differ?" baseline risk and purely prognostic factors, because anchoring cancels them. "What cannot be fixed by a smaller standard error?" bias from effect modification imbalance.

- Add a concrete clinical transitivity example before the formal definition. For instance, if age modifies the effect of $B$ versus $C$ and the $BC$ trial is younger than the $AC$ trial, then $\hat d_{BC}$ may not be transportable to the target comparison. If age only predicts outcome but does not modify treatment effect, anchoring handles the baseline difference.

- Add a short table contrasting anchored and unanchored comparisons. Columns could include what is compared, what cancels, what assumption remains, and typical risk of bias.

- In the worked example, add a final interpretation sentence in both orientations: "On this chapter's $d_{AB}$ scale, the event odds for $B$ are estimated as 1.33 times those for $A$. Equivalently, the event odds for $A$ are estimated as 0.75 times those for $B$." This would prevent sign confusion.

- Add a practical note on extracting Bucher inputs from published trials: use log OR, log RR, or log HR estimates; convert confidence intervals to standard errors if needed; subtract on the log scale; add variances if independent; exponentiate the estimate and interval.

- Add a beginner exercise before the proof-heavy exercises. It should ask the reader to identify the common comparator, state the target contrast, compute $\hat d_{AB}$ from two reported log effects, and explain in one sentence what transitivity assumes.

## Highest-priority fixes

1. Fix the sign-orientation burden. The chapter should repeatedly clarify whether the result is $A$ versus $B$ or $B$ versus $A$, especially in the Introduction, @def-anchored-comparison, and the worked example.

2. Add more intuition for transitivity before the formal definition. A novice needs to understand effect modifiers, target population, and transportability in applied terms before seeing equality across $\mathcal P_{AB}$, $\mathcal P_{AC}$, and $\mathcal P_{BC}$.

3. Strengthen the anchoring explanation with a small numerical baseline-risk example. The current algebra is good, but a novice will remember the idea better if they see unanchored bias appear from different study baselines.

4. Clarify that trial log-effect estimates are approximately unbiased or consistent in the large-sample sense used for Bucher calculations, not exactly unbiased in every finite sample.

5. Make the worked example more explicitly reader-facing. Add an orientation check, a short recipe, and a final clinical interpretation that says what the odds ratio means and what assumption it depends on.
