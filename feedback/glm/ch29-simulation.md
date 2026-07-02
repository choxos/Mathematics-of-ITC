# Feedback: Chapter 29 — Simulation

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part6/29-simulation.qmd`

## Overall impression

I came in hoping this chapter would finally show me *why* all the math in Parts II to V matters for my job: I run indirect comparisons for an HTA dossier, I have one index trial with 230 patients and a published mean for the comparator, and I need to know whether MAIC or Bucher or ML-NMR is trustworthy *at my sample size*. The opening (@sec-sim-intro, lines 7 to 27) nails that motivation: it says the consistency theorems are "statements about the horizon" and the analyst "stands at a finite distance from it." That single image carried me through the chapter. The two-sample-size framing ($n$ versus $R$, lines 30 to 42) is the most useful idea in the whole file and I will remember it.

But the chapter is dense. It reads like it was written for someone who already took a graduate asymptotics course, not for a health researcher with basic calculus. The proofs are mostly fine (the MSE decomposition, the bias MCSE, the binomial coverage are all elementary and well done), but the coverage-collapse section (@sec-sim-misspec, lines 517 to 685) suddenly becomes a real analysis lecture: Slutsky, continuity points, limsup bounding arguments, uniform integrability. I could follow the *statement* of @thm-coverage-misspecification but the proof at lines 617 to 631 lost me, and the remark at lines 666 to 683 piles on references to non-collapsibility, aggregation bias, transitivity bias, and sandwich variance without pausing to say in plain language what just happened. The miniature example (@sec-sim-example) is excellent and is the section I will re-read, but it arrives only at line 924, after 800 lines of abstraction; it should appear much earlier as a running thread, not a payoff.

The chapter also never gives me a concrete drug or trial. There is no "Suppose we are comparing a new oncology drug $A$ to $B$ for plaque psoriasis, with $BC$ as the common comparator" anywhere. Every example is symbolic ($\theta=1.5$, $\bar{\mathbf{x}}_{BC}=(0.5,0.5)$), and I had to supply the clinical meaning myself. For a chapter whose whole point is that consistency theorems do not tell you what happens at a "health-technology-assessment dossier" sample size (line 12), the refusal to name a single disease, drug, or endpoint is a missed opportunity.

## What was unclear

- **@sec-sim-intro, lines 29 to 42 (two-sample-size paragraph).** The sentence "a performance measure such as bias or coverage is a functional of the estimator's sampling distribution at a fixed $n$, hence a fixed but unknown number" (lines 35 to 36) stopped me cold. What is a "functional of a distribution"? I know what a function is (a number in, a number out) but "functional of the sampling distribution $F_n$" is never defined until @def-sim-performance-functional at line 123, much later. A one-line gloss up front ("a functional is just a rule that takes the whole distribution $F_n$ as input and returns a single number, like its mean or its variance") would save me from skimming.

- **@def-ademp, item E, line 100.** "Estimands (E). The target quantities, defined as functionals $\theta=\theta(\mathbb{P})$ of the DGM." Same problem: I do not yet know what a functional is. And the phrase "by analytic calculation or by a large auxiliary simulation" (line 103) is dropped without explanation: how do I compute the true $\theta$ from a known DGM? The chapter never shows this. For a binary-effect-modifier logistic model, is it an integral over the covariate distribution? A marginal standardization? A pointer to where this was done earlier would help.

- **@def-sim-performance-functional, lines 123 to 141.** This definition introduces "the sampling distribution $F_n$" as the law of the triple $(\hat\theta_n,\widehat{\mathrm{SE}}_n,I_n)$. I had to read it three times to realize $F_n$ is a joint distribution over a *vector-valued* random object, not a scalar. The notation $F_n$ is used as if scalar throughout (e.g., "a functional $\mu(F_n)$"), and I kept conflating it with the marginal law of $\hat\theta_n$. Saying "$F_n$ is the joint law of the whole triple; we usually only need its marginals" would resolve it.

- **@lem-sim-empse-unbiased, lines 292 to 341.** The proof of the $(R-1)$ denominator (lines 305 to 322) is the single most over-explained and under-explained passage at once. The parenthetical at lines 308 to 312 ("explicitly, $\sum_r(\hat\theta^{(r)}_n-\bar{\hat\theta})^2=\sum_r(\hat\theta^{(r)}_n-\nu)^2 -2(\bar{\hat\theta}-\nu)\sum_r(\hat\theta^{(r)}_n-\nu)+R(\bar{\hat\theta}-\nu)^2$ ...") is the algebraic identity written out twice in two different forms in the same sentence. For a weak-math reader, this is the opposite of help: I want the identity stated once, cleanly, with a one-line intuition ("centering about the sample mean instead of the population mean removes one degree of freedom"). The derivation of $\mathrm{MCSE}(\mathrm{EmpSE})$ via the chi-square law and delta method (lines 329 to 340) is correct but assumes I remember that $(R-1)S^2/\mathrm{Var}_n\sim\chi^2_{R-1}$ requires normality; the hypothesis "if in addition $\hat\theta_n$ is normally distributed under the DGM" (lines 297 to 299) is buried mid-sentence and I almost missed that the formula @eq-sim-mcse-empse is *normality-only*, not universal. That limitation should be flagged next to the formula, not only in the prose.

- **@thm-coverage-misspecification, lines 563 to 632.** The conditions (C1) to (C3) are stated cleanly, but the phrase "calibrated asymptotic bias $(\theta_0-\theta)/\sigma_n\to b$ for some $b\in[-\infty,\infty]$" (line 575) is the first place the symbol $b$ can be infinite, and it is not explained *what it means for a sequence to converge to $\pm\infty$* until the infinite-$b$ branch of the proof (lines 617 to 628). A weak reader needs the intuition first: "if the bias $\theta_0-\theta$ is a fixed nonzero constant while $\sigma_n\to 0$, the standardized bias blows up; we record that as $b=\pm\infty$." Stated before the theorem, it would make (C3) transparent.

- **@thm-coverage-misspecification proof, lines 617 to 628 (infinite $b$ branch).** This is the hardest passage in the chapter for me. The bounding argument "On the event $\{D_n\ge M\}$ we have $T_n\ge W_n+M$, hence $\{T_n\le z\}\subseteq\{W_n\le z-M\}\cup\{D_n<M\}$" (lines 620 to 621) is a set-inclusion trick I have never seen. A diagram or a one-sentence English gloss ("we are forcing $D_n$ to be large; then the test statistic is dragged above $z$ unless the random part $W_n$ compensates by being very negative, which has tiny probability") would help. As written I cannot reconstruct it without a textbook.

- **@prp-sim-efficiency-baseline, lines 788 to 832.** The hypothesis "$\{n(\hat\theta_n-\theta)^2\}_n$ uniformly integrable" (line 792) is the first time uniform integrability appears, and it is used but not motivated. The proof (lines 815 to 819) says "uniform integrability plus convergence in distribution implies convergence of the corresponding expectations; see @billingsley1995." For a reader who has never seen uniform integrability, this is a black box the proof hinges on. Either drop the proof to a remark ("the upgrade from convergence in distribution to convergence of variances requires a regularity condition; we cite the standard result") or add two sentences on what uniform integrability rules out (heavy tails, the MAIC-dominating-weight scenario of lines 843 to 845).

- **@prp-phillippo-robustness, lines 858 to 903.** The six-item ordering is the chapter's payoff for a health researcher, but several items use jargon I had to chase down: "adequate overlap" (item 3, line 877), "no-extrapolation limit @thm-maic-no-extrapolation" (item 4, line 883), "the $b=\pm\infty$ extreme of @thm-coverage-misspecification" (item 6, line 892). "Adequate overlap" is never quantified: is it ESS $>50$, ESS $>n/10$, a covariate-support condition? The ordering would be far more actionable if each item carried the rule of thumb the simulation literature actually uses.

## What wasn't elaborated enough

- **The whole "estimand under the working model" concept (lines 528 to 531).** The distinction between $\theta$ (the true estimand) and $\theta_0$ (the working-model target) is the conceptual hinge of @sec-sim-misspec, and it gets four lines. I needed: (a) a concrete instance ("when MAIC omits an imbalanced effect modifier, $\theta_0$ is the contrast the omitted-model MAIC converges to, which is the index-population contrast $d_{AC(\mathcal{P}_{AC})}$ shifted by the imbalance"), and (b) a picture relating $\theta$, $\theta_0$, and the estimator. The miniature example supplies this implicitly at lines 953 to 956 but too late.

- **The connection from @thm-coverage-misspecification back to MAIC/STC/ML-NMR.** The remark at lines 666 to 683 lists which earlier theorems the bias corresponds to (@thm-failure-of-bucher, @thm-aggregation-bias, @def-non-collapsibility) but never walks one through. I wanted: "For MAIC with an omitted effect modifier of strength $\beta_1$ imbalanced by $\Delta\bar{x}_1$ between trials, the working-model target $\theta_0$ differs from $\theta$ by approximately $\beta_1\Delta\bar{x}_1$, so the standardized bias $b\approx\beta_1\Delta\bar{x}_1/\sigma_n$, and coverage collapses once $n$ is large enough that $\sigma_n\ll\beta_1\Delta\bar{x}_1$." That single sentence would convert the theorem from abstract to operational.

- **@sec-sim-power, lines 687 to 777.** The claim "Type I error and power are governed by exactly the machinery of the previous section through the duality of tests and intervals" (lines 690 to 693) is asserted and proved, but I never got the *why care* for ITC. The remark at lines 764 to 774 says "population-adjustment simulations report power chiefly to inform the sample size a future head-to-head or single-arm study would need" but gives no example. A one-paragraph worked instance ("a future $AC$ versus $BC$ trial to detect a benefit of $0.3$ at $80\%$ power needs $n\approx\ldots$") would justify the section's existence for a health researcher who otherwise never computes power.

- **The sandwich-variance reference (line 395 to 396, lines 666 to 683).** "For MAIC and simulated treatment comparison the relevant $\widehat{\mathrm{SE}}_n$ is the sandwich standard error of @def-sandwich-variance and @thm-maic-sandwich-variance" is stated as if I remember what a sandwich variance is. I do not. The chapter assumes I carry Chapter 18 in my head. A two-line refresher ("the sandwich variance corrects the naive variance for the fact that the MAIC weights are estimated, not fixed; ignoring this gives the $\mathrm{ModSE}<\mathrm{EmpSE}$ undercoverage the simulation diagnoses") at first mention would help.

- **The unanchored comparison paragraph in @prp-phillippo-robustness (lines 895 to 902).** This is one dense sentence listing multilevel unanchored meta-regression, the shared-prognostic-factor assumption, its absolute form, subgroup aggregate data, and the shared-effect-modifier insufficiency, all in 8 lines. I cannot parse it. It needs to be split into the same six-item structure as the anchored ordering, or at least broken into clauses with the assumption names spelled out.

## Missing motivation / "why does this matter?"

- **Why simulate at all, before line 25.** The introduction says consistency is a limit statement and "four questions remain open at that distance" (lines 14 to 16), then lists them (lines 18 to 24). That is good. But it never says the obvious thing a noob needs to hear: *in a simulation we play God; we know the truth, so we can measure error directly, which we can never do with real data where the truth is unknown.* That single sentence, near line 25, would frame the entire instrument for me.

- **Why prove the bias estimator is unbiased (lines 187 to 222).** The proof of @lem-sim-bias-unbiased is two lines of algebra and obvious. What is not obvious is *why it matters*: the point is that the Monte Carlo estimator of bias is trustworthy even at small $R$, so the only thing limiting us is the $1/\sqrt{R}$ MCSE, not a systematic error in the estimator. The remark at lines 242 to 249 says this obliquely ("a bias estimate of $0.03$ with MCSE $=0.05$...") but the *theorem* is not motivated. A sentence before the lemma: "we want to know that the number we report as 'the bias' is itself unbiased; otherwise our error bar would itself be biased" would help.

- **Why the MSE decomposition is "the one genuine theorem among the performance measures" (line 411).** The line is intriguing but unexplained. The reason it matters is that it lets a simulation *partition* total error into a fixable part (variance, reducible by more data or a better method) and an unfixable part (squared bias, reducible only by correcting the model). The bias-variance remark at lines 502 to 513 says this for MAIC but only after the theorem; the theorem statement itself is unmotivated.

- **Why coverage collapse is "at first counterintuitive" (lines 522 to 525).** The chapter says it is counterintuitive that "more data makes a biased method's intervals worse" but does not say *why* it is counterintuitive: because in everyday statistics more data is always better. The intuition that "more data shrinks the interval around the wrong center, so the truth falls outside an ever-narrower window" should be stated in one sentence right at lines 524 to 525, before the formal setup, so the formal result lands as a confirmation rather than a surprise.

- **Why ADEMP is adopted as the backbone (lines 79 to 85).** I am told ADEMP "distilled good practice" and is "now-standard," but not why it is better than just running a simulation and reporting bias. The five components read as a checklist; the *reason* each component matters (you can fool yourself by simulating an un-reconstructable DGM, by reporting the wrong estimand, by hiding behavior in the summary statistic) is gestured at in lines 81 to 83 but only as a list of failure modes, not as the justification for each letter.

## Missing examples and intuition

- **No clinical example anywhere.** The single biggest gap. I want at least one running scenario named in the first paragraph and reused throughout: "We will illustrate every measure on the comparison of a new JAK inhibitor $A$ versus an interleukin-23 inhibitor $B$ for moderate-to-severe plaque psoriasis, with ustekinumab $C$ as the common comparator, the estimand being the log-odds-ratio of PASI-90 response at week 16 in the $BC$ trial population." Then every $\theta$, $\theta_0$, $\bar{\mathbf{x}}_{BC}$, $d_{BC}=3.0$ in the miniature (lines 940 to 950) becomes a real number with a unit, and the coverage collapse (lines 1009 to 1016) reads as "MAIC-with-omitted-age has $83\%$ coverage at $n=200$, $48\%$ at $n=800$, $0.1\%$ at $n=5000$," which is exactly the kind of table an HTA reviewer actually wants.

- **No diagram of the two-sample-size structure.** Lines 30 to 42 and @def-sim-performance-functional describe $n$ (statistical limit) and $R$ (Monte Carlo limit) in prose. A figure with two axes, $n$ running horizontally inside one replication and $R$ stacking replications vertically, with "consistency theorem controls this arrow" and "MCSE controls this arrow," would make the central concept instantly clear. The chapter is otherwise figure-free.

- **No plot of the coverage curve $h(b)$.** @lem-sim-coverage-unimodal (lines 535 to 561) defines $h(b)=\Phi(z-b)-\Phi(-z-b)$, proves it is even and unimodal with a peak at $b=0$ of $1-\alpha$, and shows it decays to $0$. This is begging for a plot: a bell-shaped curve over $b$, peaking at $0.95$, with the nominal line marked, the points $b=1,2,5$ from the miniature table (lines 1009 to 1013) annotated. The exercise @exr-sim-coverage-curve asks the reader to compute it by hand from a table; a figure in the section would teach it faster.

- **No walk-through of a real DGM.** The miniature (@exm-sim-miniature, lines 930 to 1021) posits $\sigma_n$ by hand ("outcome noise of variance making the per-replication sampling standard deviation ... equal to $\sigma_n$," lines 943 to 945). I never see a *generative* DGM: draw covariates, draw treatment, draw outcomes from a logistic or linear model, compute the estimator. The remark at lines 1031 to 1035 admits this ("what the miniature hides is the realism of a true data-generating mechanism, where outcomes are drawn with noise, weights are estimated, and $\sigma_n$ emerges from the design"). A second small example, even one paragraph, showing the actual draws for one replication of a logistic-outcome MAIC, would close that gap.

- **No numerical intuition for $1/\sqrt{R}$.** @cor-sim-replications-bias (lines 227 to 234) says "halving the Monte Carlo standard error requires quadrupling $R$." That is the key practical rule. I wanted a tiny table: $R=100$ gives MCSE $=\sigma/10$, $R=1000$ gives $\sigma/\sqrt{1000}\approx\sigma/31$, $R=10000$ gives $\sigma/100$, with the bias-MCSE and coverage-MCSE numbers plugged in, so I can feel the rate before I trust the formula.

## Notation and jargon problems

- **$\sigma_n$ versus $\widehat{\mathrm{SE}}_n$.** Throughout @sec-sim-misspec $\sigma_n$ is a "deterministic scale sequence" (line 567) that the analyst never sees, while $\widehat{\mathrm{SE}}_n$ is the method's reported standard error. The notation does not signal that $\sigma_n$ is *theoretical* and $\widehat{\mathrm{SE}}_n$ is *operational*; a subscript like $\sigma_n^{\mathrm{true}}$ or a remark at first use would prevent me from reading them as the same object with a hat.

- **$\theta_0$ is overloaded.** In @sec-sim-misspec (line 528) $\theta_0$ is "the estimand under the working model." In @sec-sim-power (line 697) $\theta_0$ is "the hypothesized null value." In @thm-sim-power (line 717) $\theta_0^{\mathrm{true}}$ appears, and at line 743 the proof reuses $\theta_0$ as the null. Three meanings for one symbol inside two sections. Rename the working-model target (e.g., $\theta^\star$ or $\theta_{\mathrm{work}}$) to disambiguate from the null hypothesis value.

- **$F_n$ used before definition.** @sec-sim-intro (line 119) and the remark at lines 143 to 151 use $F_n$ and "sampling distribution" before @def-sim-performance-functional (line 123) defines it. Forward references are fine in a graduate text but confusing for a noob; a parenthetical "(defined formally in the next display)" would help.

- **"Functional" used without definition until line 123.** See above; appears at lines 35, 113, 119, 126 before the formal definition. A gloss in the introduction would fix it.

- **"Scenario" (lines 98, 148, 915).** The word "scenario" appears throughout (a study comprises a finite set of DGMs, one per scenario) but is never defined as "one cell of the design grid, i.e., one combination of overlap, effect-modification strength, sample size, and method specification." A one-line definition in @def-ademp item D would prevent me from reading it as a synonym for "DGM."

- **"Regular model" / "regular estimator" (lines 790, 799).** @prp-sim-efficiency-baseline invokes @def-regular-model and @def-efficient-estimator without a gloss. A weak reader has forgotten what regularity means (differentiability in quadratic mean, finite Fisher information). Two words of reminder ("regularity excludes super-efficient estimators that exploit discontinuous behavior") would save a backtrack to Chapter 5.

- **"Local alternatives" (line 726).** @thm-sim-power part (2) uses "local alternatives" for $\Delta_n\to\Delta\in\mathbb{R}$. The term is standard in asymptotics but undefined here. The intuition ("alternatives that shrink toward the null at rate $1/\sigma_n$, so the power stays between $0$ and $1$ rather than running to $1$") is exactly what a noob needs and is absent.

- **"Telltale signature" (line 680).** Minor, but "the telltale signature of a biased method is coverage that falls as $n$ grows" is the single most useful practical sentence in the chapter and it is buried in a remark. Promote it to a callout.

## Pacing issues

- **The introduction is 78 lines and the first definition is at line 87.** @sec-sim-intro (lines 5 to 77) is excellent prose but very long for a reader who wants to get to content. The roadmap paragraph (lines 43 to 66) lists every section and its catalogue identifier; for a noob this is a table of contents disguised as a paragraph. Consider trimming or moving to a dedicated "plan of the chapter" callout.

- **@sec-sim-coverage (lines 254 to 404) is too long.** It bundles three distinct objects (EmpSE, ModSE, coverage) and proves two lemmas and a corollary in one section. The empirical-standard-error lemma (@lem-sim-empse-unbiased) with its normality-only MCSE formula could be its own subsection, with the binomial coverage lemma (@lem-sim-coverage-binomial) following. As is, I lost the thread between the $S^2$ proof and the coverage proof.

- **@sec-sim-misspec front-loads the hardest material.** The lemma @lem-sim-coverage-unimodal (lines 535 to 561) and theorem @thm-coverage-misspecification (lines 563 to 632) come before any intuition for *why* coverage collapses. The remark at lines 666 to 683 supplies the intuition but only after the formal proof. Reverse the order: state the phenomenon in plain English ("if you are biased by a fixed amount, your interval shrinks around the wrong number, so the truth eventually lies outside"), give the miniature's coverage table (lines 1009 to 1013) here as motivation, then prove it.

- **The miniature comes at the end.** @exm-sim-miniature (line 924) is the chapter's most pedagogically valuable section and it is the second-to-last. A noob benefits from meeting it early and revisiting it after each performance-measure section. Consider a stripped-down version right after @def-ademp ("here is a 5-replication toy so the symbols have numbers") and the full version at the end.

- **@sec-sim-robustness (lines 849 to 922) is one block of prose with a six-item list.** It is the most important section for a health researcher and it reads like a conclusion. Splitting the anchored ordering (items 1 to 6) from the unanchored paragraph (lines 895 to 902), and putting the "what to do in practice" reading (lines 915 to 919) into its own callout, would make it usable as a reference.

## What worked well

- **The two-sample-size framing (lines 30 to 42).** The single best idea in the chapter and the one I will carry into my own work. The "cardinal sin" sentence (lines 37 to 39) is memorable and exactly right.

- **The bias MCSE section (@sec-sim-bias, lines 159 to 252).** Clean, complete, the proof is elementary, the corollary @cor-sim-replications-bias turns the formula into a design tool, and the reporting-discipline remark (lines 242 to 249) gives a concrete $0.03$ versus $0.003$ example. This is the model for how the other sections should read.

- **The MSE decomposition and its exact finite-sample shadow (@sec-sim-mse, lines 406 to 515).** @thm-mse-decomposition and @lem-sim-mse-empirical-identity are beautifully paired: the population identity and the sample identity, both proved by the same add-and-subtract trick, with the numerical check $0.21=0.01+0.20$ in the miniature (lines 988 to 992). This is the chapter at its best.

- **The binomial coverage lemma (@lem-sim-coverage-binomial, lines 346 to 369).** Short, exact, the bound $\mathrm{MCSE}\le 1/(2\sqrt R)$ and the "$R\approx 1090$" derivation (@cor-sim-replications-coverage, lines 371 to 383) are immediately useful. I will use this number.

- **The miniature example (@exm-sim-miniature, lines 924 to 1021).** Once I finally reached it, every abstract object became concrete: the $R=5$ table, the bias $-0.1$ against MCSE $0.224$, the exact identity check, and the coverage-collapse table (lines 1009 to 1013) showing $0.83\to 0.48\to 0.001$. This is the section that makes the chapter a chapter rather than a sequence of lemmas.

- **The remark on "what the miniature hides" (lines 1023 to 1035).** Rare honesty about the limits of a toy example. I trust a chapter that admits its own example is not realistic.

- **The exercise set (lines 1095 to 1153).** @exr-sim-mcse-arithmetic and @exr-sim-coverage-curve are exactly the right level for a noob; @exr-sim-bias-variance-tradeoff is the right stretch problem. The progression from hand arithmetic to design to theory is well judged.

- **The notes and references (lines 1038 to 1093).** Thorough, honest about what is folklore versus proved, and the final paragraph on "no machine-checked counterpart" (lines 1083 to 1091) is a model of intellectual hygiene.

## Suggestions

1. **Add one running clinical scenario** (a named drug comparison, a named endpoint, a named population) introduced in @sec-sim-intro and reused in the miniature and the robustness section. Convert every $\theta=1.5$ and $\bar{\mathbf{x}}_{BC}=(0.5,0.5)$ into a number with a unit.

2. **Front-load the miniature.** Put a 5-line version of @exm-sim-miniature immediately after @def-ademp so every subsequent definition has numbers to hang on; keep the full version at the end.

3. **Reverse the order in @sec-sim-misspec.** Plain-English statement of the coverage-collapse phenomenon, then the miniature coverage table as evidence, then the lemma and theorem. Move the "telltale signature" sentence (line 680) into a callout.

4. **Disambiguate $\theta_0$.** Rename the working-model target in @sec-sim-misspec (e.g., $\theta_{\mathrm{work}}$) so it does not collide with the null value in @sec-sim-power.

5. **Define "functional," "scenario," "local alternatives," "regular" inline** at first use; one parenthetical each.

6. **Add two figures:** the two-sample-size schematic for @sec-sim-intro, and the coverage curve $h(b)$ for @sec-sim-misspec with the miniature's three points annotated.

7. **Quantify "adequate overlap"** in @prp-phillippo-robustness item 3 (line 877); give the ESS or support-condition rule of thumb the simulations actually use.

8. **Rebuild the unanchored paragraph (lines 895 to 902)** into the same itemized structure as the anchored ordering; the current single sentence is unparseable.

9. **Add a two-sentence sandwich-variance refresher** at line 395 and again at line 666, for readers who do not carry Chapter 18 in working memory.

10. **Soften the uniform-integrability step** in @prp-sim-efficiency-baseline: either prove less (state the regularity condition and cite the result) or prove more (one paragraph on what UI rules out, tied to the MAIC-dominating-weight example the remark already gives).