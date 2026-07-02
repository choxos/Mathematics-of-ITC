# Feedback: Chapter 25 — General Likelihoods

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part5/25-general-likelihoods.qmd`

## Overall impression

I came in hoping to finally understand how ML-NMR handles survival outcomes, which is the one thing I actually see in oncology HTA submissions. The chapter delivers on that promise in the end, and the worked exponential example (@exm-genlik-survival, lines 850-946) is the single most illuminating thing in the whole book for me so far. But getting there was a slog. The first three sections pile on measure-theoretic machinery (absolute continuity, Lipschitz composition, dominated convergence, Fubini/Tonelli, exponential tilts of measures) with very little hand-holding, and the motivational "why does this matter for an ITC" content is concentrated in the intro (lines 5-65) and then mostly disappears for 400 lines of formal development. As a weak-math reader I found myself surviving on the remarks (which are excellent) and drowning in the proofs (which are not aimed at me). The survival domain connection is strong throughout; the ordinal-categorical connection is thin and almost abstract by comparison.

## What was unclear

- **Lines 96-98 (after @def-survival-function):** "These properties are exactly the complement of the CDF properties established in Chapter 4... so we take them as given rather than reprove them." I do not remember Chapter 4 well enough to lean on it. A one-line restatement of the three properties (monotonicity, right-continuity, the two limits) inline would cost nothing and save me a cross-reference hunt.

- **@def-hazard, lines 104-107:** The two-sided limit definition is fine, but the jump from $P(t\le T<t+\Delta t\mid T\ge t)/\Delta t$ straight to $f(t)/S(t)$ is the whole content of the proof that follows, and as a noob I read the definition, did not understand the equality, then read the proof. The definition should say "(proved in @eq-genlik-hazard-def's proof below)" or mark the second equality as derived, otherwise it looks like I am expected to already see it.

- **@thm-survival-hazard-relation proof, lines 150-179:** This is the hardest proof in the chapter for me and it is the most compressed. Specifically:
  - Line 154 "Lipschitz there, and a Lipschitz function composed with an absolutely continuous function is absolutely continuous" is stated as if obvious. I needed a sentence reminding me what Lipschitz and absolutely continuous mean and why the composition claim is true; I had to go look it up.
  - Line 158 "$S'(s)=-f(s)$ because $S=1-F_T$" is the load-bearing derivative and it gets half a clause. I needed an explicit "since $F_T'=f$ a.e. and $S=1-F_T$, differentiate to get $S'=-f$ a.e."
  - The *Converse* (lines 172-178) is much clearer than the forward direction, which is backwards relative to what I needed.

- **@lem-survivor-weighted-hazard, lines 255-290:** The integrability envelope condition (line 258-260: "the envelope $\sup_{s\le\Sigma}h_t(s\mid\mathbf{x})$ is $f_{\mathcal{P}}$-integrable") is technical measure theory I do not have the intuition for. What goes wrong if it fails? Why do I, as a health researcher doing an ITC, care? A parenthetical "this is the regularity condition that lets us differentiate under the integral; it holds for the bounded-hazard models used in practice" would have reassured me.

- **@thm-marginal-hr-time-varying proof, lines 338-353 (the exponential-tilt argument):** This is the most technically demanding paragraph in the chapter. "Introduce the one-parameter family of tilts" (line 339) appears with no setup: I am suddenly looking at $d\mu_c(\mathbf{x})\propto\ldots$ and being asked to differentiate an exponential family in its natural parameter. As a weak-math reader I had never seen that $m'(c) = \mathrm{Var}_{\mu_c}(\rho)$ is the score-variance identity for an exponential family. This is exactly the kind of step that needs either a forward reference to where it was proved earlier in the book or a one-line "the derivative of the mean of the sufficient statistic with respect to the natural parameter is its variance (a standard exponential-family fact, see Chapter X)."

- **Lines 749-758, @thm-general-likelihood-mlnmr Part 3 (GLM reduction):** The phrase "the kernel is affine in $\theta$ for each fixed $y$" is doing a lot of silent work. It took me three readings to realize this is *not* true for most GLMs I care about (Poisson with a log link has kernel $\theta^y e^{-\theta}/y!$, which is not affine in $\theta$ for fixed $y$). So the "reduction" is really only to the identity/Bernoulli case, which the proof confirms at line 794-796. The theorem statement overgeneralizes; it should say "Bernoulli/identity-link" or explicitly note Poisson does not satisfy it.

- **@def-proportional-odds, lines 654-657:** "$\operatorname{logit}P(Y\le k\mid\mathbf{X}=\mathbf{x})=\alpha_k-\eta(\mathbf{x})$" with the *minus* sign. The sign convention is never motivated. Why $\alpha_k - \eta$ rather than $\eta - \alpha_k$? In pharmacometrics I have seen both. A parenthetical "the minus sign is the convention that makes larger $\eta$ correspond to higher severity" would have anchored it.

## What wasn't elaborated enough

- **The transition from conditional to marginal hazard (lines 292-294):** The survivor-weighted representation is the conceptual hinge of the whole chapter, and it gets one sentence of interpretation ("the marginal hazard at time $s$ is the conditional hazard averaged not over the original population but over the survivors"). I needed this unpacked much more slowly: a picture, a concrete numeric snapshot at $s=0.5$ from the example, an explicit statement that $\tilde f_t(\cdot\mid s)$ is *not* the same as $f_{\mathcal{P}}$ and that this is the entire source of the trouble.

- **@prp-censored-likelihood-density, lines 482-509:** The derivation is correct but very telegraphic. "Its density in $t$ is obtained by integrating the joint density over the censoring values $c\ge t$" (line 487) elides the step I actually needed: *why* we integrate over $c\ge t$ (because those are the censoring times compatible with observing an event at $t$). The two cases are written as formulas; I would have liked one sentence of plain English per case before the integral.

- **@thm-marginal-individual-likelihood proof, lines 547-562:** The phrase "the law of total probability, equivalently marginalization of a joint density, Chapter 4" (line 552-553) is the only justification. For the target reader this is the theorem that makes the whole method work, and it deserves more than a back-reference. A two-line "intuition: the AgD study did not record $\mathbf{x}$, so we cannot condition on it; the only honest likelihood is the one that integrates $\mathbf{x}$ out, weighted by how common each $\mathbf{x}$ is in that study" before the formal proof would have made the integral @eq-genlik-marginal-lik feel inevitable rather than imposed.

- **The remark at lines 564-582 (relation to mean aggregation and numerical integration):** This is dense and compressed. The claim "The two agree exactly when the likelihood kernel is affine in the mean" (line 567-568) is the conceptual bridge from Chapters 20-21 to this chapter, and it is dispatched in one sentence. The Bernoulli example is good but rushed. I wanted an explicit *non*-example right here (Poisson, or the survival kernel) showing the affine-in-mean condition failing and why the integral then does not collapse.

- **Pseudo-IPD reconstruction (lines 629-635):** "the reported summary is a Kaplan-Meier curve, which is not a single sufficient statistic; the individual observations entering @eq-genlik-aggregate-lik are then pseudo-IPD reconstructed from the published curve and the numbers at risk, the reconstruction whose validity is established... in Chapter 26." This is the *practical* crux of using the method on a real HTA, and it is deferred entirely to Chapter 26. As a health researcher, this is the step I most need to trust, and a one-paragraph sketch of *what* the reconstruction does (digitize the KM curve, read off $(t_i,\delta_i)$ at each step) would have kept me from feeling the chapter builds a castle on air.

## Missing motivation / "why does this matter?"

- **@sec-genlik-hazard-ratio opening (lines 195-199):** We are told "the relative effect in a survival network is reported on the log-hazard scale, so the link is $g=\log$." *Why* is it reported there? Because Cox PH is the lingua franca of oncology submissions, and regulators expect a hazard ratio. That one-sentence motivation is missing and would have grounded the whole section in my actual work.

- **@thm-conditional-loghr-ph (lines 218-232):** The theorem proves the conditional log HR is time-invariant and affine in $\mathbf{x}$. *Why* is this worth a theorem? Because it is exactly the property that makes the network estimand well-defined: a single contrast $\gamma_b-\gamma_a$ per comparison, transportable across populations. That payoff is stated only obliquely at lines 249-251. A "This is why the network can report one number per comparison" sentence in the theorem's lead-in would sell it.

- **@thm-marginal-hr-time-varying (lines 296-354):** The motivation is buried. As an HTA reviewer I have seen a thousand Cox fits report "HR=0.60." The theorem says that number is an artifact of follow-up. *That* is the punchline that matters for my work, and it is delivered at line 364-366 in a remark and again at lines 887-893 in the example. The theorem statement itself should carry a one-line "practical consequence: a single reported marginal HR is not transportable across follow-up windows or populations."

- **@sec-genlik-ordinal (lines 641-724):** The motivation is almost entirely absent. We get one line (lines 643-645) saying the proportional-odds model is "standard." For a chapter that claims ordered categorical outcomes are a major HTA outcome type (intro line 24-26), the section reads like a math interlude with no clinical anchor. Where is the concrete PASI-75 / ECOG example promised in the intro? I never see one.

- **@thm-general-likelihood-mlnmr (lines 732-767):** The unifying theorem is stated, proved, and then two remarks discuss cost and generality. But the *why this matters* is never stated cleanly: it is the reason ML-NMR is the only population-adjustment method that does not need to be rebuilt for each outcome type, which the intro (lines 41-45) says but the theorem section does not repeat. A one-line "this is the structural advantage over MAIC and STC" in the theorem's preamble would close the loop.

## Missing examples and intuition

- **No diagram of the survivor-selection mechanism.** The whole non-collapsibility story (lines 292-367) is about a covariate distribution drifting over time among survivors. A figure with three panels (risk set at $s=0$, $s=0.5$, $s=2$) showing the high-frailty stratum being depleted would convey more than the entire proof for a reader like me.

- **No numeric worked example of the marginal hazard until lines 873-893**, and that example uses the *result* without showing the intermediate arithmetic of @lem-survivor-weighted-hazard. A mini-table computing $h_C^{\mathcal{P}}(0.5)$ step by step from the survivor-weighted average would have taught me the mechanism.

- **No worked ordinal example at all.** The intro promises ECOG/PASI, the section develops proportional odds, and there is an exercise (@exr-genlik-ordinal-network, lines 1048-1055) but no in-text example. Given that the chapter is *titled* to include ordered categorical, the asymmetry is glaring. A 10-line analogue of @exm-genlik-survival for $K=3$ would fix this.

- **The "affine in mean" reduction (Part 3 of the unifying theorem) has no figure or table** mapping outcome types to "reduces / does not reduce." A small table (Bernoulli: yes; Poisson: no; survival: no; ordinal: no) would make Part 3 instantly digestible.

- **Censoring intuition is missing.** @def-censored-likelihood (lines 445-461) defines the contribution with the two cases but never *draws* a timeline showing an event vs a censoring and why one contributes the density and the other the survival probability. For a weak-math reader this is the single most picturable object in the chapter and it has no picture.

## Notation and jargon problems

- **"frailty" (line 299):** Used as a technical term ("a covariate that acts as a frailty") with no definition. In survival analysis frailty usually means unobserved random effects; here it is being repurposed to mean a multiplicative prognostic covariate $\rho(\mathbf{x})$. A parenthetical "(here, a multiplicative prognostic factor; the term is used loosely)" would prevent confusion with the frailty-distribution literature.

- **"exponential tilts" (line 332) and "natural parameter" (line 343):** Jargon from exponential-family theory, used without definition or forward reference. I had to infer that "tilt" means reweighting by $\exp(c\,\rho(\mathbf{x}))$.

- **$\operatorname{expit}$ (lines 657, 662, etc.):** Used throughout the ordinal section without a reminder that $\operatorname{expit}(z)=1/(1+e^{-z})$. It is in the notation file but I had forgotten; a one-time inline reminder would help.

- **$\tilde f_t(\cdot\mid s)$ (lines 268-273):** The tilde notation for the survivor covariate density is introduced inside the lemma, used heavily, and then the *same* symbol family appears in the theorem proof. Fine, but the *name* "survivor density" only appears in the prose after the lemma (line 293). Naming it in the definition block would help.

- **$\boldsymbol\xi$ vs $\boldsymbol\theta$ vs $\boldsymbol\theta_{jk}(\mathbf{x};\boldsymbol\xi)$ (lines 734-738):** Three parameter objects in two lines. $\boldsymbol\xi$ is the full parameter vector (notation file line 132), $\boldsymbol\theta$ is the conditional parameter, and $\boldsymbol\theta_{jk}(\mathbf{x};\boldsymbol\xi)$ is the network-mapped conditional parameter. For a noob this triply-nested symbol is hard to hold; an explicit glossary box at the start of @sec-genlik-general would save re-reading.

- **"$h_{0j}(s)$" (line 210):** The subscript $j$ on the baseline hazard (study-specific baseline) is introduced inside the PH remark but its consequence (each study has its own baseline, the network borrows strength only through $\gamma_k$ and $\boldsymbol\beta_{2,k}$) is not stated. That is a load-bearing modeling choice and should be flagged.

## Pacing issues

- **The intro (lines 5-65) is excellent and appropriately motivated, then the chapter abruptly switches to formal-mode for @sec-genlik-survival and @sec-genlik-hazard-ratio.** The drop in hand-holding between the intro and the first proof (@thm-survival-hazard-relation, lines 134-179) is steep. A short "plain English roadmap" paragraph before @def-survival-function ("we will define three equivalent descriptions of a time-to-event outcome, show the hazard determines everything, and this is what lets us put a model on the hazard scale") would smooth the transition.

- **@sec-genlik-hazard-ratio (lines 195-371) is the longest and densest section** at roughly 175 lines with three theorems/lemmas and two proofs of real difficulty. It could be split: (a) conditional HR (easy, motivational), (b) marginal hazard representation (lemma), (c) time-varying marginal HR (hard theorem). The middle one currently acts as an unmarked speed bump.

- **@sec-genlik-rmst (lines 372-436) is short and well-paced** relative to its importance; if anything it could be *expanded* because the collapsibility/transportability distinction (lines 421-434) is subtle and gets one remark.

- **The jump from @sec-genlik-aggregation (lines 523-639) to @sec-genlik-ordinal (lines 641-724) is abrupt.** After two heavy aggregation theorems, the ordinal section feels like an appendix. Given the title of the chapter, ordinal deserves more weight.

- **The worked example @exm-genlik-survival (lines 839-958) comes after all the theory and is 120 lines of dense arithmetic.** It is the best pedagogical content in the chapter but it arrives when I am already tired. Pulling a *mini*-version of Steps 1-2 forward into @sec-genlik-hazard-ratio (right after @lem-survivor-weighted-hazard) would give me a foothold before the hard theorem.

## What worked well

- The **intro (lines 5-65)** is one of the best in the book: it names the real HTA outcome types, states the question crisply, and previews the answer. The sentence "It is deeper" (line 33) is exactly the kind of motivating payoff that keeps me reading.

- The **"Why the hazard scale" remark (lines 181-191)** is a model of how to motivate a definition: constant hazard gives exponential, power-law gives Weibull, spline gives M-spline, all sharing @eq-genlik-S-exp-H. This taught me why the hazard is the modeling target in one paragraph.

- **@thm-marginal-hr-time-varying's "mechanism in words" remark (lines 356-367)** is superb and rescued my understanding of the proof. The high-frailty patients surviving longer under treatment, depleting the control risk set, pulling the marginal HR toward 1: this is the intuition I will actually remember.

- **@thm-rmst-collapsible and its remark (lines 392-434)** cleanly state the within-population vs cross-population distinction, which is the single most important conceptual point for transportability. The collapsible-but-not-transportable framing is exactly right.

- **@exm-genlik-survival (lines 839-958)** is excellent once I reached it. Every number is checkable, the $s=0$ sanity check (line 892-893) is exactly the kind of hand-hold a weak reader needs, and Step 5 ties the product back to the HMC-ready likelihood. This is the chapter's high point.

- The **remarks throughout (lines 181-191, 356-367, 421-434, 511-519, 564-582, 622-636, 715-722, 811-835, 948-958)** consistently carry the intuition the formal proofs lack. They are the reason a noob can survive this chapter.

- The **exercises (lines 1015-1080)** are well-targeted, especially @exr-genlik-mhr-attenuation and @exr-genlik-rmst-transport which push the subtle points. The starred difficulty grading is appreciated.

## Suggestions

1. **Add a plain-English roadmap paragraph before @def-survival-function** (after line 75) previewing the three descriptions (distribution, survival, hazard) and why the hazard is the target.
2. **Expand @thm-survival-hazard-relation's forward-direction proof** with explicit reminders of Lipschitz-composition-absolute-continuity and the $S'=-f$ derivative; this proof is the gateway and it is too terse.
3. **Add a figure** showing the survivor-selection mechanism (risk sets at $s=0, 0.5, 2$) in @sec-genlik-hazard-ratio; it would convey more than the exponential-tilt proof for the target reader.
4. **Forward-reference the exponential-family score-variance identity** used at line 343-347, or prove it inline in two lines; right now it is an unannounced technical step.
5. **Add a concrete ordinal example** parallel to @exm-genlik-survival (e.g., ECOG 0/1/2 with a binary covariate); the chapter's title promises ordered categorical and the body underdelivers.
6. **Pull a mini-version of @exm-genlik-survival Steps 1-2 forward** into @sec-genlik-hazard-ratio right after @lem-survivor-weighted-hazard, so the hardest theorem has a numeric anchor next to it.
7. **Soften the overgeneralization in @thm-general-likelihood-mlnmr Part 3**: "affine in $\theta$" should be explicitly tied to the Bernoulli/identity-link case, with a note that Poisson and other log-link GLMs do *not* satisfy it and retain the full integral.
8. **Add a one-paragraph sketch of pseudo-IPD reconstruction** (digitize KM, recover $(t_i,\delta_i)$ from numbers at risk) in @sec-genlik-aggregation rather than deferring entirely to Chapter 26; it is the practical step a health researcher most needs to trust.
9. **Define "frailty," "exponential tilt," and "natural parameter" inline** on first use, or cross-reference the chapter where they were established.
10. **Add a small table** mapping outcome type to "reduces to mean aggregation? yes/no" near @thm-general-likelihood-mlnmr to make Part 3 instantly readable.