# Feedback: Chapter 04 — Probability

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part1/04-probability.qmd`

## Overall impression

I am overwhelmed. This is a dense, technically demanding chapter that moves very fast from measure theory through to the multivariate normal. The opening framing connecting probability to ITCs is clear and motivating (lines 5-34), and the worked example at the end (lines 1059-1148) finally gave me something concrete to hold onto. But between those two anchors, the chapter is almost entirely formal with very few health-research touchpoints. For a health researcher whose last math was an intro biostatistics class, the jump from "a patient is an outcome $\omega$" (line 58) to the Radon-Nikodym theorem (line 273) is enormous. I genuinely could not follow large stretches of the proofs in the middle sections. The book promises to take a naive researcher to mastery, but this chapter reads like it was written for someone who already had a graduate measure theory course and just needs a refresher.

## What was unclear

- **The whole $\sigma$-algebra setup (@def-probability-space, lines 41-56).** I understand the three parts of the triple in a vague way, but the countable additivity axiom (eq-countable-additivity) is stated with the $\bigsqcup$ symbol, which I had to guess means "disjoint union." The text never defines $\bigsqcup$ explicitly. Is that standard notation I should just know? It is not in `notation.qmd`.

- **Why countable and not finite (lines 60-63).** The text says countable unions "is what separates a $\sigma$-algebra from a mere algebra of sets, and it is what makes limiting operations, on which all of analysis depends, available." I believe this matters, but I have no intuition for *what* limiting operation, *what* analysis. A one-line example of a limit of events that we actually need would help.

- **Closure properties of $\sigma$-algebras (@lem-sigma-algebra-closure, lines 67-85).** The proof uses "De Morgan's law" without restating it. A noob may not remember it. Also `limsup` and `liminf` of sets (lines 72-73) are defined inline with no intuition. I had to stop and puzzle out what $\bigcap_{m\ge 1}\bigcup_{n\ge m}A_n$ means as an event. A parenthetical "i.e. the event that $A_n$ occurs for infinitely many $n$" right there would have saved me several minutes; that intuition only shows up later in @exr-borel-cantelli (line 1186).

- **Measurable space notation (@def-random-variable, lines 104-118).** The definition introduces $(\mathcal{S},\mathcal{S}')$ as a "measurable space" without ever defining that term cleanly beforehand, and then immediately specializes to $(\mathbb{R},\mathcal{B}(\mathbb{R}))$. The prime notation $\mathcal{S}'$ for a $\sigma$-algebra is confusing because it looks like a derivative. Why not $\mathcal{A}$ or $\mathcal{S}$-subscript?

- **The pushforward $P_X$ (eq-pushforward, lines 113-117).** "Pushforward" is used as if I already know what it means. I can reverse-engineer it from the formula, but a one-sentence gloss ("the law of $X$ is obtained by pushing the measure $P$ forward through $X$") would help.

- **The change-of-variables identity (eq-change-of-variables, lines 154-158).** This is presented as a "practical dividend" but the equality of the two integrals is stated, not justified. For a noob it is not obvious that integrating $h$ over $\Omega$ against $P$ equals integrating $h$ over the values of $X$ against $P_X$. I would like at least a sentence saying "this is why we can compute everything in terms of $X$ and never look at $\Omega$ again."

- **Expectation construction (lines 162-170).** The three-stage construction (simple, nonnegative, general) is compressed into one paragraph. I understand the skeleton but the line "such sequences exist by the standard dyadic approximation" (line 207) is the first time dyadic approximation is mentioned and it is not explained. The reference to Billingsley is fine but I cannot tell if I am expected to know this already.

- **Conditional expectation definition (@def-conditional-expectation, lines 259-271).** This is the single hardest definition in the chapter for me. The "defining property" (eq-cond-exp-defining) is an integral identity, and I understand *what* it says, but I do not understand *why* this is the right definition of conditional expectation. The discrete motivation (line 254) is one sentence and then we jump to the measure-theoretic version. A worked two-line example: "if $Y$ is a constant, then $\mathbb{E}[Y\mid\mathcal{G}]=Y$; if $\mathcal{G}=\sigma(X)$ for a discrete $X$, this recovers the elementary formula" would ground it.

- **The Radon-Nikodym existence argument (lines 273-281).** This paragraph names the Radon-Nikodym theorem, a signed measure $\nu$, absolute continuity, and a density $d\nu/dP|_{\mathcal{G}}$, all in four lines. I have no idea what any of this is. If I am meant to take it on faith, say so more plainly: "this is a deep theorem of measure theory; we cite it and move on."

- **Taking out what is known (lines 318-320).** The phrase appears with a short parenthetical. I had to read it three times. A one-line "this says: if $g(X)$ is already determined by $X$, then it can be pulled out of a conditional expectation over $X$" would be much clearer.

- **The graphoid proof (@thm-graphoid-axioms, lines 423-472).** This proof is the densest in the chapter. The (G3) argument (lines 431-450) in particular chains several "by the defining property" and "taking out what is known" steps with nested conditional expectations. I lost the thread around line 445. For a health researcher this is well beyond my reach without a step-by-step annotation or a worked example on three binary variables.

- **Supporting line lemma proof (@lem-supporting-line, lines 501-518).** The slope inequality is stated and "verified" but the rearrangement from convexity to the two-sided bound (lines 506-508) is too fast. "subtracting $\varphi(s)$ or $\varphi(u)$ and dividing by the appropriate positive length" handwaves the actual algebra. I would like the two displayed inequalities written out explicitly.

- **MGF differentiation under the integral (@thm-mgf-moments proof, lines 681-697).** The bound $|x|^k\le k!\,r^{-k}e^{r|x|}$, the mean-value-theorem step, and the dominating variable argument are all correct but compressed. The line "$u\,e^{r'u}\le C\,e^{r''u}$ for $u\ge 0$" (line 690) is asserted with no derivation. Where does $C$ come from?

- **The conditional MVN proof (@thm-mvn-conditional, lines 1009-1049).** Defining $\mathbf{U}$ as the "regression residual" is clever, but the cross-covariance computation (lines 1020-1023) and the covariance of $\mathbf{U}$ (lines 1029-1032) are dense. The step where $\mathbf{U}\perp\mathbf{X}_2$ implies the conditional MGF factors (line 1038) is stated very tersely. This is the proof the intro told me to read in full (line 31); I could not follow it unaided.

## What wasn't elaborated enough

- **The transition from discrete to measure-theoretic conditional expectation (lines 254-257).** This is a pivotal moment and it gets two sentences. The $0/0$ problem for continuous $X$ is the entire motivation for the abstraction, and it deserves a fuller paragraph, ideally with a picture or a concrete example: "for continuous $X$, $P(X=x)=0$ for every $x$, so the elementary ratio is undefined; the measure-theoretic definition sidesteps the pointwise value entirely."

- **The law of total variance (@cor-total-variance, lines 345-369).** This is flagged as important for "mixed-count likelihoods later" (line 343) but the forward reference is vague. A one-sentence health example ("the variance of a hospital's mortality count decomposes into within-patient-risk variance plus between-ward variance") would make it stick.

- **Jensen's inequality and aggregation bias (lines 545-549).** The chapter says the Jensen gap "will be aggregation bias and non-collapsibility" but never shows the connection. A single concrete teaser, e.g. "a logit mean over a heterogeneous population is not the logit of the population mean", would make the abstract statement land.

- **The ESS bound (lines 583-587).** This is the one place where the chapter directly touches a weighting method (MAIC). But the derivation jumps from Cauchy-Schwarz under the empirical measure to the ESS formula in one sentence. I would like the empirical-measure setup spelled out: what is the probability space here, what are $X$ and $Y$ in this instance of Cauchy-Schwarz.

- **Poisson binomial motivation (lines 810-812).** The text says this is "the law of an aggregate event count when individual risks vary, which is exactly the situation in covariate-adjusted meta-analysis." Good, but I want one concrete trial-style sentence: "if 100 patients each have their own baseline risk $p_i$ of an event, the total event count is Poisson binomial, not binomial."

- **The multivariate normal definition via MGF (@def-mvn, lines 876-886).** Defining a distribution by its MGF is unintuitive for a noob who thinks of distributions by their densities. The text notes this "handles singular covariance matrices without special cases" (line 874) but never explains why singular covariance is a case we care about (e.g. perfect collinearity in a design, deterministic linear combinations).

## Missing motivation / "why does this matter?"

- **The opening (@sec-prob-intro) is the strongest part.** Lines 5-34 do a good job saying why probability underpins ITCs. But after that, the ITC thread almost completely disappears until the ESS remark (line 583) and the Poisson binomial remark (line 810). The middle 600 lines feel like a generic measure theory chapter, not a chapter oriented toward indirect comparison.

- **@thm-tower-property (lines 283-315).** The intro (line 18-20) flags the tower property as load-bearing for identification, but the theorem statement and proof give no ITC motivation at all. A one-line "this is the identity that lets us go from a conditional mean (what we can estimate) to a marginal mean (what we want to estimate)" would tie it back.

- **@def-conditional-independence and @thm-graphoid-axioms (lines 392-476).** The text says these "is exactly how the propensity-score reduction of Part II is justified" (lines 404-405). That is a strong claim but it is not unpacked at all. As a noob I have no idea what "propensity-score reduction" means or how a graphoid axiom gets you there. Even a forward pointer to a specific Part II section would help.

- **@thm-cov-psd (lines 615-647).** Why do I care that every PSD matrix is a covariance? The converse construction is elegant but the ITC payoff is not stated. The link to "linear models of Chapter 6" and "normal-approximation likelihoods" is mentioned in passing (line 1057) but never tied to an ITC use case.

- **@thm-mvn-conditional (lines 995-1049).** The text says the linear conditional mean is "the population analogue of a linear regression" (line 1053). Good. But why does this matter for ITC specifically? A sentence connecting to "the conditional mean we integrate over a target population's covariate distribution in ML-NMR" would close the loop.

- **Why prove things at all?** Several results (linearity of expectation, tower property) are things a noob would happily take on faith. The chapter proves them in full, which is consistent with the book's rigor policy, but it never says *why* the proof matters for a health researcher. A short remark near line 190 saying "we prove linearity from the construction because every IPW estimator we build later relies on it, and seeing the construction makes the limit theorems we cite later trustworthy" would motivate the effort.

## Missing examples and intuition

- **No running clinical-trial example.** The one clinical reading (lines 58-60: an outcome $\omega$ is a patient record) is excellent but it is never extended. I would love a single thread: define a probability space for a toy trial, define a random variable for "treatment assigned," compute a conditional expectation, show the tower property concretely. The bivariate normal worked example (@sec-worked-bvn) is good but it is pure math, not ITC.

- **No example for conditional expectation.** The discrete-to-measure-theoretic jump (lines 254-257) cries out for a tiny example: two binary covariates, one binary outcome, compute $\mathbb{E}[Y\mid X]$ both ways.

- **No example for the graphoid axioms.** These are abstract and the proof is brutal. A three-binary-variable example showing decomposition and contraction in action (e.g. "treatment $\perp$ outcome given covariates") would make them usable.

- **No example for Jensen's inequality in the ITC setting.** The $\varphi(u)=u^2$ instance (lines 545-548) is fine but purely mathematical. The ITC-relevant instance is a nonlinear link function. Even a forward-looking example with the logit link, deferred to Part II, would motivate the gap.

- **The Poisson binomial example (@sec-worked-pobin) is good** and I could follow it. More like this, please, for the harder concepts.

## Notation and jargon problems

- **$\bigsqcup$ (eq-countable-additivity, line 53).** Disjoint-union symbol, never defined. Add to `notation.qmd` or define inline.

- **$\mathcal{S}'$ as a $\sigma$-algebra (line 106).** The prime is confusing. Suggest $\mathcal{A}$ or $\mathcal{S}_{\mathrm{Bor}}$.

- **$L^1$, $L^2$ (lines 169, 226).** Introduced without expansion. A noob may not know these are function spaces. One parenthetical "the space of integrable random variables" and "the space of square-integrable random variables" at first use would fix it.

- **"Almost surely" / "a.s." (line 178 onward).** Used heavily from @thm-monotone-convergence on, but the phrase is never defined. It means "outside a set of $P$-measure zero"; say so once.

- **$\uparrow$ notation (line 178, 208).** "$X_n\uparrow X$" for monotone convergence is compact but undefined. A noob reads it as an arrow.

- **$\mathbf{1}_A$ / $\mathbf{1}\{X=x\}$ (lines 164, 254).** Indicator notation switches between subscript and brace forms with no explanation.

- **$\mathcal{N}_p$ vs $\mathcal{N}$ (line 878 vs line 838).** The subscript distinguishes dimension. Fine, but the univariate $\mathcal{N}(\mu,\sigma^2)$ uses variance as the second argument while the multivariate uses covariance. A noob will wonder if $\mathcal{N}_2(\boldsymbol{\mu},\boldsymbol{\Sigma})$ takes variance or covariance; state it.

- **$F_X(-\infty)$, $F_X(+\infty)$ (line 146).** Limits at $\pm\infty$, but written as if evaluated. Fine for the trained reader, ambiguous for a noob.

- **"Generalized inverse" / "quantile function" (line 149).** Introduced in a clause. If it is used later, define it more carefully; if not, drop it.

- **"Sigma-finite measure space" (@thm-fubini-tonelli, line 594).** Undefined term. Add a one-line gloss.

- **"Schur complement" (line 1005).** Named but not defined; the formula is right there but the name is dropped without context.

- **Notation drift between chapters.** `notation.qmd` lists $M_X(\mathbf{t})=\mathbb{E}[e^{\mathbf{t}^\top X}]$ (line 77), but the chapter writes $M_X(\mathbf{t})$ for a vector $X$ in @def-mgf (line 662) with $X$ rather than $\mathbf{X}$. Minor but it will confuse the careful reader checking against the notation chapter.

## Pacing issues

- **The opening is fast but fair.** Lines 5-34 do a lot, but the three-tool preview is genuinely helpful.

- **@sec-prob-space through @sec-conditional (lines 36-370) is a wall.** Five major sections, several deep proofs, almost no examples, in roughly 330 lines. This is where I nearly gave up. The conditional expectation section in particular introduces the Radon-Nikodym theorem, proves the tower property, and states three corollaries in under 90 lines.

- **@sec-inequalities (lines 478-600) is well-paced.** Jensen and Cauchy-Schwarz get room to breathe and the supporting-line lemma is a nice self-contained unit.

- **@sec-cov-psd and @sec-mvn (lines 604-1057) are fast again.** The multivariate normal is defined by MGF, density derived, affine maps proved, uncorrelated-blocks lemma, conditional distribution, all in sequence. Each result depends on the last and there is no pause for an example until @sec-prob-worked (line 1059). Consider interleaving a small example after @thm-mvn-linear.

- **The worked example comes too late.** @sec-prob-worked (line 1059) is excellent and I wish I had met a slimmer version of it much earlier, at least after @sec-conditional. Right now the reader survives 700 lines of abstraction before any concrete arithmetic.

- **@sec-distributions (lines 749-867) feels slightly out of place.** Cataloguing Bernoulli, binomial, Poisson, normal mid-chapter, after the MVN groundwork, is a change of gear. It might sit better before @sec-mvn so the MVN definition can lean on the univariate normal.

## What worked well

- **The introductory section (@sec-prob-intro).** The three-tool preview (expectation/tower, Jensen, MVN) is the clearest roadmap in the chapter. I knew what to watch for.

- **The clinical-trial reading of a probability space (lines 58-60).** Short, concrete, exactly the kind of grounding a health researcher needs. More of this, please.

- **The ESS bound derivation (lines 583-587).** This is the one place the chapter shows *why* a theorem matters for ITC, and it landed. Cauchy-Schwarz becomes the reason MAIC loses precision under poor overlap. Excellent.

- **@sec-prob-worked (lines 1059-1148).** The bivariate normal carried through every theorem, with checkable arithmetic, was the most educational part of the chapter for me. The law-of-total-variance check (lines 1109-1112) and the Jensen gap computation (lines 1124-1127) made the abstract results click.

- **The Poisson binomial worked example (lines 1129-1148).** Concrete, verifiable, and it directly illustrates the convexity remark about risk spreading. Good.

- **The exercises (@sec-prob-exercises).** The starred exercises (@exr-cov-psd-construction, @exr-graphoid-counterexample) are well chosen and the unstarred ones are at a reasonable level. The Borel-Cantelli exercise (@exr-borel-cantelli) cleverly doubles as the intuition for $\limsup$ of sets that was missing in the main text.

- **The notes and references (@sec-prob-notes).** The mapping back to catalogue identifiers A.1 through A.10 is helpful for orientation, and the honest statement about which foundational facts are taken as axioms in the Coq development (lines 1178-1180) is exactly the kind of transparency a careful reader appreciates.

- **Honest citation policy.** Results stated without proof are clearly marked "(cited)" in the theorem header (e.g. @thm-monotone-convergence, @thm-fubini-tonelli, @thm-mgf-uniqueness). This is good practice and I trusted the chapter more for it.

## Suggestions

1. **Add a running clinical-trial example** threaded through the abstract sections. Define a toy two-arm trial probability space in @sec-prob-space, define a treatment-indicator random variable in @sec-random-variables, compute a conditional expectation in @sec-conditional, and invoke the tower property on it. This single thread would transform the chapter for a health researcher.

2. **Expand the discrete-to-measure-theoretic conditional expectation transition (lines 254-257)** to a full paragraph with a tiny binary example. This is the conceptual hinge of the chapter and it is currently underspecified.

3. **Move a slim version of the worked example earlier.** A short bivariate-normal mini-example after @thm-mvn-linear, showing just the affine map and the marginal, would break the abstraction wall in @sec-mvn and give the reader something to hold before the conditional distribution proof.

4. **Define every piece of jargon at first use** in a parenthetical: "almost surely (i.e. with probability one, outside a set of measure zero)", "$L^1$ (the space of integrable random variables)", "$\bigsqcup$ (disjoint union)", "sigma-finite (admitting a countable cover by finite-measure sets)". These are cheap additions that massively lower the barrier.

5. **Annotate the graphoid proof (@thm-graphoid-axioms, G3 in particular)** with a concrete three-binary-variable example interleaved with the symbolic steps. The proof is currently inaccessible to the intended reader.

6. **Add ITC motivation to the load-bearing theorems.** One sentence each after @thm-tower-property, @thm-jensen, @thm-cov-psd, and @thm-mvn-conditional saying *which* ITC result it powers. The intro promises this; the body does not deliver it.

7. **Show the Jensen-ITC link concretely.** Even a deferred one-paragraph example with a logit link and a two-point covariate distribution, showing $\mathrm{logit}^{-1}(\mathbb{E}[\eta])\ne\mathbb{E}[\mathrm{logit}^{-1}(\eta)]$, would make @thm-jensen feel like the source of non-collapsibility rather than an abstract inequality.

8. **Reconcile and complete notation.** Add $\bigsqcup$, $\uparrow$, $L^1/L^2$, "a.s.", and the $\mathcal{S}'$ measurable-space notation to `notation.qmd`, and make the chapter's $X$ vs $\mathbf{X}$ usage in @def-mgf consistent with the notation chapter.

9. **Soften the Radon-Nikodym paragraph (lines 273-281).** Explicitly say "this is a deep result we cite; the construction is not needed for anything that follows." A noob who stops to look it up will lose an hour and gain nothing usable.

10. **Pace the middle sections.** @sec-prob-space through @sec-conditional is too dense for one sitting. Consider splitting @sec-conditional into "definition and existence" and "properties and the tower property" with a short example between them.