# Chapter 15 Feedback: Network Meta-Analysis: Models and Identifiability

## Overall reaction

This chapter is rigorous, coherent, and clearly written for a reader who is already comfortable thinking of network meta-analysis as a linear model. From the perspective of a novice health researcher, though, the chapter may feel as if it moves from the practical problem straight into design matrices, graph incidence matrices, image spaces, kernels, and rank conditions before the reader has a stable picture of what an evidence network is doing clinically.

The strongest intuitive thread is that NMA is Bucher enlarged from one indirect comparison to a whole web of treatments. The Introduction and the "Bucher as a two-study, one-triangle network" remark make that connection visible. But after that, the chapter often asks the reader to keep too many abstractions active at once: arm means, study baselines, network reference contrasts, study-specific contrasts, pairwise contrasts, graph edges, consistency equations, connectedness, and estimability. A smart health researcher can follow the story if they already trust the notation, but they may not yet have enough applied scaffolding to trust it.

The chapter would be much more accessible if it repeatedly translated the algebra back into trial language: connectedness means there is a chain of randomized comparisons linking two treatments; consistency means direct and indirect paths agree on the same relative effect; identifiability means a contrast is estimable from the available randomized comparisons, not necessarily credible; a loop is what makes inconsistency testable; a multi-arm trial creates correlated contrasts because the same arm is reused.

## What was clear

- The opening paragraph gives a good applied motivation for NMA: decision makers face many treatments, incomplete head-to-head evidence, repeated comparisons, and multi-arm trials.

- The sentence that NMA estimates all pairwise contrasts while honoring correlations from multi-arm trials is helpful. It signals that NMA is not just many Bucher calculations done separately.

- The "Bucher as a two-study, one-triangle network" remark is one of the best reader bridges in the chapter. It makes clear that Bucher is the path case and that adding a direct study closes a loop.

- The distinction between study levels and treatment contrasts is useful. The baseline-shift parameterization explains that each study has its own outcome level, while the reference-treatment parameterization explains how NMA ties studies together through common treatment effects.

- The consistency closure theorem has a valuable conceptual message: only $K-1$ treatment contrasts are free, and the rest must agree through loop equations. The remark that tree-shaped networks have no inconsistency test is important and memorable.

- The fixed-effect identifiability result is a strong teaching point. "The network must be connected" is an applied rule that a health researcher can remember, and the disconnected-network remark explains the practical consequence well.

- The multi-arm trial section does a good job explaining that the one-half correlation is not arbitrary. The idea that heterogeneity should not depend on which arm is called the baseline is a helpful intuition.

- The node-splitting section is clear about the practical warning that a non-significant node split is not proof of consistency. The warning that the pooled NMA estimate averages discordant direct and indirect evidence when inconsistency is large is also very useful.

- The worked example is valuable because it carries one network through the design matrix, covariance matrix, fitted contrasts, standard errors, node-split statistic, and residual deviance. It gives the reader something concrete to check.

## What was unclear

- The treatment-comparison graph definition may confuse a novice in multi-arm trials. The definition says a study contributes $A_j-1$ edges from the chosen baseline to the other arms. Clinically, a three-arm trial compares all three treatment pairs within the same randomized study. The chapter should explicitly separate "clinically direct comparisons available in the trial" from "independent contrast rows used after choosing a study baseline." Otherwise, a reader may wonder why study 4 in the example supplies rows for $1$ versus $2$ and $1$ versus $3$, but no row for $2$ versus $3$.

- The letter $C$ is overloaded early. In the Introduction, $C$ is the common comparator from Bucher. Soon after, $C$ is the total number of within-study contrasts. A novice coming directly from Chapter 14 may read $C=N-J$ and momentarily think it refers to the comparator treatment.

- The notation for treatment effects is dense. The chapter uses $d_k$, $d_{ab}$, $\delta_{j,t_{j,1}k}$, $\theta_{jk}$, and $\mu_j$ in close succession. The difference between a network contrast against treatment 1, a pairwise contrast between two treatments, and a study-specific contrast to a study baseline needs a small orientation table.

- The sign convention remains demanding. In the worked example, $d_{23}=d_3-d_2$ is treatment 3 versus treatment 2 on the chapter's convention. A novice may need repeated plain-language reminders about which treatment is in the numerator or favored direction, especially because applied papers often say "2 versus 3" in the opposite order.

- The transition from arm-based likelihoods to contrast-based estimation is too quick. The chapter defines $\theta_{jk}$ as an arm-level link-scale mean, but the worked example uses contrast estimates as the data. The remark says baselines are eliminated, but a beginner needs a more procedural bridge: start with arms, subtract the study baseline arm, keep $A_j-1$ contrasts, carry their covariance.

- The reference-treatment parameterization is mathematically clean, but the idea that the network reference treatment is arbitrary may be underplayed. A novice may think treatment 1 has a special clinical status rather than serving as a coordinate origin.

- The phrase "consistency constraint" may collide with earlier causal-inference use of consistency under SUTVA. The chapter should signal that NMA consistency is a different idea: agreement of relative effects around network paths.

- The random-effects section could be misread as saying random effects solve inconsistency. It should state more plainly that random-effects NMA allows study-to-study heterogeneity around shared network effects, but it still assumes the network is consistent in expectation.

- Node-splitting is introduced well, but the term itself is not intuitive. The chapter should say that the method splits evidence for a comparison, not literally a treatment node, because the statistic is attached to a contrast such as $d_{AB}$.

- The IPD network meta-regression theorem arrives abruptly. It is important for later chapters, but for a novice still digesting standard NMA it may feel like a second chapter has started.

## Under-explained details

- Treatment networks need more visual and clinical explanation before the formal graph definition. Terms such as vertex, edge, path, cycle, loop, connected component, direct evidence, and indirect path should be translated into trial language in one compact guide.

- The chapter should explain more slowly why a connected network can estimate a contrast even when no head-to-head trial exists, and why a loop is needed to test inconsistency. These are different ideas, and novices often conflate them.

- The baseline concept deserves more applied intuition. A study baseline is not just a nuisance parameter; it represents the outcome level in that study's population and design. The treatment contrasts are what survive after subtracting those levels.

- The consistency equations need a small numerical triangle before the general theorem. For example, if $d_{12}=0.50$ and $d_{13}=1.00$, then consistency implies $d_{23}=0.50$ on this orientation. A direct $d_{23}=0.10$ is then the kind of disagreement node-splitting examines.

- The multi-arm covariance section should explain why the shared arm creates correlation in more ordinary language before giving the variance calculation. The same baseline estimate is present in both contrast estimates, so their errors move together.

- The distinction between heterogeneity covariance and sampling covariance needs another sentence. The chapter notes that both can show one-half correlation, but a novice may not see that one describes variation in true study effects and the other describes uncertainty in estimated contrasts.

- The residual deviance section switches between arm-level deviance and the contrast-level normal example. The example uses $N_{\mathrm{obs}}=5$ contrast data points, whereas earlier $N=9$ meant arms. This difference should be highlighted so readers do not think the degrees of freedom changed mysteriously.

- The DIC material is useful but abstract. A novice health researcher may need a plain statement of when they would use it: comparing fixed-effect with random-effects models, or consistency with inconsistency models, while remembering that DIC is not a substitute for clinical judgment about transitivity.

- The exercises are mathematically useful, but several require proof confidence. There should be at least one beginner exercise that asks the reader to draw a network, identify direct and indirect evidence, decide whether the graph is connected, identify which loops exist, and state what consistency would mean in words.

## Where a novice may get lost

- The Introduction previews many theorem labels and advanced destinations before the reader has seen a single network diagram. This may overwhelm a reader who needs the big picture first.

- In "The network as a generalized linear model," the notation arrives very quickly: $J$, $K$, $\mathcal A_j$, $A_j$, $t_{j,1}$, $N$, $C$, $G$, $\theta_{jk}$, $\mathbf X$, and $\boldsymbol\beta$. This is a lot before any worked network is displayed.

- In "Consistency equations and their algebraic closure," the theorem is correct and important, but the abstraction may hide the simple message: once every treatment has a coordinate relative to treatment 1, all pairwise effects are differences of coordinates.

- In "The incidence matrix and a rank toolkit," the graph incidence proof may feel far away from health research. A novice may need a one-paragraph payoff before the proof: this matrix is just a bookkeeping device for which treatments are connected by randomized comparisons.

- In "Equivalence of the two parameterizations," terms like $\operatorname{image}(\Phi)$, $\mathcal C(\mathbf X_{\mathrm{RT}})$, and $\mathcal S_{\mathrm{cons}}$ raise the abstraction level sharply. The reader may understand neither why this subspace matters nor what has happened to the extra baseline-shift parameters.

- In the identifiability proof, the kernel argument is mathematically efficient but not novice-friendly. The applied message should be stated before and after: if a treatment component is disconnected, you can shift all effects in that component without changing any observed within-study contrasts.

- In the random-effects section, the move from $\eta_{jk}=d_k+u_{jk}$ to correlated $\delta$ contrasts is plausible but fast. A reader may not immediately see that the baseline arm's random effect is subtracted from every contrast.

- The worked example's Step 3 is dense. Accumulating $\mathbf A=\mathbf X^\top\boldsymbol\Sigma^{-1}\mathbf X$ row by row is valuable, but a novice may need labels on each row showing which trial contrast contributes which matrix term.

- The IPD network meta-regression theorem and the DIC proposition are both advanced enough that they may distract from the core Chapter 15 learning goals unless they are clearly marked as bridges to later material.

## Suggested improvements

- Add a small clinical network before the GLM formalism. For example, four treatments for the same condition, with placebo as treatment 1, two active treatments compared only through placebo, and one active head-to-head trial. Show the trial table and the network diagram before defining $\mathbf X$.

- Add a concept box for network language: treatment is a vertex; randomized comparison is an edge; a connected path permits indirect estimation; a cycle permits inconsistency checking; a disconnected component cannot be compared without extra assumptions.

- Add a notation table near the start with columns for symbol, plain-language meaning, and example. Include $\theta_{jk}$, $\mu_j$, $\delta_{j,t_{j,1}k}$, $d_k$, $d_{ab}$, and $t_{j,1}$.

- Add a sign-orientation box. State explicitly that $d_{ab}=d_b-d_a$ means treatment $b$ versus treatment $a$ on the link scale, and give one odds-ratio interpretation in both directions.

- Clarify the multi-arm coding issue. A three-arm trial contains direct randomized evidence on all treatment pairs, but after choosing a baseline it contributes only $A_j-1$ independent contrast rows; the remaining within-trial pairwise contrast is derived by subtraction and is correlated with the others.

- Add short "plain-language takeaway" sentences after the main theorems. For example, after @thm-fe-nma-identifiability: "In practice, if every treatment can be reached from every other treatment by following trial comparisons, the fixed-effect NMA can estimate all relative effects."

- Add a mini example for consistency before @thm-consistency-closure. Use three treatments and two or three numbers to show what the triangle identity predicts and what a violation looks like.

- Add a mini example for disconnected networks before or after @thm-fe-nma-identifiability. Show one network with treatments $\{1,2\}$ and a separate network with $\{3,4\}$, then explain why $1$ versus $4$ is not recoverable.

- Make the worked example more reader-facing. Add row labels to the design matrix, a small table of observed contrast, fitted contrast, residual, variance, and deviance contribution, and a final clinical interpretation of $\hat d_2$, $\hat d_3$, and $\hat d_{23}$.

- Explain why the fitted example lands exactly on the study 4 contrasts. The numbers are convenient, but the reader may otherwise infer too much from the exact fit of those two rows.

- Consider making the IPD network meta-regression section shorter or explicitly labeling it as a bridge to later chapters. A one-covariate health example would make the theorem feel less sudden.

- Add one or two easier exercises before the proof-heavy exercises. A good first exercise would ask the reader to draw a network, identify whether it is connected, list which contrasts are direct or indirect, and write one consistency equation in words.

## Highest-priority fixes

1. Add a concrete network diagram and trial table before the first formal model. The reader needs to see treatments, studies, direct comparisons, indirect paths, and loops before seeing $\boldsymbol\theta=\mathbf X\boldsymbol\beta$.

2. Clarify multi-arm trials. Explicitly distinguish clinical direct pairwise evidence from the $A_j-1$ independent contrast rows created by choosing a study baseline.

3. Add a notation and sign-orientation guide. The chapter depends on the reader keeping $d_k$, $d_{ab}$, and $\delta_{j,t_{j,1}k}$ separate.

4. Strengthen the intuition for consistency, connectedness, identifiability, and testability. These four ideas are central, distinct, and easy for a novice to blend together.

5. Make the arm-based to contrast-based transition procedural. Explain how study baselines are eliminated and why the covariance matrix must carry shared-arm correlations.

6. Make the worked example more guided. Add row labels, observed-versus-fitted residuals, degrees-of-freedom clarification, and a final health-research interpretation.

7. Rebalance the advanced end material. IPD network meta-regression and DIC are useful bridges, but they need clearer framing so they do not obscure the core NMA lesson.
