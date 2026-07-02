# Feedback: Chapter 12 — Transportability

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part2/12-transportability.qmd`

## Overall impression

I am a health researcher who has run a few MAICs in R and read a couple of NICE technical support documents. I came to this chapter wanting to understand *why* people say a shared effect modifier assumption makes relative effects "transportable." The chapter does eventually answer that, and the worked binary example (lines 787 to 823) genuinely made the central paradox click for me: the conditional odds ratio is 7.389 in both populations but the marginal is 3.24 in one and 1.86 in the other. That hit hard. But getting there was a slog. The chapter front-loads a lot of abstract machinery (population-as-distribution, structural invariance, link functions, scale alignment) before I had any concrete picture of what a "transport" actually *is* operationally, and several proofs lean on calculus moves (strict concavity, Jensen's inequality, change of measure) that are stated but not unpacked for a reader like me. The domain connection to HTA is strong in the intro and the two-step section but fades in the middle, exactly where I most needed it. By the end I understood the thesis; for the first two thirds I was often lost.

## What was unclear

- **The very first definition, `def-transport-invariance` (lines 79 to 91).** I can parse the equation `E[Y(t) | X=x, S=s] = mu_t(x)`, but the phrase "mean independent of population membership given the covariates" is thrown at me with no warmup. A one-sentence gloss in plain English ("once you know a patient's covariates, knowing which trial they came from tells you nothing more about their expected outcome under treatment") would have saved me a re-read. The analogy to conditional exchangeability at lines 93 to 98 helps, but it comes *after* the definition, and it itself uses jargon ("mean independent of treatment given covariates") that I had to reconstruct from Chapter 9.

- **`def-transportability` (lines 147 to 164), mode 2.** "Recovered by re-standardizing the source conditional model to the target covariate distribution" is the key operational idea of the whole chapter, and it is stated in one clause. I did not know what "re-standardizing" meant until I reached the transport g-formula two sections later. The definition should either point forward ("made operational in @thm-conditional-transportability") or include a one-line concrete sketch.

- **The support/overlap condition in `thm-conditional-transportability` (iv), lines 305 to 307.** "The target covariate support is contained in the source support" is stated symbolically, but I had to stop and think about what it means for a binary covariate. An aside like "if the target has old patients the source never enrolled, you cannot transport to them" would make this land. The overlap idea is load-bearing and returns in MAIC/STC; it deserves intuition.

- **The re-weighting identity `eq-transport-ipw` (lines 314 to 320).** Two things confused me. First, the jump from `E_{X~P*}[mu_t(X)]` to `E_{X~P}[w(X) mu_t(X)]` is a change of measure, and the proof at lines 339 to 345 does it in two lines. As a weak-measure-theory reader I wanted the line "we are rewriting an average over the target as a weighted average over the source, where the weight is how much more likely that covariate value is in the target than the source." That sentence is the whole intuition for MAIC and it is absent. Second, the second equality replacing `mu_t(X)` with `1{T=t} Y / e_t(X)` arrives with only the citation `@thm-ipw-unbiased`; I have not yet internalized IPW from Chapter 10 well enough for this to be obvious, and a half-line of algebra in-line would help.

- **`thm-scale-alignment` part (ii) proof, lines 545 to 562.** This is the hardest proof in the chapter for me. The move "because psi is not affine, there is a point eta* with psi''(eta*) != 0" assumes I instinctively connect "not affine" to "has nonzero second derivative somewhere," which is true but not obvious to a basic-calculus reader. Then "for a suitable nonzero c the difference Delta'(eta) = psi'(eta+c) - psi'(eta) != 0" is a mean-value-ish argument that is sketched, not shown. I believe the conclusion but I could not reproduce this proof, and the prose at lines 565 to 570 ("misalignment manufactures effect modification") is the chapter's most counterintuitive claim, so I wanted it nailed down with a tiny concrete psi like expit before the abstract argument.

- **The "anchored subtraction of @thm-bucher-unbiased" invoked at line 393 and again at line 431.** I gather from Chapter 14 context that Bucher's identity lets you subtract two relative effects that share a common comparator. But here it is used as a black box to justify `d_BC = d_1C - d_1B` *within a single population*. A one-line reminder ("because both contrasts share reference arm A and are defined in the same population f_AC, the Bucher subtraction applies") is there at 431, but I still was not sure why sharing a population matters for the subtraction. The population-specificity is the whole point of the chapter, so this step deserves more than a citation.

- **`eq-two-step-bias` (lines 409 to 418) and its proof.** The decomposition itself is just inserting and removing `d_BC(AC)`, which I followed. What I did not follow is why "Step 1 term vanishes in expectation under correct specification and overlap" is stated without a short justification (lines 416, 442 to 444). The phrase "under correct specification, overlap, and the consistency of the weighting or regression estimator it has mean zero" packs a semester of estimation theory into a clause.

## What wasn't elaborated enough

- **The structural invariance assumption and how it relates to SEMA.** Lines 99 to 103 flag the failure mode (omitted effect modifier distributed differently across populations), which is great. But invariance is then assumed throughout, and SEMA (`eq-transport-sema`, line 489) is introduced much later as a *separate* equality of interaction vectors. I spent the middle of the chapter unsure whether invariance and SEMA are the same, whether SEMA implies invariance, or whether they are orthogonal. A short paragraph explicitly relating them ("invariance says the conditional mean function is shared; SEMA says the *effect modification* part of that function is identical for the two active treatments; SEMA is a restriction on the form of the shared function, not a replacement for invariance") is badly needed.

- **`lem-collapsible-scales` (lines 232 to 272), part 2, the log scale.** The proof constructs weights `w_a(x) = mu_a(x) f_P(x) / m_a` and shows the marginal risk ratio is a weighted average of conditional risk ratios. This is the technical heart of "risk ratios transport." But the weight definition comes out of nowhere; I did not see why those particular weights. A sentence ("we weight each stratum by its contribution to the reference-arm risk") would make the construction feel motivated rather than magical. Part 3 (lines 247 to 251) is essentially deferred to `thm-noncollapsibility-or-hr` from Chapter 11, which is fine for the theorem statement but leaves a reader who skimmed Chapter 11 unable to follow the lemma's own proof.

- **The "direct collapsibility" remark (lines 274 to 282).** It distinguishes "direct collapsibility" (identity scale, population weights) from the weaker log-scale version (reference-mean weights). I read it three times and still cannot articulate *why* the weaker version is enough for direct transportability. The remark says "it still delivers the one consequence direct transportability needs, that a constant conditional effect passes unchanged to the margin," but that is the conclusion, not the mechanism. Expanding by one sentence why the weaker property suffices would close the gap.

- **The conditional transportability advantage discussion (lines 636 to 639).** "The conditional effect needs two conditions, SEMA and alignment; the marginal effect, for a non-collapsible measure, needs a third that it cannot have." This is one of the most decision-relevant sentences in the chapter, and it is two lines. I wanted a worked mini-example showing the conditional log odds ratio transporting while the marginal does not, ideally right before `cor-conditional-transport`, because the corollary's proof (lines 628 to 634) is so short it feels like a trick.

- **The RMST worked example (lines 835 to 877).** The numbers are there and reproducible, but the conceptual point, that a collapsible measure can still fail to transport via misalignment, is stated at 870 to 877 in a rush. Given that this is the *third* failure mode and the one most readers will have never encountered, a short paragraph before the computation saying "watch how the conditional hazard ratio is constant 0.5 at both x, yet the conditional RMST difference is 0.310 at x=0 and 0.374 at x=1, so the failure is already visible *before* marginalization" would set up the punchline. Right now the punchline and the setup arrive together.

## Missing motivation / "why does this matter?"

- **The whole `sec-transport-setup` section (lines 58 to 103) is formal-first, motivation-second.** I get the HTA framing from the introduction, but once we hit "a population is a probability distribution" (line 62) the domain vanishes for several paragraphs. Why is it useful to treat a population as a distribution rather than as "the patients in trial X"? Because two trials with the same eligibility criteria can still have different covariate distributions, and the distribution is what the math needs to operate on. That motivation is implicit; it should be explicit before `def-transport-invariance`.

- **`thm-direct-transportability` (lines 183 to 218).** The theorem gives two sufficient conditions, (a) equal distributions and (b) constant conditional effect on a collapsible scale. Condition (a) is dismissed in one sentence at line 220 as "rarely available." But *why* prove it at all, then? The motivation is that (a) is the silent assumption of unadjusted indirect comparison and Bucher, so naming it lets us see what those methods are really assuming. That is said at lines 176 to 181, but only before the theorem, not connected back after. A sentence after the proof ("condition (a) is the unstated premise of every Bucher comparison; condition (b) is what population adjustment tries to engineer") would tie the theorem to its purpose.

- **The two-step decomposition `thm-two-step-transport` (lines 396 to 419).** This is the chapter's organizing insight and it is beautifully stated, but I never got a clear statement of *why HTA practice ignores Step 2*. The remark at lines 458 to 466 ("why two sponsors can disagree") is excellent and should be in the main text, not a remark, because it is the concrete HTA payoff. More generally, the chapter could use a short "what this means for a reimbursement submission" paragraph after the two-step theorem: the standard MAIC report delivers `d_BC(AC)`, the decision maker wants `d_BC(P*)`, and the gap is usually unmentioned.

- **`thm-sema-insufficient` (lines 649 to 707).** The theorem is the negative result and is well proved, but its HTA stakes are understated. The intro promised (lines 33 to 35) that "the measures we most want to transport are precisely the ones that resist transport," and the theorem delivers that, but the connection back to "this is why two NICE submissions with the same trials can disagree on an odds ratio" is left to the reader. A closing sentence tying the strict-attenuation formula `eq-or-attenuation` to a real HTA decision would land the point.

- **Why prove necessity at all (the "only if" direction of `thm-sema-insufficient`)?** As a naive reader I wondered why we bother proving that non-collapsible measures *cannot* transport marginally under SEMA, rather than just showing the odds ratio fails in an example. The answer, that a single counterexample only shows failure is possible while necessity shows *no* choice of constants avoids it, is the kind of "why a theorem, not just an example" motivation this book promises. It is missing here.

## Missing examples and intuition

- **No concrete running example before the worked examples in `sec-transport-worked`.** The chapter waits until line 758 to give numbers. A tiny two-by-two toy (two populations, one binary covariate, identity scale) immediately after `thm-direct-transportability` would let readers check the theorem against arithmetic before hitting the abstract collapsibility machinery. The continuous worked example at 767 is good but comes after three heavy theorems it is meant to illustrate.

- **No picture.** The whole chapter is about how a marginal effect depends on a covariate distribution. A single figure showing two density functions `f_P1` and `f_P2` over a binary or continuous X, with the conditional effect overlaid, would make "the population is the distribution" tangible. The book is a math book, but even a schematic TikZ would help the weak-math reader.

- **The "expit" and "logit" functions are used throughout (e.g. lines 794, 806, 677) without a one-line reminder.** I know these from logistic regression, but a reader who does not will be stuck. Notation.qmd does not define them either (I checked). A footnote on first use at line 677 would suffice.

- **The density-ratio weight `w(x) = f_P*(x)/f_P(x)` (line 315) deserves an example.** For a binary X with source P(X=1)=0.3 and target P(X=1)=0.6, w(1)=2 and w(0)=0.857, and a reader who computes these by hand will never find the re-weighting identity mysterious. Exercise `exr-transport-gformula-weights` (line 935) does exactly this, but it is an exercise, not a worked illustration in the body. Promoting a version of it to the text would help.

- **No example of the *degenerate population* recovery before the remark at lines 825 to 833.** The proof of `thm-sema-insufficient` uses a point-mass population to show equality in Jensen, and the remark checks it numerically. But this is the cleanest way to see *why* attenuation depends on spread, and it appears as an afterthought. It could be a short paragraph in the proof itself.

## Notation and jargon problems

- **`d_{ab(P)}` and `d_{ab}(x)` are very similar and mean different things (marginal vs conditional).** Defined at `eq-transport-marg-effect` (line 116) and `eq-transport-cond-effect` (line 120). I repeatedly had to flip back. The notation.qmd entry (line 116 of that file) defines `d_{ab(P)}` but the conditional `d_{ab}(x)` is not in notation.qmd at all. Either add it or rename one of them; the parenthesis vs bracket distinction is easy to miss.

- **"Linear predictor" and "g-scale" (line 477).** The term "linear predictor" is used before the model `eq-transport-nmr` is written, and "g-scale" is introduced at line 494 without a crisp definition. I inferred it means "the scale on which g(mu) is linear in covariates," but a one-line definition would help.

- **"Effect-measure transform" `h` (line 499).** The letter `h` appears suddenly. It is the transform applied to the conditional means to get the reported effect. The notation.qmd has `g` for the link but no `h`. A notation.qmd entry for `h` would be consistent with the book's "single source of truth" policy.

- **`e_t(x) = P(T=t | X=x, S=src)` (line 319).** The subscript `t` on the propensity is unusual; notation.qmd (line 100) defines `e(x) = P(T=1 | X=x)` for the binary case. The generalized `e_t` is not in notation.qmd. A reader crossing from Chapter 10 will be mildly confused.

- **"Hájek form" (line 374).** The term is dropped without definition. A parenthetical "self-normalized, dividing by the sum of weights" is already there, which is good, but the name itself is jargon that a basic reader will not recognize.

- **"Anchored" vs "unanchored" (line 387).** "Anchored indirect comparison" is used throughout but never defined in this chapter; it is presumably from Chapter 14. A one-line reminder on first use would keep the chapter self-contained enough to read.

- **"Catalogue result N.1, N.3, N.4, N.8" etc. (lines 133, 377, 385, 718).** These references to the proof catalogue are opaque to a reader who does not have the catalogue open. The book's convention (per CLAUDE.md) is to note them in parentheses, which is done, but a first-time reader has no idea what "N.4" is. A footnote on first use explaining the catalogue numbering would reduce friction without violating the convention.

## Pacing issues

- **The introduction (lines 5 to 56) is excellent but long.** It promises five movements and names collapsibility, scale alignment, and the two-step view before any of them are defined. For a weak reader this is a preview that cannot yet be processed. A shorter intro that defers the "five movements" map to the end of `sec-transport-setup` (after the basic objects exist) would pace better.

- **`sec-transport-setup` to `sec-direct-transport` is the steepest climb.** In roughly 120 lines we go from "a population is a distribution" through structural invariance, marginal means, the link, marginal and conditional relative effects, generalizability, and transportability, and into the first theorem with a two-part proof and a collapsibility lemma. This is the densest part of the chapter and it has no worked numbers at all. Inserting the toy binary example here would slow it to a learnable pace.

- **`sec-collapsibility-transport` (lines 468 to 639) packs three theorems and a corollary into one section** with no numerical checkpoint until `sec-transport-worked` much later. The scale-alignment definition and theorem, the positive transport theorem, and the conditional corollary all arrive back to back. Splitting "scale alignment" into its own short subsection (it already has `sec-scale-alignment`) and giving the positive theorem its own would help, but more importantly each theorem here needs a one-line "what this says in HTA terms" gloss.

- **The worked examples (`sec-transport-worked`, lines 758 to 877) come too late.** They are the best teaching in the chapter, but by the time I reached them I had already struggled through the abstract versions of all three results. Moving the continuous example up next to `thm-collapsible-transport` and the binary example up next to `thm-sema-insufficient` would let each theorem land on contact with numbers.

- **The notes and references section (lines 879 to 922) is thorough but very dense**, and the machine-checked-status paragraph (lines 914 to 922) is important for the book's project but will be meaningless to a health researcher. A one-sentence plain-language lead-in ("none of these results have been machine-checked yet; here is what is and is not formalized") would orient the non-formal-methods reader.

## What worked well

- The introduction's framing of the paradox (lines 25 to 35) is the clearest statement I have read of why transportability is not the free lunch the folklore promises. The sentence "the measures we most want to transport are precisely the ones that resist transport" is worth the price of admission.

- The binary worked example `sec-worked-binary` (lines 787 to 823) is exemplary. Every digit is reproducible, the conditional OR (7.389) and the two marginal ORs (3.24, 1.86) are laid out side by side, and the closing sentence at 822 to 823 ("a marginal odds ratio is not a property the treatments carry from population to population") is the chapter's thesis in one line. This is exactly the kind of teaching the rest of the chapter needs more of.

- The two-step decomposition `thm-two-step-transport` and the "why two sponsors can disagree" remark (lines 458 to 466) are genuinely illuminating. I will never read a MAIC report the same way again; I now know to ask "which comparator population is this standardized to?"

- The transportability table `prp-transport-table` (lines 727 to 738) is a fantastic summary. Once I understood the three conditions, the table let me see the whole landscape at once. Putting it slightly earlier, or at least previewing its structure, would help.

- The degenerate-population remark (lines 825 to 833) is a small but perfectly chosen check. It made the Jensen-gap mechanism feel real rather than abstract.

- The exercises (lines 924 to 1003) are well targeted. `exr-transport-rr-transports` (line 955) and `exr-transport-scale-misalignment` (line 976) in particular force the reader to reproduce the two positive and negative poles of the theory. The starred exercises are appropriately harder.

## Suggestions

1. **Add a toy binary example immediately after `thm-direct-transportability`** (around line 228), with two populations and an identity-scale constant effect, so readers touch numbers before the collapsibility lemma.

2. **Move the continuous and binary worked examples up next to the theorems they instantiate** (`thm-collapsible-transport` and `thm-sema-insufficient`), rather than collecting all three in a late section. The current late placement means the abstract proofs are tested only in hindsight.

3. **Insert a short "invariance versus SEMA" paragraph** between `def-transport-invariance` and `sec-direct-transport` (around line 104) clarifying that invariance is about the whole conditional mean function being shared, while SEMA is a restriction on the effect-modification part, and that the chapter assumes invariance throughout and adds SEMA later.

4. **Unpack the change-of-measure step in the transport g-formula proof** (lines 339 to 345) with one plain-English sentence about rewriting a target average as a source-weighted average; this is the intuition behind every MAIC and it is currently buried in two lines of algebra.

5. **Soften the `thm-scale-alignment` part (ii) proof** (lines 545 to 562) with a concrete psi=expit illustration before the general non-affine argument, and add a one-line reminder that "not affine" implies "nonzero second derivative somewhere."

6. **Promote the "why two sponsors can disagree" remark** (lines 458 to 466) into the main text after `thm-two-step-transport`; it is the HTA payoff of the section and too important to relegate to a remark.

7. **Add notation.qmd entries for `d_{ab}(x)` (conditional relative effect), `h` (effect-measure transform), `e_t(x)` (generalized propensity), and `expit`/`logit`**, consistent with the book's single-source-of-truth policy. The conditional `d_{ab}(x)` in particular is central to this chapter and absent.

8. **Add a one-line plain-English gloss after each major theorem statement** ("in HTA terms, this says..."). The book is rigorous, but the author's stated goal is taking a naive researcher to mastery, and that requires the domain bridge at every theorem, not just in the intro.

9. **Add a figure**: two covariate densities `f_P1`, `f_P2` and the conditional effect function `tau(x)` overlaid, to make "the population is the distribution" visible. Even a static schematic would help the weak-math reader.

10. **Soften the notes-and-references machine-checked paragraph** (lines 914 to 922) with a one-sentence plain-language lead-in so non-formal-methods readers do not disengage at the end.