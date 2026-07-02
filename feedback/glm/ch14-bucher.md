# Feedback: Chapter 14 — Bucher's Indirect Comparison

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part3/14-bucher.qmd`

## Overall impression

I came in thinking "indirect comparison" would be the heart of what this book is about, and it is. The chapter is clearly written at the sentence level and the worked example at the end finally let me see the numbers move. But for a self-described foundational ITC method, I spent most of the chapter wondering whether I was actually allowed to understand it. The algebra is gentle (it really is just a subtraction), but the *machinery around the subtraction* is dense, and the text repeatedly tells me the assumption is "load-bearing" without ever slowing down to show me, concretely, what it would mean for it to break in a real drug trial. The result is that I could follow the proofs line by line but could not, on finishing, explain to a colleague why Bucher's method is trustworthy or when it isn't. For *the* core ITC chapter, that is a serious gap.

The biggest recurring problem is that the chapter front-loads abstraction (link-scale positions, marginal link-scale positions, the additive arm decomposition) and back-loads the one concrete example. As a noob I needed the concrete drug-trial story *first*, and the abstraction *attached to it*, not the reverse. The worked example in @sec-bucher-example is excellent and should be a template the chapter refers back to constantly, rather than a reward at the end.

## What was unclear

**The notation order reversal haunts me.** In @sec-bucher-algebra (lines 164 to 175, the remark on index order) you concede that "much applied writing uses the opposite order" and that $d_{AC}=\eta_C-\eta_A$ here. Then in the example (line 635) you compute $\hat d_{AC}=\hat\eta_C^{(AC)}-\hat\eta_A=0.69315=\log 2$ and immediately say "the comparator $C$ has twice the event odds of $A$." As a reader I had to stop and reverse-engineer: so $d_{AC}$ is the effect of *A relative to C* but computed as $\eta_C-\eta_A$? That is the opposite of how I read "$d_{ab}$ is the effect of $b$ versus $a$." The remark at lines 164 to 175 tells me the two orderings carry identical information, but it does not tell me *which sign I should expect a positive number to have*. A one-line table mapping ("$d_{AC}>0$ means $C$ has higher odds than $A$, i.e., $A$ is protective") would have saved me ten minutes of confusion.

**The marginal link-scale position definition (@def-marginal-link-position, lines 55 to 71) is the first real wall.** You write $\eta_{k(\mathcal P)}=g(\int \mu_k(x) f_{\mathcal P}(x) dx)$. I understand each symbol separately but the *operation* is unclear: am I averaging the conditional mean outcome over the covariate distribution, and *then* pushing it through the link? The remark at lines 75 to 85 says "marginalizes first, applies the link second," which helps, but I had to read it three times. A small diagram or a one-sentence gloss in plain English ("first compute the average outcome you'd see in this population under treatment $k$, then transform it to the logit/log scale") would make this landing much softer.

**@prp-trial-unbiased (lines 102 to 110) and its proof (lines 112 to 123) lost me.** The proof invokes ignorability, positivity, the identification theorem, the continuous mapping theorem, and the delta method, all in one paragraph, and concludes "to first order ... it is unbiased." For a noob this is a wall of named results. I do not know what "the conditioning on $X$ vacuous" means (line 114), I do not know why randomization makes $T$ independent of the covariates (line 114), and I definitely do not know what "to first order in the delta-method expansion ... it is unbiased" qualifies. Is it unbiased or only asymptotically unbiased? The statement says $\mathbb E[\hat d]\to d$ (line 109), which is consistency, not unbiasedness, but the proposition title says "unbiased." This conflation needs unpacking.

**The converse direction of @prp-transitivity-consistency (lines 253 to 257) is too terse.** "If two of the three contrasts are constant across populations the third is forced to equal ..." Why two? Which two? Is the assumption that *all three* are constant, or only two? The forward direction is clean; the converse reads like a footnote and I could not reconstruct it.

**@prp-baseline-cancellation (lines 490 to 500) and its proof.** The cancellation is the conceptual heart of why anchoring works, and the algebra is fine, but the *interpretation* of $\mu_j$ as "the link-scale outcome of a reference treatment in study $j$'s population" (line 482) is introduced inside a remark, not a definition, and then used as if it were a defined object. I had to back-read to find it. Also: which reference treatment? Does it matter? If study $AC$ uses $C$ as reference and study $BC$ uses $C$ as reference, is $\mu_{AC}$ the *same kind of quantity* as $\mu_{BC}$? This is never stated.

## What wasn't elaborated enough

**Transitivity (@def-transitivity, lines 205 to 219) is the single most important assumption in the chapter, arguably in the whole book, and it gets one definition and one paragraph.** The text says it is "a population-level analogue of the no-confounding assumption" (lines 221 to 223), which is a beautiful analogy, but it is left at one sentence. For the load-bearing hypothesis I needed: a concrete clinical example of when it holds, a concrete example of when it fails (the chapter defers this almost entirely to @sec-bucher-failure and then to Chapter 16), and a paragraph on how a working researcher *checks* it. The remark at lines 694 to 703 ("What the number means, and what it assumes") is the closest the chapter comes, and it is good, but it arrives 500 lines after the assumption is introduced.

**The additive arm decomposition (@eq-bucher-decomp, lines 477 to 488) is introduced in a remark and then powers the entire cancellation section.** This is too important to be a remark. I need a definition box, a picture (three studies, each with its own $\mu_j$ and shared $\alpha_k$), and a sentence connecting it to the network meta-analysis model I will see in Chapter 15. Right now it feels like a notational trick pulled from a hat.

**The "price of indirectness" (@cor-bucher-efficiency, lines 446 to 461).** The proof is two lines of algebra, but the *meaning* deserves more. The remark at lines 685 to 692 does this well for the example, but the corollary itself is stated abstractly. A sentence like "this is why an indirect comparison with a tiny $B$-versus-$C$ trial can be useless even if both direct trials are individually significant" before the example would prime the reader.

**@sec-bucher-failure (lines 705 to 734) is remarkably short for what it acknowledges is the central failure mode of the entire book.** It describes the mechanism in one paragraph (lines 714 to 726), then says "Chapter 16 makes this calculation explicit." As a noob I wanted at least one numeric illustration here, in the chapter that just taught me the method, of the bias being *some specific number*, not a deferred promise.

## Missing motivation / "why does this matter?"

The introduction (@sec-bucher-intro, lines 5 to 43) is good at naming the clinical scenario, but it never gives a *named disease and named drugs* example. "A regulator must decide whether a new drug $A$ is better than an established drug $B$" is abstract. I wanted something like: "Consider a new statin $A$ versus an older statin $B$, both compared against placebo $C$ in separate trials. No head-to-head trial exists. How should a health technology assessment decide?" This is the canonical ITC situation and the chapter never grounds it in one.

**Why prove @lem-relative-effect-algebra at all?** It is algebraically trivial (lines 151 to 162). The remark at lines 164 to 175 and the closing remark at lines 375 to 383 do eventually explain that the *subtraction is licensed* by the assumption, but at the point the lemma is stated (line 138) I had no idea why a book would devote a theorem box to $d_{ab}=-d_{ba}$. A one-sentence motivation *before* the lemma, pointing forward to the variance and cancellation results, would help.

**Why is the unanchored comparison worth a formal definition (@def-unanchored-comparison, lines 284 to 294) and a bias proposition (@prp-unanchored-bias, lines 521 to 534)?** The chapter never tells me, at the point of definition, that anyone actually does this. It is only at line 553 ("the whole reason anchored indirect comparison is the default") that I learn the unanchored comparison is a *foil*. Saying so up front would give the section a purpose.

**The link to transportability (lines 731 to 734) is one sentence.** Given that Chapter 12 is supposedly the transportability chapter and this is the load-bearing assumption, I expected at least a paragraph explaining the bridge, not a cross-reference.

## Missing examples and intuition

**There is exactly one worked example (@exm-bucher-logor, lines 607 to 672) and it is on the log odds-ratio scale only.** The exercises ask about hazard ratios (@exr-bucher-recompute, lines 777 to 783) and risk ratios (@exr-bucher-scales, lines 792 to 799), but the body of the chapter never shows the same subtraction working on a different scale. Since the whole point is "contrasts add on the link scale," seeing the identical arithmetic on a log hazard ratio would cement the abstraction.

**There is no diagram of the triangle.** The phrase "the algebra is the algebra of a triangle" (line 19) is evocative but there is no figure. A simple picture: three nodes $A$, $B$, $C$, with the available edges $AC$ and $BC$ drawn solid and the missing edge $AB$ drawn dashed, would make the entire chapter easier to navigate, especially the cancellation section.

**The cancellation mechanism (@prp-baseline-cancellation, @prp-unanchored-bias) cries out for a numeric illustration** using the same kind of two-by-two setup as the main example. Instead the only numeric cancellation practice is an *exercise* (@exr-bucher-unanchored, lines 801 to 808). Putting a small numeric "anchored vs unanchored on the same data" side-by-side in the body would make the bias concrete.

**No intuition for why the variance *adds*.** @thm-bucher-variance (lines 413 to 424) is proved in two lines, and the corollary on efficiency follows, but I never got the intuition that "independent uncertainties accumulate." A sentence pointing back to the Pythagorean intuition (uncertainties add in quadrature when independent) would help a noob who remembers a little physics.

## Notation and jargon problems

**"Link-scale position" (line 59) is jargon coined in this chapter.** It is not in `notation.qmd`. A reader who skips ahead will not find it defined anywhere else. Either add it to `notation.qmd` or define it more gently here.

**$\eta_{k(\mathcal P)}$ versus $\eta_{ijk}$ in `notation.qmd` (line 125).** The notation file defines $\eta_{ijk}$ as "linear predictor for individual $i$ in study $j$ on arm $k$," but this chapter uses $\eta_{k(\mathcal P)}$ for the *marginal* link-scale position. These are different objects with confusingly similar symbols. The chapter should flag the distinction explicitly.

**$\mu_j$ overloading.** In `notation.qmd` line 127, $\mu_j$ is "study-$j$ baseline (intercept)." In this chapter (line 482) $\mu_j$ is "the link-scale outcome of a reference treatment in study $j$'s population." Are these the same? If so, say so; if not, the reuse is dangerous.

**"Square-integrable" (line 394) is used without definition.** A noob with basic calculus does not know this term. A parenthetical "(finite variance)" would fix it.

**"Homoskedastic random-effects model" (line 442) and "the correlation is exactly one half" (line 443).** This is dropped in without setup and deferred to @thm-re-nma-correlation. Either remove the half-sentence or give the one-sentence intuition now.

**"Ecological bias" (line 723, @def-ecological-bias).** The term is introduced in a forward reference with no gloss. A noob does not know what it means.

**"Node-splitting" (line 702, line 729).** Same problem: introduced by forward reference with no inline gloss.

## Pacing issues

**The chapter front-loads three abstract sections (@sec-bucher-scale, @sec-bucher-algebra, @sec-bucher-transitivity) before any estimator is named.** The Bucher estimator itself only appears at line 277 (@eq-bucher-estimator), roughly a third of the way in. For the *foundational* ITC method I expected to meet the estimator early and then learn why it works. The current order is: define marginal effects, prove they add, define transitivity, *then* name the estimator. Reversing to "here is the estimator, here is the triangle, here is why it is unbiased, here is the assumption that licenses it" would be far friendlier.

**@sec-bucher-logodds (lines 561 to 600) interrupts the flow.** After the cancellation section I was ready for the worked example, but instead I got a delta-method derivation of the log-odds variance. This is necessary material, but it is technical and breaks the momentum toward the example. It might sit better as an appendix callout or a boxed "we will need this" result stated without proof, with the proof in an appendix.

**The proof of @prp-logodds-variance (lines 581 to 599) is the densest in the chapter** and it is not central to Bucher's theorem. A noob who has just struggled through transitivity does not need a delta-method derivation here. Stating the variance formula and pointing to Chapter 5 for the derivation would keep the chapter focused on ITC.

**The notes section (lines 736 to 773) is excellent but very long.** It is useful for a researcher but its length, at the end of an already dense chapter, contributes to fatigue. Consider trimming the catalogue cross-references.

## What worked well

The introduction's clinical framing (lines 7 to 13) is exactly the right tone and immediately tells me why the chapter exists. The "disarmingly simple" paragraph (lines 15 to 25) is the best piece of exposition in the chapter: it states the estimator in one line, names the assumption, and tells me the rest of the book is the study of when the assumption fails. That is a model of clarity.

The worked example @exm-bucher-logor (lines 607 to 672) is genuinely excellent. Every number is checkable by hand, the five-step structure is easy to follow, and the three closing remarks (lines 676 to 703) tie the numbers back to the theory beautifully. The "price of indirectness, concretely" remark (lines 685 to 692), showing two significant direct comparisons combining into an uninformative indirect one, is the single most illuminating paragraph in the chapter.

The "Where each hypothesis is spent" remark (lines 365 to 373) is outstanding and should be a template for other theorem proofs in the book. Telling me exactly which assumption is used at which step, and naming transitivity as the weak link, is exactly what a noob needs.

The exercises are well designed: @exr-bucher-recompute and @exr-bucher-tables give practice, @exr-bucher-scales forces engagement with the link-scale idea, and the starred exercises (@exr-bucher-correlated, @exr-bucher-transitivity-bias) point forward meaningfully.

## Suggestions

1. **Open with a named clinical example** (a specific disease and drug class) and refer back to it throughout. Keep $A$, $B$, $C$ as the symbols but anchor them to a concrete scenario in the first paragraph.
2. **Add a triangle figure** with nodes $A$, $B$, $C$, solid edges $AC$ and $BC$, dashed edge $AB$. Reference it in @sec-bucher-intro and @sec-bucher-algebra.
3. **Introduce the Bucher estimator earlier**, around line 19, even before transitivity is formalized, so the reader has a concrete object to attach the abstraction to.
4. **Promote the additive arm decomposition (@eq-bucher-decomp) from a remark to a definition**, with a small figure showing shared $\alpha_k$ and study-specific $\mu_j$.
5. **Expand @def-transitivity with a clinical example** of holding and failing, in the body, not deferred to @sec-bucher-failure or Chapter 16.
6. **Add a one-line sign-convention table** near @sec-bucher-algebra so readers know what a positive $d_{ab}$ means in the chosen orientation.
7. **Add a small numeric anchored-vs-unanchored side-by-side** in @sec-bucher-cancellation using the same tables as the main example, so the bias is seen, not just algebraized.
8. **Move the log-odds variance derivation (@prp-logodds-variance proof) to an appendix or state it without proof**, keeping the chapter focused on the ITC content.
9. **Soften @prp-trial-unbiased**: separate consistency from unbiasedness, and either prove less or prove more slowly, not both.
10. **Add inline one-sentence glosses for "ecological bias," "node-splitting," "homoskedastic random-effects," and "square-integrable"** at first use.
11. **Reconcile the $\mu_j$ and $\eta$ notations** with `notation.qmd` explicitly, or add the new symbols to `notation.qmd`.
12. **Expand @sec-bucher-failure** with at least one numeric bias illustration, even a small one, so the reader leaves the chapter having seen the failure mode, not just been told it exists.