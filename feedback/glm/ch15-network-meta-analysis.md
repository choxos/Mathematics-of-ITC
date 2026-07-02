# Feedback: Chapter 15 — Network Meta-Analysis

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part3/15-network-meta-analysis.qmd`

## Overall impression

I'll be honest: I found this chapter very hard going. It is clearly written for someone who already
thinks in linear algebra and graph theory, not for a health researcher like me who can do basic
calculus but gets shaky when faced with null spaces, incidence matrices, and rank arguments. The
core idea, that an NMA is just a generalized linear model and "which contrasts can the network
estimate?" reduces to "which columns of X are independent?", is genuinely powerful and I *wanted* to
understand it. But the chapter keeps the ITC domain at arm's length for long stretches while it does
pure algebra, and I lost the thread of *why* the algebra mattered for my actual work (deciding
whether drug B beats drug A across a messy pile of trials). The worked example at the end
(@sec-nma-example) was the lifeline; it should come much earlier. There are several places where a
sentence of motivation, a concrete drug name, or a one-line intuition would have saved me pages of
confusion.

## What was unclear

**The very first paragraph (@sec-nma-intro, lines 7-16)** lost me at "the subtraction
$\hat d_{AB}=\hat d_{AC}-\hat d_{BC}$ that the algebra of contrasts licenses under transitivity." I
know from Chapter 14 roughly what Bucher's estimator is, but the phrase "the algebra of contrasts
licenses" is jargon-as-punctuation: it does not explain *what* algebra, *why* subtraction is
licensed, or what "under transitivity" formally means here. A reader like me needs one sentence
saying, in words: "Because relative effects on the link scale add up (the effect of B vs A plus the
effect of C vs B gives the effect of C vs A), we can subtract two independent estimates that share a
common comparator to get a third."

**@def-nma-arm-model (lines 74-92):** The definition jumps straight to "the arm-based network model
writes the vector $\boldsymbol\theta=\mathbf X\boldsymbol\beta$" with no warmup. I had to re-read
three times. What is $\boldsymbol\theta$ a vector *of*, concretely? It says "all arm means" but I did
not immediately see that one entry of this vector is "the log-odds of response on the drug-2 arm of
trial 7." A one-line concrete unpacking of the vector, e.g. "$\boldsymbol\theta=(\theta_{1,1},
\theta_{1,2},\theta_{2,1},\theta_{2,3},\dots)^\top$, one entry per arm, ordered as trial-1-then-trial-2,"
would have anchored me.

**@eq-nma-linpred and the GLM framing (lines 81-91):** The model couples "a response distribution
from an exponential family" with the linear predictor, then gives the binomial example
$r_{jk}\sim\mathrm{Bin}(n_{jk},g^{-1}(\theta_{jk}))$. But $\theta_{jk}$ was *defined* as
$g(\bar\mu_{jk})$, so $g^{-1}(\theta_{jk})=\bar\mu_{jk}$. This circular-feeling move (define theta as
g of the mean, then put the mean as g-inverse of theta) is mathematically trivial but pedagogically
disorienting for a weak reader. A diagram or a single worked numeric sentence ("if $g$ is the logit
and $\theta_{jk}=0.5$, then $\bar\mu_{jk}=g^{-1}(0.5)\approx0.62$") would dispel the fog.

**@lem-incidence-rank (lines 272-307):** The proof is clean *if* you already know what a signed
incidence matrix is. I had to puzzle out the orientation convention ("$-1$ at the tail, $+1$ at the
head") and the fact that $\mathbf{Bv}$ computes *differences across edges*. The proof never says in
words "the incidence matrix maps a vertex-labeling to the vector of edge-wise differences of that
labeling," which is the one sentence that makes the kernel argument click. Without it, the
"equalizes across every edge" step reads as a magic trick.

**@thm-consistency-closure part 4 (lines 212-214, 234-239):** The converse/uniqueness argument is
dense. "Setting $a=b=c$ gives $e_{aa}+e_{aa}=e_{aa}$" is correct but I had to sit with it; a beginner
benefits from being told explicitly "plugging the same index into the loop identity gives the
diagonal." The antisymmetry step "setting $c=a$" is similarly slick; one extra clause ("because the
loop identity holds for *all* triples, we may choose the triple freely") would slow the pacing enough.

**@thm-parameterization-equivalence part 2 (lines 374-380, 409-425):** The bijection argument uses
$\Psi:\boldsymbol\theta\mapsto(\boldsymbol\mu^{\mathrm{BS}},\boldsymbol\delta)$ and then composes it
with $\Phi$. I got lost in the composition and the two coordinate systems. A small diagram, or even a
tabular "this parameter in BS coordinates corresponds to this parameter in RT coordinates," would
help. The remark at lines 437-448 ("Why the surplus is harmless and where it bites") is excellent and
should arguably appear *before* the theorem, not after, because it gives the intuition that the
theorem then formalizes.

**@thm-re-nma-correlation (lines 580-633):** The model $\eta_{jk}=d_k+u_{jk}$ with
$u_{jk}\sim\mathcal N(0,\tau^2/2)$ is introduced with no motivation for *why* $\tau^2/2$ rather than
$\tau^2$. I only understood the $\tau^2/2$ choice after reading the whole proof: it is so that the
*contrast* variance comes out to $\tau^2$. But the theorem statement presents the half as if it were
obvious. The preceding lemma (@lem-half-correlation-forced) explains *why* one-half for the
correlation, but the *variance* $\tau^2/2$ is a separate, equally unmotivated choice. One sentence:
"the factor one half on the arm-level variance is chosen so that the contrast variance is the
network heterogeneity $\tau^2$," would fix it.

## What wasn't elaborated enough

**Connectivity and the real world (around @thm-fe-nma-identifiability, lines 457-537):** The theorem
says identifiability requires the graph to be connected. For a health researcher the practical
question screams out: "what does a disconnected network look like in practice, and what do I do?"
The remark at lines 529-537 gestures at it but never gives a concrete example. I wanted: "Suppose
trials exist for Drug A vs placebo and for Drug B vs placebo, but no trial ever connects the
placebo-arm studies to a separate cluster of Drug C vs Drug D trials; then A-vs-B is identifiable but
A-vs-C is not." A figure of a disconnected graph with drug labels would be worth a page of prose.

**The contrast-based vs arm-based distinction (lines 112-123):** The remark is compact and I had to
read it twice. The key claim, "Passing from the arm-based to the contrast-based likelihood is exactly
the elimination of the per-study baselines $\mu_j$," is stated but not shown. For a weak reader, a
two-equation display: "$\theta_{j1}=\mu_j$, $\theta_{j2}=\mu_j+\delta_{j,12}$; subtract to get
$\delta_{j,12}=\theta_{j2}-\theta_{j1}$, and $\mu_j$ vanishes," would make the "elimination"
tangible rather than abstract.

**Node-splitting mechanics (@sec-nma-nodesplit, lines 648-746):** The definition
(@def-node-splitting, lines 683-697) says the indirect estimate is "computed from the network with
the direct $AB$ evidence removed." But *how* is it computed, operationally? Is it just re-fitting
the whole GLS without those rows? The worked example (Step 5, lines 1047-1068) shows it, but the
definition section does not, and I was confused until I reached the example. A forward pointer at
the definition ("the example of @sec-nma-example, Step 5, makes this explicit") would bridge the gap.

**Residual deviance (@def-residual-deviance, lines 851-883):** The binomial formula is dropped in,
and the derivation remark follows, but the *interpretation* is thin. The remark says "$D_{\mathrm{res}}$
is approximately $\chi^2_{N-p}$" and "a value far in excess signals lack of fit," but never tells me
what counts as "far in excess," nor that the comparison is to the residual degrees of freedom
$N-p$. The worked example (Step 6, line 1080) uses "$0.40\ll 3$" but never explains the rule of
thumb. A sentence like "values near $N-p$ are good; values several times $N-p$ are worrisome" is what
a practitioner needs.

**DIC thresholds (@def-dic, lines 885-902):** The thresholds "below about 3 are not meaningful" and
"above 5 are substantial" are stated with no source and no intuition. Where do 3 and 5 come from? A
health researcher applying DIC needs at least a one-line justification or a citation to where these
rules of thumb are derived.

## Missing motivation / "why does this matter?"

**Why a network at all?** The introduction (lines 5-16) says an HTA "is rarely so tidy" and must
"weigh a dozen treatments," but it never says *why* we pool everything into one model instead of just
running many separate pairwise Bucher comparisons. The motivation "pooling borrows strength: a
contrast with no direct head-to-head trial is informed by indirect paths, and multi-arm trials are
handled without throwing away the correlation structure" is implicit but never stated as the
payoff. For a reader coming from Chapter 14 who only knows the single triangle, the leap to a full
network needs a motivational paragraph: "If we only did pairwise Bucher we would ignore the fact that
all the contrasts are mutually consistent or mutually contradictory; the network tests that, and
borrows information across loops."

**Why prove the parameterization equivalence?** @thm-parameterization-equivalence is a substantial
theorem (lines 361-435) and I read it without understanding *why* I should care that two
parameterizations agree on a subspace. The remark after (lines 437-448) hints that the surplus
degrees of freedom are "where inconsistency lives," but that is the *whole point* and it appears only
in a remark. A motivating sentence before the theorem: "We need to know that the
reference-treatment parameterization, which bakes consistency in, does not silently drop any
plausible arm-mean pattern; the theorem says it captures exactly the consistent ones, and the
surplus baseline-shift parameters are precisely the ones the data can contradict," would give the
theorem a purpose before I slog through it.

**Why the one-half correlation matters (@sec-nma-random, lines 539-646):** The chapter proves
$\rho=1/2$ is forced by basis invariance and realized by exchangeable arm effects. But the *clinical*
reason I should care is buried: a three-arm trial is *not* two independent two-arm trials, and
treating it as such gives wrong standard errors. The remark at lines 635-646 makes this point in a
subordinate clause. For a health researcher who has definitely, at some point, naively split a
three-arm trial into two comparisons in a meta-analysis, this is the single most actionable lesson
of the chapter and deserves a standalone motivational sentence up front.

**Why identifiability matters for ITCs:** @thm-fe-nma-identifiability is the central theorem, but the
chapter never says in plain words: "If your network is disconnected, no statistical trick can
estimate the missing contrast; you must either find a connecting trial or bring in external
population-adjustment assumptions (Part V)." The remark at lines 529-537 gets close but frames it as
forward-looking ("the task that unanchored population adjustment confronts") rather than as the
*reason* the theorem is clinically load-bearing.

**Why consistency / loop closure:** @thm-consistency-closure is elegant but its ITC payoff, that
loops are the *only* place inconsistency can be tested, is stated only in the remark at lines 253-264
and then in passing. A health researcher's question is "how do I know my network is trustworthy?"
and the answer, "only closed loops can be checked; an open tree must be taken on faith," is the
practical heart of the theorem. It should be foregrounded.

## Missing examples and intuition

**No running drug example.** The entire theoretical development (lines 56-841) uses abstract labels
$1,2,3,\dots,K$ and studies "$j$." Not once is a real or plausible drug named. A health researcher
internalizes through concreteness: "placebo, low-dose statin, high-dose statin, ezetimibe." Even a
single parenthetical "(think: placebo = treatment 1, Drug X = treatment 2, Drug Y = treatment 3)"
dusted through the definitions would keep me oriented. The worked example (@sec-nma-example) uses
numeric estimates but still no clinical referent; I never learned whether 0.5 is a big log-odds
ratio or a small one in context.

**No picture of a network.** The treatment-comparison graph $G$ is defined formally
(@def-nma-arm-model, lines 76-79) and invoked throughout, but there is not a single figure of an
actual network. For a chapter whose central object is a graph, this is a glaring gap. A figure
showing: (a) the Bucher path (tree), (b) the closed triangle, (c) a disconnected two-component
network, (d) a star with a multi-arm trial at the center, would make @thm-fe-nma-identifiability,
@thm-consistency-closure, and the node-split discussion instantly readable.

**No intuitive bridge from Chapter 13.** Chapter 13 covered pairwise meta-analysis
(fixed/random effect, DerSimonian-Laird, $I^2$). The chapter nods to it (lines 654-680,
@prp-network-contrast-pooling reduces to the two-study fixed-effect meta-analysis of Chapter 13),
but never says plainly: "NMA is pairwise meta-analysis with more than two treatments and a shared
network structure; everything you learned about inverse-variance pooling carries over, plus the
graph geometry." That one sentence would have made me feel I was building on known ground.

**No numeric intuition for the one-half.** The one-half correlation is proven algebraically; I would
have liked a tiny numeric illustration: "two contrasts each with variance $\tau^2$, correlation
$1/2$; their difference has variance $\tau^2$, exactly the same, which is the point." The proof
contains this arithmetic (line 568) but presents it as algebra, not as the punchline.

## Notation and jargon problems

**$C$ for within-study contrast count vs $c$ for connected components:** @eq-nma-totalcontrasts
defines $C=N-J$ as the total within-study contrast count; @thm-fe-nma-identifiability uses $c$ for
the number of connected components. The case distinction is easy to miss and I conflated them on
first reading. A different letter (say $q$ for components, or $\kappa$) would avoid the collision.

**$\mathcal S_{\mathrm{cons}}$ vs $\mathcal C$:** @thm-parameterization-equivalence defines
$\mathcal S_{\mathrm{cons}}$ for the consistency-constrained subspace; @thm-consistency-closure
uses $\mathcal C$ for the set of consistent contrast families. Two different "consistency" symbols
for two different objects in adjacent sections. They are not the same space (one is arm means, one
is contrast families), and a beginner will trip.

**"Saturated relabeling" (line 357):** The phrase "the baseline-shift parameterization is a
saturated relabeling of the arm means and ranges over all of $\mathbb R^N$" uses "saturated" in the
statistical sense (as many parameters as data points) without flagging it. A weak reader knows
"saturated" only from "saturated fat" or "saturated model" in deviance, and the connection is not
obvious.

**"Profiling out" baselines (line 339, 987):** The phrase "the baselines profiled out" / "eliminating
the per-study baselines" is used as if the reader knows what profiling means. It does not point to a
definition or a Chapter 6 reference. A one-clause gloss "(i.e. solving them out of the likelihood by
concentrating on the contrasts)" would help.

**$J_m=\mathbf 1_m\mathbf 1_m^\top$ (line 596):** Introduced without warning inside
@thm-re-nma-correlation. The notation table has it, but a reader mid-chapter will not remember.
Restating "$J_m$ is the $m\times m$ all-ones matrix" on first use is cheap and saves a lookup.

**$\tilde{\mathbf d}$ vs $\mathbf d$ (lines 398-399, 487):** The proof introduces
$\tilde{\mathbf d}=(d_1,\dots,d_K)$ "with $d_1=0$" to distinguish the padded vector from the
$K-1$-vector $\mathbf d$. The tilde convention is introduced inline and never re-declared; I had to
scroll back to find it each time. A standing remark or a dedicated symbol would be cleaner.

## Pacing issues

**The graph-theory toolkit (@sec-nma-rank, lines 266-352) lands too early.** The chapter introduces
the incidence matrix and the Gram-matrix lemma *before* it has motivated why rank is the key
question. I read @lem-incidence-rank and @lem-nma-gram as abstract linear-algebra facts with no
apparent purpose, and only retroactively, at @thm-parameterization-equivalence and
@thm-fe-nma-identifiability, did I see why. A brief forward pointer at the start of @sec-nma-rank
("We will need these two facts to settle, first, the equivalence of the parameterizations and,
second, the identifiability of the contrasts") would justify the detour.

**The worked example comes last (@sec-nma-example, lines 963-1096).** This is the single biggest
pacing problem. Every theoretical section would be easier with a concrete running example threaded
through it. Delivering the example only at the end means a reader fights through ~900 lines of
abstract machinery before seeing a single number. I strongly suggest introducing the triangle network
of @exm-nma-triangle *right after @def-nma-arm-model*, then referring back to it at each subsequent
theorem: "here is its design matrix, here is its incidence matrix, here is what the one-half
correlation looks like in it."

**@thm-consistency-closure before @thm-parameterization-equivalence.** The closure theorem
(lines 193-251) is pure contrast algebra with no model context yet; it reads as a standalone lemma
about antisymmetric arrays. Then @thm-parameterization-equivalence uses "consistency-constrained
subspace" which depends on @eq-nma-consistency-constraint but not directly on the closure theorem.
The ordering feels out of step; the closure theorem might sit better *after* the parameterizations
are both on the table, as the analysis of the redundancy that the reference-treatment form bakes in.

**@sec-nma-deviance (lines 843-961) feels detached.** After the identifiability and
random-effects theory, the deviance/DIC section reads like an appendix pasted into the chapter. The
connective tissue ("a fitted model must be checked") is one sentence. The DIC in particular
(@def-dic, @prp-dic-pd) introduces a Bayesian posterior, expectation over the posterior, and a
quadratic-deviance assumption, none of which were previewed earlier; for a weak reader this is a
sudden gear shift into material that belongs more naturally in Chapter 8 (hierarchical Bayes).

## What worked well

The **Bucher-as-network remark** (lines 99-110) is the clearest bridge in the chapter: it names the
exact numbers ($K=3$, $N=4$, $J=2$, $C=2$), draws the path $A-C-B$, and shows exactly where Bucher
sits inside the larger apparatus. This is the model for how to write the rest.

The **worked example** (@exm-nma-triangle, lines 970-1096) is excellent once I reached it. Every step
is numeric, every matrix is written out, and the final pooling check (line 1066-1068, confirming the
full-network estimate equals the inverse-variance blend) is the kind of closure that builds
confidence. Step 5 (the node-split) is the best pedagogical moment in the chapter.

The **"What each hypothesis buys, and the failure modes" remark** (lines 825-841) after
@thm-ipd-nmr-identifiability is exactly the kind of post-theorem interpretation I wanted everywhere:
it tells me what each assumption is *for* and what breaks if I drop it. If every theorem had a
remark this concrete, the chapter would be far more accessible.

The **"Loops carry the constraints" remark** (lines 253-264) gives the graph-theoretic reading of
@eq-nma-loopcount in plain language and is the one place the cycle-rank intuition lands.

The **exercises** (@sec-nma-exercises, lines 1149-1219) are well chosen and range from mechanical
(@exr-nma-design, @exr-nma-incidence) to conceptual (@exr-nma-ipd-collinear, @exr-nma-pooling). The
starred exercises reward the reader who pushed through the theory.

## Suggestions

1. **Add a figure of a treatment-comparison network** (Bucher path, closed triangle, disconnected
   graph, star/multi-arm) right after @def-nma-arm-model. The chapter's central object is a graph;
   not drawing it is a false economy.

2. **Move @exm-nma-triangle forward**, introducing it as a running example immediately after the
   arm-model definition, and revisit it at each theorem. Deliver the full six-step computation in
   @sec-nma-example as the *completion* of the running thread, not as a revelation.

3. **Name drugs.** Replace abstract $1,2,3$ with "placebo, Drug A, Drug B" in at least the
   definitions, the closure theorem, and the identifiability theorem. Concreteness is the beginner's
   handhold.

4. **Add a one-paragraph "why this chapter" motivation** at the head of @sec-nma-intro that says,
   in health-researcher language, *why* pooling into a network beats running many Bucher comparisons,
   and *what* the chapter will let the reader do that Chapter 14 did not.

5. **Reorder @sec-nma-rank** so that the two lemmas are introduced with a forward pointer to their
   uses, or defer the lemmas to an appendix and cite them inline. Rank facts with no stated purpose
   are demoralizing.

6. **Gloss jargon on first use:** "saturated," "profiling out," "$J_m$," the $\tilde{\mathbf d}$
   convention. Each is a 30-second fix that saves a 5-minute reread.

7. **Add intuition sentences before the heavy theorems:** before @thm-parameterization-equivalence
   ("the surplus baseline-shift parameters are where inconsistency hides"), before
   @thm-consistency-closure ("loops are the only testable structure"), before
   @thm-fe-nma-identifiability ("disconnected means no estimate, period"). The remarks that say these
   things *after* the theorems should be split, with the headline intuition moved before.

8. **Explain the $\tau^2/2$ arm-level variance** at the point it is introduced in
   @thm-re-nma-correlation, not retroactively through the proof.

9. **Give residual-deviance and DIC rules of thumb with sources.** "Far in excess of $N-p$" and
   "differences below 3 / above 5" need either a derivation pointer or an explicit citation so the
   reader can trust the numbers.

10. **Resolve the $C$/$c$ and $\mathcal S_{\mathrm{cons}}$/$\mathcal C$ notation collisions**, and
    restate inline any symbol (like $J_m$) that is used only rarely.