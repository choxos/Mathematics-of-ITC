# Feedback: Appendix E — Reference Implementations

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation. I can read a
logistic regression table and run a Cox model in R, but I have never written Stan code and I do not
have the math of GLMs, copulas, or QMC in my head.
**File:** `appendices/E-reference-implementations.qmd`

## Overall impression

This appendix is clearly written *for the author and for someone who already understands ML-NMR,
ML-UMR, MAIC, STC, and QBA at the theorem level*. The mapping tables are elegant: every function is
linked back to a specific theorem or equation in the main text. As a *reference card* for a
mathematician who already read Chapters 1 through 30, it works. But the appendix is explicitly titled
"Reference Implementations," and for a health researcher like me who comes to the appendix precisely
*because* the math got heavy and I was hoping the code would make it concrete, it fails. It is a map,
not a guide. The very first sentence of @sec-impl-scope warns me: "This is a map, not a tutorial." That
is honest, but it also means the appendix does not do the one thing I most needed it to do: show me a
real trial, with real drug names and real numbers, being analyzed end to end, with the code annotated
line by line against the math.

I read the whole thing (413 lines) and I have a list of questions I still cannot answer: What does my
data frame actually need to look like before I call `set_ipd()`? What is an `mlumr_data` object? Why
does `add_integration()` want a `distr(qnorm, ...)` and not just a mean and a standard deviation? Where
does the value `n_int = 64L` come from, and what happens if I pick 16 or 4096? What does a Stan file
*look like on the inside*, beyond the two-line snippet at lines 88 to 91? None of these are answered,
and they are exactly what a beginner needs.

## What was unclear

**The two Stan lines at lines 88 to 91 are thrown at me with almost no decoding.** The text says
`theta_agd_arm_ii` "holds the $N$ values $g^{-1}(\eta_{jk}(\mathbf{x}^{(m)}))$" and `nint` is $N$. But I do
not know Stan indexing conventions. The slice `theta_agd_arm_ii[(1 + (i-1)*nint):(i*nint)]` is doing
something clever: it is pulling out, for study-arm `i`, the block of integration points that belongs to
that arm. I had to stare at it for five minutes to realize the array is *stacked* (all arms'
integration points concatenated), and the slice is just recovering arm `i`'s slice. A one-sentence
gloss of the indexing, ideally as a comment *inside* the Stan block, would have saved me that work. The
second line `agd_arm_r ~ binomial(agd_arm_n, theta_agd_arm_bar)` is Stan's sampling syntax: I know enough
to read it as "the observed count `r` is binomial with count `n` and probability
`theta_agd_arm_bar`," but a reader who has never seen `~` in Stan will not know this is a likelihood
statement, not an assignment. No comment explains it.

**The adjusted-binomial formula at @eq-impl-adjusted-binomial (lines 97 to 102) lost me completely.**
You give me
$$n'_{jk}=n_{jk}\,\frac{\bar\theta_{jk}^{\,2}}{\overline{\theta^2}_{jk}}, \quad p'_{jk}=\frac{\overline{\theta^2}_{jk}}{\bar\theta_{jk}}.$$
I can see the algebra that $n'p'=n\bar\theta$ preserves the mean. What I *cannot* see is why this
particular reparametrization is the right way to "inflate the variance to the mixture's." Where did
$\overline{\theta^2}$ come from? You mention it once ("forms $\overline{\theta^2}_{jk}=N^{-1}\sum_m
\theta_m^2$") but you never connect it to the *variance* of the Bernoulli mixture. A beginner needs the
chain: the true aggregate variance is $\mathrm{Var}=\overline{\theta^2}-\bar\theta^2$, and this
reparametrization makes a binomial whose variance matches that. As written, I am asked to take it on
faith that this is "the implementation of the aggregate likelihood." I went back to @eq-agg-aggregate-
likelihood and still could not reconstruct the link.

**The QMC pipeline equation at @eq-impl-qmc (lines 113 to 118) is the single most opaque line in the
appendix.** It packs four nested transformations into one display:
$\mathbf{x}^{(m)}=(F^{-1}(u_1),\dots)$, $u_q=\Phi((L\mathbf{z})_q)$, $\mathbf{z}=\Phi^{-1}(\mathbf{a})$.
I read this as: take a Sobol point $\mathbf{a}$, push it through the normal quantile, multiply by the
Cholesky factor, push *that* through the normal CDF, and then through the marginal quantile functions.
That is a lot to hold at once, and it is the *central* computational idea of the whole ML-NMR machinery.
I needed this broken into a four-row table, one row per arrow, with the *R argument* that produces each
step. The table at lines 123 to 128 names the arguments but does not show them in the order of the
pipeline. As a result I cannot see, for example, that `cor` feeds $L$ and `distr(qnorm,...)` feeds
$F^{-1}$. The mapping is implicit; I had to work it out.

**`distr(qfun, ...)` at line 125 is used before it is explained.** It appears in the code block at lines
65 to 66 with no prior definition. Line 125 then says "distr wraps a base-R `q*` function." But what
*is* it? Is it a function that returns a function? A list? Why does it take `qnorm` (a function) as its
first argument and then keyword arguments `mean =`, `sd =`? A single sentence and a tiny example
(`distr(qnorm, mean = 55, sd = 12)` is a closure that, given $u$, returns
`qnorm(u, mean = 55, sd = 12)`) would have made it click.

**Lines 313 to 318 on the MAIC weights are dense.** The dual objective
$Q(\boldsymbol{\beta})=\sum_i \exp(\boldsymbol{\beta}^\top \mathbf{x}_i^{c})$ is stated, the stationary
condition is "exactly the moment balance," and then "estimate_weights(method = 'BFGS')" performs the
minimization. But I do not see, in code, *where* the moment balance is checked or *what* the gradient of
$Q$ is. A beginner wants to see: (a) the centered covariates $\mathbf{x}_i^{c}$ being formed, (b) the
objective $Q$ written as an R function or as a comment, (c) the gradient being the imbalance
$\sum_i w_i \mathbf{x}_i^{c}$, and (d) the solution $\hat{\boldsymbol\beta}$ feeding $w_i=\exp(\hat{\boldsymbol\beta}^\top\mathbf{x}_i^{c})$.
None of that is shown. The jump from the theorem to "call BFGS" skips the entire bridge.

## What wasn't elaborated enough

**The `set_ipd()` and `set_agd_*()` family (lines 48 to 56) is the entry point for the entire package,
and it gets one table row each.** I have no idea what the data frames look like. Does IPD need a column
called `study`? Is `trt` a factor or a character? What does `r = r` mean in `set_ipd(ipd_data, study,
trt, r = r)` (line 62): is `r` on the left a fixed argument name and `r` on the right my column name?
This is the *most basic* thing a beginner needs, and the code block at lines 61 to 69, which is the only
full R call in the multinma section, does not explain it. I would have liked a three-row toy data
frame printed, for both IPD and AgD, with column names, so I can see the shape of the input.

**The survival section (@sec-impl-mlumr-survival, lines 253 to 263) is the fastest-paced section in the
appendix.** In ten lines it covers: KM digitization, pseudo-IPD inversion, nine parametric families,
M-spline and pexp baselines, `make_knots()`, the non-collapsibility of the hazard ratio (with the
workaround `predict(type = "loghr")`), and RMST transport. Each of those is a chapter in the main text,
and each deserves at least a paragraph. I came out of this section knowing that survival is *supported*
but not how to actually do it. What does the digitized-KM input look like? How many points do I need?
Why nine families, and how do I choose? The sentence "Because the hazard ratio is non-collapsible" is
asserted as if I already know what collapsibility means; the notation table does not define it, and the
main-text cross-reference (@thm-mlumr-target-survival) is not a substitute for a one-line gloss here.

**The doubly-robust estimator (@sec-impl-uitc-dr, lines 324 to 340) is described in prose but never
shown in code.** The table at lines 332 to 336 lists three arguments (`weighting`, `augmentation`,
`cor_method`/`n_sim`) but there is no call to `dr_estimator()` anywhere in the appendix. For the one
estimator that is *unique* to `uitc` and not delegated to `mlumr`, this is a real gap. I do not know what
the call looks like, what `augmentation = "weighted_gcomp"` does differently from `"residual"`, or how
`n_sim` interacts with `n_int`. A short worked call, even five lines, would close this.

**The QBA section (@sec-impl-uitc-qba, lines 342 to 361) lists eight functions in a table and explains
two.** The E-value gets a formula and a sentence. `qba_unmeasured_itc()` gets a sentence about NORTA.
But `qba_tipping_itc()`, `qba_prob_itc()`, `probsens()`, `confounders()`, `misclass()`, `selection()`
get nothing but a one-line table cell. I cannot tell, from this appendix, what the *difference* is
between `qba_tipping_itc()` and `qba_prob_itc()`: both are "sensitivity analysis on the unanchored
estimand," and the table rows read nearly identically. The distinction between deterministic tipping
and probabilistic bias analysis is load-bearing, and it is not made here.

## Missing motivation / "why does this matter?"

**There is no "why use ML-NMR instead of MAIC" anywhere.** The appendix tells me *what* each package
computes, but not *when* I would reach for it. The decision table at lines 389 to 393 partitions by
network type (connected vs disconnected), which is correct, but a health researcher does not always
know whether their network is connected. A short motivating paragraph per package, anchored to a
concrete HTA scenario ("you have an IPD trial of drug A versus placebo and a published AgD trial of
drug B versus placebo; you need A vs B for your submission; here is which package you load and why"),
would have made the whole appendix feel like it answers a question I actually have.

**The remark at lines 24 to 31 explains that the correspondence is "at the level of mathematical
object, not source line,"** but it does not say *why* that is the right choice. A beginner might
reasonably ask: then why is this in an appendix and not just a table on the book's website? The answer,
presumably, is that the appendix is meant to be read *alongside* the chapters, as a verification that
the code is doing what the theorems say. But that motivation is never stated. I was left wondering what
the appendix is *for* in my reading workflow.

**The sentence at lines 104 to 106 about the naive plug-in being biased** is the only place the
*point* of the aggregation integral is stated, and it is buried. The motivation, "the naive estimator
is biased and here is the bias theorem," should lead the section, not close it. As a beginner I want to
know, before I see any code, *why I should care*: because the obvious thing (evaluate the model at the
mean covariate) is wrong, and the theorem quantifies how wrong.

**`n_int = 64L` at line 66 is unmotivated.** Why 64? The Koksma-Hlawka bound at line 126 tells me the
error decays like $N^{-1}(\log N)^d$, but nothing tells me how to *pick* $N$ in practice, how the
dimension $d$ enters, or what the cost is. A sentence like "64 is a common default; double it and
check the estimate moves by less than your tolerance, using `plot_integration_error()`" would make
this actionable.

## Missing examples and intuition

**There is no worked example anywhere in the appendix.** The single concrete call at lines 61 to 69
is a template with placeholder column names (`ipd_data`, `agd_data`, `age_mean`, `age_sd`,
`sex_prop`). I never see real data, real numbers, or a real result. For a book whose stated goal is to
take "a naive researcher to mastery," an appendix of reference implementations with no numerical
example is a missed opportunity. Even one short block, say:

> Using the plaque psoriasis network (5 studies, 2 IPD, 3 AgD, binary PASI-75 response), with mean age
> 45 and 38% female in the AgD study, the call is [...], and `relative_effects()` returns a log-OR of
> -0.82 (95% CrI -1.21, -0.43) for drug B vs A.

would have made every abstract object in the map concrete.

**No intuition is built for the copula.** The Gaussian copula appears at @eq-impl-qmc and is referenced
again at line 128 (Sklar's theorem) and lines 357 to 359 (NORTA). But there is no picture, no analogy,
no "the copula lets us glue arbitrary marginal distributions together with a specified correlation
structure." For a health researcher who has never seen a copula, the symbol $C_\Omega$ and the
construction $LL^\top=\Omega$ are pure formalism. A two-sentence intuition and a pointer to the figure
in Chapter 22 would help.

**The love plot and balance table at line 310 are named but not shown.** MAIC lives or dies by
covariate balance, and `love_plot()` / `balance_table()` are the diagnostic. A beginner needs to see
what a *good* love plot looks like and what a *bad* one looks like, or at least a description of the
axis and the threshold (standardized mean difference < 0.1 is a common rule). The function is listed
and then dropped.

**The "collapse to standard NMA" sentence at lines 147 to 148** is a beautiful observation (when all
studies are AgD with no covariates, ML-NMR collapses to NMA) and it is mentioned in passing. This is
exactly the kind of sanity-check intuition a beginner should be handed explicitly, with the code to
reproduce it (`nma(net, trt_effects = "fixed")` with no `regression =`). It is the computational
witness of @thm-mlnmr-generalizes-nma, and it deserves a callout box, not a subordinate clause.

## Notation and jargon problems

**"SPFA" and "SEMA" are used (lines 146, 218, 219, 271) but defined only in the notation table, which
expands them as "shared prognostic factor assumption" and "shared effect modifier assumption."** The
appendix never re-glosses them, so a reader who skips the notation chapter is stranded. Given that
the *entire* `mlumr` section turns on the SPFA (it is the identification assumption), it should be
defined in the appendix body the first time it appears.

**"Anchored" vs "unanchored" (lines 11, 184, 284, 389 to 393) is used constantly and never defined
here.** I know from the chapter titles that this is about whether the two treatments share a common
arm, but the appendix assumes I carry that context. A one-line definition at first use ("anchored: the
two treatments were both compared with a common reference, so a network closes; unanchored: no common
reference, so a direct contrast is not identified without population adjustment") would fix this.

**`trt_effects = "fixed"` at line 68** is the only place the fixed-vs-random distinction appears, and
it is not glossed. A beginner may not know this means "fixed-effect (common-effect) NMA" as opposed to
"random-effects," and that the choice changes the model Stan fits.

**The notation $\bar{\mathbf{x}}_j$ and $\boldsymbol{\Sigma}_j$ at line 21** is introduced in the scope
paragraph, but the appendix then uses $\bar\theta_{jk}$, $\overline{\theta^2}_{jk}$,
$\mathbf{x}^{(m)}$, $\mathbf{a}^{(m)}$, $\mathbf{z}^{(m)}$ without re-introducing them. Some are in the
notation table; some ($\mathbf{a}^{(m)}$ for the Sobol point, $\mathbf{z}^{(m)}$ for the normal-score
point) are not. I had to infer them from context.

**"G-computation" at line 245** is jargon from the causal-inference literature; the notation table does
not define it. A reader of this appendix may not have read Chapter 19 recently. One line ("G-computation:
fit the outcome model on the IPD, then average its predictions over the target covariate distribution")
would make @prp-stc-gcomp and the `stc()` function legible.

**"Non-collapsible" at line 259** is the most technical piece of undeclared jargon in the appendix. It
is the reason the HR section is structured the way it is, and it is never defined. The notation table
does not include it. This is a genuine barrier for a beginner.

## Pacing issues

**The multinma section (@sec-impl-multinma, lines 33 to 181) is the longest and the most carefully
paced**, but even it front-loads the model equation (@eq-impl-mlnmr-model at lines 36 to 38) and only
later explains its pieces. The linear predictor
$\eta_{ijk}=\mu_j+\boldsymbol{\beta}_1^\top\mathbf{x}_{ij}+(\boldsymbol{\beta}_{2,k}^\top\mathbf{x}_{ij}+\gamma_k)$
is the whole model; a beginner should be walked through each term ($\mu_j$ baseline, $\boldsymbol\beta_1$
prognostic, $\boldsymbol\beta_{2,k}$ effect modification, $\gamma_k$ treatment effect) before the
pipeline table. Instead the equation is dropped and the reader is expected to absorb it.

**The mlumr section (@sec-impl-mlumr, lines 182 to 282) is much shorter and far denser.** It packs the
pipeline, two model variants, two Stan snippets, the benchmarks, and survival into 100 lines. The
multinma section had 150 lines for a comparable scope. The result is that ML-UMR, which is arguably the
*newer and less familiar* method, gets less explanation than ML-NMR. This is backwards from a
beginner's needs.

**The uitc section (@sec-impl-uitc, lines 284 to 383) is the most table-heavy.** Six tables in 100
lines. Tables are efficient for experts and brutal for beginners. I read six tables in a row and
retained almost none of it. At least one of the MAIC, DR, or QBA subsections should be expanded into
prose with a code block, to break the table monotony and give a beginner something to follow.

**The survival subsection (lines 253 to 263) is ten lines and covers a chapter's worth of material.**
This is the worst pacing in the appendix. Either it should be expanded, or it should explicitly defer
to the main text with a sentence like "this subsection only locates the survival functions; read
Chapter 25 and the `mlumr` survival vignette before using them."

## What worked well

The **object-to-code maps** (lines 150 to 161, 265 to 282, 369 to 383) are the strongest part of the
appendix. Three clean tables, one per package, each row tying a book object to a chapter result to a
function. For a reader who *has* read the chapters, these are genuinely useful as a lookup. The
convention of citing `@thm-...`, `@eq-...`, `@def-...` consistently makes the maps checkable.

The **explicit warning about name collisions** between `multinma` and `mlumr` (lines 395 to 397) is
excellent practical advice. This is the kind of thing that saves a beginner hours of debugging, and it
is stated clearly and early enough to matter.

The **remark at lines 24 to 31** is honest and useful: it tells me the correspondence is at the
mathematical-object level and that signatures may drift, and it tells me to verify against installed
help pages. This sets expectations correctly.

The **decision table at lines 389 to 393**, once you know whether your network is connected, is a clean
routing rule. The observation that `uitc` consumes `mlumr_data` objects directly (lines 398 to 400),
so a single data setup feeds five methods, is the most useful practical sentence in the appendix.

The **bias framing at lines 104 to 106**, where the naive plug-in is contrasted with the integrated
mean and `multinma` is stated to "never form the naive quantity for a nonlinear link," is the kind of
opinionated guidance I want more of. It tells me the package has a stance, not just a function.

## Suggestions

1. **Add one fully worked numerical example** to each of the three package sections, using a real or
   realistic trial (e.g., the plaque psoriasis or multiple myeloma vignette data from `multinma`).
   Show the input data frame, the call, and the printed result with a one-line interpretation. This
   single change would do more for a beginner than any other.

2. **Annotate every Stan snippet inline.** The two-line block at lines 88 to 91 should carry a
   comment per line, and the indexing slice should be explained in a sentence. Stan's `~` sampling
   syntax should be glossed the first time it appears. The `mlumr` snippet at lines 224 to 227 should
   get the same treatment, plus a gloss of `inv_link_binary_vec` and `Xq_int[k] * beta_tilde`.

3. **Add a four-row "pipeline arrow" table for the QMC construction** (lines 108 to 131), one row per
   transformation in @eq-impl-qmc, each row showing the symbol, the R argument that produces it, and a
   one-line gloss. Order the rows in the *order the data flows*, not the order the arguments are
   listed.

4. **Define SPFA, SEMA, anchored, unanchored, non-collapsible, and G-computation at first use** in
   the appendix body, in a one-line parenthetical each. Do not rely on the notation table or the main
   text for terms that are load-bearing in the appendix.

5. **Expand the survival subsection** (lines 253 to 263) to at least 25 lines, with a description of
   the digitized-KM input format, a pointer to the vignette, and one sentence per family group
   (parametric vs M-spline vs pexp) on when to use it. Or explicitly defer it with a "read Chapter 25
   first" sentence.

6. **Show the input data shape.** Before the first `set_ipd()` call (line 62), print a 3-row toy IPD
   data frame and a 2-row toy AgD data frame with column names. This is the single most useful
   concrete addition for a beginner and it costs ten lines.

7. **Add a "how to choose `n_int`" paragraph** after line 131, with the default, the cost scaling,
   and the `plot_integration_error()` convergence check. Tie it explicitly to the Koksma-Hlawka rate
   so the theorem becomes actionable.

8. **Lead the aggregation section with the motivation.** Move the "naive plug-in is biased" framing
   (currently lines 104 to 106) to the *top* of @sec-impl-multinma-aggregation, so the reader knows
   *why* the integral matters before seeing it.

9. **Differentiate `qba_tipping_itc()` from `qba_prob_itc()`** in prose (lines 344 to 361). One is
   deterministic root-finding on a sensitivity parameter; the other puts a prior on the bias
   parameters and Monte-Carlos. Two sentences would make the distinction stick.

10. **Add a short `dr_estimator()` call** in @sec-impl-uitc-dr, showing the arguments in context. It
    is the one estimator native to `uitc`, and it currently has no code example at all.