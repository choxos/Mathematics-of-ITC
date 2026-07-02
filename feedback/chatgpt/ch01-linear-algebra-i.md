# Chapter 1 Feedback: Linear Algebra I

## Overall reaction

This is a rigorous and serious opening chapter. As a novice health researcher, I would trust that the author knows exactly where the mathematics is going. The introduction and the two-arm design-matrix example make the relevance to regression, treatment indicators, and identifiability visible.

The main issue is that the chapter often feels like a conventional abstract linear algebra chapter with a health example at the beginning and end, rather than a guided mathematical bridge for a health researcher. The formal sequence is coherent, but the reader who is weak in abstract mathematics may not yet have enough concrete anchors to understand why each definition matters before being asked to follow several pages of theorem proof.

The chapter succeeds best when it says what a mathematical object means for a trial design. It is hardest when it introduces a formal object, proves several facts about it, and only much later reconnects it to the design matrix or indirect treatment comparison.

## What was clear

The opening motivation is strong. The connection among the design matrix, column space, rank, null space, and identifiability is exactly the kind of map a health researcher needs before entering the formal material.

The definition of a real vector space is precise, and the coordinate-space example is helpful because it tells the reader that the familiar object $\mathbb{R}^n$ is the main case. The statement that vectors are written as columns by default is also useful.

The matrix-vector product section is clear. Defining $A\mathbf{x}$ as a linear combination of the columns is pedagogically useful because it prepares the reader for column space and for fitted values in regression.

The rank-nullity proof is one of the clearer proof sections because it has an evident strategy: extend a kernel basis to a full basis, then show the images of the added basis vectors span and are independent. The labels "Spanning" and "Independence" help.

The worked two-arm design example is the strongest part of the chapter for the target reader. "Constant within each treatment group" makes the column space concrete. "Within-group mean-zero contrasts" gives the left null space a recognizable meaning. The dummy-variable trap remark is also effective because it translates null spaces into a familiar modeling mistake.

## What was unclear

The promise that the chapter develops the vocabulary "from nothing" is only partly met for a novice health researcher. The chapter starts with axioms, abstract sets, finite linear combinations, Steinitz exchange, and basis-extension arguments before giving many small health-oriented examples. A motivated reader can follow the words, but may not know what to care about.

The role of a vector changes across the chapter without enough signposting. Sometimes a vector is a list of patient outcomes, sometimes a column of a design matrix, sometimes a coefficient vector, sometimes an abstract element of $V$, and sometimes a solution to $A\mathbf{x}=\mathbf{b}$. A mathematically trained reader handles this naturally. A health researcher may need a short "what the vector represents here" reminder at transitions.

The transition from linear independence to basis and dimension is logically clean but intuition-light. The health meaning of independence as "no column is redundant given the others" appears later, but it would help earlier, especially around @def-linear-independence, @def-basis, and @def-dimension.

The phrase "the treatment effect is identifiable precisely when the relevant contrast is constant on the coset $\boldsymbol\beta+\mathcal{N}(\mathbf{X})$" is important but too compressed for Chapter 1. At that point, "contrast," "coset," and "constant along a null direction" are not yet fully intuitive. This is a high-value sentence, but it needs a worked mini-example or a plain-language translation immediately after it.

The four fundamental subspaces section is mathematically organized, but a novice may struggle with which subspaces live in $\mathbb{R}^n$ and which live in $\mathbb{R}^m$. The text states this, but the distinction is easy to lose once transposes, row space, null space, and left null space are all in play.

The row operations section says Gaussian elimination is taken as standard. For the intended audience, that may be too optimistic. The exercises require reduced row-echelon form, pivots, and pivot columns, but the chapter does not give a worked elimination example.

## Under-explained details

The notation $\operatorname{span}(S)$ is defined precisely, including the empty-sum convention, but the intuitive meaning could be clearer. A novice-friendly sentence such as "span means every vector you can build by mixing these ingredients with real-number weights" would help.

The connection between "image" for a linear map and "column space" for a matrix needs extra emphasis. The chapter defines both correctly, but a novice could see them as separate terms rather than the same idea in two languages.

The kernel and null space would benefit from a health-model interpretation earlier. For example: if $\mathbf{z}$ is in the null space of $\mathbf{X}$, changing $\boldsymbol\beta$ by $\mathbf{z}$ changes the coefficients but not any fitted value. That sentence appears in spirit later, but it should appear close to @def-kernel-image or @def-rank.

The left null space is under-motivated until the worked example. It would help to preview that left-null vectors represent patterns in the observed outcome vector that the model cannot reproduce. In the two-arm example, within-group deviations are exactly such patterns.

Orthogonal complement, internal direct sum, affine subspace, and coset are introduced or used quickly. Even when they are defined or deferred, the reader may not know whether they are essential now or vocabulary for later chapters. Brief "do not worry yet" signposts would reduce cognitive load.

The normal-equations matrix $\mathbf{X}^\top\mathbf{X}$ appears in the worked example before ordinary least squares has been developed. The preview is useful, but it needs one or two sentences explaining why multiplying by $\mathbf{X}^\top$ is coming later and what problem the normal equations solve.

## Where a novice may get lost

The Steinitz exchange theorem is likely the first major obstacle. The result is important for dimension, but the proof is long and abstract. A reader may not see why replacing $\mathbf{w}_{k+1}$ with $\mathbf{u}_{k+1}$ matters, or how this relates to redundant columns in a design matrix.

The sequence from reduction to a basis, basis extension, and then rank-nullity is formally efficient but demanding. A novice may need a small numerical example showing a spanning set being thinned and an independent set being extended before seeing the general lemmas.

The row-rank-equals-column-rank proof via rank factorization is elegant but abstract. The new matrices $C$ and $F$, the uniqueness of the coefficients $F_{kj}$, and the transpose argument may be hard to track without a concrete matrix beside it.

The four-subspaces theorem could overwhelm readers because it combines dimension counts, transposes, orthogonality, and two ambient spaces at once. A table with columns for "subspace," "lives in," "dimension," "health interpretation," and "what it tells us" would make this section much easier.

The solvability section moves from $A\mathbf{x}=\mathbf{b}$ to identifiability in regression and indirect comparison. The leap is mathematically valid, but a novice may need the translation: $A$ is the design, $\mathbf{x}$ is the unknown parameter vector, $\mathbf{b}$ is the pattern we are trying to match, and nonzero null directions mean different parameter values give the same predictions.

The exercises are mostly proof-oriented and may feel inaccessible after one chapter. The dummy-variable exercise is well aligned with the audience, but several others ask for abstract proofs before the reader has built much confidence. More warm-up computation and interpretation exercises would help.

## Suggested improvements

Add a small running health example near the start, before the vector-space axioms. A table with patient ID, treatment arm, one covariate, and outcome would let the reader repeatedly see rows as patients, columns as model ingredients, $\boldsymbol\beta$ as unknown effects, and $\mathbf{X}\boldsymbol\beta$ as fitted values.

After each major formal definition, add a short "reader translation" paragraph. Useful targets are vector space, subspace, span, linear independence, basis, dimension, linear map, kernel, image, rank, and nullity.

Add a compact notation-role table. For example: $\mathbf{y}$ is often an outcome vector, $\boldsymbol\beta$ is a coefficient vector, $\mathbf{x}$ may be a generic solution vector in $A\mathbf{x}=\mathbf{b}$, and columns of $\mathbf{X}$ are model features. This would prevent the common novice confusion that all vectors represent the same kind of object.

Move some of the design-matrix intuition earlier. The chapter already has excellent material in the final worked example. A few shorter preview examples earlier would make the formal sections easier to absorb.

Add a visual or tabular guide to the four fundamental subspaces. The most useful version would show $\mathcal{C}(A)$ and $\mathcal{N}(A^\top)$ in outcome space $\mathbb{R}^m$, and $\mathcal{C}(A^\top)$ and $\mathcal{N}(A)$ in coefficient space $\mathbb{R}^n$.

Add one worked Gaussian elimination example before @prp-rank-equals-pivots or before the exercises. It does not need to be long. The reader needs to see how pivots, rank, and null-space solutions are found in practice.

Rebalance the exercises by labeling them as warm-up, computation, interpretation, proof, and starred challenge. Add at least two easier health-context exercises, such as identifying redundant design columns or explaining which treatment-effect contrast remains estimable.

## Highest-priority fixes

1. Add an early running design-matrix example and reuse it throughout the chapter, not only in the introduction and final worked example.

2. Add intuition paragraphs after the definitions of span, independence, basis, rank, image, and null space.

3. Expand the identifiability and coset discussion in @sec-la1-systems with a tiny coefficient example showing two different parameter vectors that produce the same fitted values.

4. Add a four-subspaces table that clearly separates coefficient space from outcome space and gives a health-model interpretation for each subspace.

5. Add one worked elimination example and make the first exercises more accessible before asking for abstract proofs.
