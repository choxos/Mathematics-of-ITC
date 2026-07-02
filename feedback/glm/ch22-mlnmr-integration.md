# Feedback: Chapter 22 — ML-NMR Integration

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part5/22-mlnmr-integration.qmd`

## Overall impression

I am a health researcher who knows what an odds ratio is, has run a logistic regression in R, and vaguely remembers integrals from undergrad. I came to this chapter because I use ML-NMR in my HTA work and wanted to understand what `multinma` is actually doing when it says "Sobol points" and "copula." I leave it *partially* enlightened: the high-level story (we average over a covariate distribution, and we need special points to do it well in many dimensions) is clear, and the worked example in @sec-qmc-example is the single most helpful part of the chapter. But the middle of the chapter is a wall of pure mathematical machinery (Legendre polynomials, Hardy-Krause variation, digital nets over finite fields, Riemann-Stieltjes integration by parts) that I could not follow, and the connection to actual trials, drugs, and patients almost completely disappears between @sec-qmc-intro and @sec-qmc-example. For a book that promises to take a naive researcher to mastery, this chapter assumes a lot of real analysis and number theory that I do not have, and it rarely pauses to tell me why I am proving a particular result before it proves it.

The chapter is well-structured and the prose is confident; my complaint is not that it is wrong but that it is pitched above its stated audience and under-motivated for a health researcher.

## What was unclear

- **@sec-qmc-reduction, @eq-qmc-pullback (lines 78-83).** The change-of-variables identity is stated as a "pushforward measure" fact and dropped in one line. I do not know what a pushforward measure is, and the notation $\psi=\varphi\circ T$ versus $\varphi=g^{-1}\circ\eta_{jk}$ requires me to hold three named functions in my head with no picture. A diagram or a one-sentence plain-English version ("we are just renaming the variables so the integral is over the unit square") would help enormously. The phrase "pullback to the cube" (line 76) is jargon I had to look up.

- **@sec-qmc-quadrature, @thm-quadrature-error (lines 110-131).** This theorem assumes I know what a Legendre polynomial is, what orthogonality with respect to Lebesgue measure means, and what Hermite interpolation is. None of these are introduced. The statement "let $x_1,\dots,x_k$ be the $k$ roots of the Legendre polynomial $P_k$" means nothing to me as a health researcher. This entire section reads like it was lifted from a numerical-analysis textbook without translation.

- **@thm-quadrature-error, Part 2 proof (lines 149-175).** The Hermite interpolating polynomial, the Hermite remainder formula, the integral mean value theorem, and the leading coefficient $c_k=(2k)!/(2^k(k!)^2)$ of the Legendre polynomial are all invoked as facts I am supposed to already hold. I do not. The proof is correct but it is not "from the ground up"; it leans on several classical facts that are merely referenced, not stated. This contradicts the book's stated rigor scope for Part I prerequisites but is fine *if* those facts were actually proved earlier; I could not tell whether they were.

- **@cor-tensor-quadrature-curse proof (lines 221-229).** The sentence "quadrating them in turn" (line 226) is not a word I recognize and the bound $E_k\sum_{m=1}^{d}\sup|\partial_m^{2k}f|\cdot 2^{d-1}$ appears without enough explanation of where the $2^{d-1}$ comes from. Also the substitution $k=N^{1/d}$ giving $O(N^{-2k/d})$ with "the understood reading that $k$ is fixed" is confusing: if $k$ is fixed then $-2k/d$ is a constant exponent, and the casual reader will read it as if the rate improves with $k$, which it does not in the way written.

- **@def-hardy-krause-variation (lines 334-349).** This is the single hardest definition in the chapter for me. "The $d$-fold alternating difference of $f$ over a grid box" is undefined; I do not know what an alternating difference is. The Vitali variation formula $V^{(d)}(f)=\int|\partial_1\cdots\partial_d f|$ for $f\in C^d$ is stated but not motivated. The face-restriction definition $f|_J$ with "the face $\{u_i=1:i\notin J\}$" took me several readings to parse. I think a small picture of the faces of a 2D or 3D cube with the anchored corner at $\mathbf{1}$ would make this definable for a beginner.

- **@thm-koksma-hlawka proof, multidimensional case (lines 415-426).** After a full and careful one-dimensional proof, the multidimensional case is dispatched in one paragraph that cites "Niederreiter (1992, Chapters 2 and 4)" and says "we do not reproduce the multidimensional integration-by-parts bookkeeping here." For the theorem that is the entire justification of QMC, this is a frustrating drop. I understand it is hard, but a sketch of what the $2^d-1$ face integrals *mean* geometrically, even without the full proof, would soften the cliff.

- **@def-sobol-net (lines 461-493).** This definition is the densest in the chapter. "Primitive polynomial over $\mathbb{F}_2$," "direction numbers," the recurrence with $\oplus$ (bitwise exclusive-or), and the final coordinate formula @eq-qmc-sobol-point are all introduced in one block with no warm-up. I do not know what a primitive polynomial over $\mathbb{F}_2$ is or why it matters, and the recurrence @eq-qmc-sobol-point-recurrence (line 483) is given without any explanation of *why* that recurrence builds an equidistributed sequence. The remark at line 495 (van der Corput) helps for the first coordinate, but the higher coordinates remain a black box.

- **@thm-hypercube-integration proof, Part 1 (lines 784-802).** The sentence "a distribution is determined by its margins and its copula" (line 793) is the load-bearing step and is asserted without a reference to where that was proved. It follows from Sklar's uniqueness, but the chain "margins $F_{j,i}$ + copula $C_{\Omega_j}$ $\Rightarrow$ distribution $f_j$" deserves to be stated as its own one-line corollary of @thm-sklar, not slipped into the proof.

## What wasn't elaborated enough

- **The curse of dimensionality argument (@sec-qmc-quadrature, lines 205-235).** The punchline "ML-NMR routinely runs at $d=3$ to $10$, so product quadrature is out" (line 233) is the most important practical sentence in the section, but it is delivered in one line. I would have liked a concrete sense of *what* $d$ is: in a plaque psoriasis network, which covariates? In an NDMM network, which? Telling me $d=3$ to $10$ without naming the covariates leaves the abstraction floating.

- **Why $N^{-1/2}$ is "slow" (@sec-qmc-montecarlo, lines 36-38 and @thm-mc-rmse remark, lines 296-308).** The remark says $N^{-1/2}$ is slow and that re-randomization "destroys the smooth Hamiltonian." For a reader who does not know HMC, "destroys the smooth Hamiltonian" is opaque. The remark assumes I already understand leapfrog steps, the Hamiltonian, and the stationarity guarantee of Metropolis-Hastings. A one-paragraph sidebar explaining, in health-researcher terms, "the fitting algorithm needs the likelihood to be a smooth, reproducible function of the parameters; random points make it jittery, so the fit wanders" would make this decisive objection comprehensible.

- **The Gaussian copula's "zero tail dependence" (@sec-qmc-gaussian, line 741).** This is mentioned in one clause and never explained. What is tail dependence? Why does the Gaussian copula have zero of it? When does it matter for an HTA? The remark says "a $t$-copula or vine copula is the remedy" but gives no further pointer. This is a dangling concept.

- **Randomized / scrambled Sobol' nets (@sec-qmc-kokska remark, lines 439-451 and @sec-qmc-pipeline remark, line 843).** Scrambled QMC is mentioned twice as the fix for discrete margins and for $d\gtrsim 20$, but it is never defined or explained even qualitatively. What does "scrambling" do? Why does it recover rates? I am told to go to Owen (1998) with no in-chapter intuition.

- **The probability integral transform's two directions (@sec-qmc-pit, @thm-inverse-cdf).** The theorem is clean, but the *why now* is underexplained. I am told (line 513) it is "the atom of that construction," but I would benefit from a one-line statement of the whole pipeline *before* the pieces: "we will turn uniform points into covariate values by inverting each marginal CDF; the theorem below says that works." The chapter does say this later (@sec-qmc-pipeline), but the PIT section itself feels unmotivated in isolation.

## Missing motivation / "why does this matter?"

- **Why prove the Gauss-Legendre error formula in full (lines 110-191) just to discard it?** The chapter spends ~80 lines on a theorem it then throws away because of the curse of dimensionality. A health researcher will ask: "why did I just learn this?" The motivation at line 104-108 ("gold standard in 1D, then show why it does not survive") is stated, but the sheer length of the proof relative to its eventual irrelevance feels disproportionate. Either shorten the proof or add a sentence at the top like "we develop the 1D gold standard in full because its error structure is the benchmark against which QMC is measured."

- **Why Sobol' specifically?** The chapter never says why Sobol' rather than Halton, Faure, or Niederreiter sequences. @sec-qmc-sobol says "the construction used by ML-NMR software" (line 456) and cites @sobol1967, but for a health researcher the choice is arbitrary. One sentence: "Sobol' is the default because Joe and Kuo (2008) published direction numbers up to $d=21200$ that are well tested, and because software (multinma, Stan) ships them" would close this gap.

- **Why a copula at all, rather than just assuming joint normality?** This is a deep "why" that the chapter gestures at but never nails. @sec-qmc-sklar remark (lines 663-672) says the AgD study reports margins but not the joint law, so we *supply* the copula. But why not just assume the covariates are jointly normal and be done? The answer, I think, is that some covariates are binary or skewed, but the chapter does not say this crisply. A health researcher with a binary sex covariate and a continuous age covariate needs to hear: "joint normal would be wrong for the binary margin; the copula lets you keep a normal for age and a Bernoulli for sex and still glue them."

- **Why does this matter for ITCs specifically?** The introduction (@sec-qmc-intro) ties the integral to the AgD likelihood, which is good, but the *consequence* for an actual indirect comparison is never drawn. I want a sentence like: "if this integral is wrong, the odds ratio of drug B versus drug C in the target population is wrong, and the HTA recommendation is wrong." The whole chapter is computational machinery with the clinical payoff implicit.

- **Why is the "fixed nodes" design decision so important (lines 95-100, 815-832)?** The remark at lines 815-832 is excellent and is the real reason QMC beats MC for ML-NMR, but it arrives very late. It should be foreshadowed in the introduction as the *point* of the chapter, not revealed near the end.

## Missing examples and intuition

- **No clinical / trial example until @sec-qmc-example, and even there it is abstract.** The worked example (@exm-qmc-logit) uses $X\sim\mathcal{N}(0,1)$ and $\eta(x)=\mu+x$ with no drug names, no disease, no trial. For a chapter in a health textbook, this is a missed opportunity. Even a framing sentence: "think of $X$ as baseline disease severity in a plaque psoriasis trial, $\mu$ as the drug effect, and $\theta_\bullet$ as the modeled response rate on the secukinumab arm of an AgD study" would anchor everything.

- **No picture of a low-discrepancy point set versus random points.** The van der Corput remark (lines 496-508) lists seven fractions; a two-panel scatter figure (random vs Sobol' in 2D) would make "uniformity not randomness" instantly intuitive. The chapter has zero figures, which is striking for a geometric subject.

- **No picture of the transport map $T$.** The pipeline @eq-qmc-pipeline is a chain of four transforms; a flow diagram (cube $\to$ normal $\to$ correlated normal $\to$ correlated uniform $\to$ covariate space) would make @thm-hypercube-integration far more approachable than the algebraic proof.

- **No concrete discrete-margin example.** The caveat about discrete margins inflating Hardy-Krause variation (lines 439-451, 574-582) is mentioned three times but never shown. A tiny example: binary $X\in\{0,1\}$ with $p=0.3$, plot or tabulate $\psi(u)=\mathrm{expit}(\mu+F^{-1}(u))$ and show the jump, would make the abstract warning tangible.

- **The two-covariate trace (@exm-qmc-copula-trace) is good but tiny.** It traces one point. I would value a small table of, say, four points each pushed through the pipeline, so I can see the correlation "doing its work" across multiple nodes, not just one. The exercise @exr-qmc-logit-pipeline asks me to do exactly this, but the chapter itself does not.

## Notation and jargon problems

- **$\mathrm{expit}$ (line 60).** Defined once as $e^z/(1+e^z)$, good, but the word "expit" is unfamiliar to many health researchers who know it as "inverse logit" or "logistic." A parenthetical "(the logistic function)" would help.

- **$\Phi_{\boldsymbol{\Omega}}$ (line 688).** This notation for the joint CDF of $\mathcal{N}(\mathbf{0},\boldsymbol{\Omega})$ is introduced inside the definition of the Gaussian copula without a forward reference to [Notation]. The notation file lists $\Phi$ but not $\Phi_{\boldsymbol{\Omega}}$.

- **$V_{\mathrm{HK}}$, $D_N^*$, $V^{(d)}$, Vitali variation (lines 330-348).** These are in [Notation] (lines 144-145), good, but the *concept* of Vitali variation versus Hardy-Krause variation is jargon-dense and the in-chapter definition does not connect to the notation table entry.

- **"Anchored at $\mathbf{1}$" (line 342).** Why $\mathbf{1}$ and not $\mathbf{0}$? This is a standard convention but never explained; a beginner will wonder why the anchor is the top corner.

- **$\oplus$ as bitwise XOR (line 484).** Defined inline, good, but the recurrence mixes ordinary integer multiplication ($2\,a_{i,1}\,m_{i,\ell-1}$) with XOR ($\oplus$), and it is not obvious that the multiplication is *not* over $\mathbb{F}_2$ but over the integers then XORed. This will trip up anyone trying to implement it.

- **"Quadrating" (line 226).** Not a standard English word in this sense; I believe the intent is "applying quadrature." Replace with "applying the rule."

- **$f$ used for both the integrand and the covariate density.** In @thm-koksma-hlawka (line 358) $f$ is the integrand on the cube; in @eq-qmc-aggregation $f_j$ is the covariate density. The reuse of $f$ is mildly confusing, especially since the chapter also uses $\varphi,\psi$ for the same objects. Settling on one symbol family would help.

- **"Pullback" (line 76).** Differential-geometry jargon; not in the notation file and not glossed.

## Pacing issues

- **The chapter front-loads two dense paragraphs (@sec-qmc-intro, lines 5-63) that reference nine prior theorems and four prior definitions before any new content.** As a health researcher I was exhausted before @sec-qmc-reduction. The roadmap paragraph (lines 31-56) is excellent in content but should be broken into shorter sentences or a bulleted "what this chapter will do" list.

- **The jump from @sec-qmc-montecarlo to @sec-qmc-kokska is abrupt.** MC is dispatched with a clean theorem and a variance argument; then Koksma-Hlawka hits the reader with two dense definitions (star discrepancy, Hardy-Krause variation) and a full proof in immediate succession. There is no transition paragraph saying "MC was probabilistic; we now seek a deterministic bound, which requires two new quantities."

- **@sec-qmc-sobol is paced too fast.** After the careful analytic proofs of the preceding sections, the Sobol' definition crashes through primitive polynomials, direction numbers, a recurrence, and a point formula in ~30 lines with no example or intuition beyond the van der Corput remark. This is the single hardest section to read and it gets the least scaffolding.

- **@sec-qmc-pit and @sec-qmc-sklar are well-paced** (these are the cleanest sections for a beginner), but then @sec-qmc-gaussian re-accelerates with Cholesky factorizations and the Owen $T$-function reference in quick succession.

- **The worked example (@sec-qmc-example) arrives only at the end.** For a beginner, the natural reading order would be: skim the pipeline picture, see the worked example, *then* go back and learn the theorems that justify it. Putting one small numerical illustration earlier (e.g., right after @eq-qmc-pullback) would give the abstract machinery a concrete hook to hang on.

## What worked well

- **@sec-qmc-example (@exm-qmc-logit) is genuinely excellent.** The seven-point Sobol' computation with the symmetry argument in Part A, the monotone convergence table in Part B, and the explicit MC contrast are exactly the kind of hand-computable, reproducible example the book promises. This is the section I will return to.

- **The two-covariate trace (@exm-qmc-copula-trace) makes the copula step visible** in a way the preceding definitions could not. The numeric trace $\mathbf{u}\to\mathbf{z}\to\tilde{\mathbf{z}}\to\tilde{\mathbf{u}}\to\mathbf{x}$ is pedagogically perfect.

- **The "fixed nodes, smooth in parameters" remark (lines 815-832)** is the clearest statement in the chapter of *why* QMC and not MC, and it should be elevated.

- **The Koksma-Hlawka one-dimensional proof (lines 369-413)** is, despite my complaints about prerequisites, a beautiful and self-contained argument; the identity @eq-qmc-kokska-identity (line 396) that the error is the integral of the discrepancy against $df$ is a genuine insight I am glad to have seen.

- **The remarks throughout are generally stronger than the theorems at speaking to a health researcher.** The "Why Sklar is the right tool for aggregate data" remark (lines 663-672) and the "Evaluating versus sampling the copula" remark (lines 732-744) are models of accessible explanation; more of this voice in the main text would transform the chapter.

- **The exercises (@sec-qmc-exercises) are well chosen and graded.** @exr-qmc-pit-discrete in particular directly addresses my complaint about the missing discrete-margin illustration.

- **The notes and references (@sec-qmc-notes) are thorough and honest** about what is proved in the book versus cited to Niederreiter, Stoer-Bulirsch, Nelsen.

## Suggestions

1. **Add two figures:** (a) random points vs Sobol' points in 2D; (b) a flow diagram of the pipeline $T$ from cube to covariate space. These would do more for a beginner than any amount of additional prose.
2. **Insert a one-paragraph clinical framing** at the top of @sec-qmc-intro naming a concrete AgD scenario (e.g., a plaque psoriasis or NDMM network with named covariates) and stating that a wrong integral means a wrong odds ratio and a wrong HTA recommendation.
3. **Move a small numerical teaser** (3-4 Sobol' points, one line of the pipeline) to immediately after @eq-qmc-pullback so the abstraction has a concrete anchor before the machinery begins.
4. **Soften the prerequisites in @sec-qmc-quadrature:** either state the Legendre/Hermite facts inline in a small preamble, or explicitly point back to where in Part I they were proved. Do not invoke "a classical fact about orthogonal polynomials" (line 134) without a chapter reference.
5. **Add a picture and a plain-English gloss to @def-hardy-krause-variation:** draw the faces of a 2D cube anchored at $\mathbf{1}$ and say "variation is the total up-and-down wiggling of the function, summed over all lower-dimensional faces."
6. **Explain *why* Sobol'* (Joe-Kuo direction numbers, software availability) in one sentence at the top of @sec-qmc-sobol, and explain primitive polynomials over $\mathbb{F}_2$ in two sentences before using them.
7. **Foreshadow the "fixed nodes" design decision** in the introduction as the organizing principle of the chapter, not as a late remark.
8. **Define or briefly motivate "tail dependence"** where the Gaussian copula's zero tail dependence is mentioned (line 741), or drop the mention if it is not developed.
9. **Fix "quadrating" (line 226)** to "applying quadrature," and clarify the integer-vs-$\mathbb{F}_2$ arithmetic in the Sobol' recurrence (line 483).
10. **State the "margins + copula determine the distribution" step** as an explicit corollary of @thm-sklar and reference it in @thm-hypercube-integration's proof, rather than asserting it inline.
11. **Add a discrete-margin worked micro-example** (binary covariate, show the jump in $\psi$) to make the Koksma-Hlawka caveat concrete instead of repeated abstractly three times.
12. **Reconcile the symbol $f$**: use $\psi$ consistently for the cube integrand inside theorems and reserve $f_j$ for the covariate density, to avoid the dual use in @thm-koksma-hlawka vs @eq-qmc-aggregation.