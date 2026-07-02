# Feedback: Chapter 02 — Linear Algebra II

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part1/02-linear-algebra-ii.qmd`

## Overall impression

I made it through, but honestly I felt like I was reading a math book that occasionally remembered it was supposed to be about health research. The opening hook (`#sec-ortho-intro`, lines 5 to 31) sold me hard on ITCs, MAIC, STC, ML-NMR; that was exciting. But then from section `#sec-ip-spaces` onward the ITC thread basically disappears for about 500 lines, and I was wading through pure abstract linear algebra with nothing to hold onto. The worked example at the end (`#sec-ch02-example`) is a line fit through four points that has nothing to do with medicine, trials, or patients. I kept asking: when am I going to see a covariate? When am I going to see a treatment group? The payoff never came in this chapter. The math itself looks careful and complete, and I believe the proofs, but as a beginner I lost the thread more than once.

## What was unclear

- **Line 31, the typeface convention.** "operator matrices that the notation chapter writes without bold (the identity $I_n$, the projection $P_{\mathcal{M}}$, the hat matrix $H$) keep that lighter typeface." I read this three times and still do not understand the rule. Is the hat matrix bold or not? When I look at `notation.qmd` line 54 it says $H = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$, with $H$ not bold and $\mathbf{X}$ bold. So which am I supposed to use in my head when I see $P_{\mathcal{M}}$? This convention paragraph needs an explicit two-line example showing one bold matrix and one light operator side by side.

- **Lines 41 to 51, the inner product definition.** Axiom (2) says "linearity in the first argument," and then line 50 to 51 says "By symmetry, linearity holds in the second argument as well, so $\langle\cdot,\cdot\rangle$ is bilinear." For someone with weak math, "bilinear" is jargon. What does bilinear buy me? Why is it called "bi"? A one-line parenthetical ("bilinear = linear in each slot separately") would fix this.

- **Lines 60 to 69, the Mahalanobis remark.** This is the single most exciting paragraph for a health researcher in the whole chapter, and it is buried in a remark. "$A=\boldsymbol{\Sigma}^{-1}$, the inverse covariance of a covariate distribution, gives the Mahalanobis distance that underlies the matching geometry of MAIC." I have heard of Mahalanobis distance but I do not actually know what it measures in plain terms. Is it "how far is this patient's covariate vector from the average patient, scaled by how spread out the covariates are"? Say that. And "the matching geometry of MAIC in Part IV" is a forward reference I cannot verify. Give me a tiny concrete picture: two trial populations, one patient who is an outlier under Euclidean distance but reasonable under Mahalanobis. Right now this remark teases something I cannot visualize.

- **Lines 100 to 123, the Cauchy-Schwarz proof.** The trick of looking at $\|\mathbf{u}-t\mathbf{v}\|^2 \ge 0$ as a quadratic in $t$ is the standard proof, but for a noob it comes out of nowhere. Why would I think to minimize a quadratic in $t$? The motivation is missing. A sentence before the proof like "The idea: $\|\mathbf{u}-t\mathbf{v}\|^2$ is always nonnegative, so the quadratic it defines in $t$ cannot have real roots unless its discriminant is nonpositive; that discriminant is exactly Cauchy-Schwarz" would give me the why. Also line 110 to 111 jumps straight to "minimized at $t^\star=\langle\mathbf{u},\mathbf{v}\rangle/\|\mathbf{v}\|^2$" without showing the derivative. A weak-math reader needs that derivative written, or at least the words "differentiate with respect to $t$ and set to zero."

- **Lines 125 to 143, the triangle inequality corollary.** The proof is three lines and I followed it algebraically, but I have no geometric picture. There is no figure, no diagram. For a chapter whose entire thesis is "geometry is the engine," the absence of any illustration of a right triangle with legs $\mathbf{u}$ and $\mathbf{v}$ and hypotenuse $\mathbf{u}+\mathbf{v}$ is a real gap.

- **Line 153, the angle definition.** "Cauchy-Schwarz lets us define the angle $\vartheta$ between nonzero vectors by $\cos\vartheta=\langle\mathbf{u},\mathbf{v}\rangle/(\|\mathbf{u}\|\,\|\mathbf{v}\|)\in[-1,1]$." The fact that this ratio lands in $[-1,1]$ is exactly what Cauchy-Schwarz guarantees, and I think the text assumes I will see that. Spell it out: "Cauchy-Schwarz is precisely the statement that this ratio is between $-1$ and $1$, so the arccosine defining $\vartheta$ makes sense." Without that link, the sentence reads as a definition that happens to work.

- **Lines 218 to 233, the Gram-Schmidt theorem statement.** The recursion in `#eq-gram-schmidt` is dense. I stared at the fraction $\langle\mathbf{a}_k,\mathbf{u}_i\rangle/\langle\mathbf{u}_i,\mathbf{u}_i\rangle$ for a while before I realized that is "the coefficient of $\mathbf{u}_i$ in the projection of $\mathbf{a}_k$ onto $\mathbf{u}_i$." The text does not say this in words before the formula. A sentence right after the equation reading "each term subtracts the component of $\mathbf{a}_k$ already lying in the directions we have built" would make the recursion legible.

- **Lines 235 to 275, the Gram-Schmidt proof.** This is the hardest proof in the chapter and it is done as strong induction with three simultaneous claims. For a beginner, strong induction itself is shaky; juggling three invariants (nonzero, orthogonal, span equality) at once is brutal. I would benefit from the proof being broken into three labeled subproofs, each its own paragraph, rather than woven through one induction. The orthogonality check at lines 257 to 262 is correct but I lost track of why "the only surviving term in the sum is $i=j$." Make that explicit: all other terms vanish because $\langle\mathbf{u}_i,\mathbf{u}_j\rangle=0$ when $i\ne j$, which is the induction hypothesis.

- **Lines 397 to 419, the fundamental subspaces orthogonality.** The result `#prp-fundamental-orthogonality` is a key bridge back to Chapter 1, but the proof at line 415 to 416 ends with "taking complements of both sides and using @cor-complement-dimension yields $\mathcal{C}(\mathbf{A}^\top)=\mathcal{N}(\mathbf{A})^\perp$." I could not reconstruct the last step. The double complement $(\mathcal{M}^\perp)^\perp=\mathcal{M}$ from `#eq-double-complement` is doing work here, and the text does not name it. Say "applying $(\cdot)^\perp$ to both sides and invoking $(\mathcal{M}^\perp)^\perp=\mathcal{M}$."

- **Lines 552 to 595, the projection matrix characterization.** The sufficiency direction (lines 570 to 586) shows the residual is orthogonal to $\mathcal{M}$ by checking $\langle\mathbf{v}-P\mathbf{v},P\mathbf{u}\rangle=0$ for a *general* element $P\mathbf{u}$ of $\mathcal{M}$. That step "$P\mathbf{u}$ is a general element of $\mathcal{M}$" needs justification: why does every element of $\mathcal{C}(P)$ look like $P\mathbf{u}$? It does by definition of column space, but a noob will not see that instantly. One parenthetical would help.

- **Lines 769 to 785, the QR uniqueness proof.** This is the most compressed proof in the chapter. The claim "an upper-triangular matrix with positive diagonal and orthonormal columns is the identity" is proved by induction on columns, and I followed it, but only barely. The leap at line 782 to 783, "the only possibly nonzero entries of column $j$ are $s_{jj}$ and entries below the diagonal, which vanish by upper-triangularity," is doing two things at once. Split it: first, orthogonality to earlier standard basis columns kills the above-diagonal entries; second, upper-triangularity kills the below-diagonal entries; so only $s_{jj}$ survives.

- **Lines 829 to 834, the conditioning remark.** "$\kappa(\mathbf{A}^\top\mathbf{A})=\kappa(\mathbf{A})^2$" is stated with no definition of $\kappa$ (the condition number). It has not been introduced in this chapter or in `notation.qmd` (I checked, it is not there). For a noob, a condition number is an unfamiliar object. Define it inline or point to where it will be defined.

## What wasn't elaborated enough

- **The projection theorem itself (`#thm-projection-theorem`, lines 427 to 479).** This is the centerpiece of the chapter, the thing the preface said everything rests on, and the statement at lines 431 to 441 is given in three parts with no accompanying diagram. For a theorem that is "geometric and exact," there is no geometry shown. A single figure of a vector $\mathbf{v}$, a subspace $\mathcal{M}$ drawn as a plane, the closest point $\mathbf{m}^\star$, and the perpendicular residual would make this theorem click in five seconds. Without it, the proof at lines 444 to 478 reads as algebra.

- **The remark at lines 483 to 491.** It introduces the symbol $P_{\mathcal{M}}\mathbf{v}$ and the word "residual" informally, in a remark, *after* the theorem. The name "orthogonal projection" and the symbol should appear inside the theorem statement or immediately before the proof, not buried after. I had already finished the proof before I learned the object had a name.

- **The normal equations remark (lines 713 to 723).** This is the closest the chapter gets to reconnecting to statistics, and it is excellent, but it is one remark. "It is worth emphasizing that @thm-normal-equations-geometry uses no probability whatsoever: it is a statement about distances in $\mathbb{R}^n$" (lines 720 to 722) is a profound point that deserves more than two sentences. Why does the separation matter? Because it tells me the geometry is true regardless of the noise model, which is exactly the kind of thing a health researcher using OLS in a paper needs to know.

- **The double complement `#cor-complement-dimension` (lines 375 to 395).** The dimension identity $\dim\mathcal{M}+\dim\mathcal{M}^\perp=\dim V$ is a big structural fact and it gets half a proof. "A basis of $\mathcal{M}$ together with a basis of $\mathcal{M}^\perp$ is a basis of $V$" (lines 387 to 389) needs the explicit check that the union is linearly independent, not just the parenthetical. Beginners cannot fill in "their union is independent since the only shared vector is $\mathbf{0}$."

## Missing motivation / "why does this matter?"

- **The whole middle of the chapter, sections `#sec-orthonormal`, `#sec-gram-schmidt`, `#sec-orthogonal-complement`, `#sec-projection-matrices`.** The intro promised ITC connections. From line 33 to roughly line 616 there is essentially no mention of health, trials, covariates, or comparison. The only touch is the Mahalanobis remark at lines 60 to 69. I understand these are prerequisites, but a one-sentence ITC callback at the start of each section would keep me oriented. For example, before Gram-Schmidt: "MAIC and ML-NMR both fit models by solving normal equations; the orthonormal basis we build now is what makes that solve numerically stable in software." Before the projection matrix characterization: "The hat matrix in Chapter 6 will be exactly such a symmetric idempotent matrix, and its diagonal entries are the leverages that flag influential trial arms."

- **Why prove Cauchy-Schwarz at all (lines 91 to 123)?** I know it is a famous inequality, but the chapter uses it for two things: the triangle inequality and the angle definition. Neither of those is obviously load-bearing for ITCs. Tell me, in one sentence, what breaks in later chapters if Cauchy-Schwarz is false. Otherwise the proof feels like ceremony.

- **Why prove the Gram-Schmidt process by strong induction with three invariants (lines 235 to 275)?** The remark at lines 277 to 283 hints that modified Gram-Schmidt is what software uses, but the chapter proves the *unmodified* version in full. A noob asks: if the modified one is what matters, why prove the unstable one in such detail? A sentence saying "the modified version is algebraically identical, so this proof covers it; we prove the classical form because its induction is transparent" would settle that.

- **Why the QR factorization at all (section `#sec-qr`, lines 730 to 834)?** The remark at lines 828 to 834 explains the conditioning argument, which is good, but it never says "this is what R's `lm()`, Stata's `regress`, and Stan's linear algebra actually call." A health researcher who runs `lm(y ~ x)` every week would be motivated to learn QR if told that is literally the function being called under the hood.

- **The exercises (lines 962 to 1041).** Every exercise is pure math. There is not a single exercise that says "here is a tiny two-arm trial with two covariates, build the design matrix, do the projection, interpret the residual." The closest is `#exr-line-fit` (line 981), and it is four abstract points. A health-flavored exercise would tie the chapter to the book's purpose.

## Missing examples and intuition

- **No figure anywhere.** A chapter on orthogonality, projection, and geometry with zero diagrams is a genuine problem for a beginner. The minimum I would want: a picture for the triangle inequality, a picture for the projection theorem (vector, plane, perpendicular drop), a picture for Gram-Schmidt (two vectors, subtract the projection of the second onto the first), and a picture for the QR factorization (the columns of $\mathbf{A}$ becoming the orthonormal columns of $\mathbf{Q}$).

- **No non-Euclidean example for the inner product.** The only fully worked inner product is the Euclidean dot product (line 54 to 57). The weighted inner product in the remark (lines 60 to 69) is stated but never computed on numbers. A two-dimensional numerical example with a specific $A=\begin{bmatrix}2&0\\0&1\end{bmatrix}$, two vectors, and the resulting angle being different from the Euclidean angle, would make the abstract definition concrete and preview Mahalanobis.

- **The worked example `#sec-ch02-example` (lines 836 to 932) is abstract.** It fits a line $y = \tfrac12 + x$ through four points. There is nothing wrong with it, and it is well paced, but it is the *only* fully worked example in a thousand-line chapter, and it carries zero health content. A parallel mini-example, even just three lines long, with a design matrix containing a treatment indicator and a covariate, and a sentence saying "this is the shape of every regression you will run in Part II," would have converted the abstract example into something I recognize from my own work.

- **No example of an orthogonal projection matrix other than the hat matrix.** `#thm-projection-matrix-characterization` (lines 552 to 595) is a characterization theorem with no small explicit $P$ exhibited. A $2\times2$ or $3\times3$ numerical symmetric idempotent matrix, shown to project onto its column space, would make the theorem tangible.

- **No example of the orthogonal complement.** `#def-orthogonal-complement` (lines 300 to 306) and `#thm-orthogonal-decomposition` (lines 339 to 347) are core, but I never see a concrete subspace and its concrete complement written out with numbers. A two-line example in $\mathbb{R}^3$: $\mathcal{M}$ is the $xy$-plane, $\mathcal{M}^\perp$ is the $z$-axis, would anchor the abstraction.

## Notation and jargon problems

- **$\delta_{ij}$, the Kronecker delta (line 161).** Used without definition. It is in no table of `notation.qmd` (I checked the whole file). Define it on first use: "$\delta_{ij}=1$ if $i=j$, $0$ otherwise."

- **"Internal direct sum" (line 346).** The symbol $V=\mathcal{M}\oplus\mathcal{M}^\perp$ appears with the parenthetical "an internal direct sum" but no definition. What makes a direct sum "internal" versus external? A noob has no idea. Either define it or drop the adjective.

- **"Positive definite" and "symmetric positive definite" (lines 60 to 64).** Used in the Mahalanobis remark with a forward reference to Chapter 3 `#thm-pd-characterization`. For a reader at chapter 2, "positive definite" is undefined. The remark says "the characterization of such matrices is the business of Chapter 3," but it does not even give the definition here. A one-line "a symmetric matrix $A$ is positive definite if $\mathbf{x}^\top A\mathbf{x}>0$ for all $\mathbf{x}\ne\mathbf{0}$" would let me read the remark without jumping.

- **"Quadratic-form norm" (line 64).** The term is introduced in a remark and points to `notation.qmd`, where line 40 defines $\|\mathbf{x}\|_A=\sqrt{\mathbf{x}^\top A\,\mathbf{x}}$. Fine, but the chapter never calls it a "quadratic form" again or explains the name. One clause: "called a quadratic form because $\mathbf{x}^\top A\mathbf{x}$ is a degree-two polynomial in the entries of $\mathbf{x}$."

- **$\kappa(\cdot)$, the condition number (line 830).** Not in `notation.qmd`, not defined in the chapter. See above.

- **$\operatorname{span}$, $\operatorname{rank}$, $\mathcal{C}$, $\mathcal{N}$ (throughout).** These come from Chapter 1 and are fair to assume, but the cross-references like `@def-column-space` and `@thm-rank-nullity` (line 18) are dropped without a glossary reminder. A small "recall from Chapter 1" box at the start listing the five symbols reused would help readers who read chapters out of order.

- **Mixed typeface for matrices (line 28 to 31 versus `notation.qmd` line 9).** `notation.qmd` says bold uppercase for matrices ($\mathbf{X}$). This chapter says data and factor matrices are bold uppercase, but operator matrices like $I_n$ and $P_{\mathcal{M}}$ are light. But then $\mathbf{A}$, $\mathbf{Q}$, $\mathbf{R}$ are bold (line 28). The rule is consistent but never summarized in a single displayed example, so I kept misreading whether $P_{\mathcal{M}}$ was bold or not in later equations.

## Pacing issues

- **The opening section `#sec-ortho-intro` (lines 5 to 31) is excellent but sets up expectations the rest of the chapter does not meet.** It names MAIC, STC, ML-NMR, the projection theorem, the normal equations, and QR, all in one breath. Then the chapter spends 600 lines before any of those pay off. The pacing cliff between the intro and `#sec-ip-spaces` is steep.

- **Section `#sec-ip-spaces` (lines 33 to 148) front-loads three definitions and two proofs with no example.** Inner product, norm, Cauchy-Schwarz, triangle inequality, reverse triangle inequality, all in one section, all abstract. For a noob this is the hardest section to get through, and it is the very first one after the intro. Inserting the weighted-inner-product numerical example here would slow the pace to something survivable.

- **The Gram-Schmidt section `#sec-gram-schmidt` (lines 213 to 296) is proof-heavy with no intermediate example.** The theorem statement, the long induction proof, a remark about numerical stability, and the corollary that orthonormal bases exist, all flow with no worked mini-example. The full numerical example only comes at the end of the chapter (lines 851 to 861). A two-vector Gram-Schmidt in $\mathbb{R}^2$ right after the theorem would have let me check the formula on paper before reading the proof.

- **The worked example `#sec-ch02-example` (lines 836 to 932) comes after all the theory.** This is the standard pure-math ordering, but for a beginner the example is what makes the theory legible. Moving a trimmed version of the example (at least Steps 1, 3, and 5) to right after `#thm-normal-equations-geometry` would give readers a concrete anchor for the last two sections.

- **The exercises ramp from mechanical to starred very fast.** `#exr-gram-schmidt-r3` (line 964) is mechanical, `#exr-projection-plane` (line 972) is fine, then `#exr-oblique-vs-orthogonal` (line 1033) is a starred equivalence proof with a four-part characterization. There is no intermediate "verify the normal equations on a tiny health-flavored dataset" exercise bridging the mechanical and the theoretical.

## What worked well

- **The introduction `#sec-ortho-intro` (lines 5 to 31).** This is the best writing in the chapter. It tells me exactly why the chapter exists, what it will prove, and where each result lands later. The sentence "Underneath all of them sits one geometric fact" (lines 12 to 15) is the kind of orientation I desperately need.

- **The notes and references section `#sec-ch02-notes` (lines 934 to 960).** It honestly states what is standard, what is reused where, and why proofs were given in full. The line "we deliberately proved them with no probabilistic input so that the geometry and the statistics stay cleanly separated" (lines 946 to 947) is the kind of methodological note I appreciate.

- **The worked example is genuinely complete.** Steps 1 to 6 (lines 851 to 932) carry one problem through every construction, verify the answers match, and check the orthogonality and trace identities by hand. As a template for "how to do this yourself," it is excellent, even if the data is abstract.

- **The remark at lines 713 to 723 connecting the normal equations to the hat matrix of Chapter 6.** This is the moment the chapter's promise starts to pay off. It names $H$, $M$, $\hat{\boldsymbol\beta}$, and the BLUE theorem, and it states clearly that no probability was used. More of this, please.

- **The honesty about Coq coverage (lines 957 to 960).** Saying explicitly that this chapter has no machine-checked counterparts, and why, is better than silence. It sets correct expectations for Part II.

## Suggestions

1. **Add at least three figures:** the projection theorem (vector, plane, perpendicular residual), the Gram-Schmidt step (two vectors, subtract the projection), and the QR factorization (columns of $\mathbf{A}$ recombining into orthonormal columns of $\mathbf{Q}$). A chapter whose thesis is geometric needs pictures.

2. **Add a small health-flavored example early, in or right after `#sec-ip-spaces`.** A two-covariate design matrix with a treatment indicator, a weighted inner product with a diagonal $A$, and a one-sentence callback to "this is the shape of every regression in Part II." This converts the abstract opening into something a health researcher recognizes.

3. **Add one-sentence ITC callbacks at the start of each of the five middle sections.** Gram-Schmidt, orthonormal sets, orthogonal complement, projection matrices, normal equations. One sentence each is enough to keep me from forgetting why I am here.

4. **Define all jargon on first use, even if it is "standard."** Specifically: $\delta_{ij}$, "internal direct sum," "positive definite," "quadratic form," "bilinear," and $\kappa$ (condition number). Add $\delta_{ij}$ and $\kappa$ to `notation.qmd`.

5. **Split the Gram-Schmidt induction proof (lines 235 to 275) into three labeled subproofs** (nonzero, orthogonal, span), each its own short paragraph, rather than interleaving the three invariants through one induction. Beginners can hold one invariant at a time, not three.

6. **Move a trimmed version of the worked example (Steps 1, 3, 5) to immediately after `#thm-normal-equations-geometry`,** so readers have a concrete anchor before the QR section. Keep the full six-step version at the end as a capstone.

7. **Add a health-flavored exercise:** a tiny two-arm dataset with one covariate, build the design matrix, solve the normal equations, compute the residual, verify orthogonality, and report $R^2$. This is the single highest-leverage change for the book's stated audience.

8. **Clarify the typeface convention (line 28 to 31) with a displayed side-by-side example** showing one bold data matrix and one light operator matrix, so the reader is never in doubt about which category a symbol falls into.

9. **Expand the Mahalanobis remark (lines 60 to 69) into a short named subsection or a longer worked remark** with a numerical example and a plain-language gloss. Right now the single most ITC-relevant paragraph in the chapter is a throwaway.