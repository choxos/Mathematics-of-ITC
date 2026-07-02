# Appendix F Feedback: Solutions to Selected Exercises

## Overall reaction

Appendix F is no longer a stub. It now has a substantial chapter-by-chapter solutions appendix, with solutions to the starred exercises from Chapters 1-30. That is a major improvement, and the basic promise of the appendix is now clear: it is not an answer key of final results, but mostly full worked derivations.

As a novice health researcher trying to learn the mathematics behind ITCs, I would find this appendix useful, but still intimidating. The solutions are mathematically polished and often complete, but they sometimes begin at the level of someone who already knows which theorem to use. When I am stuck on an exercise, I need help choosing the first move before I can appreciate the proof.

The biggest remaining need is not more algebra. The appendix needs more teaching scaffolding around the algebra: strategy notes, prerequisite labels, common mistakes, and final applied interpretations. Those would make the solutions feel like a learning companion rather than only a record of correct proofs.

## What was clear

The selection rule is clear now. The opening says Appendix F gives solutions to starred exercises, and the appendix is organized by chapter in book order. This matches the chapter exercise sections, where starred exercises are flagged as having full worked solutions.

The coverage is broad. I found two solution headings for every numbered chapter from Chapter 1 through Chapter 30. That makes the appendix feel complete for the current book structure.

The solution labels are useful. Headings such as `Solution to @exr-maic-bias-decomp` and `Solution to @exr-qba-itc-evalue-star` make the source exercise traceable, especially once Quarto resolves the cross-references.

Many solutions are genuinely worked out. They show intermediate algebra, not just final answers. Good examples include the Gram matrix rank proof, the sandwich variance derivation, stabilized weights, Bucher correlated contrasts, ML-NMR aggregation, PSIS tail thresholds, quantitative bias analysis, simulation power, and the Coq faithfulness discussion.

The later ITC-focused solutions often end with the right applied lesson. For example, the RMST and non-collapsibility solutions usually connect the calculation back to transportability, target populations, or scale choice. That is exactly what a beginner needs.

## What was still unclear

The appendix does not yet tell me how to use it. Should I read the solution only after a full attempt, read it as a companion while working, or use it as a review chapter? A short "How to use these solutions" paragraph would help.

The level of detail varies. Some solutions carefully explain the whole chain of reasoning, while others move quickly through advanced tools such as Rayleigh quotients, Stein's lemma, REML likelihood algebra, generalized Pareto tails, Gaussian copulas, and Coq proof tiers. The harder solutions need one extra orientation sentence before the technical work begins.

The exercise headings use slugs, but not plain exercise titles. In the rendered book the cross-reference may help, but as a learner I would still appreciate headings like `Solution to @exr-stc-delta: Delta-method variance of marginal STC`. The plain title would reduce lookup friction.

It is not always clear which prior result I am supposed to know. The solutions cite theorem and equation slugs, but a novice may not remember what those slugs mean. A "Uses:" line in plain language would be easier than only seeing `@thm-rmst-collapsible` or `@lem-mlnmr-aggregate-monotone`.

The appendix does not distinguish between essential solution steps and advanced proof detail. Some proof-heavy sections are important for rigor, but a health researcher may only need the practical lesson on first reading. Marking optional advanced details would lower the intimidation factor.

## Potential correctness issues

These are higher priority than style because they may confuse readers who are checking their own work against the appendix.

In `@exr-graphoid-counterexample`, the proposed counterexample does not appear to show the claimed failure. If `X=Y=Z`, then after conditioning on `Z`, both `X` and `Y` are constants, so they are conditionally independent. Also, if `W` is degenerate, conditioning on `(Z,W)` is effectively the same as conditioning on `Z`. The conclusion therefore looks like it should hold, not fail. This example needs to be replaced or reworked with a genuinely non-positive support pattern.

In `@exr-glm-noncollapse`, the text says `a/(1+a)` is strictly convex. That function is actually concave for positive `a`. The proof mainly uses monotonicity and a covariance argument, so this sentence should be deleted or reworded.

In `@exr-james-stein-sure`, the positive-part James-Stein paragraph overstates the result by saying the estimator has weakly smaller loss pointwise. Positive-part James-Stein is a risk-dominance result, not a guarantee of smaller realized loss for every fixed sample outcome and every parameter value. This should be stated as risk dominance, with the pointwise claim removed.

In `@exr-qba-norta-margins-star`, part (b) is internally confusing. The solution first says the bivariate Bernoulli cell probability is a strictly increasing function of the latent Gaussian correlation, which means distinct latent correlations give distinct bivariate Bernoulli laws in the nondegenerate case. It then talks as if different latent correlations can map to the same law. The intended point may be Sklar non-uniqueness for discrete margins, but that is different from non-uniqueness of the Gaussian copula parameter.

In the same NORTA solution, part (c) starts with `rho^N = 1`, where identical lognormal margins give `X_1 = X_2` and therefore Pearson correlation `1`. The solution then switches to `rho^N = 0.5` to show strict inequality. Either the exercise prompt should use a non-unit latent correlation, or the solution should match the stated case.

## Under-explained details

Several solutions need a short "strategy" sentence before the derivation. For example: "To prove this rank identity, compare null spaces"; "To handle the odds ratio, write the marginal odds as a weighted average"; or "To solve the NORTA exercise, separate marginal recovery from dependence." That would teach the problem-solving move, not just the proof.

The early math chapters should more often explain why the result matters later. The algebra is correct, but a beginner may not see why dimension formulas, oblique projections, eigenvalue inequalities, or covariance construction matter for regression, weighting, and ITC bias. One sentence after each early solution could connect the result to later modeling work.

Some numerical solutions would benefit from small tables. The calculations are reproducible, but a beginner would have an easier time checking inputs, intermediate values, and final contrasts if they were laid out in a compact table.

The appendix should add common-mistake callouts for topics that are easy to confuse: positivity versus zero-probability conditioning, non-collapsibility versus effect modification, collapsibility versus transportability, naive MAIC variance versus sandwich variance, and latent Gaussian correlation versus observed covariate correlation.

The Coq solutions are clearer than expected, but they assume the reader already understands what proof tiers and named premises mean. A tiny glossary reminder inside the first Coq solution would help readers who jump directly to Appendix F.

## Where a novice may get lost

A novice may get lost at the first line of several solutions because the first move is not motivated. If I do not know why the min-max principle, Taylor expansion, sandwich estimating equation, or Gaussian copula construction is the right tool, the rest of the derivation becomes hard to follow even when each step is valid.

The notation load is high. Many solutions reuse symbols from the chapter without reintroducing them. This is efficient for experts, but not for someone using the appendix because they are already confused.

The transition from mathematical result to ITC meaning is sometimes too fast. The best solutions say what the result means for target population choice, effect-modifier imbalance, uncertainty, or bias. That style should be made consistent across all applied chapters.

The proof-heavy early chapters can feel disconnected from the health research goal. A short final sentence like "This is why collinearity breaks a regression adjustment" or "This is why a distance summary can miss nonlinear effect modification" would keep the learner oriented.

Some advanced derivations are complete but compressed. The REML, James-Stein, ML-NMR approximation, QMC, NORTA, and Coq sections may need extra signposting for readers who are not mathematically fluent.

## Suggested improvements

Add a short opening note with a recommended workflow: try the exercise first, read the strategy if stuck, then compare the full solution.

Add a one-line `Strategy:` before difficult solutions. This should say the main trick or theorem before the algebra starts.

Add a one-line `Uses:` note for each solution, using plain labels rather than only theorem slugs. Example: `Uses: Jensen's inequality, odds-ratio non-collapsibility, and target-population averaging.`

Include plain exercise titles in solution headings, not only slugs. This would make the appendix easier to browse.

For multi-step numerical solutions, add compact tables of inputs, intermediate quantities, and final interpretation.

Add common-mistake notes for the high-risk conceptual distinctions that recur throughout the book.

Mark optional proof-heavy sections as advanced detail when the applied lesson can be understood without every derivation.

Make the final interpretation sentence consistent across ITC chapters. Each applied solution should answer: "What does this calculation tell me about an indirect comparison?"

## Highest-priority fixes

1. Replace the opening with a stronger reader guide, not just the selection policy.

2. Check and repair the specific correctness issues in `@exr-graphoid-counterexample`, `@exr-glm-noncollapse`, `@exr-james-stein-sure`, and `@exr-qba-norta-margins-star`.

3. Add `Strategy:` and `Uses:` lines to the hardest solutions.

4. Add plain exercise titles beside the exercise slugs.

5. Add common-mistake callouts for positivity, non-collapsibility, transportability, MAIC variance, and latent versus observed correlation.

6. Add more applied closing sentences to the early mathematical solutions so the reader sees how the proof supports later ITC methods.
