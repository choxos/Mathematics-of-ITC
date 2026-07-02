# Chapter 2 Feedback: Linear Algebra II

## Overall reaction

This is a strong, rigorous chapter, and I can see why it belongs before regression and indirect treatment comparisons. The opening motivation is especially helpful because it tells me that projection is not an abstract detour: it is the geometry behind least squares, residuals, fitted values, and later methods such as STC, ML-NMR, and MAIC.

From the perspective of a motivated health researcher with weak abstract mathematics, the chapter is also intimidating. It quickly becomes a long sequence of definitions, lemmas, proofs, and matrix facts. The logic is mostly careful, but the reader support is uneven. I often understood that a statement had been proved before I understood why I should care, how to picture it, or how it would reappear in a health research problem.

The biggest comprehension issue is not proof correctness. It is that the chapter sometimes assumes the reader can translate formal statements into applied meaning. A novice reader needs more short bridge paragraphs that say, in plain language, "Here is what this theorem means for data, models, fitted values, residuals, and later ITCs."

## What was clear

The first section gives a clear reason for studying orthogonality. The paragraph connecting STC, ML-NMR, MAIC, least squares, model column spaces, and orthogonal residuals is one of the most useful parts of the chapter for the intended reader.

The definitions of inner product, norm, orthogonality, orthonormal sets, and orthogonal complement are stated cleanly. Even when the proofs are demanding, the objects themselves are introduced in a disciplined way.

The projection theorem is clearly identified as the centerpiece. The chapter repeatedly signals that this theorem is the foundation for normal equations, the hat matrix, and ordinary least squares. That helps the reader keep track of the destination.

The worked example is valuable because it carries one design matrix and one outcome vector through Gram-Schmidt, QR, normal equations, fitted values, residuals, RSS, TSS, and the hat matrix. That continuity is much better than using disconnected examples.

The remark after the normal equations is very helpful. It explains that Chapter 6 adds the statistical layer later, while this chapter is only about geometry in $\mathbb{R}^n$. That separation would help many applied readers.

## What was unclear

The weighted inner product and Mahalanobis distance remark appears before a novice reader has enough grounding in positive definite matrices, inverse covariance matrices, or why covariance creates a geometry. The connection to MAIC and distance matching is promising, but too compressed.

The proof of Cauchy-Schwarz uses the quadratic in $t$ and the minimizer $t^\star$ quickly. A reader who has not recently studied quadratic minimization may not see why this particular $t$ is chosen or why the equality case means linear dependence.

The phrase "orthonormality makes coordinates trivial to read off" is mathematically true, but it needs translation. A health researcher may not immediately see that $\langle \mathbf{m}, \mathbf{q}_i\rangle$ is a coordinate because the basis vectors have been normalized and made perpendicular.

The notation $V=\mathcal{M}\oplus\mathcal{M}^\perp$ is introduced after the decomposition theorem, but the applied meaning of a direct sum is not spelled out. The reader may need a sentence saying that every vector splits into one explainable part and one leftover part, with no overlap between them.

The projection theorem proof uses several similar symbols, especially $\mathbf{m}$, $\mathbf{m}_0$, $\mathbf{m}^\star$, and $\mathbf{w}$. The proof is logically organized, but a novice can lose track of which object is the candidate fit, which is any possible fit, and which is the residual.

The distinction between the fitted vector $\mathbf{A}\hat{\mathbf{x}}$ and the coefficient vector $\hat{\mathbf{x}}$ needs more emphasis. The theorem says the fitted vector is always unique, while coefficients may not be unique unless $\mathbf{A}$ has full column rank. That is an important applied point, but it is easy to miss.

The projection matrix section uses the same symbol $P_{\mathcal{M}}$ for the map and the matrix. This is standard, but for a new reader it may feel like a new object has silently appeared.

The QR section is clear at a formal level, but the uniqueness proof and the conditioning statement are probably above the immediate needs of a novice health researcher. The main applied message, "software solves least squares this way because it is more stable," could be made more prominent before the proof details.

## Under-explained details

The chapter should explain more explicitly what "the vectors a model can produce" means. In the worked example, the column space of $\mathbf{A}$ is the set of all fitted value vectors from straight lines. That idea is central and should be stated before the normal equations and again in the example.

The residual orthogonality condition needs an applied translation. In the line-fitting example, $\langle \mathbf{r}, \mathbf{a}_1\rangle=0$ means the residuals sum to zero, and $\langle \mathbf{r}, \mathbf{a}_2\rangle=0$ means the residuals have zero weighted sum against the regressor. That is a perfect opportunity to connect geometry to familiar regression diagnostics.

Full column rank needs more intuition. A health researcher will benefit from examples such as duplicate covariates, an intercept plus perfectly redundant indicator variables, or trying to estimate more independent parameters than the data support.

The phrase "normal equations are always consistent" is surprising. It should be paired immediately with "consistent does not mean unique." Otherwise a reader may think every least-squares problem has a unique solution.

The connection between $P^\perp_{\mathcal{M}}=I-P_{\mathcal{M}}$, the residual maker $M$, and Chapter 6 should be repeated in plainer language. This is one of the highest value pieces of notation for later chapters.

The exercises assume substantial proof maturity. The computational exercises are useful, but the later proof exercises may be too steep unless the reader has seen a few shorter concept checks first.

## Where a novice may get lost

A novice may get lost in the transition from the opening ITC motivation to the abstract definition of an inner product space. The move is legitimate, but the chapter could use a short paragraph saying that the next few definitions build the vocabulary needed to define "closest fit."

The Gram-Schmidt formula is a likely sticking point. The expression subtracts several projection terms at once, and the reader has not yet had much visual or numeric practice with "subtracting the part already explained." The worked example helps later, but an earlier two-vector mini-example would make the theorem easier to enter.

The orthogonal complement section is dense. It moves from $S^\perp$ to span identities, direct sums, double complements, and fundamental subspaces. These are all relevant, but a novice may not know which facts are load-bearing for regression and which are supporting structure.

The projection theorem proof is the most important proof in the chapter, but it is also where symbol overload is most dangerous. I would expect a novice to understand the first read only partially, especially the part that proves every minimizer must have orthogonal residual.

The projection matrix characterization proof is probably too abstract for the target reader without a preceding "what to watch for" paragraph. Symmetric and idempotent are not intuitive properties until the reader sees that idempotent means projecting twice changes nothing.

The normal equations section depends on null spaces, column spaces, Gram matrices, and rank-nullity all at once. A reader who only weakly retained Chapter 1 may struggle here. This section needs more reminders and less reliance on the reader remembering what each subspace means.

The QR uniqueness proof is unlikely to be accessible on first pass. It may be acceptable in a pure-mathematics text, but it should be marked as less essential for the applied narrative, or followed by a short plain-language summary of what the reader should retain.

## Suggested improvements

Add short "In words" paragraphs after the most important results: Cauchy-Schwarz, orthogonal decomposition, the projection theorem, projection matrix characterization, and the normal equations. These should translate the formal statement into a sentence about data fitting, residuals, or model predictions.

Add a small running health research interpretation to the worked example. For example, treat $\mathbf{b}$ as a mean outcome in four ordered covariate groups and the second column as a centered or uncentered covariate. Then interpret the fitted vector as predicted outcomes and the residual vector as unexplained outcome differences.

Before the normal equations, insert a bridge that says: choosing coefficients $\mathbf{x}$ is not the same as choosing fitted values $\mathbf{A}\mathbf{x}$. The projection theorem gives the best fitted values first; the normal equations then find coefficients that produce those values.

Expand the rank discussion with a concrete health data example. For instance, if a model includes both "female" and "male" indicators plus an intercept, one column is redundant. This would make nonunique coefficients and rank deficiency feel real rather than technical.

Move some of the ITC motivation from the introduction into the body of the chapter. The opening promises relevance to STC, ML-NMR, and MAIC, but the middle sections mostly become pure linear algebra. A sentence at the end of major sections could remind the reader how the concept will return later.

Make the weighted inner product remark more gradual. Add one sentence saying that covariance weighting changes the meaning of distance by downweighting directions where the population naturally varies more and upweighting directions where differences are more unusual.

Add an early two-dimensional visual intuition example, even if only described verbally. A point above a line, its nearest point on the line, and the perpendicular residual would give the reader a mental picture before the full theorem.

Add a few easier exercises before the proof-heavy ones. Useful prompts would ask the reader to identify the column space in words, interpret residual orthogonality in a small regression, distinguish fitted values from coefficients, and explain why projecting twice changes nothing.

Consider labeling the QR uniqueness proof or the oblique projection material as optional on first reading. The results are rigorous and relevant, but they may distract from the core learning goal if the reader is still trying to understand projection and residuals.

## Highest-priority fixes

1. Add plain-language interpretation after the projection theorem and the normal equations. These are the core results, and the novice reader needs to know exactly what they mean for fitted values and residuals.

2. Strengthen the worked example by interpreting the matrix columns, fitted values, residual orthogonality, RSS, TSS, and $R^2$ in applied terms, not only as arithmetic.

3. Clarify the fitted vector versus coefficient vector distinction, especially the fact that fitted values can be unique even when coefficients are not.

4. Add concrete rank-deficiency examples from regression or trial covariate modeling so "full column rank" feels like an applied condition.

5. Insert bridge sentences before the abstract sections on orthogonal complement, projection matrices, and QR so the reader knows why each new layer is needed.
