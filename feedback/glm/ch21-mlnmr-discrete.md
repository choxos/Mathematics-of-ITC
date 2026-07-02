# Feedback: Chapter 21 — ML-NMR for Discrete Outcomes

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part5/21-mlnmr-discrete.qmd`

## Overall impression

I came in wanting to understand how ML-NMR handles the binary and count outcomes that dominate the health technology assessments I actually work on, things like number of responders out of $n$, or stroke counts. The chapter clearly knows its material and the proofs are careful and complete, but as a beginner I felt lost for long stretches. The opening jumps straight into the "aggregation principle" and "response scale" jargon assuming I remember Chapter 20 in detail, and the motivating question of *why discrete outcomes are hard at all* gets buried under a long preview of the chapter's structure before I have any intuition for what is even being aggregated. The Le Cam proof is impressive but I could not tell you why I, a health researcher, should care about a total-variation bound when my collaborator just wants a likelihood to plug into Stan. The fully worked example at the end finally grounded me, and I wish that kind of concreteness had appeared much earlier. By the end I understood the three routes to an aggregate binary likelihood, but the journey there was pitched above my head and light on the clinical "why."

## What was unclear

- **The conditional-vs-marginal distinction (the Remark at lines 72 to 84)** is described as "the principal hazard of this subject," yet it is packed into a single remark with no diagram, no toy numbers, and no anchoring example. I had to read it four times. A small table or an inline microexample, "imagine two patients, one at risk 0.1 and one at 0.7," would have made it click. Instead the same distinction is reexplained much later in Step 7 of the worked example (lines 805 to 817), where it finally makes sense. The remark should foreshadow that example or borrow its punchline.

- **Line 28 to 30:** "the rate of the conditional Poisson is random, and marginalizing over it yields not a Poisson but a *mixed* Poisson." The phrase "mixed Poisson" is dropped here in the introduction without a definition; the formal statement only arrives at @thm-poisson-aggregate (lines 191 onwards). As a noob I read "mixed" as "mixture model" and got confused about whether there is a latent class. A one-line gloss, "a Poisson whose rate is itself drawn from a distribution and then integrated out," at first mention would save me.

- **The proof of @prp-marginal-binomial (lines 103 to 111)** leans on "the tower property" and "@def-binomial" without restating them. I dimly remember the tower property from Chapter 4 but I had to flip back. For a foundational proposition that the whole chapter hinges on, a half-sentence recall, "by the tower property, $\mathbb{E}[P(Y_i=1\mid X_i)]=P(Y_i=1)$," would lower the barrier. Right now the proof assumes I can hold the conditioning and the definition simultaneously in my head.

- **@lem-poisson-convolution's "second proof" (lines 162 to 170)** introduces the MGF route as if I already know why we would want two proofs of the same fact. The narrative payoff, that the MGF makes the contrast with the Bernoulli case precise, only lands in the subsequent remark (lines 173 to 183). I would have liked a signpost before the second proof: "We record a second proof because its mechanism, not its conclusion, is what we reuse." Without that I wondered why we were proving something twice.

- **The proof of @thm-poisson-aggregate Part 2 (lines 233 to 257)** uses the law of total variance but writes out the derivation of *that* law from scratch (lines 250 to 252) mid-proof. That digression broke my reading flow. I would either trust the reader to recall $\operatorname{Var}(Y)=\mathbb{E}[\operatorname{Var}(Y\mid X)]+\operatorname{Var}(\mathbb{E}[Y\mid X])$ from Chapter 4, or move the derivation to a remark. Embedding it in the proof body makes the proof look longer and harder than it is.

- **Lines 259 to 275 (Part 3, Gaussian covariates):** the jump "$\eta(X)\sim\mathcal N(m,s^2)$, therefore $W=e^{\eta(X)}$ is log-normal" is stated in one sentence. A weaker reader like me needs to be told *why* an affine function of a multivariate normal is univariate normal, and *why* exponentiating a normal gives a log-normal with those specific moments. The chapter cites @def-normal but does not show the key step, $M(t)=\mathbb{E}[e^{t\eta(X)}]$ being the normal MGF evaluated at $t$. This is the load-bearing calculation for the whole overdispersion formula and it deserves two more lines of scaffolding.

- **The Le Cam coupling construction @eq-lecam-pair (lines 529 to 535)** is presented as a definition the reader is asked to verify. But where did those four joint probabilities *come from*? I stared at it wondering how anyone would think to set $P(B_i=1,P_i=0)=e^{-p}-(1-p)$. A sentence of motivation, "we put as much mass as possible on the diagonal $B_i=P_i$, then dump the Poisson overflow onto $P_i\ge 2$ while respecting the Bernoulli marginal," would make the construction feel discovered rather than handed down.

- **The coupling inequality @lem-coupling-inequality (lines 477 to 495)** is proved but the *direction* is easy to misread. I initially thought the inequality went the other way, that TV bounds the disagreement probability. A clarifying sentence, "Coupling gives an upper bound on TV, not a lower bound, because we are free to choose the coupling that disagrees least," would prevent that confusion.

## What wasn't elaborated enough

- **The Poisson-binomial mass function @eq-pobin-pmf (lines 356 to 360)** is shown as a sum over all $\binom{n}{y}$ subsets, then declared "hopeless to evaluate directly" (line 37). But the chapter never circles back to say *how bad*: for a trial of $n=400$ and $y=120$ responders, $\binom{400}{120}$ is astronomically large. One concrete number, in a callout, would make the "why we need approximations" argument viscerally clear instead of abstract.

- **The Barbour-Hall refinement (lines 583 to 595)** is mentioned in a remark but the factor $\min(1,\lambda^{-1})\sum_i p_i^2$ is never derived or even intuitively explained. The remark then does a numerical example ($n=100$, $\bar p=0.3$, bound $0.3$) and concludes the Poisson is poor, which is great, but I wanted to know *where* the $\lambda^{-1}$ factor comes from physically. A one-line "events spread over a larger expected count dilute the per-event error" would help.

- **The negative-binomial remedy remark (lines 292 to 304)** introduces the negative binomial as "the count-data analogue of the adjusted binomial," says it is "by moments rather than in law," and then never returns to it. For a chapter supposedly about the discrete likelihoods ML-NMR actually uses, this is a dangling thread. Does multinma use the negative binomial? Is it ever preferred in practice? The remark raises a tool and then leaves the toolbox.

- **The "copula" connection is essentially absent.** The Notation file (lines 142 to 145) defines the Gaussian copula $C_\Omega$ and the QMC machinery, and the Notes (lines 866 to 874) gesture at Chapter 22's quasi-Monte Carlo integration, but this chapter never tells me how the discrete likelihood relates to the copula-based integration that ML-NMR is famous for. A beginner who has heard "ML-NMR uses a Gaussian copula" will wonder where it went. Even a single sentence, "the integration nodes that produce the $p_i$ are drawn via the copula of Chapter 22; this chapter treats them as given," would close the loop.

- **The effective sample size parallel (@thm-adjusted-binomial Part 2, lines 631 to 634)** notes that $N^*$ equals the ESS functional of Chapter 18 (@thm-maic-ess-bound). This is a beautiful connection but it is stated, not unpacked. Why should a *weighting* concept from MAIC reappear in an *unweighted* likelihood construction? The structural reason, that both are Cauchy-Schwarz tightenings of "effective number of equal-information units," is worth a paragraph for readers like me who need the bridge drawn explicitly.

## Missing motivation / "why does this matter?"

- **The introduction (lines 5 to 60)** never says, in plain health-researcher terms, *why discrete outcomes need a whole chapter*. I am told they are "counts and binary events that dominate health-technology assessment," but I am not told what breaks. A motivating paragraph framed around a concrete trial, e.g. "Suppose study AB reports 73 responders out of 200 on drug A, but we only have summary covariates; the naive binomial likelihood Bin(200, $\bar p$) ignores that those 200 patients have heterogeneous risk," would give me a stake in the chapter before the math starts.

- **@lem-poisson-convolution (lines 134 to 171)** is proved in full, but the chapter does not say *why we prove it here* until the remark at lines 173 to 183. As a noob I sat through two proofs of a fact I thought was obvious (sum of Poissons is Poisson) before learning that the point was the *contrast* with the Bernoulli case. The motivation should precede the lemma, not follow it.

- **Le Cam's theorem @thm-le-cam-tv (lines 515 to 571)** is the chapter's most technically demanding result. But the *practical* motivation is buried in the later remark (lines 582 to 596): the Poisson surrogate is poor at moderate risks. I would have engaged much better with the proof if, before it, the chapter had said: "We prove a sharp bound because it tells us *quantitatively* when the Poisson shortcut is safe and when it lies; the bound $\sum_i p_i^2$ is the ruler." Right now the proof reads as mathematics for its own sake until the sobering remark two pages later.

- **The conditional law @eq-poisson-agg-conditional (lines 199 to 201)** is presented as a stepping stone, but I never learned *which questions in ML-NMR require the conditional law and which require the marginal*. The remark at lines 113 to 126 gestures at this ("three purposes") but lists them abstractly. A table mapping "question you have" to "law you need" would be transformative for a beginner.

## Missing examples and intuition

- **There is no clinical example until @exm-aggregate-binomial (line 707), roughly 700 lines into the chapter.** That is far too long for a beginner to wait. A reader like me needs a tiny drug-and-trial scenario in the introduction, e.g. an oncology trial reporting responder counts for drug A versus placebo, to ground every subsequent symbol.

- **@thm-poisson-aggregate's Gaussian-covariate part (lines 218 to 225)** has no worked numerical instance in the chapter body. There is Exercise @exr-overdispersion-gaussian (lines 934 to 941) with $\theta_\bullet=3$, $\beta_{\mathrm{tot}}=0.5$, $\sigma=0.8$, but that is in the exercise section, not the text. Moving a stripped-down version of that calculation inline, right after the theorem, would show me what "overdispersion by $n\sigma_W^2$" actually looks like in numbers.

- **The Le Cam coupling (lines 524 to 571)** would benefit enormously from a tiny numerical illustration of the single-pair coupling, e.g. "for $p=0.2$, the disagreement probability is $0.2(1-e^{-0.2})\approx 0.036$." The construction is purely symbolic and I lost the thread of which probability lived where. One concrete $p$ would anchor it.

- **The adjusted binomial @thm-adjusted-binomial (lines 609 to 667)** introduces $N^*$ as a "continuous size parameter" and the Gamma-function mass (lines 686 to 688) but never illustrates what $\mathrm{Bin}(3.7, 0.45)$ looks like or why a non-integer size is statistically sensible. A beginner finds a binomial with non-integer $n$ deeply weird; a sentence acknowledging that and pointing to the Gamma-function interpolation as the resolution would calm the reader.

- **No diagram anywhere.** The conditional-vs-marginal split, the three routes to an aggregate likelihood, and the relationship among the Poisson binomial, adjusted binomial, integrated binomial, and Le Cam Poisson are all inherently relational. A single figure showing the four distributions on one axis (as the worked example computes them) would replace paragraphs of prose.

## Notation and jargon problems

- **$\boldsymbol\beta_{\mathrm{tot}}=\boldsymbol\beta_1+\boldsymbol\beta_{2,k}$ (lines 219 to 220)** is introduced inside the theorem statement of @thm-poisson-aggregate without reminding me what the subscripts mean. The Notation file (lines 128 to 130) defines $\boldsymbol\beta_1$ as "main (prognostic) covariate effects" and $\boldsymbol\beta_{2,k}$ as "treatment-by-covariate interactions," but I had to go look that up. Inline glosses at first use within Part V would spare the cross-referencing.

- **"$\operatorname{expit}$" (line 716)** is used in the worked example but defined only parenthetically as "$\operatorname{expit}(z)=e^z/(1+e^z)$." The Notation file does not list expit. A beginner may know "logit" but not its inverse; a pointer to where expit is first defined (presumably @def-link-function) would help.

- **"Effective sample size" is overloaded (line 632 vs line 684).** Chapter 18's ESS (a weighting concept) and the adjusted binomial's $N^*$ (a likelihood parameter) are deliberately the same functional, which the chapter flags. But a beginner could conclude $N^*$ *is* the MAIC ESS and confuse the two contexts. Disambiguating language, e.g. "$N^*$ is the *likelihood* effective sample size, structurally identical to the *weighting* ESS of Chapter 18 but playing a different role," would prevent conflation.

- **"$W=W(X)=e^{\eta(X)}$" (line 186)** is introduced as the "random conditional rate," but $W$ also appears as a vector space symbol in the Notation file (line 31). Within a single chapter this is fine, but a noob flipping between this chapter and Part I might stumble. Worth a note that $W$ here is a scalar random rate, not a vector space.

- **The phrase "the log-link aggregate identity of Chapter 20 (@thm-log-link-mgf)" (lines 269, 843)** is referenced twice but never restated. For the central calculation of Part 3, restating $\theta_\bullet=e^{m+s^2/2}$ inline, even redundantly, would keep me from having to break flow.

## Pacing issues

- **The introduction is too long and previews too much (lines 5 to 60).** It summarizes the count case, the binary case, Le Cam, the adjusted binomial, and the worked example before any of them are developed. As a beginner I was overwhelmed by the roadmap and had forgotten the preview by the time I reached each section. A tighter introduction that poses the two organizing questions and defers the answers would read better.

- **The Poisson section (@sec-poisson, lines 128 to 309)** is well paced internally, but the two remarks that follow @thm-poisson-aggregate (lines 278 to 304) are dense and run together. The "negative-binomial remedy" remark in particular feels like it belongs in a subsection of its own or in the Notes; jammed between the theorem and the catalogue pointer it interrupts the chapter's forward motion.

- **The leap from @lem-poisson-convolution (a warm-up) to @thm-poisson-aggregate (a three-part theorem with a Gaussian specialization) is steep.** There is no intermediate example or remark to consolidate the conditional law before the marginal law is layered on. A short "checkpoint" remark after Part 1 of @thm-poisson-aggregate, e.g. "Pause: we now know the conditional aggregate exactly; the rest of the theorem asks what happens when we stop conditioning on the covariates," would reorient the reader.

- **Section @sec-lecam (lines 431 to 598)** front-loads three supporting lemmas (total variation, three forms, coupling inequality, exponential inequality) before the main theorem. This is rigorous but means roughly 80 lines of machinery precede the payoff. A brief "here is the strategy" paragraph at the section's start, listing the four ingredients and why each is needed, would give the reader a map through the buildup. The strategy is hinted at lines 497 to 502 but only after two of the lemmas are already proved.

- **The worked example @exm-aggregate-binomial (lines 707 to 818)** is excellent but long; it runs seven steps over 110 lines. Breaking it into named subexamples, or moving Steps 6 and 7 (the comparison and reconciliation) into their own subsection, would make it easier to teach from and to refer back to.

## What worked well

- **The fully worked example @exm-aggregate-binomial** is the chapter's high point for a beginner. Every number is exact and checkable, the three routes are laid side by side, and the final reconciliation (lines 805 to 817) tied the conditional-versus-marginal theme together with concrete variances ($1.20$ versus $1.00$). This is exactly the kind of grounding the rest of the chapter lacks.

- **The remark on "the asymmetry with the binomial" (lines 173 to 183)** is genuinely illuminating once I reached it. Contrasting the Poisson MGF (which multiplies into the same form) against the Bernoulli MGF (which does not unless all $p_i$ are equal) gave me the structural reason the whole chapter exists in one paragraph.

- **The honesty about what each surrogate guarantees (lines 669 to 681)** is exemplary. The chapter is explicit that the adjusted binomial has no total-variation guarantee while Le Cam's Poisson does, and insists the two "should never be conflated." This clarity is rare and welcome.

- **The exercises (lines 884 to 941)** are well chosen and span the chapter's ideas, including starred challenges (@exr-lecam-coupling, @exr-adjbin-thirdmoment) that probe sharpness and the limits of moment matching. Exercise @exr-adjbin-thirdmoment in particular cements *why* matching stops at two moments.

- **The Notes section (lines 832 to 881)** is candid about what is and is not in the Coq development (lines 876 to 880) and flags missing bibliography entries (Barbour-Hall, Chen) as "proposed additions." This transparency about gaps builds trust.

## Suggestions

1. **Add a concrete clinical motivating example in the introduction.** Name a therapy area (oncology response, cardiovascular event counts), give numbers, and show the naive binomial failing before the machinery begins. This gives the whole chapter a reason to exist for a health researcher.

2. **Move a stripped-down version of the worked example's first two steps up to just after @prp-marginal-binomial.** The conditional-versus-marginal distinction needs numbers immediately, not 600 lines later.

3. **Add a one-line gloss at first use of "mixed Poisson," "$\operatorname{expit}$," "$\boldsymbol\beta_{\mathrm{tot}}$," and the law of total variance.** Each costs a clause and saves a beginner a lookup.

4. **Insert a "strategy" paragraph at the head of @sec-lecam** listing the four ingredients (TV definition, three-forms lemma, coupling inequality, exponential inequality) and the plan (single-pair coupling, independent assembly, union bound). The reader should see the scaffolding before climbing it.

5. **Motivate @lem-poisson-convolution's second proof before giving it.** One sentence, "We record a second proof because its mechanism is what fails for the Bernoulli," reframes the redundancy as purpose.

6. **Expand the Gaussian-covariate part of @thm-poisson-aggregate** with two more lines on why an affine function of a multivariate normal is normal and why exponentiating gives a log-normal with $M(1)$ and $M(2)$ moments. This is the chapter's headline overdispersion formula and deserves the extra scaffolding.

7. **Add a diagram.** A single figure plotting the four distributions from the worked example (Poisson binomial, adjusted binomial, integrated binomial, Le Cam Poisson) on one axis would convey more than the prose comparison at lines 786 to 800.

8. **Close the copula loop.** Tell the reader, even in one sentence, how the $p_i$ in this chapter connect to the Gaussian-copula integration nodes of Chapter 22, so the chapter does not feel divorced from the ML-NMR pipeline a beginner has heard about.

9. **Reconcile the introduction's length with the body's demands.** Trim the preview of Le Cam and the adjusted binomial in the introduction (lines 40 to 50) to a single sentence each; the body develops them fully and the preview dilutes the punch.