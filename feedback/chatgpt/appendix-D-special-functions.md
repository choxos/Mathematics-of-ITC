# Appendix D Feedback: Special Functions for Numerical Integration

## Overall reaction

Appendix D is rigorous and often elegant, but from the perspective of a novice health researcher it still reads more like a compact mathematical reference than a learning bridge. I can see why each object belongs in the book, especially after reading Chapters 22 and 25, but the appendix often assumes I already understand why a health technology assessment reader should care about these functions before the proofs begin.

The strongest parts are the moments when the appendix ties a special function directly to an ML-NMR task: the normal MGF explains the log-link shortcut, the probit-logit example checks the Chapter 22 logit integral, and the van der Corput example connects the radical inverse to the seven-point Sobol' set. The weakest parts are the transitions into the error function, Owen's T, and the digital-net algebra, where the mathematical object appears before the novice reader has a practical mental picture of the computational problem it solves.

For a reader who has just reached Chapters 22 and 25, this appendix is useful as a proof repository. It is less usable as a study aid. I would need more signposting about which pieces are essential for understanding the ML-NMR pipeline, which pieces are implementation background, and which pieces are optional analytic shortcuts.

## What was clear

The opening paragraph gives a helpful map of the appendix. It names the normal MGF, error function, Owen's T, probit-logit approximations, and radical inverse in one place, and it says which Part V results each supports. That is exactly the kind of orientation a novice needs.

The normal MGF section is the clearest pedagogical section. The move from "log link means expectation of an exponential" to "linear predictor in normal covariates is normal" to "evaluate the MGF at \(t=1\)" is concrete. The corollary on closed-form log-link aggregation is especially helpful because it exposes the practical bias correction \(e^{v/2}\). The worked two-covariate example makes the covariance term visible rather than leaving it hidden inside a quadratic form.

The probit-logit approximation section is also useful because it explicitly answers a practical question: if logit aggregation has no closed form, what analytic shortcut can I use to check or initialize a numerical integration? The worked example comparing the one-probit and two-probit approximations with the Chapter 22 QMC value is one of the most novice-friendly pieces of the appendix.

The Sobol' section becomes much clearer once it reaches the seven-point van der Corput example. Seeing \(1/2, 1/4, 3/4, 1/8,\ldots\) reflected into the same points used in Chapter 22 gives a concrete hook for the idea that Sobol' points are deliberately spread out, not random.

The repeated use of exact equations and named theorem cross-references is valuable for later lookup. As a reference, the appendix is internally organized and the notes section gives a reasonable source trail.

## What was unclear

The error function section does not yet make its role in ML-NMR feel necessary. It says software computes \(\Phi\), \(\Phi^{-1}\), and tails through \(\operatorname{erf}\), but a novice coming from Chapter 22 mostly sees \(\Phi^{-1}\) as a black-box normal quantile in the Sobol' pipeline. The appendix should make the computational reason more explicit: every Sobol' point must be pushed through \(\Phi^{-1}\), and stable computation of normal probabilities and tails is therefore not decorative, it is part of making the integration pipeline numerically reliable.

Owen's T is introduced as the bivariate analogue of the error function, but I did not have enough intuition before the proof machinery started. The wedge probability representation helps, but only after the definition has already appeared. A novice health researcher may not understand why a wedge in two independent normals is the right shape to think about, or how that wedge connects to bivariate normal probabilities, Gaussian copulas, and expected squared probit values.

The bivariate normal probability identity is mathematically polished, but the purpose of the diagonal case is easy to miss. The text says "exactly the case probit aggregation requires", yet the reader is not first reminded of what quantity in the likelihood needs a second moment, why \(\mathbb{E}[\Phi(a+bZ)^2]\) appears, or why this is relevant to Chapter 25 style likelihood aggregation. The proof is self-contained, but the motivation is too compressed.

The probit-logit approximation section states that the logistic distribution is a scale mixture of normals with a density \(w(s)\), then immediately says the nodes and weights are pinned by Taylor matching. For a novice, this raises questions that the text does not answer: Do I need to know \(w(s)\)? Are the weights true quadrature weights for that mixture or just coefficients chosen to match derivatives? Why is matching near zero the right criterion for health outcomes where event probabilities may be near the tails?

The Sobol' digital-net section is hard to absorb after the accessible Chapter 22 pipeline. It introduces \(\mathbb{F}_2\), generating matrices, primitive polynomials, direction numbers, rank conditions, and exclusive-or arithmetic. The novice reader may understand that this is how Sobol' sequences are built, but may not know what to retain for applied ML-NMR work. The section needs a stronger "what you need to know versus what software handles" distinction.

## Under-explained details

The appendix uses several terms before giving a novice-level explanation of their role: "analytic shortcut", "closed form", "special function", "asymptotic expansion", "tail probability", "radical inverse", "digital net", and "direction numbers". These are not undefined in a formal sense, but the practical meaning could be clearer.

The error function section would benefit from a small numerical example. For instance, show how \(\Phi(1.96)\) is obtained from \(\operatorname{erf}(1.96/\sqrt{2})\), then explain why a tail-safe function such as \(\operatorname{erfc}\) matters when probabilities are very small. Health researchers often meet \(1.96\), confidence intervals, and tail probabilities before they meet \(\operatorname{erf}\), so this would make the function feel less alien.

The Owen's T definition gives no immediate numeric scale. I would like one sentence saying what values of \(h\) and \(a\) mean geometrically, followed by a small probability interpretation before the formal lemma. The current example \(a=0.5, b=1\) for the expected squared probit is useful, but it asks the reader to trust the value \(T(0.3536,0.5774)=0.0778\) without showing how they would obtain it in software or with a table.

The bivariate normal material would be easier if it connected more explicitly to the Gaussian copula remark in Chapter 22. Chapter 22 says evaluating the copula is not needed for ML-NMR sampling, but bivariate normal probabilities still matter for understanding and checking. Appendix D could say: "This identity is not needed to generate QMC covariate nodes, but it explains the bivariate normal probability object that appears if one evaluates the copula or computes the probit second moment."

The probit-logit approximation section needs clearer caveats about when the approximation is acceptable. The maximum absolute errors are reported, but a health researcher would also want to know whether those are errors in event probabilities before integration, errors after averaging over a covariate distribution, or both. The text should distinguish approximation error in \(\operatorname{expit}(z)\) from approximation error in \(J(m,\tau)\).

The Sobol' rank condition is under-explained for the intended reader. I can follow that full rank means exact balance in dyadic boxes, but I need a sentence translating this into applied terms: the sequence avoids leaving large empty regions of the covariate distribution after the inverse-CDF and copula transforms. That applied interpretation is present in Chapter 22, but it should be repeated here before the algebra intensifies.

## Where a novice may get lost

A novice may get lost at the first differentiation-under-the-integral argument in Owen's T. The appendix says a dominating envelope exists and displays it, but a reader weak in analysis may not know what problem this solves. A short reminder that this is the formal permission to move the derivative inside the integral would help.

The correlation heat equation for the bivariate normal is likely to feel like a sudden detour. It is used efficiently, but the reader may not see why differentiating the bivariate probability with respect to \(\rho\) is a natural move. A bridge sentence before the lemma could explain that changing \(\rho\) gradually from independence to the desired correlation lets us build the bivariate probability from the independent case.

The expected squared probit proof is clever but cognitively dense. It introduces \(U_1,U_2,Z\), turns a squared conditional probability into a joint probability, then standardizes to a correlated bivariate normal. For a novice, this is a high-value proof that needs a short verbal roadmap before the algebra: square a probability, interpret it as two independent latent probit draws, then recognize their shared dependence through \(Z\).

The Taylor-matching derivation of the two-probit coefficients is not very reproducible for a learner. It says solving the three equations numerically yields the displayed coefficients. That may be acceptable for a reference, but a novice who wants to verify the claim needs either a tiny table of residuals, a note about the solver, or a statement that this is a numerical construction rather than a hand derivation.

The digital-net rank proof is correct but probably too abstract for a reader who mainly wants to understand why Chapter 22 uses Sobol' nodes. The proof moves through binary digit vectors, row stacks, affine subspaces over \(\mathbb{F}_2\), and elementary intervals. Without a small two-dimensional example, the applied point may be lost.

Chapter 25 readers may also miss the connection. Appendix D focuses heavily on mean aggregation and the logit example, while Chapter 25 integrates likelihood kernels for survival and ordinal outcomes. The appendix should explicitly say that Sobol' and inverse-CDF machinery is the same whether the integrand is a mean, a Bernoulli likelihood contribution, a censored survival likelihood, or an ordinal category probability.

## Suggested improvements

Add a short "How to use this appendix" paragraph after the opening. It should classify the sections: MGF for exact log-link aggregation, error function for normal probabilities and quantiles used in the pipeline, Owen's T for bivariate normal and probit checks, probit-logit approximations for fast analytic checks of logit aggregation, and Sobol' construction for understanding the QMC point sets used in Chapters 22 and 25.

Add one motivating health example before the special functions begin. For example: "An AgD arm reports an event count, age is unobserved but summarized by a mean and variance, and the model uses a logit link. We need to average the event probability over the covariate distribution. The rest of the appendix explains why this is easy for log links, approximate for logit links, and numerically handled by Sobol' QMC in general." That would anchor the whole appendix.

In the error function section, add a small boxed translation table:

| Health-statistics task | Function used |
|---|---|
| normal p-value or confidence-limit tail | \(\Phi\), \(\operatorname{erfc}\) |
| transform Sobol' uniform \(u\) into a normal covariate | \(\Phi^{-1}\), hence \(\operatorname{erf}^{-1}\) |
| avoid numerical underflow in extreme tails | \(\operatorname{erfc}\) or \(\operatorname{erfcx}\) |

Before Owen's T, add a plain-language picture of the wedge probability and its relation to bivariate normals. A figure is not necessary, but even a two-sentence geometric description would help: \(h\) sets a vertical cutoff for one normal variable, and \(a\) sets the slope of a boundary for the second.

For the bivariate normal identity, add a short applied note after the theorem: this identity is most useful for analytic probit second moments and for understanding bivariate normal probabilities, but ML-NMR QMC sampling does not require evaluating the full Gaussian copula CDF.

For the probit-logit approximations, add a small "interpretation of the error" paragraph. Explain whether the reported maximum absolute errors are on the inverse-link scale before aggregation, and then show that in the Chapter 22 \(J(0.5,1)\) example the integrated error is much smaller. That makes the approximation's practical status clearer.

For Sobol' sequences, add one very small two-dimensional digital-net example before the rank theorem, even if it uses only four points. The current one-dimensional van der Corput example is excellent, but the jump to arbitrary generating matrices is steep. A novice needs to see what "balanced in boxes" means in a two-covariate setting.

Improve cross-links to Chapter 25. The appendix should mention survival and ordinal likelihood integration explicitly in the Sobol' or numerical integration discussion, not only mean aggregation and logit probabilities. Chapter 25 is where the reader learns that the integrand can be \(h^\delta S\) or an ordinal category probability, and Appendix D should reassure them that the same QMC machinery applies.

## Highest-priority fixes

1. Add more bridge text before Owen's T and the bivariate normal identity. This is the most likely place a novice reader will lose the plot.

2. Add a practical explanation of why \(\operatorname{erf}\), \(\operatorname{erfc}\), and \(\operatorname{erf}^{-1}\) matter for Chapter 22's \(\Phi\) and \(\Phi^{-1}\) computations.

3. Add a "what to retain" note before the Sobol' generating-matrix material, separating applied understanding from implementation detail.

4. Add explicit Chapter 25 cross-links explaining that the same Sobol' QMC machinery integrates general likelihood kernels, not only aggregate means.

5. Add one or two small numerical examples where the reader can reproduce a special-function value or approximation with standard software, especially for Owen's T and the error function.
