# Feedback: Chapter 17 — Population Adjustment Theory

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part4/17-population-adjustment-theory.qmd`

## Overall impression

I came into this chapter knowing that indirect comparisons (ITCs) are used when two drugs have never been
trialled head-to-head, and that "population adjustment" is some fix for when the trial populations differ.
That is roughly the level I am at. This chapter is clearly the theoretical core of the book and it is
*dense*. I felt like I was reading a pure-math paper that occasionally remembered it was about drugs. The
ideas are important and I *think* I understood the headline (anchored only needs effect modifiers in the
adjustment set; unanchored needs prognostic variables too; scale matters), but I had to reread almost every
paragraph several times, and several proofs lost me. There is a real and good worked example at the end
(@exm-pat-anchored) that rescued me, but it comes after 900 lines of abstraction. I would have given up
before reaching it if I were not reviewing. The chapter is internally coherent and the theorem statements
are careful, but the gap between the prose register and my background is wide.

## What was unclear

- **The very first paragraph (@sec-pat-intro, lines 7-14).** It front-loads references to
  @thm-bucher-unbiased, @def-constancy-relative-effects, @def-effect-modifier, @thm-failure-of-bucher,
  Chapter 14, Chapter 16. As a reader I am told "this chapter is the systematic response to that failure"
  before I have been reminded in plain words what the failure actually *was*. One sentence of plain-English
  recap ("Bucher subtracts two relative effects; it is unbiased only if those relative effects do not
  depend on covariates that differ between trials; if they do, the subtraction mixes populations") would
  have oriented me. Instead I have to hold five cross-references in my head to parse the motivation.

- **"Scale-specific" in the intro (lines 28-41).** The paragraph distinguishing the model link $g$ from the
  reporting scale $h$, and "aligned" vs not, is the single most important conceptual move in the chapter,
  and it is dispatched in one paragraph with four cross-references (@def-link-function,
  @def-scale-alignment, @def-non-collapsibility, @thm-noncollapsibility-or-hr). I had no working intuition
  for what $g$ and $h$ *are* concretely until the worked example at line 971. A sentence like "for a
  logistic model $g=\mathrm{logit}$ is the scale the model is fit on; if a decision maker wants a risk
  difference then $h=\mathrm{id}$, and $h\circ g^{-1}$ is not the identity" would have made the abstraction
  land. As written I had to trust the symbols.

- **@eq-pat-nmr (lines 119-122).** The linear predictor is dropped on me with the gloss "$\mu_j$ is the
  study baseline, $\boldsymbol\beta_1$ the prognostic main effects, $\gamma_k$ the treatment main effect,
  $\boldsymbol\beta_{2,k}$ the treatment-by-covariate interactions." I can parse that, but I have no
  picture of what this model *looks like* for a real trial. There is no "suppose we have a trial of drug A
  vs placebo C in 400 patients with covariates age, sex, baseline severity; then $\eta$ looks like ..."
  moment. The model is the spine of the whole chapter and it is introduced as pure symbols.

- **The reference-second index convention (lines 130-132).** "$\tau^{g}_{kC}(x)$ is the conditional analogue
  of the trial contrast $d_{kC}=\eta_C-\eta_k$ and a positive value means $k$ improves the (worse is larger)
  outcome relative to $C$." This sentence took me four reads. The sign convention is buried inside a
  parenthetical, and "worse is larger" is a convention I had to keep re-deriving. Given that *every*
  subsequent number in the worked example depends on this sign, it deserves a dedicated short paragraph
  and maybe a one-line table of "positive $\tau$ means X."

- **@prp-pat-conditional-transport (lines 208-233) and its proof.** The "change of measure" step
  (lines 226-230) is the key trick of the whole chapter, and it is shown as one line:
  "$f_{\mathcal P^{*}}(x)=w(x)f_{\mathcal P}(x)$". As a weak-math reader I needed to be told *why* this is
  legitimate (it is just the Radon-Nikodym / importance-sampling identity, and it requires the support
  condition), and ideally to see the discrete version first (sums reweighted by $f_*/f$), because the
  continuous version looks like magic. The overlap assumption is invoked but its role (it is what stops the
  ratio from blowing up) is not stated in the proof even though it is in the proposition header.

- **@thm-anchored-paic-consistency parts (a)-(e) (lines 383-437).** The five-part theorem is the centerpiece
  and it is genuinely hard. Part (c) (lines 420-424) says "in general
  $\theta\neq\Delta^{\mathrm{Marg},g}$, even under SEMA and scale alignment." I read this three times and
  could not tell whether it is saying "the method fails" or "the *estimand* the method targets is the
  conditional one, which is a different number from the marginal one." The latter is what is meant, and the
  proof (lines 472-483) makes it clear, but the theorem statement itself reads like a failure. The phrasing
  "Non-recovery of a non-collapsible marginal effect" is technically precise but actively misleading to a
  novice: nothing was "not recovered," the method simply targets a different estimand.

- **Part (e) "class-wise necessity" (lines 431-434, proof lines 496-509).** "Over the class of
  data-generating mechanisms ... the estimand is asymptotically biased. No claim is made for any specific
  mechanism." I think I understand this means "there exists a bad mechanism, but yours might be fine by
  coincidence," but "class-wise necessity" is jargon I had to infer. A one-line gloss ("necessity holds on
  average over a class, not pointwise for every member") would help. The phrase appears in the intro
  (line 37) too, before it is defined.

- **@thm-shared-em-identifiability proof (lines 689-709).** The step "with full column rank of the design
  and a strictly monotone link, the coefficients of a generalized linear model are identified (Chapter 7)"
  is a big jump. Chapter 7 is far away in my memory; a one-line reminder of *what* identifiability means
  here (the map from parameters to the conditional mean is injective) would have made this less of a
  black box. The AgD identification step (lines 698-706) is much clearer because the arithmetic is shown.

- **@prp-testable-untestable-constancy proof (lines 786-804).** The argument that SEMA is untestable rests
  on "the set of $(\gamma_B,\boldsymbol\beta_{2,B})$ consistent with the AgD is the entire hyperplane." I
  followed the algebra but the *intuition* (one scalar summary cannot pin down a vector of interactions)
  is never stated in words. For a reader like me, the geometric picture ("a single equation defines a
  hyperplane; SEMA picks one point on it; the data cannot tell you which point is right") is the
  load-bearing insight and it is hidden inside the symbols.

- **@thm-target-population-estimand (lines 823-851).** By the time I reach this theorem I have already seen
  most of its content scattered through the chapter, and it reads as a recap. That is fine, but as a
  novice I could not tell what was *new* here versus what was being consolidated. A sentence framing it as
  "the clean summary statement" would help.

## What wasn't elaborated enough

- **The effect-modifier vs prognostic-variable distinction (@sec-pat-em-pv, lines 284-347).** This is
  called "the algebraic heart of the chapter," and it gets two lemmas with proofs, but the *definition*
  of "prognostic" and "effect modifier" is deferred entirely to Chapter 11 (@def-prognostic-variable,
  @def-effect-modifier). For a reader picking up the book at Part IV, there should be at least a one-sentence
  inline restatement: "a prognostic variable moves the outcome under *both* arms; an effect modifier moves
  the *difference* between arms." Without that, @lem-pat-pv-cancellation and @lem-pat-em-not-pv are proofs
  of statements I cannot connect to my vocabulary.

- **The witness constructions in @prp-pat-absolute-implies-relative (lines 270-275) and
  @lem-pat-em-not-pv (lines 335-340).** Both use the toy model $\mu_a=\mu_b=w$ or $\mu=\mu=w$. These are
  clever but so minimal that I could not tell what feature of the world they are isolating. A half-sentence
  after each saying "this is the case where a covariate shifts the baseline risk but leaves the treatment
  contrast untouched" would make them pedagogically useful rather than just logically sufficient.

- **"Directly collapsible" vs "collapsible" (lines 411-418, 461-470).** The theorem distinguishes a measure
  that is "directly collapsible" (identity scale, @prp-emcoll-rd-direct) from one that is "collapsible"
  with a constant conditional contrast (@thm-collapsible-transport). The distinction is doing real work in
  part (b) but it is never explained in the chapter; it is outsourced to Chapter 11. A two-line aside
  contrasting "marginal = conditional for *every* covariate distribution" (direct) versus "marginal =
  conditional *when the conditional contrast is constant*" (ordinary) would make part (b) readable.

- **The overlap assumption.** It appears in (iv) of both theorems and in @prp-pat-conditional-transport,
  but its *meaning* for population adjustment is never spelled out. I gathered it means "the target
  population's covariates must be within the range seen in the trial," i.e. no extrapolation, but the
  chapter never says that in plain terms. For a health researcher this is the practically scary assumption
  (what if the target population has sicker patients than the trial ever enrolled?) and it deserves a
  sentence or two of motivation, not just a citation to @def-positivity.

- **The reweighting form of @eq-pat-cond-transport (lines 215-219).** This is the bridge to MAIC and it is
  introduced as "the two faces of population adjustment" (lines 235-239), which is a nice framing. But the
  weight $w(x)=f_{\mathcal P^{*}}(x)/f_{\mathcal P}(x)$ is the population *density ratio*, and the chapter
  never reconciles this with the entropy-balancing weights $w_i=\exp(\alpha+\boldsymbol\beta^\top x_i)$
  that MAIC actually uses (which appear in notation.qmd line 140 but not in this chapter). A novice will
  ask "how do I get $f_*/f$ if I do not know the densities?" and the chapter silently defers that to
  Chapter 18. One sentence acknowledging the gap would help.

## Missing motivation / "why does this matter?"

- **Why prove @lem-pat-conditional-additivity (lines 363-381)?** It is "pure algebra" and feels trivial,
  and the chapter says so. But its *purpose* is what makes the whole anchored architecture work: it is why
  subtracting two re-standardized contrasts gives the right answer. That is never said. As a novice I
  wondered why a one-line algebraic identity earns a named lemma and a proof; the answer is "it is the
  conditional analogue of Bucher's additivity and the linchpin of the whole estimand," and that should be
  stated up front.

- **Why does the unanchored case need prognostic variables? (lines 542-622).** The remark at lines
  613-622 says "the price of dropping the anchor" and calls unanchored comparison "a method of last
  resort." This is great. But the *clinical* motivation is thin: when does a health researcher actually
  face an unanchored setup? The phrase "disconnected networks (Chapter 26)" is the only hint. A concrete
  example ("drug A approved on a single-arm study, drug B from a placebo-controlled trial, no common
  comparator") would make this feel real rather than abstract.

- **Why is scale alignment a practical issue and not a pedantic one? (lines 426-429, part (d)).** Part
  (d) mentions hazard model vs restricted mean survival time as the instance. This is the most clinically
  real example in the theorem (oncology HTAs argue about HR vs RMST constantly) and it is mentioned only
  to be deferred to "later chapters." A two-sentence clinical framing here ("a Cox model gives a hazard
  ratio; if the decision maker wants mean survival time in months, balancing on the log-hazard scale does
  not deliver it") would make part (d) land instead of feeling like a footnote to a footnote.

- **Why care about the testability result (@prp-testable-untestable-constancy, lines 771-815)?** The
  remark at 807-815 says the assumptions "must be defended by domain knowledge: pharmacological similarity,
  mechanistic argument, and sensitivity analysis." That is the *whole practical takeaway* of the chapter
  for a health researcher, and it is buried in a remark after a technical proposition. For my perspective
  this is arguably the most important sentence in the chapter and it deserves to be foregrounded, perhaps
  even in the introduction.

## Missing examples and intuition

- **There is exactly one worked example (@exm-pat-anchored, lines 895-991) and it is excellent, but it
  comes at line 895 of 1118.** Everything before it is symbols. A reader like me needs a *small* concrete
  running thread starting near the top: the same three treatments $A,B,C$, the same binary covariate,
  used to instantiate each definition as it is introduced (conditional constancy, absolute constancy, the
  prognostic-vs-EM split, SEMA). The example exists; it is just in the wrong place, or rather there should
  be miniature versions of it interleaved earlier.

- **No concrete drug/trial scenario anywhere in the body.** Treatments are $A,B,C$ throughout. I
  appreciate the abstraction for the theorems, but a single boxed aside giving the example a clinical skin
  ("$A$ = a new oral anticoagulant, $B$ = standard-of-care DOAC, $C$ = warfarin, $X$ = age above 75,
  outcome = major bleed") would help a health researcher anchor the symbols. The worked example at line
  895 is deliberately abstract too; even there a clinical label would help.

- **No diagram of the two architectures.** @sec-pat-architectures (lines 92-112) describes anchored vs
  unanchored in prose. A small network diagram (two nodes joined through a common $C$ vs two disconnected
  components) is the standard way this is taught in HTA courses, and its absence is felt. The book has a
  diagram skill available; this is the canonical place to use it.

- **No intuition for the collapsing/ESS loss in Step 5 (lines 953-969).** The ESS computation is shown but
  the *why* (matching a rarer covariate value forces big weights on few subjects, inflating variance) is
  only hinted at with "balancing one covariate has cost a quarter of the nominal sample." A sentence on
  the mechanics ("we are upweighting the 50 rare $X=1$ subjects to stand in for 100") would make the ESS
  formula feel like something I derived rather than something I verified.

- **No visualization of the collapsibility gap.** Step 6 (lines 971-990) shows the marginal OR (0.796)
  differs from the conditional OR (0.857). That is the entire non-collapsibility story in numbers, and it
  is powerful, but a reader who does not already *feel* why the OR is non-collapsible will just see two
  numbers that disagree. A two-sentence intuition ("the marginal OR averages risks before taking the
  ratio; the conditional OR averages ratios; the logit is nonlinear so these differ") would convert
  surprise into understanding.

## Notation and jargon problems

- **$\tau$ sign and indexing.** The reference-second convention ($\tau^g_{ab}=g(\mu_b)-g(\mu_a)$, so
  $\tau^g_{kC}$ has $C$ second) is used consistently but is genuinely confusing on first encounter: a
  positive $\tau^g_{kC}$ means treatment $k$ is *better* (lowers a worse-is-larger outcome), which is the
  opposite of the naive "$k$ minus $C$" reading. This is flagged once (lines 130-132) and then never
  re-flagged. I mis-signed three computations before it stuck.

- **$m_t(\mathcal P)$ vs $\bar\mu_{t(\mathcal P)}$.** Line 75 notes the marginal mean "is the same
  quantity written $\bar\mu_{t(\mathcal P)}$ in Chapter 14." Two notations for one object across chapters
  is a tax on the reader; even if Chapter 14 used the bar form, this chapter could note "we drop the bar
  for brevity" once and move on, rather than carrying the alias.

- **$\Delta^{\mathrm{Marg},h}$ and $\Delta^{\mathrm{Cond},h}$ superscripts.** The scale superscript ($h$
  or $g$) and the Marg/Cond superscript stack, and in long equations (e.g. line 149-151) I kept losing
  track of which scale a given $\Delta$ was on. Color or a clearer typographic separation (e.g.
  $\Delta^{\mathrm{Cond}}_{h}$) might help; at minimum the convention should be restated when the
  estimand-scales section (lines 138-161) introduces both, because that section is where the overload
  peaks.

- **"Class-wise necessity."** Used at lines 37, 431, and 506 but never given a crisp definition in prose.
  I inferred it means "necessity holds for the class as a whole, not for each member," but the term is
  borrowed from philosophy of science / statistics and should be glossed once.

- **"SPFA" in notation.qmd (line 146) is never used or expanded in this chapter** even though SEMA is
  central. If the shared prognostic factor assumption is the unanchored analogue of SEMA (as the notation
  pairing implies), the chapter that owns the unanchored theorem is the natural place to name it, but it
  is not mentioned. Either it belongs here or the notation entry is premature.

- **"Overlap" / "positivity" used interchangeably.** @def-positivity is cited for the overlap condition,
  but the chapter switches between the words "overlap" (lines 211, 398, 567) and "positivity"
  (notation.qmd line 100, and the cited definition). For a novice these feel like different concepts; the
  equivalence should be stated once.

## Pacing issues

- **The introduction (lines 5-60) is extremely dense.** It packs in: the Bucher recap, the IPD/AgD
  distinction, the three methods (MAIC/STC/ML-NMR), scale specificity, aligned vs not, the "iff is false"
  caveat about non-collapsibility, the two architectures, the four conditions needed for each, SEMA, the
  scale-dependence counterexample, testability, and the g-formula estimands. That is essentially the
  whole chapter's table of contents in 56 lines. As a novice I was overwhelmed before the first
  definition. Splitting the intro into "what problem we are solving" and "a map of the chapter" would
  help; right now they are fused.

- **Five theorems/lemmas in the EM-vs-PV section and anchored section (@sec-pat-em-pv through
  @sec-pat-anchored, lines 284-540) come with no breathing example.** This is ~250 lines of
  definition-lemma-theorem-proof with one tiny witness model and no concrete trial numbers until line
  895. This is the steepest part of the chapter for a beginner and it is exactly where an interleaved
  mini-example would pay off most.

- **The methods preview (@sec-pat-methods-preview, lines 993-1012) comes after the full theory and the
  worked example, which is the right order, but it is only 20 lines.** Given that MAIC, STC, and ML-NMR are
  the *reason* a health researcher reads this chapter, the preview feels disproportionately thin. Three
  bullet points is not enough to connect the abstract estimand to the three concrete procedures; I left
  the chapter unable to say in one sentence how MAIC differs from STC operationally, only that one
  reweights and one regresses.

- **The exercises (lines 1055-1118) are good and well-calibrated** (the starred ones are clearly harder),
  but there is a cliff: the body of the chapter rarely walks through a computation, yet the exercises ask
  for computations on three scales, recomputation under a different target, SEMA identification
  arithmetic, and an unanchored bias proof from first principles. A worked template for at least the first
  of each kind in the body would make the exercises reachable rather than intimidating.

## What worked well

- **The worked example @exm-pat-anchored is genuinely excellent.** Six steps, every number checkable,
  building from conditional risks to the unadjusted bias, the correction, the weighting realization with
  ESS, and finally the scale mismatch. This is the chapter at its best and I learned more from these 100
  lines than from the preceding 800.

- **The "two faces of population adjustment" framing (lines 235-239)** tying the integral form
  (outcome regression = STC) and the reweighting form (weighting = MAIC) to the same identity is a
  beautiful and clarifying move. It gave me a single mental hook for the whole methods part of the book.

- **The machine-checked tags** (lines 310, 333, 534) are reassuring and well-placed; they tell me exactly
  which algebraic core has been verified without cluttering the prose.

- **The closing remark "Which estimand to target" (lines 876-885)** is the clearest single statement of
  the chapter's practical lesson and is written at a level I could follow. "A population-adjusted method
  is consistent for a *named estimand on a named scale*" is the sentence I will remember.

- **The "Where the comparator earns its keep" remark (lines 512-520)** finally made the anchored vs
  unanchored distinction click for me, because it names the mechanism (the comparator term
  $g(\mu_C(x,w))$ cancels in the contrast). If the whole chapter were written at this level of
  mechanism-naming prose, I would have struggled far less.

- **The notes and references (lines 1014-1053)** are thorough and give a clear provenance for each piece
  of the theory, including the explicit acknowledgement that the Coq development deliberately does not
  formalize the scale-specific theorems. This honesty about scope is valuable.

## Suggestions

1. **Open with a plain-English recap of the Bucher failure** (3-4 sentences, no cross-references) before
   the dense intro paragraph. Give the reader the problem before the response to it.

2. **Interleave a stripped-down version of @exm-pat-anchored throughout the chapter.** Introduce the
   three conditional risks and the binary covariate at @sec-pat-setup, then re-instantiate each
   definition (conditional constancy, absolute constancy, EM vs PV, SEMA, testability) on those same
   numbers. Keep the full six-step example at the end as the capstone.

3. **Add a network diagram for the anchored vs unanchored architectures** in @sec-pat-architectures.

4. **Reframe part (c) of @thm-anchored-paic-consistency** from "Non-recovery of a non-collapsible
   marginal effect" to "The method targets the conditional estimand, which differs from the marginal one
   on non-collapsible scales." Same content, much less alarming to a novice.

5. **Add one-sentence plain-English glosses** for "class-wise necessity," "directly collapsible vs
   collapsible," "overlap/positivity," and "prognostic vs effect modifier" at first use, even though each
   is defined in Chapter 11. Part IV readers may be arriving here directly.

6. **Add a clinical skin** (one boxed aside naming $A,B,C,X$ as real drugs and a real covariate and a
   real outcome) so the symbols stop floating in the abstract.

7. **Expand the methods preview** (@sec-pat-methods-preview) from 20 lines to a short section with one
   sentence each on *how* MAIC, STC, and ML-NMR operationally compute the standardized contrast, so the
   reader leaves with a bridge to Chapters 18-20 rather than a cliff.

8. **Foreground the testability remark** (lines 807-815): the practical message "the core assumptions
   cannot be checked from two-study data and must be defended by domain knowledge and sensitivity
   analysis" is the single most important thing a health researcher takes from this chapter, and it
   currently sits in a remark after a technical proof.

9. **State the overlap assumption's practical meaning** ("the target population must not contain
   covariate values the trial never saw; otherwise the reweighting ratio is undefined or extrapolates")
   wherever it is invoked.

10. **Reconcile or flag the $w(x)=f_*/f$ density-ratio weight against the entropy-balancing weight
    $w_i=\exp(\alpha+\boldsymbol\beta^\top x_i)$** used by MAIC. A single sentence acknowledging that the
    density ratio is the theoretical target and entropy balancing is how MAIC estimates it without
    knowing the densities would close the biggest operational gap between this chapter and Chapter 18.