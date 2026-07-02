# Appendix B Feedback: Matrix Calculus

## Overall reaction

Appendix B is rigorous, organized, and more trustworthy than a formula-only matrix calculus appendix. As a novice health researcher, I would appreciate that it fixes one convention for gradients and Jacobians, proves each identity, and shows how the compound-symmetry covariance example connects the formulas to restricted likelihoods. The appendix has a real pedagogical spine: define the derivative, introduce differentials, use trace algebra, then apply the identities to inverse, determinant, log determinant, Woodbury, and a covariance example.

The main problem is that the appendix still feels like a compact graduate mathematics reference rather than a learning bridge for someone who is weak in abstract mathematics. It often proves why a result is true before explaining how a health researcher should recognize when to use it in a likelihood, a delta-method variance calculation, or a population-adjusted indirect comparison. The reader who already understands first-order approximations, trace manipulation, and matrix shapes will do well. The reader who is learning those ideas for the first time will probably need more plain-language signposts, more shape checks, and more health or ITC motivation between the formal blocks.

The appendix is useful, but it does not yet fully meet the promise of taking a naive researcher toward mastery. It is strongest as a reference after the reader has already seen matrix calculus once. It is weaker as a first encounter with gradients, Jacobians, differentials, trace tricks, and log determinants.

## What was clear

The opening paragraph clearly states why matrix calculus matters in this book. It names normal equations, scores, Fisher information, restricted likelihoods, matching weights, and variance propagation. That is exactly the right framing for an ITC reader, because it tells me these formulas are not ornamental mathematics.

The convention section is one of the most helpful parts. Defining the gradient as a column vector and the Jacobian as an output-by-input matrix removes a common source of confusion. The sentence linking the least-squares gradient and the score function to this convention is especially useful.

The identification lemma for matrix derivatives gives a practical workflow: expand, keep the linear term in the perturbation, write it as `tr(G^T H)`, and read off the derivative. That is a clear central method. The short plain-language paragraph after the proof is more accessible than the proof itself and should be treated as a model for other sections.

The quadratic-form section is well motivated by least squares. The explanation after the theorem, where the least-squares objective is expanded and the normal equations follow, is a good example of how abstract identities can be anchored in a familiar statistical calculation.

The log-determinant section is useful and relevant. The remark about symmetric matrices and doubled off-diagonal entries is advanced, but it is valuable because covariance matrices are symmetric and this is a real source of layout errors.

The compound-symmetry worked example is the most novice-friendly applied part. It uses a concrete covariance matrix, derives an inverse, derives a determinant, checks the log-determinant derivative two ways, and verifies with numbers. That kind of redundancy helps a reader build trust.

The summary table is helpful as a lookup device. It makes the appendix usable later when a reader is working through Chapters 8, 13, 18, 19, 24, or 25 and needs to find an identity quickly.

## What was unclear

The appendix says it is deliberately self-contained, but for a novice it is not fully self-contained. It assumes comfort with open sets, norms, `O(.)`, `o(.)`, adjugates, cofactors, Cramer's rule, block determinants, Schur complements, and differentiability between finite-dimensional spaces. Those are legitimate prerequisites, but the text should be more honest about which earlier chapters the reader may need to revisit.

The notation departs from the main notation chapter in a way that may confuse novices. The notation chapter says matrices are usually bold uppercase, but Appendix B uses unbolded `A`, `X`, `U`, `V`, and `C` throughout. That is standard in abstract matrix algebra, but a novice health researcher may wonder whether `X` is a random variable, a design matrix, a generic matrix, or a covariate. A short note explaining that unbolded matrix letters are used locally for generic matrix variables would help.

The move from ordinary derivatives to differentials is too fast. The sentence "treat `dX := H` as a free increment" is efficient for a trained mathematical reader, but it will sound mysterious to someone learning the method. The appendix should say more directly that `dX` is a bookkeeping symbol for a small change in every entry of `X`, and that `dF` is the first-order change in `F` caused by that perturbation.

The trace trick is not yet accessible enough. The trace properties are proved, but the actual skill a novice needs is recognizing how to rearrange expressions until the perturbation appears in the canonical form `tr(G^T dX)`. For example, in the proof of the trace derivative, the step from `tr((dX)^T A X)` to a form involving `dX` is correct, but it is not slow enough for a weak math reader.

The Woodbury section is mathematically clear but pedagogically abrupt. I understand that it reduces a large inverse to a small inverse, but I do not yet know what `A`, `U`, `C`, and `V` would look like in a meta-analysis or mixed model. The current sentence about random-effects meta-analysis is helpful, but it is too compressed.

The compound-symmetry example uses `sigma^2` and `tau^2`, but it does not fully translate those into health-research language. A novice may need one or two sentences saying that `sigma^2` is within-study or residual variation in the balanced example, while `tau^2` is between-study heterogeneity, and that the all-ones matrix makes every study-level estimate share the same random-effect component.

## Under-explained details

Gradients and Jacobians need more shape commentary. The appendix defines their shapes, but later formulas would be easier to follow if they repeatedly checked dimensions. For example, after `nabla q(x) = (A + A^T)x`, the text could explicitly say that `(A + A^T)` is `n x n`, `x` is `n x 1`, and the gradient is `n x 1`. This may feel elementary, but it is exactly what novice readers need when they are trying not to transpose the score or Jacobian incorrectly.

The Hessian is introduced as the Jacobian of the gradient, but the reader is not given much intuition for why the Hessian matters in likelihoods. A sentence connecting it to curvature, standard errors, Fisher information, and Newton or Fisher scoring would make the definition more relevant.

The differential rules are under-explained as a method. The reader sees linearity, product rule, transpose rule, and trace rule, but not enough examples of how to combine them in a realistic calculation. A small boxed recipe would help: write the expression, apply product and inverse rules, discard terms involving two perturbations, move `dX` to the final position inside a trace, then read off the derivative.

Trace tricks need a warning that cyclic movement is not general commutation. The appendix proves `tr(AB) = tr(BA)`, but later calculations depend on cycling factors in longer products. A novice may incorrectly infer that factors can be rearranged freely. The text should explicitly say that `tr(ABC) = tr(BCA) = tr(CAB)`, but `tr(ABC)` is not generally equal to `tr(ACB)`.

The log-determinant material would be much easier to motivate if it first showed the multivariate normal log-likelihood term:

```text
-1/2 [log det V(theta) + r^T V(theta)^(-1) r]
```

Then the reader would immediately see why the two derivative identities in the remark are the core pieces of REML and meta-analysis likelihood scores.

The symmetric-gradient remark is important, but it may be too dense for the first pass. It would benefit from a tiny `2 x 2` example showing that changing the off-diagonal covariance parameter changes two matrix entries at once. Without that example, the doubled off-diagonal statement may feel like a technical trap rather than an understandable chain-rule consequence.

The determinant lemma proof is elegant, but the choice of the block matrix `P` appears out of nowhere. A novice reader needs a sentence like: "This block matrix is chosen because one Schur complement produces the small matrix `C^(-1) + V A^(-1) U`, while the other produces the large matrix `A + U C V`."

The summary table is useful but could be more usable if it had a "where used" column. A novice health researcher is likely to ask, "Which identity do I need for REML, for the delta method, for least squares, for MAIC weights, or for ML-NMR likelihoods?"

## Where a novice may get lost

A novice may get lost at the first use of little-o notation in the derivative definitions. The definitions are precise, but they assume the reader already understands first-order approximation. A short sentence saying "the `o(||h||)` term is smaller than linear in the perturbation, so it disappears when identifying the derivative" would reduce anxiety.

The transition from scalar functions of vectors to scalar functions of matrices is another likely stumbling point. The appendix says the matrix derivative has the same shape as the argument, but a novice may still wonder why a derivative with respect to a matrix is itself a matrix rather than a very large Jacobian. The Frobenius inner product explanation is correct, but it needs a more intuitive bridge.

The differential notation `dF`, `dX`, and `d(X^(-1))` may feel like a new algebraic object rather than a shorthand for the linear part of a perturbation. Readers who have only seen single-variable calculus may try to treat `dX` like a scalar differential and may not understand why matrix order matters.

The proof of the product rule may be too abstract because it relies on terms being `O(||H||^2)` and therefore `o(||H||)`. This is right, but a novice might not see why multiplying two first-order matrix changes produces a second-order term.

Jacobi's formula may be intimidating. Cofactors, adjugates, minors, and row expansion are all technical, and the appendix uses them quickly. Since most health researchers only need the log-determinant derivative, the text should tell readers they may accept Jacobi's formula on first reading and return to the proof later.

The Woodbury proof is a long algebraic verification. It is defensible as proof, but it will be hard for a novice to see the computational idea through the symbols. The reader needs an intuitive preview before the proof and a numerical or shape-based recap after it.

The compound-symmetry example is helpful but still abstract. A novice may not know why `1_n 1_n^T` is the right matrix for a common random effect, why its rank is one, or why reducing an `n x n` inverse to scalars matters computationally. Those points should be spelled out.

The final notes and references are useful, but they may make the appendix feel like reference material for mathematicians rather than a bridge for health researchers. The downstream uses are listed, but they come after all the difficult content. Some of those motivating links should appear earlier.

## Suggested improvements

Add a short "How to read this appendix" paragraph near the start. It could say that readers interested in least squares should focus on gradients and quadratic forms, readers interested in the delta method should focus on Jacobians and the chain rule, readers interested in REML and meta-analysis likelihoods should focus on inverse and log-determinant identities, and readers interested in efficient computation should focus on Woodbury and the determinant lemma.

Add a plain-language box after the differential definition. It should explain, without proof, that a differential is the linear part of the change in a function. A simple scalar analogy would help: if `f(x + h) = f(x) + f'(x)h + small error`, then the matrix version replaces `h` by `H` or `dX`.

Add dimension checks to the main identities. This could be done in short parenthetical comments rather than long explanations. For a novice, seeing that every multiplication is conformable is often the difference between understanding and copying.

Add a trace-manipulation mini example before the trace derivative theorem. For instance, show how to rewrite `tr(A dX B)` into canonical form. The goal should be to teach the reader how to move from a differential expression to the derivative, not only to prove individual identities.

Add a likelihood bridge before the log-determinant theorem or immediately after it. Use the multivariate normal or REML form with residual vector `r(theta)` and covariance `V(theta)`, then show that the score needs derivatives of both `log det V(theta)` and `r^T V(theta)^(-1) r`.

Add a tiny symmetric covariance example for the doubled off-diagonal issue. A `2 x 2` covariance matrix with parameter `rho` in both off-diagonal positions would make the chain-rule point concrete.

In the Woodbury section, avoid using `V` as the generic factor name if possible, because the book also uses `V` for covariance matrices and vector spaces. If the identity must be stated in standard notation, add a note that this `V` is only a local matrix factor and is not the covariance matrix `V` used later.

Add a small map from Woodbury symbols to the compound-symmetry example. For example, state explicitly that `A = sigma^2 I_n` is the easy diagonal part, `u v^T = tau^2 1_n 1_n^T` is the rank-one random-effect part, and the hard inverse becomes a scalar denominator.

Strengthen the health and ITC motivation in the compound-symmetry example. The example should say why a balanced one-way random-effects covariance appears in meta-analysis, what `tau^2` means as heterogeneity, and why the derivative with respect to `tau^2` is needed for estimating heterogeneity.

Revise the summary table to include a "used for" column. Examples: least-squares normal equations, delta-method variance, REML score, multivariate normal likelihood, random-effects meta-analysis, MAIC or STC variance propagation, and low-rank computation.

Consider marking some proofs as optional on first reading. This would not reduce rigor. It would help novice readers separate the formulas they must learn to use from the algebraic verification they can revisit once the applications make sense.

## Highest-priority fixes

1. Add more bridge text explaining differentials as first-order changes, with one scalar analogy and one matrix example before the formal differential rules.

2. Add an applied likelihood bridge showing exactly how `log det V(theta)` and `a^T V(theta)^(-1) a` arise in multivariate normal, REML, or random-effects meta-analysis likelihoods.

3. Expand the trace-trick pedagogy. Teach the canonical-form workflow explicitly, including a warning that cyclic trace movement is allowed but arbitrary reordering is not.

4. Make Woodbury less abstract by mapping `A`, `U`, `C`, and the local factor `V` to random-effects or compound-symmetry covariance structures, and consider reducing the notation collision with covariance `V`.

5. Make the compound-symmetry example more health-research-facing by defining `sigma^2`, `tau^2`, `n`, and `1_n 1_n^T` in terms of studies, residual variation, shared random effects, and between-study heterogeneity.

6. Add shape checks and "where used" cues to the main identities and summary table so a novice can use the appendix as a safe reference while reading the modeling and computation chapters.
