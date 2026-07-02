# Feedback: Chapter 10 — Adjustment Methods

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part2/10-adjustment-methods.qmd`

## Overall impression

I came to this chapter expecting to learn "adjustment methods" because the title made me think of the methods I actually use at work: MAIC, STC, ML-NMR, the things in the HTA submission templates. The opening paragraph raised my hopes by naming those exactly (lines 37-44), promising that "mastering the four estimators here is therefore mastering the mathematical core of population adjustment." That is the sentence I needed. But then the chapter spent the next thousand lines proving theorems about conditional independence, $\sigma$-algebras, and influence functions, and I lost the thread. I am honest with myself: I have basic calculus, I can follow an expectation being manipulated if each step is justified, but I do not have measure theory reflexes and I do not own semiparametric theory. This chapter assumes both. It is beautiful, rigorous, and for a graduate statistician; for a health researcher trying to reach "mastery" from a naive starting point, which the preface says is the goal, it skips too much too fast. The single worked example near the end (Section 11) saved me, but it arrived very late and only covered a fraction of what the theorems promised.

## What was unclear

- **Lines 5-22 ("From identification to estimation").** The very first sentence refers to `@thm-consistency-identity`, `@def-ignorability`, `@def-positivity`, `@def-ate`, `@thm-ate-identification` as if I already carry them in my fingers. I gather these are from Chapter 9, but a one-line plain-English gloss of each ("consistency = your observed outcome really is the potential outcome for the treatment you got"; "ignorability = no unmeasured confounding given $X$"; "positivity = every patient had a nonzero chance of each treatment") would let me read this paragraph without flipping back. As written I had to stop and reverse-engineer what the assumptions meant from the standing-assumptions box at lines 58-71, which is itself dense.

- **Lines 24-35.** "There are exactly two surfaces one can model." I do not yet know what a "surface" is in this sense. Is $m_t(x)$ a surface because $x$ is a vector and the mean is a function over that space? Say so. The leap from "two surfaces" to "the augmented IPW estimator combines the two and enjoys a remarkable insurance property" (line 30-32) drops the word "insurance" with no definition. Insurance against what? I had to wait until Section 6 to learn it means "consistent if either model is right," and even then I wanted the metaphor unpacked once.

- **Lines 60-71 (Standing assumptions box).** The box uses `$\perp$`, "$\sigma$-algebra," "graphoid axioms," "tower property" as though I have them loaded. The graphoid axioms especially: the chapter leans on "G2" and "G4" (lines 106-107, 358-360) repeatedly, but I never saw them stated or summarized here. A two-line reminder of what G2 (decomposition) and G4 (contraction) say would cost little and save me from trusting the proof on faith.

- **Line 156.** "extended from bounded to integrable factors" is meaningless to me. What is being extended, why does bounded not suffice, and why does the chapter bother with the extension if every realistic outcome is bounded anyway? The proof at lines 216-227 uses truncations $V_n=(V\wedge n)\vee(-n)$ and "conditional dominated convergence" (line 223), neither of which is intuitive to a weak-math reader. I can mimic the algebra but I cannot tell you why the limit step is legal.

- **Lines 158-202 (`#lem-ci-binary-criterion`).** This is the load-bearing lemma of the chapter and it is genuinely hard. The reverse direction (lines 179-201) does a move I had to read five times: it argues that because every function of a binary $T$ is affine in $\mathbf{1}_{\{T=1\}}$, controlling one test function controls all. That is clever and I want to believe it, but I would have liked a one-sentence aside: "*this is the only reason we assumed $T$ is binary; for a multi-valued treatment this lemma is false and the whole shortcut collapses.*" Without that, I cannot tell how fragile the argument is.

- **Lines 248-293 (`#thm-rosenbaum-rubin`, proof).** The proof is terse and chains three abbreviations: the criterion lemma, the tower property, and "$\sigma(e(X))\subseteq\sigma(X)$." I followed part (1) eventually. Part (2) (lines 280-292) lost me at "the right-hand side is, by construction of conditional expectation, a $\sigma(b(X))$-measurable random variable, hence almost surely equal to a measurable function of $b(X)$" (lines 289-291). This is the measure-theoretic fact that conditional expectation is measurable with respect to its conditioning $\sigma$-algebra; for someone with weak measure theory it reads like magic. I needed the fact stated, even parenthetically, before it gets wielded.

- **Lines 324-353 (`#thm-ps-sufficiency`, proof).** The line "`$\sigma(W)\vee\sigma(b(X))\subseteq\sigma(W)\vee\sigma(X)$`" (line 330) trades on the inclusion $\sigma(b(X))\subseteq\sigma(X)$, which is true because $b$ is a function of $X$, but it is never spelled out. Same for why conditioning on $(W,b(X))$ can be repackaged via the tower property on the bigger $\sigma$-algebra $(W,X)$. A diagram or a one-line "because $b(X)$ carries less information than $X$" gloss would help enormously.

- **Lines 673-678 (`#eq-aipw-error`).** "The estimator is consistent precisely when the error term $\mathbb{E}[R]$ vanishes." Why "precisely"? I see that $\mathbb{E}[R]=0$ gives unbiasedness of the functional, but consistency of the sample estimator also needs $\hat e,\hat m_1$ to converge, which is not the same statement. The conflation tripped me up.

- **Lines 797-812 (`#thm-eif-bound`).** This is the hardest theorem in the chapter and it is essentially imported. I appreciate the honesty at lines 860-870 ("we take this characterization as a cited external result"), but for a beginner the jump from "influence function" to "efficient influence function" to "semiparametric efficiency bound" is three conceptually distinct ideas presented in two paragraphs. I never learned what makes an influence function *efficient* as opposed to merely *an* influence function. The Cramér-Rao analogy at lines 882-884 is the closest I got to intuition, and it deserved to be frontloaded.

- **Lines 856-858.** "a rigorous statement requires sample splitting or a Donsker condition, for which we refer to ..." This is the moment a practitioner asks "so do I need cross-fitting in my MAIC?" and the chapter punts. Even one sentence saying whether MAIC/STC/ML-NMR in practice need sample splitting would have closed the loop to the motivating paragraph at the top.

## What wasn't elaborated enough

- **The propensity score as a *estimand* versus a *fitted model*.** The chapter switches between the true $e(x)$ and the estimate $\hat e(x)$ (e.g., lines 431-443) without flagging the conceptual gap. The identification theorems hold for true $e$; the estimator plugs in $\hat e$. For a beginner the fact that consistency of $\hat\tau^{\mathrm{IPW}}$ requires $\hat e\to e$ *uniformly* (line 443) is a strong condition buried in a subordinate clause. Why uniform and not pointwise? What goes wrong otherwise?

- **Stabilized vs. Hájek vs. raw weights (Section on stabilized weights, lines 445-484).** Three estimators appear in twenty lines: raw Horvitz-Thompson, stabilized weights $sw$, and the Hájek (normalized) estimator. I had to read carefully to see that "stabilized" and "Hájek" are different objects, that $sw$ multiplies by marginal probabilities while Hájek divides by a sample sum, and that the chapter ends up endorsing Hájek for practice (line 480-484). A small table contrasting the three would have been worth a hundred words.

- **The "matching as nonparametric standardization" remark (lines 604-616).** This remark quietly introduces the treated-on-the-treated (TOT/ATT) versus ATE distinction, which the chapter has been suppressing under "every theorem below is stated for $\psi_1$" (lines 121-123). Suddenly at line 613-615 I learn one-to-one matching targets the ATT, not the ATE, because it reweights toward the treated covariate distribution. This is a foundational distinction for ITCs (anchored vs. unanchored is foreshadowed at line 615) and it deserves a full subsection, not a parenthetical. I needed the estimand rewritten explicitly under the treated-covariate distribution before I could see why matching misses the ATE.

- **Neyman orthogonality (lines 747-758).** The remark previews "rate double robustness," directional derivatives, $\sqrt n$-consistency, and asymptotic normality in five sentences and defers the derivative to Exercise `#exr-neyman-orthogonality`. For a beginner this is the single most practically important idea of the modern literature (it is why you can plug in Super Learner / random forests for $\hat e,\hat m$), and it is dispatched in a remark. Expand into a short subsection with a picture of "first-order error killed, second-order error survives."

- **Non-collapsibility footnote (lines 1020-1024).** The closing note mentions that "collapsibility makes the marginal and conditional contrasts agree, which is why @eq-adj-ate-target and @eq-gformula need no scale correction." This is the first mention of collapsibility in the chapter and it lands in the references section. A reader who has heard that odds ratios are non-collapsible will be alarmed that the whole chapter silently assumed the difference scale. One paragraph explaining the scope assumption would prevent a serious misunderstanding later.

## Missing motivation / "why does this matter?"

- **Why prove `#lem-adj-regression-identity` at all?** The proof (lines 97-111) is short but the *reason* matters: it is the step that licenses every later theorem to talk about $Y(t)$ while only ever computing on $Y$. As a beginner I read it as bookkeeping. A sentence such as "*this is what lets us pretend an observable regression is a counterfactual regression, and it is the hinge on which the whole chapter turns*" would have made me care.

- **Why is the propensity score a *balancing* score rather than just a confounder summary?** The chapter defines balancing scores abstractly (lines 132-149) before motivating them. I never learned, before the definition, the practical worry: "we cannot match on a 30-variable $X$ because cells get thin, so we need a scalar that preserves the no-unmeasured-confounding guarantee." Line 127 gestures at the curse of dimensionality but the link to *why balancing is the right abstraction* is implicit.

- **Where is the ITC?** The opening (lines 37-44) and the closing remarks (line 543-544, 614-615) are the only places an indirect comparison is named. In between, the chapter reads like a generic causal-inference chapter. Each section would benefit from a closing "what this becomes in MAIC/STC/ML-NMR" pointer: e.g., after IPW (Section 4) say "MAIC is exactly this with $e$ reparametrized as $\exp(\alpha+\beta^\top x)$ and the weights normalized to a Hájek form"; after standardization (Section 5) say "STC is exactly this, with the regression fit on the IPD arm and predictive-averaged over the AgD covariate distribution"; after AIPW (Section 6) say "ML-NMR is the doubly robust analogue, achieving the same insurance at the network level." Without these hooks the chapter's own thesis at line 43-44 is unfulfilled.

- **Why the efficiency bound matters for a health researcher.** The bound $V^\ast$ (line 805) is presented as a mathematical optimum. But the practical question an HTA reviewer asks is "is my MAIC variance trustworthy?" The connection to ESS (lines 540-544) is the closest the chapter comes; I wanted the same link made for the efficiency bound: "*when overlap is poor, $V^\ast$ blows up, and that is a fundamental limit no estimator can beat, so a wide CI from MAIC under poor overlap is not a bug of MAIC but a feature of the problem.*"

- **Missing: what happens when ignorability fails.** Every theorem assumes ignorability. The chapter never says what breaks if ignorability is false, which is exactly the situation health researchers worry about (unmeasured confounding in the AgD source). Even a one-paragraph "all of this is void without ignorability; QBA (Chapter 28) is what you do then" would frame the chapter's scope honestly.

## Missing examples and intuition

- **No illustrative example before the formal machinery.** Sections 2-6 (balancing scores, propensity score, IPW, g-computation, AIPW, EIF) are pure theorem-proof. The single worked example at Section 11 (lines 896-1007) is excellent but arrives after roughly 700 lines of abstraction. A tiny two-stratum example *at the start of Section 4 (IPW)* would let readers track the algebra of `#thm-ipw-unbiased` against numbers, instead of waiting until the end.

- **No graphical intuition for balancing.** The balancing-score concept (Section 2) is geometrically obvious if you draw it: treated and control covariate distributions overlapping within each level of $b(X)$. A figure, or even a verbal description of the picture, is absent. For a beginner a single schematic would replace pages of measure theory.

- **No numerical illustration of the Rosenbaum-Rubin coarsest property.** `#thm-rosenbaum-rubin` part (2) is the hardest to feel. The worked example at lines 896-1007 does not exercise it: it never shows that $e(X)$ is a function of some other balancing score, nor that stratifying on $e$ uses minimal information. An extra worked sub-example would make the "coarsest" claim tangible.

- **No example of the variance blowup.** `#prp-ipw-variance` says variance diverges as $\operatorname{ess\,inf} e(X)\to 0$. The worked example computes an ESS fraction of 0.30 (lines 956-961), which is nice, but there is no plot or table showing variance *as a function of* the positivity margin. A small table with $\varepsilon\in\{0.4,0.2,0.1,0.05\}$ and the resulting variance would make the "cost of poor overlap" visceral rather than symbolic.

- **No finite-sample picture.** Every result is asymptotic ("consistent," "$\sqrt n$-consistent," "$\xrightarrow{d}$"). A beginner studying adjustment methods needs at least one simulated finite-sample histogram comparing IPW, g-computation, and AIPW at $n=200$, so the reader can see that AIPW's variance is not always smaller in finite samples despite being efficient asymptotically.

- **No example of the failure modes.** The chapter states that IPW fails in variance under poor overlap and that g-computation fails in bias under model misspecification (lines 592-602), but never *shows* it. Two short simulations, or even two arithmetic mini-examples with a misspecified $\hat m_t$, would convert the abstract complementarity into something I remember.

## Notation and jargon problems

- **$\mu_t$ vs. $m_t$ (lines 73-95).** This is the most consequential notational decision of the chapter and it is introduced briskly. The rationale (lines 74-78) is that "the equality between them *is* the identification step and we do not want to assume it silently." Excellent instinct, but the novice then has to track two symbols that coincide for the rest of the chapter. A marginal note each time one is used for the first few theorems ("recall $m_t=\mu_t$ under (A)") would prevent silent confusion.

- **$P_X$-almost every $x$ (line 90, 109, etc.).** "$P_X$" is the marginal law of $X$. This is standard but never defined in the chapter; I had to infer it. Notation.qmd does not list $P_X$ either (checked). Define it once.

- **$\sigma(W)\vee\mathcal{G}$ (line 163, throughout).** The join of $\sigma$-algebras is used heavily and never defined. A weak-math reader meets it first at line 163 and must guess "smallest $\sigma$-algebra containing both." One definition in the standing-notation box would fix this.

- **"$\blacktriangleleft$" (line 239).** Notation.qmd line 22 defines it, but a reader inside the chapter does not see the definition. A footnote on first use is safer than relying on a distant notation file.

- **"Essential infimum" $\operatorname*{ess\,inf}$ (line 500).** Never defined. I know the plain infimum; the essential version is subtler and matters precisely here (the variance blows up on a set of positive measure, not everywhere). One sentence.

- **"Regular estimator" (line 764, 809).** "Regular asymptotically linear" appears in the EIF section without definition. Regularity has a precise meaning (insensitivity to local perturbations) and is the whole reason the bound applies; a beginner cannot skip it.

- **"Nuisance functions" (line 626, 634, 682, etc.).** Epidemiologists sometimes use "nuisance" to mean "a confounder we adjust for." Here it means "the parts of the estimator we do not care about asymptotically, namely $\hat e,\hat m_t$." Disambiguate on first use.

- **$p_1,p_0$ (line 463).** Defined inline as $P(T=1),P(T=0)$ but the notation does not scream "marginal probability of treatment"; it looks like it could be a generic parameter. Spelling $p_T:=P(T=1)$ once would be clearer.

- **Inconsistent estimator hats.** $\hat\psi_1^{\mathrm{IPW}}$, $\hat\tau^{\mathrm{IPW}}$, $\hat\tau^{\mathrm{OR}}$, $\hat\tau^{\mathrm{AIPW}}$, $\hat\psi_1^{\mathrm{AIPW}}$ are used; sometimes a superscript, sometimes a subscript-free functional form. A consolidated "estimators used in this chapter" table would help, mirroring the notation tables.

## Pacing issues

- **Sections 2 and 3 (balancing scores, propensity score) are the densest in the book so far.** Two measure-theoretic lemmas (`#lem-ci-binary-criterion`, `#lem-ci-factorization`) and two major theorems (`#thm-rosenbaum-rubin`, `#thm-ps-sufficiency`) arrive in roughly 230 lines, before the reader has seen a single estimator. For a beginner this is a wall. Consider deferring `#lem-ci-factorization` to where it is first needed (the IPW proof, line 411-419) so that Sections 2-3 carry only `#lem-ci-binary-criterion`.

- **Section 6 (AIPW) crams three ideas into one section**: the pointwise cancellation identity, double robustness, and Neyman orthogonality. Each deserves its own subsection with its own worked numeric check; currently Neyman orthogonality is a remark (lines 747-758) that references an exercise, which is too fast for the practical payoff it carries.

- **Section 7 (EIF) accelerates to maximum density at the end.** After 700 lines of careful bias proofs, the variance bound is dispatched in one theorem with a partially imported proof. The pacing is backloaded: the hardest mathematics gets the least exposition. Either expand this section or precede it with an intuitive "what is an influence function" interlude that defines asymptotic linearity, the influence function, and efficiency separately before combining them.

- **Exercises appear only at the very end (Section 12).** Embedded exercises after each section (e.g., "verify part (2) of `#thm-rosenbaum-rubin` on a two-point $X$") would pace the reader's absorption. Currently all eight exercises are stacked together after the most abstract section, which discourages attempted engagement.

- **The transition from identification (Section 1) to balancing (Section 2) skips the curse of dimensionality in practice.** Line 16-18 says stratification is infeasible because "most strata contain a single unit, or none." Then Section 2 jumps to the abstract balancing definition. The bridging sentence, "*so we look for a low-dimensional summary of $X$ that still kills confounding,*" is implied but not said, and the word "summary" appears only later (line 128). One connecting sentence would smooth the gear change.

## What worked well

- **The opening framing (lines 37-46)** is exactly the motivational hook a health researcher needs: four estimators, mapped to MAIC/STC/ML-NMR, with a clear thesis. Even though the chapter does not always deliver on the promise, the statement of intent is exemplary.

- **The four-step structure of the IPW proof (lines 396-428).** Labeling the steps "consistency / tower and pull-out / ignorability factorizes / cancel and average" is pedagogically excellent and the kind of scaffolding I wish every proof in the chapter had. I could actually follow this proof.

- **The double-robustness proof by cases (lines 698-733).** Splitting into "condition on $(Y(1),X)$" versus "condition on $(T,X)$" and showing the *other* factor centers is the cleanest exposition of double robustness I have read. The symmetry remark at lines 735-745 nails the intuition.

- **The worked example (Section 11, lines 896-1007).** Carrying a single concrete population through all four estimators, including a "both models wrong" failure case at lines 983-990, is gold. Computing $V^\ast=14.333=\tfrac{43}{3}$ and comparing to the balanced-design $V^\ast=11$ (lines 1004-1007) finally made the efficiency bound feel real.

- **The remark contrasting IPW and standardization (lines 592-602).** "IPW refuses to extrapolate but pays in variance; standardization extrapolates freely but pays in bias if the model is wrong" is the single most quotable sentence in the chapter and a genuine teaching success.

- **Honesty about imported results (lines 860-870, 887-894).** Explicitly marking the semiparametric efficiency theorem as cited, and noting the absence of a Coq counterpart for `#thm-eif-bound`, builds trust. The machine-checked tags throughout are also a strong and unusual feature.

- **The exercise suite (Section 12)** is well chosen: control-arm analogues, the randomized-trial degeneracy, recomputation with harder numbers. Exercise `#exr-recompute` (lines 1122-1131) in particular forces the reader to redo the worked example with worse overlap, which is exactly the muscle memory a beginner needs.

## Suggestions

1. **Add a "plain-English assumptions" box** right after the standing-assumptions box (lines 58-71), translating each item into researcher-language ("no unmeasured confounding," "everyone had a real chance of either treatment," "outcomes have finite variance"). Two paragraphs, huge payoff.

2. **Insert a small worked example at the start of Section 4 (IPW)** using the same two-stratum population as Section 11, so the reader watches `#thm-ipw-unbiased` operate on numbers immediately, not 500 lines later.

3. **Add an "ITC callback" at the end of each section** (one sentence): Section 4 → MAIC, Section 5 → STC, Section 6 → ML-NMR, Section 7 → the variance ceiling that every population-adjusted method shares. This delivers on the thesis at lines 37-44 and combats the "generic causal inference chapter" feeling.

4. **Promote the ATT-vs-ATE distinction** (currently buried at lines 613-615) to a short subsection in Section 5, with the estimand rewritten under $P(X\mid T=1)$. This is the mathematical pivot for the anchored/unanchored split and the reader meets it too late as is.

5. **Expand Neyman orthogonality (lines 747-758)** from a remark to a subsection, with the derivative computation shown in outline rather than exiled to an exercise, plus a sentence on whether cross-fitting is used in MAIC/STC/ML-NMR in practice.

6. **Provide a small comparison table** of raw / stabilized / Hájek weights within Section on stabilized weights (lines 445-484): columns for definition, mean weight, variance behavior, used in practice? Three rows, replaces a hundred words of careful prose.

7. **Define the measure-theoretic prerequisites in the standing-notation box**: $P_X$, $\sigma(W)\vee\mathcal{G}$, $\operatorname*{ess\,inf}$, "regular estimator," "nuisance function." Each is a one-liner and each removes a stumbling block.

8. **Soften the pacing of Sections 2-3** by deferring `#lem-ci-factorization` to the IPW proof where it is first used, and by stating the graphoid axioms G2 and G4 in a margin note at their first use rather than assuming recall.

9. **Frontload the Cramér-Rao analogy** for the efficiency bound (currently lines 882-884) to the opening of Section 7, so the reader enters the theorem knowing what kind of object to expect.

10. **Add a short "what this chapter does *not* solve" paragraph** at the end of Section 1: it does not handle unmeasured confounding (Chapter 28 QBA), nor non-collapsible scales (Chapter 11), nor network structure (Chapter 15). This frames scope honestly and prevents a beginner from thinking adjustment methods solve everything.