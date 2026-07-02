# Feedback: Chapter 06 — Linear Regression

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation. I can do derivatives and I once fit a regression in R, but I do not know what a quadratic form is, I have never seen a spectral theorem, and I am reading this book because I want to actually understand the MAIC/STC/ML-NMR papers I keep citing.
**File:** `chapters/part1/06-linear-regression.qmd`

## Overall impression

I made it through, but only because I read each proof three times. This chapter is beautiful and clearly written by someone who really loves the geometry of least squares, but it is written for a mathematician, not for me. The intro (lines 7 to 26) promised me that everything would be motivated and that I would understand *why squares*, and by the end I sort of did, but the journey there lost me several times. The biggest problem is not rigor, it is that the ITC/health-research thread announced in the introduction completely vanishes for roughly 900 lines and only reappears briefly in the notes (lines 1113 to 1119). I spent most of the chapter wondering "why am I being shown this?" until I forgot why I started.

The worked example in @sec-lr-example (lines 1007 to 1094) is the best part of the chapter and I wish there had been three more like it scattered throughout. As written, the first 1000 lines are wall-to-wall theorem-proof-remark with almost no contact with reality.

## What was unclear

**The introduction's "four optimality principles" claim (lines 22 to 26).** I was told that under normal, homoskedastic, independent errors the least-squares estimator is "simultaneously the projection of the data onto the model space, the best linear unbiased estimator, the maximum likelihood estimator, and the minimum-variance unbiased estimator of every linear functional." As a noob I read this four times and could not keep the four things apart, because they were not named or ordered. It would help enormously to enumerate them as (i) projection, (ii) BLUE via Gauss-Markov, (iii) MLE, (iv) UMVU via Cramér-Rao, and say one sentence on *why* each is a different statement (one is geometric, one is among linear estimators with only two moments, one is likelihood-based, one is among *all* unbiased estimators). As written the sentence is a wall of jargon I cannot parse on first read.

**G2 "homoskedasticity and no correlation" (lines 52 to 54).** I now know what homoskedasticity means, but the very first time I met it (here) I did not. The phrase "equal variances across units" (line 68) helps, but there is no picture and no data example. What does heteroskedasticity *look like*? When would a health researcher expect it? (Clustered trials? Baseline covariates with different scales?) The remark at lines 69 to 72 mentions the sandwich variance repair but I do not yet know what that is, so the forward-reference lands flat.

**The rank-nullity argument in @lem-gram-nullspace (lines 96 to 118).** This is the "algebraic hinge of the whole chapter" and it is the first place I genuinely got stuck. The proof has three separate conclusions (null spaces equal, ranks equal, column spaces equal, positive definiteness) all crammed together, and the step "the two spaces have the same dimension by the rank identity just proved together with rank(Xᵀ)=rank(X)" (line 111 to 112) took me a long time to unpack. For a noob it would help to split this into three short lemmas or at least three labeled paragraphs, and to spell out why rank(Xᵀ)=rank(X) is being invoked.

**@thm-ols-normal-equations proof, the "if and only if" (lines 173 to 188).** The expansion S(b)-S(β̂)=||Xd||²≥0 is clean but I lost the logic of the iff. The text says "every solution of the normal equations is a global minimizer" and then "conversely, if β̂ is a minimizer then ∇S(β̂)=0". I needed an explicit sentence: forward direction (NE ⇒ global min) is the ||Xd||² argument; reverse direction (global min ⇒ NE) is the first-order condition. The two are bundled into one paragraph and the reader has to do the disentangling.

**The consistency argument (lines 189 to 192).** "the right-hand side lies in the column space of the coefficient matrix" is asserted with no picture. I had to draw it. A one-sentence gloss in plain English ("the normal equations are always solvable, they just may not have a unique solution") would save the noob reader a lot of pain.

**@thm-rss-chisq proof (lines 557 to 583).** This is the distributional heart of the chapter and it is the hardest proof for me. The spectral theorem step "idempotence forces each eigenvalue to satisfy λᵢ²=λᵢ, hence λᵢ∈{0,1}" (line 561 to 562) is correct but I had to convince myself of it separately. More importantly, the reordering step "Reorder so that Λ=diag(I_{n-p},0)" (line 564) hides a nontrivial fact: *why* are there exactly n-p unit eigenvalues? The text says "the number of unit eigenvalues equals rank(M)=tr(M)=n-p" but the claim "rank of an idempotent equals its trace" is waved at parenthetically ("by the same eigenvalue argument") rather than stated as its own mini-lemma. For the reader who is meeting idempotent projections for the first time, this is the crux and it deserves its own named result.

**@thm-ftest proof (lines 689 to 738).** The identity H₁H₀=H₀H₁=H₀ (lines 691 to 694) is asserted with a parenthetical justification I could follow, but the step "P²=(H₁-H₀)²=...=H₁-H₀=P" (lines 696 to 697) expands four terms in one line and I had to write it out myself. Then the independence argument stacks Pε and M₁ε and computes cross-covariance σ²PM₁=0, but I had lost track of *why* P and M₁ project onto orthogonal subspaces; that was shown two paragraphs up (PM₁=0) but the connection "PM₁=0 ⇒ the subspaces are orthogonal ⇒ the projected Gaussians are independent" is not spelled out.

**The general linear hypothesis remark (lines 750 to 753).** The statistic F=(Rβ̂-q)ᵀ[...]⁻¹(Rβ̂-q)/(qs²) is dropped into a remark with the note "Exercise @exr-lr-general-hypothesis develops this form." This is the *most useful* form of the F test for a health researcher (it is what `linearHypothesis()` in R computes) and it is exiled to a starred exercise. I think this deserves a proper theorem statement, not a remark-plus-exercise.

**@prp-rank-deficient-pseudoinverse part (2) (lines 977 to 981).** "a linear functional cᵀβ is invariant across solutions if and only if c∈C(Xᵀ) (such functionals are called estimable)." The word **estimable** is introduced in a parenthetical with no definition box, no example, and no forward signposting, even though the remark at lines 1002 to 1004 promises it will return "in network meta-analysis and population adjustment" in Part III. This is a load-bearing concept for the rest of the book and it is buried.

## What wasn't elaborated enough

**The hat matrix motivation (lines 233 to 241).** H is defined, then immediately 5 properties are proved. But *why* should I care about H? The only hint is the parenthetical "it puts the hat on y." For a noob: the diagonal h_ii tells you how much observation i pulls its own fit; this is the basis of leverage, Cook's distance, and every regression diagnostic I have ever seen. The leverage concept is exiled to @exr-lr-leverage (lines 1142 to 1147). Given how central leverage is to regression diagnostics in practice, it should at least be named in the main text, not hidden in an exercise.

**The trace trick (lines 444 to 452).** "a scalar equals its own trace, and the trace is linear and cyclic" is stated as folklore. I have seen this trick before but a weak-math reader has not. It deserves a one-line lemma earlier (or a forward reference to Chapter 1) because it is used in at least two proofs (@thm-sigma2-unbiased and implicitly elsewhere).

**Moment generating function facts (lines 469 to 473).** The two MVN lemmas are proved in full, which I appreciate, but the *use* of the MGF is itself a black box for me. Why does the MGF determine the distribution? Why is factorization of the joint MGF into marginals equivalent to independence? These are stated as "both facts are established in Chapter 4" (line 472 to 473), which is fine, but a one-line intuition would help the reader who has not yet absorbed Chapter 4.

**The profile likelihood argument (lines 866 to 883).** "Crucially this minimizer does not depend on σ², so it is the joint maximizer's β-coordinate as well" is the key insight of profile likelihood, and it is dispatched in one sentence. For a noob this is the most non-obvious step in the whole MLE proof. A sentence like "because the β that maximizes ℓ for any fixed σ² is the same β regardless of σ², that same β must maximize the joint likelihood" would make it click.

**The Cramér-Rao statement (lines 890 to 923).** The block-diagonal information argument (lines 920 to 923) is compressed to two lines and assumes I remember what "the β-block of the inverse information is unchanged" means. I do not, not really. This is the capstone optimality theorem of the chapter and it is the tersest part.

## Missing motivation / "why does this matter?"

**Why squares? — answered too late.** The intro (lines 19 to 21) explicitly asks "why squares? Why minimize the sum of squared residuals rather than, say, the sum of absolute residuals?" This is a fantastic hook. But the answer is deferred until @sec-lr-mle (line 830), roughly 800 lines later. Between the question and the answer I have learned projection, Gauss-Markov, the t and F tests, ANOVA, and R², all without ever being told why I am squaring. A one-paragraph "preview of the answer" right after the question (lines 21 to 22) would keep me going: "we will see in @sec-lr-mle that under Gaussian errors minimizing squares is exactly maximum likelihood; absolute residuals would correspond to a Laplace error model instead."

**Gauss-Markov: why do I care that it is BLUE?** @thm-ols-blue is proved beautifully but the *motivation* is missing. Why does "best among *linear* unbiased estimators" matter to me as a health researcher? The remark at lines 411 to 416 hints that under normality we can drop the "linear" qualifier, but the practical payoff ("so when you run `lm(y ~ x)` and read the standard errors, you are getting the best you can do without stronger assumptions") is never stated in plain language.

**The t and F tests: where is the health example?** @thm-ttest and @thm-ftest are proved in full generality but there is no example like "we fit a model of blood pressure on dose and three covariates; here is the table; here is what T_j=2.5 means; here is the F test for the global null." The worked example at the end (lines 1007 to 1094) is for simple linear regression with n=5 and abstract x and y. It verifies the arithmetic but it does not connect to anything I care about.

**ITC connection is essentially absent.** This is my biggest single complaint. The introduction (lines 7 to 14) makes a compelling promise: every population-adjustment method is at its core a regression. That promise is not honored until the notes (lines 1113 to 1119), 1000 lines later. There is no intermediate reminder. A reader like me, by line 600, has forgotten why we are proving all this. I would love to see, for example after @thm-ols-normal-equations, a short callout: "In STC (Chapter 19) we will fit exactly this model on IPD and then evaluate Xβ̂ at the comparator trial's mean covariates; the normal equations are what makes that prediction well-defined." Or after @thm-ols-blue: "MAIC (Chapter 18) replaces XᵀX with a weighted version; the Gauss-Markov logic is what tells us the weighted estimator is still optimal under its own assumptions."

**Why prove everything?** The CLAUDE.md says every result is proved in full, which is a laudable goal, but the chapter never tells the *reader* why. A noob health researcher will skim the proofs. A sentence in the intro like "we prove these results in full because every later chapter leans on them; if you trust the formulas you may skip the proofs on first reading, but the proofs are here so that nothing downstream is a black box" would set expectations.

## Missing examples and intuition

- **No data example until line 1007.** A small numeric example right after @thm-ols-normal-equations (showing X, XᵀX, (XᵀX)⁻¹, β̂) would make the formula concrete immediately, instead of 850 lines later.
- **No picture.** The projection derivation (lines 196 to 218) is geometric and cries out for a figure: y as a point in Rⁿ, C(X) as a plane, ŷ as the foot of the perpendicular, r orthogonal. There is no figure anywhere in the chapter. For a noob this is the single most helpful thing that could be added.
- **No picture of the ANOVA decomposition.** @prp-anova-decomposition (lines 762 to 789) is a right-triangle Pythagorean statement. A figure showing the orthogonal decomposition of the centered y into its regression component and its residual component would make R² instantly intuitive.
- **No picture of the chi-squared argument.** @thm-rss-chisq rotates the coordinate system so M becomes diagonal; a figure showing the n-p "free" directions versus the p "constrained" directions would make the degrees-of-freedom divisor stick.
- **No causal / health example.** Even one sentence like "suppose y is change in HbA1c and X contains treatment indicator, baseline HbA1c, age, and sex; then β_treatment is the adjusted treatment effect and the F test asks whether the model beats the intercept-only model" would ground the whole chapter.
- **The remark at lines 220 to 229** mentions QR factorization for numerical stability but gives no example. A noob who has used `lm()` does not know that R never forms XᵀX explicitly. One sentence on what `lm()` actually does would connect the theory to the tool.

## Notation and jargon problems

- **"Loewner sense" / "matrix sense" / "positive semidefinite difference" (lines 354 to 356).** The term "Loewner order" is introduced in a parenthetical with no definition. notation.qmd defines A⪰0 and A≻0 but not the Loewner partial order. A noob will not know that "Cov(tilde)-Cov(hat)⪰0" means "every linear functional of tilde has variance at least as large." This is stated two lines later but the jargon comes first.
- **"Estimable" (line 958).** Introduced in a parenthetical, no definition box, see above.
- **"Quadratic form" (line 163).** Referenced as @def-quadratic-form (so presumably defined elsewhere) but a noob meeting it here for the first time gets no gloss. The gradient/Hessian computation at lines 164 to 168 is the first multivariable calculus in the chapter and it is dense.
- **"Whitening" (line 1176, exercise hint).** Used in @exr-lr-general-hypothesis with no definition anywhere I could find in notation.qmd.
- **"Profile log-likelihood" (line 868).** Standard term, but a noob has not met it. One sentence: "substitute the maximizing β̂ back into ℓ to get a function of σ² alone."
- **Notation conflict risk:** notation.qmd lists ESS as "effective sample size" for weighting methods (line 139) AND ESS_reg as explained sum of squares (line 56). The chapter uses ESS_reg consistently, which is good, but the reader of the whole book will meet both and the similarity of the abbreviations is a genuine trap. The footnote at lines 60 to 62 of notation.qmd flags this, but a remark in the chapter itself when ESS_reg is first used (line 137) would help.
- **"Effective sample size" appears in notation.qmd but the chapter never uses it**, which is fine, but it means a reader cross-checking notation.qmd against this chapter will be confused about why ESS (without subscript) is listed.

## Pacing issues

- **The first 1000 lines have essentially one example, and it is at the very end.** The pacing is theorem-proof-remark, theorem-proof-remark, for nine sections. A noob cannot absorb this much abstraction without intermittent contact with numbers. Inserting the worked example earlier, or breaking it into pieces (arithmetic after @thm-ols-normal-equations, t-test after @thm-ttest, F-test after @thm-ftest), would dramatically improve readability.
- **@sec-lr-normal (lines 465 to 623) is very long and dense.** It proves two MVN lemmas, then normality of β̂, then chi-squared of RSS, then independence of β̂ and s². This is four distinct results packed into one section with two supporting lemmas up front. Splitting it into "supporting MVN facts" and "the three distributional pillars" would help.
- **The MLE section (@sec-lr-mle, lines 830 to 936) crams three results into one section:** OLS=MLE, the profile likelihood for σ², and the Cramér-Rao efficiency. Each deserves its own subsection header.
- **The rank-deficiency section (@sec-lr-rank, lines 938 to 1005) comes after the worked example would naturally have ended the chapter.** A noob is tired by this point. The estimability concept is important enough that it might belong earlier, or at least be flagged as "the concept you will need for Part III."
- **The exercises are good but unevenly starred.** @exr-lr-gm-weighted and @exr-lr-general-hypothesis are starred (hard) and are exactly the ones a health researcher would most benefit from (weighted least squares is the bridge to MAIC; the general linear hypothesis is what `linearHypothesis()` does). Consider making them not-starred or providing more hint.

## What worked well

- The two-derivations structure (@sec-lr-ols, lines 120 to 229) is excellent. Seeing calculus and projection give the same answer, with the remark at lines 220 to 229 explaining *why* they agree, was the moment the geometry clicked for me.
- The worked example (lines 1007 to 1094) is gold. Every number checks out, the F=T² identity is verified numerically, and the eigenvalue structure of M is illustrated concretely. This is the template for what the rest of the chapter needs.
- The remark at lines 458 to 463 explaining the n-p divisor geometrically ("the residual lives in the (n-p)-dimensional space") is exactly the kind of intuition I want everywhere.
- The remark at lines 616 to 623 on *why* independence is Gaussian-specific ("the rotational symmetry of the isotropic normal") is lovely and I wish more proofs had this kind of one-line "here is the picture" coda.
- The cross-referencing is thorough and consistent; I could always find where a cited result lived.
- The honest note at lines 1121 to 1123 that this chapter has no Coq counterpart is good scholarly hygiene.
- The notes section (lines 1096 to 1123) honestly credits Strang and Bingham-Fry and is clear about what is standard versus what was proved here.

## Suggestions

1. **Add at least two figures:** one of the projection geometry in @sec-lr-ols, one of the ANOVA right-triangle in @sec-lr-anova. These two pictures carry more intuition than any proof.
2. **Move (or duplicate) the worked example's arithmetic earlier.** Insert the computation of β̂, the residuals, and RSS right after @thm-ols-normal-equations; keep the t-test, F-test, and eigenvalue portions at the end.
3. **Add a one-paragraph "preview of why squares" immediately after the question at line 21**, pointing to @sec-lr-mle, so the reader does not spend 800 lines wondering.
4. **Thread the ITC connection through the chapter, not just the intro and notes.** After each major theorem, one sentence on what it buys you in MAIC/STC/ML-NMR. Specifically: after @thm-ols-normal-equations, mention STC's predict-at-comparator-population step; after @thm-ols-blue, mention that MAIC's weighted estimator is the GLS analogue (and forward-reference @exr-lr-gm-weighted); after @prp-rank-deficient-pseudoinverse, mention estimability of treatment contrasts in NMA.
5. **Promote "estimable" to a definition box** (a `::: {#def-estimable}` block) in @sec-lr-rank, with a one-sentence example.
6. **Promote the general linear hypothesis to a stated theorem** rather than a remark-plus-exercise; it is the form practitioners actually use.
7. **Add a short "diagnostics" remark** near @def-hat-matrix naming leverage and pointing to @exr-lr-leverage, so the hat matrix is not purely abstract.
8. **Define "Loewner order" explicitly** the first time it is used (line 355), or add it to notation.qmd.
9. **Add at least one health-flavored example**, even if small: HbA1c on treatment and baseline covariates, or log-odds on dose. Abstract x and y throughout makes the chapter feel like a pure-math text rather than a math-for-ITC text.
10. **Split @sec-lr-normal into subsections** (MVN lemmas; normality of β̂; chi-squared RSS; independence) so the reader has intermediate resting points.
11. **Soften the expectation that every proof is read linearly.** A note in the intro that proofs may be skipped on first reading without losing the through-line would help a noob who is drowning.