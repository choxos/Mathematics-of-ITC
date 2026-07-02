# Feedback: Chapter 24 — Computation

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part5/24-computation.qmd`

## Overall impression

I came in hoping to finally understand *how* ML-NMR actually gets fit on a computer and *how* I know I can trust the output, because every paper I read just says "we fit it in Stan" and moves on. This chapter does eventually get me there, and the worked example at the end (@sec-comp-example) is the single most useful thing in the chapter because every number is checkable. But I spent most of the chapter feeling like I was reading a math paper aimed at someone who already knows MCMC, not a textbook chapter aimed at a health researcher who has maybe run `stan_glmer` once. The density of undefined jargon, unstated prerequisites, and "we proved this in Chapter 8" forward references is very high for a chapter that claims to build on Parts I to IV. I now know *more* about why funnels break HMC and why $\widehat R$ works, but I still could not sit down and run a diagnostic with confidence, and I have no idea what a Stan program for ML-NMR even looks like.

## What was unclear

- **Introduction (@sec-comp-intro), lines 15-21.** This paragraph dumps "MCMC," "HMC," "No-U-Turn Sampler," "Stan," "detailed-balance argument," "invariance," "leapfrog geometry," and "divergent transitions" in six lines with zero restatement. As a noob I have no mental model of what a Markov chain Monte Carlo sampler *does* before this chapter uses it as the load-bearing object. The chapter says "we proved in Chapter 8 that HMC leaves the target posterior invariant" but I do not remember Chapter 8 well enough to lean on, and no recap is offered. A two-sentence "MCMC explores the posterior by proposing parameter values and accepting or rejecting them; HMC uses a physics analogy (a puck sliding on a landscape) to propose long, low-rejection moves" would have saved me.

- **@lem-comp-reparam (lines 97-104) and its proof (106-123).** The proof uses "diffeomorphism," "change-of-variables formula," "pushing forward," and "Jacobian determinant" as though I have them loaded in working memory. I have a vague memory of change of variables from a calculus class years ago, but "diffeomorphism of $\mathbb R^J$" is not defined or motivated here. Why does smoothness matter? Why does the constant Jacobian matter? The sentence "A diffeomorphic reparameterization leaves all integrals, hence all posterior expectations and quantiles of any $h$, invariant" is the whole point and it gets one line at the end of the proof.

- **@lem-comp-leapfrog-stability (lines 133-167).** The leapfrog integrator is referenced as "as in @def-hmc" but I do not have @def-hmc in front of me and the three leapfrog substeps are never restated. The proof starts "With $U'(x)=\omega^2 x$, the three leapfrog substeps of @def-hmc read..." and then writes down the updates without telling me what a "half step," "momentum," or "r" even is. I gathered that $r$ is momentum but only by inference. The matrix $A$ in @eq-comp-leapfrog-matrix appears with no intuition for why the entries look like that. The trace/discriminant/eigenvalue argument is fine for someone fluent in linear algebra but I had to read it three times.

- **@thm-comp-param (lines 203-235).** The phrase "no single global $\epsilon$ is both stable in the neck of the funnel and efficient in its mouth" is the clearest sentence in the section, but it comes *after* the formal statement. The funnel as a geometric object is never drawn or described concretely before it is invoked. I had to google "Neal's funnel" to picture it. A figure or even a verbal description ("imagine a trumpet bell: wide where $\tau$ is large, pinched to a needle where $\tau$ goes to $0$") would have made the whole section click.

- **@thm-gelman-rubin, Part 2 (lines 340-347).** The expression "$Nv_N\to\sigma^2(1+2\sum_{k\ge1}\rho_k)$ as $N\to\infty$" is dropped in with a forward reference to @prp-comp-acf-variance, which is two sections later. I read this as "trust me, here is a formula you have not seen yet." The notation $\xrightarrow{p}$ is used without being re-explained (notation.qmd lists it but I had forgotten).

- **@prp-comp-acf-variance (lines 421-447).** "Second-order stationary" is used repeatedly and never defined. I think it means "constant mean and covariance depends only on lag" but the chapter never says so. "Lag-$k$ autocorrelation" is defined by a formula but the *intuition* (how correlated is draw $t$ with draw $t+k$?) is not given before the symbol $\rho_k$ is used everywhere.

- **@sec-comp-integration (lines 513-607).** The phrase "the integrand $f=g^{-1}\!\circ\eta_{jk}\circ\Psi$ folds the inverse link, the linear predictor, and the copula-plus-inverse-CDF transform $\Psi$" is impenetrable for a noob. I do not have a picture of what $\Psi$ does, I only know it was "Chapter 22." A one-line "in words: turn a uniform grid point into a realistic patient covariate vector, compute their predicted outcome, and average" would have made this readable.

- **@lem-comp-loo-identity (lines 645-693).** The proof is the longest in the chapter and it chains several algebraic moves ("removing $y_i$ divides the full likelihood by the $i$-th factor," "Bayes' theorem," "self-normalized form") without narrating the strategy up front. I could follow each line but lost the thread of *why* we were doing each step. A one-paragraph "here is the plan: relate the LOO posterior to the full posterior by a single importance ratio, then read off the harmonic-mean form" before the proof would help enormously.

- **@thm-dic-waic-loo, Part 1 proof (lines 744-761).** The cumulant generating function $K_i(t)$ is introduced and Taylor-expanded, but cumulant generating functions are not in my working vocabulary and the chapter does not remind me what one is. "Third cumulant $\kappa_{3,i}$" appears with no definition. I am asked to accept that $K_i(1)=\log\mathbb E[e^{\ell_i}]$ and $K_i(-1)=\log\mathbb E[e^{-\ell_i}]$ are the two predictive densities, which is the crux of the whole argument, and it is stated in one clause.

## What wasn't elaborated enough

- **The leapfrog integrator.** It is the mechanical heart of the chapter (every stability and funnel result depends on it) and it is never written down here, only referenced as @def-hmc in Chapter 8. For a chapter whose entire point is "the geometry HMC must traverse," the reader needs the integrator re-explained in-line, even if briefly.

- **What Stan actually does.** "Stan" is named once in the introduction and once in the notes. There is no description of what the reference software pipeline looks like: what does the user write, what does the sampler do under the hood, how do warmup and sampling phases relate, what is adaptation. The remark at line 241-244 says "the reference software implements the non-centered parameterization by default" but I never learn what that implementation *is*.

- **The No-U-Turn Sampler.** NUTS is named in line 16 and then never mentioned again in the entire chapter. Given that NUTS is the actual algorithm Stan runs, this is a surprising gap. I am told HMC has a fixed trajectory length and step size and then never told how NUTS removes those choices; the whole "why NUTS instead of plain HMC" question is begged by the introduction and dropped.

- **Warmup vs. sampling.** The chapter repeatedly says "post-warmup length $N$" (line 258) but never explains what warmup is, why draws from it are discarded, or how adaptation during warmup relates to the step-size and mass-matrix story of @sec-comp-param.

- **Divergent transitions.** Line 230 mentions "divergent transitions" as the practical signature of a funnel, and line 243 says a residual funnel shows up as "a cluster of divergent transitions concentrated at small $\tau$." But what a divergent transition *is* (the leapfrog integrator producing an NaN or an energy error above a threshold) is never defined. As a health researcher I will see "divergent transitions" in my Stan output and need to know what it means.

- **Why $N=64$ Sobol' points suffice.** The remark at lines 592-605 asserts empirical grid sizes but gives no sense of *how* one checks this in practice or what the consequence of too few points is. The doubling rule is described abstractly but I never see it inside an actual ML-NMR fit, only on a one-dimensional toy integral.

## Missing motivation / "why does this matter?"

- **Why HMC at all?** The chapter assumes HMC is the right sampler for ML-NMR and never says why. A noob health researcher has maybe used Gibbs or Metropolis and needs to know: HMC scales to high dimensions where random-walk Metropolis fails, and ML-NMR has tens of correlated parameters. The motivation "random-walk samplers die in high dimensions; HMC uses gradient information to take long directed steps" is exactly the pitch a working researcher needs and it is absent.

- **Why prove the leapfrog stability lemma?** @lem-comp-leapfrog-stability is a self-contained fact about a harmonic oscillator and it is not obvious from the chapter why we are spending a page on it. The punchline ("the largest usable step is $2/\sqrt{\lambda_{\max}}$") lands at line 170-172, but the *reason* we care, namely that this single inequality explains both the funnel pathology and the non-centered fix, is only made explicit at the very end of @thm-comp-param. I would have preferred the motivation up front.

- **Why the two parameterizations matter for ITCs specifically.** The funnel is a generic hierarchical-model problem. The remark at lines 237-245 does connect it to ML-NMR's $\mu_j$ and $\delta_{j,1k}$, but only in a remark. The *consequence* for a health technology assessment submission ("your NMA has three studies per contrast, so you are in the prior-dominated regime, so use NCP or you will get divergences and an untrustworthy $\tau$") is the thing a health researcher needs and it is buried.

- **Why model comparison at all in this chapter.** @sec-comp-ic and @sec-comp-psis appear with no ITC motivation. In practice a health researcher compares competing ML-NMR models (different outcome models, different covariate sets, anchored vs. unanchored) and needs to know which fits better. The chapter never says "you will be asked, in an HTA submission, to justify your choice of outcome model or covariate set, and WAIC/LOO is the Bayesian answer to that question."

- **Why the doubling rule rather than just using more points.** The operational question "why not always use $N=256$?" is never addressed. Computation cost is the obvious answer (every likelihood evaluation re-runs the QMC sum inside HMC, so the cost scales with $N$ times the number of leapfrog steps times the number of post-warmup draws) but the chapter never makes this cost explicit.

## Missing examples and intuition

- **No figure of the funnel.** This is the single biggest pedagogical gap. The funnel is the central object of @sec-comp-param and it is described only in prose. A plot of $(\log\tau, \theta_j)$ draws from a centered vs. non-centered fit, or even a schematic, would make the section immediately graspable.

- **No example of reading a real $\widehat R$ / $N_{\mathrm{eff}}$ table.** The worked example (@sec-comp-example) computes the numbers from scratch on toy data, which is great, but a noob also needs to see a *realistic* Stan summary table and be told how to read it: "this is what bulk-ESS = 87 means, this is what $\widehat R = 1.13$ on $\tau$ means, here is what you do about it."

- **No ML-NMR-flavored example for the integration error.** The doubling rule is illustrated on $\int_0^1 \operatorname{expit}(0.4+0.8\Phi^{-1}(u))\,du$, a single one-dimensional cell. But ML-NMR's whole difficulty is *multivariate* covariate integration. A small two-covariate example (say age and baseline severity in a plaque psoriasis trial) would have shown why $d>1$ changes the game.

- **No example of an influential observation in an ITC.** The PSIS section says $\widehat k_i$ "flags aggregate cells or studies whose removal would most change the fit" (lines 903-905) but never gives a concrete scenario ("study $j=BC$ has $\widehat k=0.8$, meaning this one study is doing a lot of the work for the $d_{BC}$ contrast; refit without it and check robustness"). That is the health-researcher use case and it is absent.

- **No intuition for the harmonic-mean failure.** The remark at lines 897-908 explains why the harmonic mean fails but the *picture* (a few draws with tiny likelihood contribute gigantic $1/p$ weights that swamp the sum) is never given. One sentence of imagery would fix it.

## Notation and jargon problems

- **$\mathrm{ESS}$ vs. $N_{\mathrm{eff}}$.** The remark at lines 54-62 correctly disambiguates these, but they are confusingly similar symbols for conceptually similar quantities and the distinction will be lost on a noob who skims. Consider a more visually distinct symbol for the MCMC one, or at least a margin-note reminder the first time $N_{\mathrm{eff}}$ appears after the remark.

- **$c_j$ "curvature contributed by the data term" (@lem-comp-funnel, line 179).** This is defined inline as "the negative second derivative of the data log-likelihood in $\theta_j$" but $c_j=0$ in the prior-dominated limit is stated as a parenthetical with no explanation of *why* weak data means zero data curvature. I had to derive it myself: weak data means the likelihood is flat means the second derivative is small. Say it.

- **"Hardy-Krause variation" $V_{\mathrm{HK}}(f)$ (line 532).** Used in @eq-comp-kh and immediately conceded to be "unknown and usually uncomputable." If it is uncomputable, the reader needs to know what *kind* of object it is (a multivariate generalization of total variation) at least in a footnote; otherwise the bound reads as magic.

- **"Star discrepancy" $D_N^*$ (line 533).** Named but never defined in this chapter, only referenced as @thm-koksma-hlawka. A noob has no idea what "discrepancy" measures (how evenly the points fill the cube).

- **"Observed information" $\mathcal J$ (line 729).** Defined as $-\nabla^2\log p(\mathbf y\mid\bar{\boldsymbol\xi})$ but the term "observed information" and its relation to Fisher information are not recapped. A noob who did Chapter 5 a while ago will not have it ready.

- **"Cumulant" and "third cumulant $\kappa_{3,i}$" (line 719, 749).** Never defined. A cumulant is not everyday vocabulary for a health researcher.

- **"Self-normalized" importance sampling (line 684).** The term is used without definition. The formula @eq-comp-is is self-normalized, but the reader is not told what distinguishes self-normalized from ordinary importance sampling (the denominator is also estimated, so the unknown normalizing constant drops out).

- **"Generalized Pareto distribution" (line 834).** Named and fit but its shape and scale parameters and what the shape $k$ *means physically* (tail heaviness) are not explained before @lem-comp-gpd-moments uses $k$ heavily.

## Pacing issues

- **The chapter front-loads formalism before any intuition.** The first section after the introduction (@sec-comp-param) opens with a normal hierarchy and immediately dives into a diffeomorphism proof. There is no "here is the problem we are trying to solve, in pictures" paragraph. For a chapter whose audience is health researchers, opening with the funnel picture and the failure mode would pace the math much better.

- **@thm-gelman-rubin is very heavy for what it says.** Three parts, a long proof, two lemmas of expectation identities, all to land at "$\widehat R$ should be near 1." A noob reader is exhausted by the time the diagnostic is actually defined (@eq-comp-rhat, line 329), which is what they came here for. Consider stating $\widehat R=\sqrt{\widehat V/W}$ and its interpretation first, *then* proving the properties.

- **@sec-comp-ess reuses machinery from @sec-comp-rhat.** The proposition @prp-comp-acf-variance is referenced inside @thm-gelman-rubin (Part 2) two sections *before* it is stated. This forward dependency makes the chapter read out of order. Either move the autocorrelation variance proposition earlier or remove the forward reference.

- **The model-comparison sections (@sec-comp-ic, @sec-comp-psis) come as a long dense block** with no worked example until the very end of the chapter. Splitting the worked example so that a mini-example follows each section (one for $\widehat R$, one for $N_{\mathrm{eff}}$, one for the doubling rule, one for WAIC/LOO) would pace the abstraction better than one mega-example at the end.

- **@thm-dic-waic-loo is the densest theorem in the chapter** (three parts, a proof that spans 60 lines, cumulant generating functions, Bernstein-von Mises, observed vs. empirical Fisher information). It is a lot to absorb in one sitting and is the place a noob is most likely to give up. Splitting it into two theorems (one for WAIC=LOO, one for the effective-parameter trace formula) would help.

## What worked well

- **The worked example @exm-comp-diagnostics (lines 927-1015)** is excellent. Every number is reproducible with a calculator, the $\widehat R$ arithmetic is walked through step by step, and the integration-error example with explicit Sobol' values and the exact Gauss-Hermite reference value is exactly what a noob needs. This is the model for how the rest of the chapter could be paced.

- **The "two effective sample sizes" remark (lines 54-62).** Proactively disambiguating $\mathrm{ESS}$ (MAIC weighting) from $N_{\mathrm{eff}}$ (MCMC autocorrelation) is thoughtful and saved me from a real confusion. This kind of cross-reference remark should be a pattern throughout the chapter.

- **@exm-comp-ar1 (lines 483-496).** The AR(1) example with concrete numbers ($\phi=1/3$ gives efficiency $1/2$; $\phi=0.9$ gives $1/19$) made the abstract $N_{\mathrm{eff}}$ formula instantly interpretable. More like this, please.

- **The remark on "what $\rho$ is for QMC vs. Monte Carlo" (lines 580-590).** Explaining why the doubling rule is sharper for QMC ($\rho\approx 1/2$) than for Monte Carlo ($\rho\approx 0.707$, true error up to $2.4\times$ the increment) is a genuinely useful operational fact and well stated.

- **The exercises (lines 1054-1122).** They are well chosen, range over the whole chapter, and several have solutions in Appendix F. The leapfrog-and-funnel exercise (@exr-comp-leapfrog) and the deterministic $\widehat R$ lower bound (@exr-comp-rhat-floor) are particularly good for forcing active engagement.

- **The honest "no machine-checked counterpart" remark (lines 910-916).** Stating plainly that the formalized tree ends before this material is refreshing and sets correct expectations. The book's integrity about its own scope is a strength.

## Suggestions

1. **Open @sec-comp-param with the funnel in plain English and ideally a figure** before the diffeomorphism proof. A noob needs to see the trumpet-bell shape and hear "random-walk samplers get stuck in the neck; HMC diverges there" before any algebra.
2. **Re-explain the leapfrog integrator inline** in @sec-comp-param (three substeps, what $r$ is, what $\epsilon$ is) rather than referencing @def-hmc. The whole stability and funnel analysis depends on it.
3. **Add a one-paragraph "what is HMC / why HMC / what is NUTS" box** at the top of the chapter, aimed at the health researcher who has used Stan but never thought about the engine.
4. **Define "divergent transition," "warmup," "adaptation," and "No-U-Turn Sampler"** in a short glossary box or in the introduction; they recur throughout the practical remarks but are never defined.
5. **Reorder so that $\widehat R$ is stated and interpreted before its proof.** Give the reader the punchline ($\widehat R\le 1.01$, near 1 means converged, far above 1 means the chains disagree) and *then* derive the expectation identities.
6. **Move @prp-comp-acf-variance before @thm-gelman-rubin**, or remove the forward reference in Part 2 of @thm-gelman-rubin, so the chapter does not depend on a result two sections downstream.
7. **Tie each section to a concrete ITC scenario.** The funnel remark at lines 237-245 is the model: name the actual ML-NMR parameters ($\mu_j$, $\delta_{j,1k}$), name the HTA context (few studies per contrast), and name the practical consequence (use NCP or get divergences). Replicate this pattern for the integration section (a two-covariate psoriasis example) and the model-comparison section (an influential-study $\widehat k$ example).
8. **Add a realistic Stan summary table** (even fabricated) to @sec-comp-example showing how a health researcher actually reads `summary(fit)` output: columns for mean, sd, bulk-ESS, tail-ESS, $\widehat R$, plus a row with a problem flagged.
9. **Split @thm-dic-waic-loo into two theorems**, define "cumulant" and "observed information" inline, and add a one-line strategy paragraph before each proof.
10. **Add intuition imagery for the harmonic-mean failure** (a few draws with tiny likelihood contributing gigantic weights) and for the funnel, even if only in prose.