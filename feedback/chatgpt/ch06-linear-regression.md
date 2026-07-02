# Chapter 6 Feedback: Linear Regression from First Principles

## Overall reaction

This is a strong and serious chapter, but it currently reads more like a mathematically complete regression chapter than a chapter designed to carry a novice health researcher into the mathematics of indirect treatment comparisons. The proofs are careful, the sequence of results is logical, and the worked example is useful. The main weakness is pacing. The chapter often gives a good intuitive sentence, then quickly moves into dense matrix notation, projection geometry, or distribution theory before the applied reader has enough anchors.

For a smart health researcher who is weak in abstract mathematics, the chapter would be more usable if it repeatedly answered three questions: what object are we estimating, what does this mean in trial or population-adjustment language, and why does this step matter later for ITC? The introduction makes that promise, but many later sections become internally focused on least-squares theory and only return to ITC motivation in the notes.

## What was clear

- The opening motivation is helpful. The link from simulated treatment comparison, multilevel network meta-regression, and matching weights to regression gives the reader a reason to care about ordinary least squares.
- The split between Gauss-Markov assumptions G1, G2, and normality G3 is well explained. The statement that G3 is only needed for exact finite-sample tests and intervals is especially useful.
- The distinction between fitted values and residuals is developed well. The projection derivation makes the phrase "line of best fit" much more precise than an ordinary introductory statistics treatment.
- The discussion of $n-p$ degrees of freedom is one of the better novice-facing explanations in the chapter. The idea that residuals live in an $(n-p)$-dimensional space gives a reason for the divisor instead of presenting it as a convention.
- The worked example is valuable because it carries one data set through estimates, residuals, sums of squares, standard errors, t tests, and the F test. The repeated checks against earlier formulas help the reader see that the theory is connected.
- The rank-deficiency section is important and well motivated by categorical predictors coded with an intercept and all group indicators. That example is likely to feel familiar to applied researchers.

## What was unclear

- The introduction says matching weights are "the solution of a weighted regression." A novice health researcher may find this confusing because matching-adjusted indirect comparison is usually introduced through reweighting to match aggregate covariate moments, not as a regression problem. This sentence needs either a short explanation or softer wording.
- The definition of the linear model moves quickly from rows of $\mathbf{X}$ to $\mathcal{C}(\mathbf{X})$. A reader who only vaguely remembers linear algebra may not yet understand why "the systematic part of the response lies in the column space" is the same as saying the mean response is a linear combination of regressors.
- The conditional interpretation of $\beta_k$ is too compressed. The remark says a coefficient is the conditional effect of a one-unit change in a regressor with all others held fixed, then immediately mentions identity links, marginal effects, nonlinear links, and non-collapsibility. This is important for ITC, but it needs a small health example, such as age as a prognostic variable or treatment-by-baseline-risk interaction as an effect modifier.
- "Best" in the Gauss-Markov theorem is introduced through Loewner ordering. The text states what it means, but a novice may not understand why a matrix inequality is the right way to compare estimators. A brief scalar translation before the theorem would help.
- The normal-theory section becomes abstract very quickly. Affine closure, moment generating functions, Gaussian block independence, spectral decomposition, and chi-squared distributions appear in close sequence. Each result is proved, but the applied meaning of the results is easy to lose.
- The Cramér-Rao efficiency result may feel like a sudden escalation. It is mathematically relevant, but a novice health researcher may not understand how it changes their practical view of regression beyond "OLS is optimal under normality."

## Under-explained details

- The chapter should more explicitly distinguish error terms from residuals. The notation is correct, but a novice may not grasp that $\boldsymbol{\varepsilon}$ is unobserved noise while $\mathbf{r}$ is calculated after fitting the model.
- The design matrix deserves a small table or miniature example before the formal definition. For example, show an intercept column, a treatment column, age, and baseline severity, then map those columns to $\beta_0,\beta_1,\beta_2,\beta_3$.
- Full column rank is essential, but the intuition arrives late. Before proving the Gram matrix lemma, it would help to say plainly that full rank means no regressor column can be reconstructed from the others, so the coefficients are identifiable.
- The term "normal equations" is named but not explained historically or intuitively. A novice may wonder why the equations are called normal. A short note that "normal" here means perpendicular would connect it to residual orthogonality.
- The sandwich variance is mentioned as a repair for failed G2 before the reader has enough context. Since the definition is outside the chapter, this could use one sentence saying it estimates uncertainty without requiring the simple $\sigma^2 I_n$ covariance structure.
- The t quantile notation $t_{n-p,1-\alpha/2}$ and the F quantile notation in the worked example are used without much interpretation. Many health researchers know confidence intervals mechanically, but not this notation.
- The worked example uses abstract $x$ and $y$ values. The calculations are clear, but the example would teach more if $x$ and $y$ had a light health interpretation, such as baseline severity predicting change in a continuous outcome.

## Where a novice may get lost

- The first likely loss point is the jump from "best fit" to column spaces and projections. The text is correct, but it assumes the reader still has Chapters 1 to 3 fresh in memory. A bridge paragraph with a plain-language picture would help.
- The proof of the normal equations by calculus may be difficult for readers who are not comfortable with gradients of quadratic forms. The proof verifies the result, but an intermediate line explaining what each term means in scalar regression would reduce intimidation.
- The hat matrix and residual maker section introduces useful objects, but the matrix properties may feel like a list of algebraic facts. The reader may need to know why $H^2=H$ matters in practice, for example because applying the fitting operation twice changes nothing.
- The Gauss-Markov proof is elegant but abstract. The decomposition $C=A+D$ is not intuitive on first reading. A sentence saying that $D$ represents any extra linear operation added to OLS, and that unbiasedness forces this extra operation to ignore the model space, would help.
- The chi-squared proof is probably the hardest section for the target reader. The sequence from idempotent matrices to eigenvalues to independent squared standard normals needs a short roadmap before the proof and a short recap after it.
- The rank-deficiency section is valuable but comes late. Some novices may already be confused earlier by the repeated full-rank assumption. A short preview near the first full-rank assumption would reassure them that common coding problems are handled later.

## Suggested improvements

- Add a small "reader map" after the introduction. It could say that the chapter has four layers: geometry gives the estimator, Gauss-Markov gives optimality without normality, normality gives exact tests, and rank deficiency explains what happens when coefficients are not all identifiable.
- Add one health-motivated design matrix example near the definition of the linear model. Use columns for intercept, treatment, age, and baseline severity. This would make $\mathbf{X}$ and $\boldsymbol{\beta}$ less abstract.
- Revisit ITC motivation at the start or end of major sections. For example, after Gauss-Markov, explain that later outcome regressions in STC rely on the same idea of estimating conditional mean structure. After rank deficiency, connect estimability to treatment contrasts in networks.
- Add bridge sentences before technical proofs. The most important places are the Gram matrix lemma, Gauss-Markov, the chi-squared RSS theorem, and Cramér-Rao efficiency.
- Move some interpretive content closer to the relevant theorem rather than saving it for the notes. The notes make useful links to STC, ML-NMR, non-collapsibility, and sandwich variance, but the reader needs those links during the chapter.
- Make the worked example more clinically recognizable without changing the arithmetic. For instance, describe $x$ as baseline disease severity and $y$ as change in outcome. Then state what the slope, residuals, standard error, and nonsignificant t test mean in that setting.
- Add a short unworked or partially worked example of a treatment indicator regression. Even a two-arm trial with $y_i=\beta_0+\beta_1T_i+\varepsilon_i$ would help readers see how regression connects to treatment effects.
- Add novice-facing exercise scaffolding. Several exercises are mathematically appropriate, but the starred exercises are quite hard. The nonstarred exercises could include one calculation-focused problem using a small health data table and one interpretation-focused problem about assumptions.

## Highest-priority fixes

1. Add a concrete health research design-matrix example immediately after the linear model definition.
2. Add a bridge from coefficient interpretation to prognostic variables, effect modifiers, and treatment effects before mentioning non-collapsibility.
3. Add short roadmaps before the Gauss-Markov proof and the chi-squared residual-sum-of-squares proof.
4. Make the worked example clinically interpretable, or add a second mini example involving treatment, baseline covariates, and a continuous outcome.
5. Strengthen the ITC throughline throughout the chapter, not only in the introduction and notes.
