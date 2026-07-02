# Feedback: Appendix B — Matrix Calculus

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation. I have taken a semester of calculus and a basic biostatistics course, and I have used R for regression. I have never seen matrix calculus, I do not know what a Jacobian or Hessian really is beyond hearing the words, and "differential" makes me think of differential equations (which I dropped). I am reading this because I want to understand the derivations in the MAIC, STC, and ML-NMR chapters, which I keep getting told "just follow from differentiating a likelihood."
**File:** `appendices/B-matrix-calculus.qmd`

## Overall impression

This appendix frightened me. It is clearly written by someone who already knows all of this and is laying it out tidily for other people who already know it. The opening paragraph (lines 5 to 14) is the strongest part, because it actually tells me why the appendix exists: normal equations, score and Fisher information, restricted likelihood, matching weights, Jacobians for MAIC/STC. That gave me hope. But by the time I reached the conventions section (line 32) the tone had already shifted to "we fix one set of layout conventions" and "we adopt the differential as the working tool" (lines 16 to 18), and I was lost on the first reading because no one explained what a layout convention even is or why I should care about a "differential" before I had seen a single example. The appendix reads as a reference card with proofs attached, not as a teaching appendix that takes a naive reader to mastery, which is the stated goal of the whole book.

The single biggest structural problem: there is not one worked numerical example until the very end (the compound-symmetry section, line 663), and that example is about REML variance components, not about any ITC method. For an appendix whose entire reason for existing is to serve the MAIC, STC, ML-NMR, ML-UMR, and transportability chapters, the worked example is drawn from the wrong part of the book. I finished the appendix able to recite identities but unable to tell you what the gradient of a logistic regression log-likelihood looks like, which is the thing I actually need.

## What was unclear

- **"We fix one set of layout conventions" (line 16).** I do not know what a layout convention is. The phrase "numerator layout" versus "denominator layout" never appears, yet the summary table (line 738) casually says "the gradient and matrix derivative use the denominator (same-shape) layout." This is the first time the word "denominator" appears, and it is in a summary. I had to look it up online. The appendix should say, in the conventions section, that there are two competing traditions (numerator layout and denominator layout), that they give transposed answers, and that we are picking denominator layout because the gradient keeps the shape of the argument. As written, a reader cannot tell me whether the gradient is a row or a column without scanning ahead.

- **The relationship `nabla f = J_f^top` (lines 73 to 75).** This is presented as a one-line consequence of comparing two definitions. It is the single most confusing fact in the appendix for a beginner, because the gradient is a column and the Jacobian of a scalar is a row, and "they are transposes" sounds contradictory until you realize they are different objects. I needed a sentence like: "The gradient and the Jacobian of a scalar function are not the same object; the gradient is a column vector, the Jacobian is a row vector, and one is the transpose of the other. We will use the gradient (column) throughout the book." Without that, the line reads as a paradox.

- **"Differentials turn matrix differentiation into ordinary algebra" (lines 17 to 20).** This is the central pedagogical claim of the appendix and it is asserted, not shown. I do not know what a differential is. The first time a differential is actually computed is the product rule proof (line 164), which already assumes I am comfortable writing `F(X+H) = (F + dF + o)(G + dG + o)`. For someone whose only calculus is "derivative is the slope," the leap to "treat dX as a free increment" (line 140) is not obvious. I needed one tiny scalar example first: show me `f(x) = x^2`, write `f(x+h) = x^2 + 2xh + h^2`, identify `df = 2x dx`, then say "we do exactly this for matrices." Without that bridge, "the differential" feels like a new kind of object rather than a notation for the linear term.

- **The Frobenius inner product as "the" inner product (lines 93 to 96).** I know the dot product of two vectors. I do not know why, for matrices, the inner product is `tr(A^T B)`. The definition is given (line 95) but no intuition is offered: it is just the dot product of the entries if you flatten the matrices, and that one sentence would have made it click. As written it looks like an arbitrary ceremony involving a trace.

- **Lemma `lem-mc-identification` (lines 104 to 125).** This is billed as "the single most useful tool in this appendix" (line 101 to 102), and its proof is short and correct, but the lemma statement itself is nearly a tautology of the definition. A beginner cannot see why this is useful from the lemma alone; the usefulness only appears when it is applied (e.g. in the trace derivative proof, lines 314 to 334). The appendix should say, right after the lemma: "This is useful because computing a differential is easy (it obeys product, transpose, and trace rules) while computing a derivative entrywise is hard. Once we have the differential in the form `tr(G^T dX)`, we read off the derivative for free." That sentence is the whole reason the differential method exists, and it is missing.

- **"The Frobenius norm is submultiplicative" (line 170).** Used without proof or citation. I do not know what submultiplicative means in this context (`||AB||_F <= ||A||_F ||B||_F`). The notation table in `notation.qmd` does not define it either. One line of justification or a forward reference would help.

- **`X^{-T}` notation (line 28).** Defined once in the intro, good. But in the summary table (line 750) and the log-det theorem (line 413) it is used as if obvious; I had to scroll back to line 28 twice. Consider re-stating it at first heavy use.

- **The "symmetric gradient" remark (lines 431 to 451).** This is the densest paragraph in the appendix. The point, that differentiating with respect to the free parameters of a symmetric matrix doubles the off-diagonal entries, is important and correct, but it is delivered in a single 20-line block with no displayed intermediate. I could not reconstruct the "2X^{-1} - diag(X^{-1})" formula (line 438) without working it out on paper. A displayed derivation, or at least splitting the diagonal and off-diagonal cases into two sentences, would make this readable.

- **Schur complement proof (lines 554 to 566).** The block factorization is verified by "multiplying the right side" but the multiplication itself is not shown; only the (2,1) and (2,2) blocks are stated (lines 561 to 562). I had to do the (1,1) and (1,2) blocks myself to convince myself the factorization holds. For a foundational identity used twice in the determinant-lemma proof, showing all four blocks would cost four lines and remove all doubt.

## What wasn't elaborated enough

- **The Hessian (lines 76 to 83).** It is defined as "the Jacobian of the gradient map" in two lines. For a beginner who has never computed a Hessian, this is too fast. There is no example of a Hessian, no statement of why we care (it is the curvature; it tells us whether a stationary point is a min, max, or saddle; it is the Fisher information up to a sign), and no link back to the line in the preface (lines 8 to 9) about "negative expected Hessian." A reader meeting Hessians here for the first time will not connect this to the inference chapter.

- **The chain rule, part (2) (lines 614 to 621, proof at 642 to 649).** The statement uses the Frobenius inner product and then immediately rewrites it as a trace, and the proof says "This is part (1) after flattening the matrix into a vector." The flattening step is exactly where beginners stumble: which order do you stack columns? does the order matter? The proof says "stacking columns" (line 643) but never confirms that the conclusion is independent of the stacking order. One sentence: "the trace is invariant to the choice of flattening, so the result does not depend on it" would close this.

- **Jacobi's formula proof (lines 391 to 405).** The proof is correct and compact, but the key sentence "each cofactor C_{ik} is built from the minor that deletes row i, so C_{ik} does not depend on any entry of row i" (lines 393 to 394) is doing all the work and is stated in one breath. A reader who has not recently done a Laplace expansion will not see why deleting row i removes dependence on every entry of row i. Spelling out that the minor is the determinant of the submatrix obtained by striking out row i and column k, and therefore contains no entry with first index i, would make this self-contained.

- **The inverse-derivative componentwise form (lines 348 to 351).** The derivation (lines 359 to 367) uses `dX = E_{ij}` and reads off the (k,l) entry. The index gymnastics `(X^{-1}E_{ij}X^{-1})_{kl} = (X^{-1})_{ki}(X^{-1})_{jl}` is stated, not explained. I had to expand the sum myself to see that the only nonzero (E_{ij})_{pq} is at p=i, q=j. One parenthetical "(the only nonzero entry of E_{ij} is the (i,j) entry, equal to 1)" would make this transparent.

- **The restricted-likelihood score remark (lines 652 to 661).** This is the bridge to Chapters 8 and 13, and it is a remark, not a worked example. It states two specializations and says "These are exactly the building blocks of the restricted-likelihood score." For the appendix that is supposed to make those chapters tractable, this is the moment to actually assemble the score: write `ell_R(theta) = -1/2 log det V(theta) - 1/2 r^T V(theta)^{-1} r`, differentiate term by term using the two identities, and present the resulting score. As written, the reader is told the building blocks exist but never sees the building.

## Missing motivation / "why does this matter?"

- **Why the differential method at all?** The intro (lines 16 to 22) says differentials "avoid the index gymnastics that make componentwise differentiation error-prone." That is a motivation for the method, but it is never demonstrated. A single side-by-side: compute `d/dX tr(X^T A X)` entrywise (messy, three lines of indices) and then by the differential (two clean lines), would sell the method instantly. Right now I am asked to take on faith that differentials are easier.

- **Why do I care about the layout convention?** The appendix never tells me what goes wrong if I pick the wrong convention. A sentence like "If you see a formula in a paper that disagrees with ours by a transpose, it is almost certainly a layout difference, not an error" would save me hours of confusion when I read MAIC papers.

- **The Woodbury identity (Section `sec-mc-woodbury`, lines 453 to 540).** The motivation (lines 455 to 459) is good: "invert a matrix that differs from an easily inverted one by a low-rank correction." But the ITC connection is never made concrete. Where in MAIC or ML-NMR does a low-rank correction to a diagonal matrix actually arise? The compound-symmetry example (line 663) is the only concrete instance, and it is for REML, not for any population-adjustment method. A one-paragraph pointer to the specific matrix in, say, the ML-NMR marginal likelihood that has the Woodbury form would tie the appendix to its stated purpose.

- **The matrix determinant lemma (lines 568 to 594).** Same issue. It is proved cleanly, but I am never told which ITC computation needs it beyond "restricted likelihood" and "REML." The CLAUDE.md map says this appendix serves Chapters 18 and 19 (MAIC, STC) and 20 to 26 (ML-NMR, ML-UMR), but none of those connections are drawn in the appendix text itself.

- **Why is the gradient a column vector (line 47)?** The convention is stated, but the reason is not. The reason is that we want the first-order expansion `f(x+h) = f(x) + grad^T h`, and putting the transpose on the gradient makes `grad` live in the same space as `x`, which is geometrically natural. Saying this would make the convention feel motivated rather than arbitrary.

## Missing examples and intuition

- **No scalar warm-up before the matrix definitions.** Before Definition `def-mc-gradient` (line 39), I would have benefited from a one-paragraph scalar recap: "Recall that for a scalar function of one variable, the derivative is the number f'(x) such that f(x+h) = f(x) + f'(x)h + o(h). All of matrix calculus is the same statement with x replaced by a vector or matrix and the product replaced by an inner product." This reframes everything as a generalization rather than a new subject. It is missing.

- **No example of a gradient computation until the quadratic form (line 229), and even that is abstract.** The first time I see a gradient actually computed is the quadratic-form proof. A worked example with explicit numbers, e.g. `f(x) = 3x_1^2 + 2x_1 x_2 + x_2^2`, written as a quadratic form, gradient computed two ways (entrywise and via the formula), would make the theorem land.

- **No example of a Jacobian computation at all.** The Jacobian is defined (lines 56 to 67) and used in the chain rule, but no concrete function `g: R^2 -> R^2` is ever differentiated to produce a 2x2 Jacobian matrix. A beginner has no picture of what this matrix "looks like."

- **No example of a matrix derivative (Definition `def-mc-matrix-derivative`, line 88).** The simplest possible matrix derivative, `f(X) = tr(X)`, gives `d f / dX = I`, and this is mentioned in passing at line 311 and line 332 but never shown as a standalone worked example with the Frobenius inner product. The first real matrix derivative the reader is asked to verify is `tr(X^T A X)` (line 309), which is not trivial.

- **The worked example (Section `sec-mc-example`, line 663) is the only concrete one, and it is purely REML.** As noted, this is the wrong domain for an ITC book. A second worked example, even a short one, showing the gradient of a logistic-regression log-likelihood (which underpins ML-NMR's binary-outcome likelihood) or the gradient of the MAIC weight objective, would make the appendix feel like it belongs to this book rather than to a generic matrix-calculus reference.

- **No geometric picture anywhere.** The gradient is the direction of steepest ascent; the Hessian is curvature; the Jacobian is a local linear approximation. None of this is said. A reader with weak math needs the geometric hook to remember the algebra.

## Notation and jargon problems

- **`o(||h||)` and `O(||h||^2)` (lines 24, 44, 168, 253, etc.).** Landau symbols are used from line 24 onward and are listed in `notation.qmd` (line 80) but never explained in the appendix. A beginner does not confidently distinguish `o` from `O`. One sentence: "o(||h||) means a term that, divided by ||h||, vanishes as h -> 0; O(||h||^2) means a term bounded in absolute value by a constant times ||h||^2" would fix this.

- **"Open set" (lines 41, 58, 90).** Used in every definition, never explained. A health researcher does not know what an open subset of `R^n` is. Either drop it (say "on a neighborhood of x") or add a parenthetical.

- **"C^2" (line 83).** The Hessian symmetry claim uses "whenever f is C^2." The notation `C^2` (twice continuously differentiable) is not defined here or in the notation file. A beginner will not know that this is the hypothesis under which mixed partials are equal.

- **"Capacitance matrix" (line 501).** Introduced as a name with no motivation. Why is `C^{-1} + V A^{-1} U` called a capacitance? The term comes from electrical engineering applications; in a statistics book it is an unexplained proper noun. Either drop the name or add a one-line gloss.

- **"Adjucate" / "adj" (lines 22, 338, 371, 381, 400).** The adjugate is referenced repeatedly and identified with `cof(X)^T` only at line 400, deep in the Jacobi proof. The notation file does not define adjugate or cofactor. For a self-contained appendix, the adjugate and cofactor should be defined at first use (line 22), not at line 400.

- **Bold versus plain for matrices.** `notation.qmd` (line 9 to 11) says bold uppercase for matrices, plain for scalars. But this appendix uses plain `A, X, U, V` for matrices throughout (e.g. line 232, line 500) and bold only for vectors. This is consistent with a "matrix-calculus convention" but it conflicts with the book's standing convention and is never flagged. A reader who memorized `notation.qmd` will be confused that `X` is a matrix here but `mathbf{X}` is a matrix in the regression chapter. One sentence acknowledging the switch would help.

- **`mathbf{1}_n` (line 669).** Used in the worked example; defined in `notation.qmd` (line 35) as the n-vector of ones. Good, but a reader of the appendix alone will not know it. A parenthetical "(the n-vector of ones)" at first use would make the example self-contained.

## Pacing issues

- **The opening two paragraphs (lines 5 to 30) are the right pace; everything after line 32 accelerates sharply.** The transition from "here is why this matters" to "here are three definitions and a lemma with proof" with no example in between is too fast. A short scalar warm-up section between the intro and the conventions would reset the pace.

- **Section `sec-mc-differential` (lines 132 to 203) is the densest in the appendix.** It contains the differential definition, four rules with a combined proof, and three trace properties with a proof, in roughly 70 lines. There is no breathing room, no example, no "let us try this on `f(X) = tr(X)`." A reader who stalls here will stall for the rest of the appendix, because everything downstream uses these rules. This section needs an example interlude.

- **Section `sec-mc-woodbury` (lines 453 to 540) is 90 lines of pure algebra with no application until the very end of the appendix.** The Sherman-Morrison and Woodbury proofs are verification-by-multiplication, which is rigorous but feels like symbol pushing. A reader will lose the thread. An intermediate checkpoint, e.g. "let us verify the rank-one formula on a 2x2 example before proving the general case," would restore intuition.

- **The worked example (Section `sec-mc-example`, lines 663 to 732) comes too late.** By the time I reach it I have processed nine theorems and lemmas with no concrete instance. Moving a small numerical example to immediately after the conventions section (line 100), and a second after the differential rules (line 203), would pace the learning.

- **The summary table (lines 740 to 754) is useful but arrives after the worked example, which already reviews the key identities.** The table is somewhat redundant with the example and could be moved earlier (right after the conventions) as a roadmap, with a pointer back at the end.

## What worked well

- The opening paragraph (lines 5 to 14) honestly tells me where each class of identity is used. This is rare in math appendices and genuinely helpful.
- The decision to prove every identity from the definition (line 13 to 14) is the right call for a book that claims everything is proved in full. The proofs are, as far as I could check, correct.
- The identification lemma `lem-mc-identification` (line 104), once understood, is a genuinely powerful unifying tool. The appendix is organized around a single good idea, not a grab bag.
- The numerical check at the end of the worked example (lines 714 to 727), with explicit 3x3 matrices and arithmetic shown entry by entry, is exactly the kind of verification a weak-math reader needs. More of this elsewhere would transform the appendix.
- Cross-references to book theorems (`@thm-delta-method`, `@def-score`, `@def-quadratic-form`, `@thm-invertibility-characterization`) appear early and often, so I can tell this appendix is wired into the rest of the book.
- The notes-and-references section (lines 756 to 785) names the sources (Magnus and Neudecker, the Matrix Cookbook, Harville) and is honest about what is standard. The final paragraph (lines 778 to 785) mapping identities to downstream chapters is the clearest statement of purpose in the appendix and could profitably be moved up.

## Suggestions

1. **Add a scalar warm-up.** Between the intro (line 30) and the conventions section (line 32), insert half a page recalling the one-variable derivative as `f(x+h) = f(x) + f'(x) h + o(h)` and stating that every definition below is this sentence with the product replaced by an inner product. This single move would reframe the appendix as generalization rather than new material.

2. **State the layout choice and its rival explicitly in the conventions section.** Name numerator and denominator layout, say which we use and why (same-shape, geometrically natural), and warn that papers using the other convention give transposed answers. Put the phrase "denominator (same-shape) layout" from line 738 up at line 32.

3. **Add two short worked examples early.** One immediately after the differential rules (line 203): differentiate `f(X) = tr(X)` and `f(X) = tr(A X)` from scratch using the rules, arriving at `I` and `A^T`. One immediately after the quadratic-form theorem (line 260): a 2-variable numeric quadratic with the gradient computed two ways. Each costs 10 lines and pays for itself many times over.

4. **Add a worked ITC example.** Replace or supplement the compound-symmetry REML example with one drawn from the book's actual subject: e.g. compute the gradient of the MAIC weight objective `sum_i w_i log w_i` with respect to the weight parameters, or the gradient of a Bernoulli log-likelihood with respect to a coefficient vector. This is the example the target reader is here for.

5. **Expand the Hessian definition (lines 76 to 83).** Add: what the Hessian means geometrically (curvature), why symmetry follows (mixed partials, under the `C^2` hypothesis you should define), and why we care in this book (Fisher information is the negative expected Hessian; this links the appendix to `@def-score`).

6. **Break up the dense sections.** Section `sec-mc-differential` (lines 132 to 203) and the symmetric-gradient remark (lines 431 to 451) each want to be two subsections with an example or a displayed intermediate in between.

7. **Define jargon at first use, not deep in a proof.** Adjucate and cofactor at line 22; `C^2` and "open set" at line 41; "capacitance" at line 501; Landau symbols at line 24. A small glossary box at the top of the conventions section would also work.

8. **Add a one-paragraph "why differentials" demonstration.** Show one derivative computed both entrywise and via the differential, side by side, so the reader sees the payoff of the method the appendix is organized around.

9. **Reconcile the bold-matrix convention or flag it.** Either use `mathbf{X}` for matrix variables here to match `notation.qmd`, or state explicitly at line 30 that matrix calculus conventionally uses plain capitals and that this appendix follows that local convention.

10. **Move the final mapping paragraph (lines 778 to 785) up to the intro.** It states the appendix's purpose more clearly than the intro currently does. The intro would then tell me not only that the identities are used downstream but specifically which identity feeds which chapter.