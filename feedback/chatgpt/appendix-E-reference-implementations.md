# Appendix E Feedback: Reference Implementations: multinma, mlumr, and uitc

## Overall reaction

Appendix E is useful as a compact map from the book's mathematics to three R packages, but it is not yet gentle enough for a novice health researcher who is learning indirect treatment comparisons for the first time. The appendix assumes that the reader already knows why they would choose ML-NMR, ML-UMR, MAIC, STC, or QBA, and mainly shows where each mathematical object appears in package functions or Stan files. That makes it valuable for a technically confident reader, but harder for a motivated health researcher who needs practical orientation before reading formulas and implementation tables.

The strongest part is the repeated object-to-code mapping. It tells the reader that `set_ipd()`, `set_agd_arm()`, `add_integration()`, `nma()`, `mlumr()`, and `uitc()` are not arbitrary software names; they correspond to mathematical constructions from earlier chapters. The main weakness is that the appendix often moves from package workflow to theorem labels without an intermediate explanation of the research question, data layout, model assumption, and interpretation of output.

## What was clear

The opening purpose is clear about the appendix's role: it is a bridge from proved mathematical objects to computational objects, not a full software tutorial. That expectation helps the reader understand why the code is brief and why the tables matter.

The division among the three packages is also clear in broad terms. `multinma` is for connected networks with IPD and AgD, `mlumr` is for disconnected unanchored two-treatment evidence, and `uitc` is the umbrella for unanchored PAIC methods and bias analysis. The final table in "Using the three packages together" is especially helpful and should probably appear earlier, because it gives the novice the first practical decision rule.

The `multinma` pipeline table is one of the most helpful parts of the appendix. It gives a simple sequence from registering IPD and AgD, to combining the network, to adding integration points, to fitting the model. The `mlumr` pipeline table does the same for the unanchored setting. These tables are easier to follow than the later Stan-file details.

The explanation that ML-NMR averages inverse-linked individual means, rather than applying the inverse link to an average predictor, is important and relatively well motivated. This is a key idea for health researchers, because it explains why population adjustment is not just plugging mean age and mean sex into a regression model.

The `uitc` dispatcher section is practically useful. Showing `uitc(dat, method = c("maic", "stc", "mlumr", "naive", "dr"))` quickly tells the reader that these methods can be compared on the same data object.

## What was unclear

The appendix does not give enough plain-language context before the first mathematical model in the `multinma` section. A novice may not yet understand what a connected network means operationally, what IPD and AgD look like in the same analysis, or why a common regression model can be shared across studies. The formula for $\eta_{ijk}$ appears before a concrete data picture, so it may feel like symbols first and research problem second.

The data requirements for each package are scattered. For `multinma`, the reader needs to know which columns are required in IPD, which summaries are required for arm-based AgD, which summaries are required for contrast-based AgD, and what extra information is needed for survival outcomes. For `mlumr`, the reader needs to know that the comparator AgD must include outcome summaries and covariate summaries. For `uitc`, the reader needs to know that the input is an `mlumr_data` object, but the appendix does not slow down enough to explain what that object contains.

The distinction between conditional and marginal effects is underdeveloped for a novice. The table listing `relative_effects()`, `predict()`, and `marginal_effects()` is helpful, but it does not explain which result a health technology assessment reader would usually report, or how the same fitted model can produce different answers depending on the target population.

The SPFA and relaxed model discussion in `mlumr` is too compressed. "Shared prognostic factors" and "treatment-specific prognostic effects" are named, but a novice needs an example. For instance, if age predicts outcome similarly under treatments A and B, that supports the SPFA model; if age predicts outcome differently by treatment, the relaxed model is trying to represent that difference. Without that bridge, the terms may look like software switches rather than identification assumptions.

The QBA section lists many functions quickly. A novice health researcher may not know when to use an E-value, a tipping-point analysis, probabilistic bias analysis, or classical QBA on a 2 by 2 table. The section needs a short practical workflow, such as first estimate the unanchored effect, then run an E-value as a screening calculation, then use `qba_unmeasured_itc()` or `qba_tipping_itc()` for a more explicit sensitivity analysis.

## Under-explained details

The example `multinma` call uses arguments such as `study`, `trt`, `r`, `n`, `likelihood = "bernoulli2"`, `link = "logit"`, `trt_effects = "fixed"`, and `regression = ~ (age + sex):.trt`. A novice needs a short explanation of what each argument means in ordinary trial terms. For example, `r` is the number of responders, `n` is the arm size, and `.trt` tells the formula where treatment interactions enter.

The sentence saying prognostic main effects are added automatically with `center = TRUE` needs more explanation. A health researcher may not know whether that means the covariates are centered within studies, centered against the target population, or centered internally for computation. Since centering affects how coefficients are interpreted, this needs a brief practical note.

The adjusted binomial discussion in `multinma` is mathematically precise but hard for a novice. The reader needs a simple explanation of why the two-parameter binomial approximation exists: patients with different covariates have different response probabilities, so the aggregate arm is a mixture, and the usual binomial variance may be too small if that heterogeneity is ignored.

The QMC section is too fast. Sobol' nets, Gaussian copulas, marginal quantile functions, Cholesky factors, and Koksma-Hlawka bounds are all introduced in a few lines. For a novice, the missing practical bridge is: because the published trial usually reports only means, standard deviations, proportions, and maybe correlations, the software creates a grid of plausible covariate profiles that match those summaries, then averages model predictions across that grid.

The survival subsection in `mlumr` needs more staging. Reconstructed pseudo-IPD from Kaplan-Meier curves, parametric hazards, M-splines, piecewise exponential baselines, non-collapsible hazard ratios, and RMST are all important but dense. A novice would benefit from a short note saying which survival output is easiest to interpret and why RMST is often more transportable than a hazard ratio.

The Stan model file tables may be too implementation-centered for the target reader. They are useful for reproducibility, but a novice may not know why they are being shown. The appendix should say explicitly whether this material is for ordinary users, advanced readers checking implementation fidelity, or package developers.

## Where a novice may get lost

A novice may get lost at the transition from "the package fits ML-NMR" to the first model equation. The reader needs a concrete example first: one IPD trial comparing A and B, one aggregate trial comparing B and C, and a target population with age and sex summaries. Then the symbols $j$, $k$, $i$, $\mathbf{x}_{ij}$, $\gamma_k$, and $\boldsymbol{\beta}_{2,k}$ would have something to attach to.

The appendix repeatedly cites chapter objects such as @thm-aggregation, @eq-agg-naive, @def-sobol-net, @thm-target-population-integral, and @thm-mlumr-stc-equivalence. These are useful cross-links for an expert reader, but for a novice they can become a wall of labels. Each major table should have one sentence explaining the plain meaning of the most important linked result.

The difference between `multinma::add_integration()` and `mlumr::add_integration()` may be confusing. The appendix says `mlumr` reuses the QMC and copula machinery, but it would help to say that in `multinma` the integration may be attached to several AgD studies in a connected network, while in `mlumr` it is mainly used to represent the comparator population in a disconnected two-treatment comparison.

The relationship among `naive()`, `stc()`, `mlumr(model = "spfa")`, and `uitc(method = ...)` could be clearer. A novice may not understand whether these are competing primary analyses, diagnostics, benchmarks, or sensitivity analyses. The appendix says to always run `naive()` as a reference point, which is good, but it should also explain what patterns of agreement or disagreement would be reassuring or concerning.

The `uitc` section may feel like a different topic because it suddenly includes MAIC, doubly robust estimation, comparator distance, and QBA. The connection to the earlier book mathematics is present through theorem labels, but the reader needs a transition explaining that `uitc` is less about fitting one Bayesian model and more about organizing several unanchored adjustment and sensitivity workflows around the same comparator problem.

## Suggested improvements

Move the "Using the three packages together" decision table near the beginning. A novice should first learn which package answers which research situation, then read the package-specific details.

Add a one-page "data needed by each method" table. Columns could include method, network structure, required IPD, required AgD outcomes, required covariate summaries, survival data requirements, and main output. This would directly answer the novice's practical question: what do I need before I can run this?

Add one small running example that appears in all three package sections. It does not need to be executable in full, but it should name treatments, studies, outcomes, covariates, and target population. For example, Trial 1 has IPD for A versus B, Trial 2 has aggregate results for B versus C, and the target population has age and sex summaries. Then the appendix can say when that example belongs in `multinma`, when it becomes a disconnected `mlumr` problem, and when `uitc` methods are sensitivity or alternative analyses.

Add short "what output should I look at?" paragraphs after each pipeline. For `multinma`, explain when to inspect `relative_effects()`, `predict()`, and `marginal_effects()`. For `mlumr`, explain how to compare `naive()`, `stc()`, and `marginal_effects()`. For `uitc`, explain how to compare `estimate`, `se`, intervals, balance diagnostics, effective sample size, and QBA plots.

Add novice bridge sentences before implementation details. Before the Stan snippets, say why a user should care about the implementation line. Before the QMC equation, say that the software is approximating the comparator covariate distribution from summaries. Before the SPFA table, say that the model choice is not just technical; it encodes what the researcher is willing to assume about how covariates predict outcomes across treatments.

Add more cross-links to conceptual chapters in prose, not only theorem labels. For example, "If the distinction between conditional and marginal effects is unclear, reread Chapter 23 before using `marginal_effects()`." Similar guideposts would help for Chapter 18 before MAIC, Chapter 19 before STC, Chapter 22 before QMC, Chapter 24 before Stan diagnostics, Chapter 26 before ML-UMR, and Chapter 28 before QBA.

## Highest-priority fixes

1. Put the package choice table at the start and expand it into a beginner decision guide.

2. Add a data requirements table for `multinma`, `mlumr`, and `uitc`, including IPD fields, AgD summaries, covariate summaries, survival inputs, and expected outputs.

3. Add one concrete running example with named treatments, trials, covariates, and target population so the notation and function calls have a practical anchor.

4. Explain conditional versus marginal outputs in plain language, especially how `relative_effects()`, `predict()`, and `marginal_effects()` differ and which one a health researcher might report.

5. Add bridge text before the QMC, adjusted binomial, SPFA, survival, and QBA material. These are the points where a motivated novice is most likely to lose the connection between the book's mathematics and the package workflow.

6. Clarify how to use `naive()`, `stc()`, ML-UMR, MAIC, and doubly robust estimates together, including what disagreement among methods might mean in practice.
