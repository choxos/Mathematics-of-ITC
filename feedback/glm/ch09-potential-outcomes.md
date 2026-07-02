# Feedback: Chapter 09 — Potential Outcomes

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part2/09-potential-outcomes.qmd`

## Overall impression

I'll be honest: I struggled. This chapter reads like it was written for someone who already took a semester of measure-theoretic probability and a causal inference course, not for a health researcher with basic calculus. The *ideas* are beautiful and I can feel they matter for ITCs, but the chapter buries them under heavy notation, terse proofs, and forward references to theorems I have not met yet. The opening two paragraphs (lines 5 to 37) are genuinely clear and exciting, and the worked example in @sec-po-example saved me. But the middle sections, especially @sec-po-assumptions and @sec-po-identification, lost me repeatedly. I had to keep flipping back to Notation and forward to chapters I have not read. As the *first* chapter of Part II, it is doing too much at once, too fast, with too little hand-holding.

## What was unclear

- **The very first sentence of the chapter body (line 5)** throws me into the deep end. "The statistics of Part I lets us describe a joint distribution of covariates, treatments, and outcomes, and from samples of that distribution it lets us estimate conditional expectations such as $\mathbb{E}[Y\mid T=t,X=x]$ and marginal expectations such as $\mathbb{E}[Y]$." This presupposes I remember Part I in detail. A one-line "recall from Chapter 4/5" pointer would help me know where to go back to.

- **Lines 20 to 22** pile on jargon in a single breath: "Neyman-Rubin potential-outcomes model," "stable-unit-treatment-value assumption," "consistency identity." I know these get defined later, but reading them unpacked in the roadmap with no gloss made my eyes glaze. Could the roadmap give a one-clause gloss for each?

- **@def-potential-outcome (lines 46 to 58)** is the crux and it is *hard*. "Fix a probability space $(\Omega,\mathcal{F},P)$ whose points $\omega\in\Omega$ index the units of a population." As a weak-math reader, $\Omega$ as "a set of patients" is fine, but "the probability space whose points index the units" is backwards to my intuition: I think of patients as the *data*, not as the sample space. One sentence explaining "think of $\omega$ as one patient; the probability space is the formal version of 'draw a patient at random from the population'" would have helped enormously.

- **Line 55**, the formula $Y(t)=t\,Y(1)+(1-t)\,Y(0)$ "as a function of the label." I stared at this. It looks like it is defining $Y(t)$ in terms of $Y(1)$ and $Y(0)$, but $Y(1)$ and $Y(0)$ are the *named* potential outcomes. Is $t$ here a random variable or a fixed label? The line says "label," but then $Y(T)$ in @thm-fundamental-problem uses $T$ which *is* random. The switch from $t$ to $T$ (lowercase vs uppercase) is doing a lot of load-bearing work and is never explicitly called out here. Notation convention 2 (notation.qmd line 12) covers it in general, but a one-line callout at the first use would save me.

- **@thm-fundamental-problem (lines 82 to 117).** The theorem statement is dense: "There exist two pairs of potential outcomes ... and a common assignment $T$, such that the observed data $(T,Y)$ and $(T,Y')$ have the same joint distribution, yet the individual treatment effects differ." I had to read it four times. The proof is actually clearer than the statement. The *statement* could be rewritten in plain English first: "Two different worlds can produce identical observed data but have different causal effects, so no analysis of the observed data alone can recover the effect."

- **@thm-consistency-identity proof (lines 187 to 202)** is fine, but the masked identities @eq-consistency-masked are stated with no intuition. *Why* would I ever want to multiply the consistency identity by $T$? The text after the proof (line 204) says the swap is "the single bridge across which all identification travels," which is great, but I did not understand *why* masking is useful until I read @lem-mean-potential-identification much later. A forward pointer at @eq-consistency-masked saying "these masked forms are what let us isolate the $t=1$ arm alone in the IPW estimator of the next chapter" would have motivated them.

- **@cor-consistency-swap proof (lines 222 to 229)** lost me completely. "Conditional expectation given $(T=t,X)$ is *local* to that event: it is determined by the values of its integrand on $\{T=t\}$, since for any two integrands $f,g$ with $f=g$ on $\{T=t\}$ and any $X$-measurable test set the defining integrals of $\mathbb{E}[f\mid T=t,X]$ and $\mathbb{E}[g\mid T=t,X]$ coincide (both integrate over the sub-event of $\{T=t\}$)." This is the *locality* of conditional expectation and it is asserted, not proved, in a single dense sentence. As a weak-math reader I have no grip on "the defining integrals ... coincide." This is exactly the kind of measure-theoretic fact that, per CLAUDE.md, should be cited to a Part I result, but the citation (@thm-consistency-identity, not a Part I theorem) does not land it. I suspect the real reference is a conditional-expectation locality lemma from Chapter 4; please name it explicitly.

- **@def-ignorability (lines 329 to 342)** presents three forms back to back with no warm-up. "Strong ignorability: $\bigl(Y(0),Y(1)\bigr)\perp T \mid X$, the joint law of the two potential outcomes is conditionally independent of treatment given $X$." I understand the symbol from notation.qmd line 71, but *what does it mean in words for a clinician?* "Given a patient's covariates, knowing which treatment they got tells you nothing about what their outcome would have been under either treatment." That sentence is nowhere. The health-domain gloss is entirely absent in this definition.

- **@lem-ignorability-hierarchy proof (lines 353 to 370)** is the hardest proof in the chapter for me. It invokes "graphoid axiom G1 of @thm-graphoid-axioms" and "the decomposition axiom (G2)." I have not seen graphoids. The proof then does a truncation argument with $f_m(v)=\max(-m,\min(m,v))$ and "conditional dominated convergence." I *think* I follow the idea (approximate the unbounded function by bounded ones and pass to the limit), but "conditional dominated convergence" is stated as a named theorem I have to trust. Where is it in Part I? The truncation step "$f_m(V)\to V$ pointwise with $|f_m(V)|\le|V|\in L^1$" is compact to the point of being a sketch. For a weak-math reader this proof needs two more lines explaining the truncation and naming the dominated convergence reference by its chapter.

- **@def-positivity (lines 384 to 398).** The jump from weak to strict positivity is abrupt. "$P_X$-almost every $x$" appears here for the first time in the chapter without the $P_X$ notation having been introduced in-text (it is implicit in the probability table but never spelled out as "the marginal law of $X$"). I had to infer $P_X$ means "the distribution of $X$." One clause: "where $P_X$ denotes the marginal distribution of the covariates $X$" would fix it.

- **@lem-mean-potential-identification proof (lines 428 to 443).** The "chain of three identities" is the heart of the chapter and it is described in prose at line 415 ("peel off the covariate by the tower property, swap the treatment-assignment conditioning by ignorability, swap the potential outcome for the observed one by consistency") but the *proof itself* does not label which line is which step. I had to map them myself. Numbering or color-coding the three equalities with "(tower), (ignorability), (consistency)" inline would make this centerpiece legible.

- **@sec-po-selection, @thm-naive-selection-bias (lines 504 to 537).** The add-and-subtract trick (line 529) is standard to someone who has seen algebraic identities, but it is presented as if obvious. "Add and subtract the counterfactual control mean among the treated, $\mathbb{E}[Y(0)\mid T=1]$." *Why* that quantity? As a beginner I would never have chosen to add and subtract *that*. One sentence: "we choose $\mathbb{E}[Y(0)\mid T=1]$ because it is the counterfactual that lets us isolate the ATT in the first bracket and confounding in the second" would make the move feel motivated rather than magical.

- **@cor-naive-unbiased-rct (lines 546 to 561).** "marginal ignorability, $\bigl(Y(0),Y(1)\bigr)\perp T$ (no conditioning on $X$), as in a marginally randomized experiment." This is the first time "marginally randomized" appears; is that the same as "simply randomized"? A health researcher knows "RCT" but "marginally randomized experiment" is jargon. Tie it to the concrete trial design.

## What wasn't elaborated enough

- **The connection from single-population identification to multi-study ITC (@sec-po-bridge, lines 661 to 677) is the whole point of the book, and it gets 17 lines.** This is the section I most wanted to read and it is the most compressed. "An indirect treatment comparison is the same logic applied *across* populations" is a claim I want to *see*, not just be told. A tiny diagram (study $AB$ and study $AC$, each identifying its own within-study effect, the $A$ arm as the common anchor) would make the bridge concrete. Right now it is all prose and forward references.

- **The relationship between ATE, ATT, ATC and *when each is the right estimand for an ITC* (lines 256 to 317).** Line 256 says the ATT is "the one most relevant when a regulator asks what a drug did for the patients who took it." Great, one sentence. But for ITCs specifically, which estimand do MAIC, STC, ML-NMR target? This is never said. I finished the chapter not knowing whether the rest of the book chases the ATE or the ATT, and that seems like essential framing for Part II's first chapter.

- **The non-collapsibility aside (lines 286 to 290).** "it should not be confused with the conditional-versus-marginal distinction for nonlinear effect measures developed under collapsibility in @def-non-collapsibility and revisited in @def-collapsibility, where averaging a constant stratum effect need not return that constant." This is a warning about a trap I have not been shown yet, forward-referencing two definitions in the *next* chapter. It is too early. Either cut it or give the one-sentence version (e.g., "on an odds-ratio scale, a constant stratum effect does not average to itself") so I have a hook.

- **The remark at lines 488 to 494** ("The proof used only mean ignorability ... Strong ignorability is the assumption usually *stated*"). This is a genuinely important subtlety and it is tucked into a remark. It deserves a paragraph in the main text explaining *why* we assume the stronger form if the weaker suffices: because randomization delivers strong ignorability for free, and because the balancing-score theory needs it. The remark asserts this but does not explain it.

## Missing motivation / "why does this matter?"

- **Why prove @thm-fundamental-problem at all?** The text says (lines 75 to 80) "The individual effect is exactly what we would like to know and exactly what we can never observe." That is the motivation. But the *theorem* is a non-identifiability result, and its proof constructs two toy worlds. *Why formalize impossibility?* The payoff is stated only implicitly later (line 121: "We cannot recover individual effects, but with the right structural assumptions we can recover *averages*"). I would have loved a sentence right after the proof: "This theorem is the reason the rest of the book targets *population averages*, not individual predictions; it is the logical warrant for every estimand that follows."

- **Why three strengths of ignorability?** @def-ignorability presents strong, weak, mean with no motivation for *why there are three*. The payoff comes only at line 374 ("the identification proof below uses only mean ignorability ... which is the weakest sufficient form"). That is the motivation and it arrives three screens too late. Up front, say: "we distinguish three because the identification proof needs only the weakest, yet randomization gives the strongest for free, and the balancing theory of the next chapter needs the strongest."

- **Why the adjustment formula is called the "g-formula" (line 452).** It is named once and never explained. Robins is mentioned in the notes (line 686) but the *why* of the name is absent. A one-clause gloss ("g" for "generalized"; it generalizes to time-varying treatments) would satisfy the curious.

- **Why positivity has a "strict" version (lines 390 to 394).** The motivation is actually given well at lines 402 to 405 ("strict positivity is what *stable estimation* needs, because estimators that divide by $e(X)$ ... have variance that grows as the propensity approaches $0$ or $1$"). This is good. But it comes *after* the definition and is easy to miss; consider pulling the variance intuition up next to @eq-strict-positivity itself.

- **The ITC-specific "why" is almost entirely deferred to @sec-po-bridge.** Every section between the intro and the bridge is pure single-population causal inference with the ITC motivation reduced to one-line nods (e.g., line 405, line 567). For a book *about* ITCs, I expected the domain hook to appear in each section, not only at the end. Where is the ITC-relevant aside in @sec-po-estimands? In @sec-po-assumptions? They are sparse.

## Missing examples and intuition

- **There is exactly one worked example (@exm-confounding-gformula) and it is excellent**, but it arrives at line 577, after every theorem. I badly wanted a *mini* example right after @def-potential-outcome: "Suppose patient $\omega$ would have HbA1c 7.0 on drug A and 8.5 on drug B; her ITE is 1.5, but we only see one of 7.0 or 8.5." Two lines, huge intuition payoff, sets the tone for the whole chapter.

- **No example for SUTVA failure.** Lines 151 to 153 give one-sentence vignettes (vaccine interference, "surgery" bundling procedures). Good, but too compressed. A two-sentence concrete ITC-relevant example: e.g., in a network of oncology trials, if one center's "chemotherapy" regimen differs in dose from another's, SUTVA-2 is violated and the whole potential-outcomes edifice wobbles. Make the stakes visible.

- **No example illustrating the *three* ignorability forms.** The lemma orders them, but I never see a concrete population where mean holds but weak fails (that is left to @exr-po-mean-vs-weak). Putting a tiny two-by-two table inline showing "equal means, different variances" would make the hierarchy tangible without forcing me to the exercise.

- **No example of positivity failure before @exr-po-positivity-failure.** The formal consequence (variance blow-up, non-identification) is described in prose at lines 402 to 408, but a concrete picture (e.g., "imagine a trial of drug B that enrolled only elderly patients; there is no overlap with a drug C trial of only young patients, so no reweighting can compare them") would make it click. The ITC-overlap story is mentioned in prose at line 405 but never dramatized with a study pair.

- **The selection-bias decomposition @eq-naive-decomposition is illustrated numerically only at the very end.** A small schematic *before* the theorem, e.g., "treated group sicker at baseline, so even with no drug effect the treated would outscore the controls; that gap is selection bias," would prime the reader for the algebra.

## Notation and jargon problems

- **$P_X$-almost every $x$ (lines 388, 394).** $P_X$ is never defined in-text. Notation.qmd does not list it either. Define it on first use: "$P_X$, the marginal law of $X$."

- **$\mathbb{E}_X[\cdot]$ (lines 424, 432, etc.).** This subscript-$X$ expectation notation is used heavily from @lem-mean-potential-identification onward but is never explicitly defined as "expectation over the marginal distribution of $X$." Notation.qmd lists $\mathbb{E}[X]$ and $\mathbb{E}[X\mid Z]$ (line 69) but not $\mathbb{E}_X$. A beginner will read $\mathbb{E}_X[\mathbb{E}[Y\mid T=t,X]]$ and not know which expectation is outer. Add it to notation.qmd and explain on first use.

- **$\mu_t^{\mathrm{obs}}(x)$ vs $\mu_t(x)$ (lines 456 to 457, 591).** The chapter uses $\mu_t(x)=\mathbb{E}[Y(t)\mid X=x]$ (the *potential* mean, unobservable) and $\mu_t^{\mathrm{obs}}(x)=\mathbb{E}[Y\mid T=t,X=x]$ (the *observable* regression). They coincide under ignorability (line 591). The distinction is load-bearing and central to the whole identification argument, but it is introduced in a clause inside @thm-ate-identification (line 456) with no callout box. Consider a named definition for $\mu_t^{\mathrm{obs}}$ so the reader can latch onto it; right now it feels like a notational afterthought.

- **"graphoid axiom G1," "decomposition axiom (G2)" (lines 354, 355).** These come from @thm-graphoid-axioms in Chapter 4, but a reader who is weak on math will not remember them. A parenthetical restatement, e.g., "(G2: if $T$ is independent of a pair, it is independent of each member)" right at the use, would save a cross-chapter lookup.

- **"conditional dominated convergence" (line 366).** Stated as a named result with no reference. Where is it proved? If it is in Part I, cite it inline like the others (@thm-...).

- **"machine-checked" tags** appear on nearly every result (e.g., lines 60, 96, 149, 185, 220, 251, etc.). For a beginner these are noise; they interrupt the reading flow with file/lemma strings I cannot use. The convention is explained in notation.qmd line 23, but in-chapter they are visually heavy. Consider footnotes or a margin format rather than blocking the statement.

- **"functional of the observed-data distribution" (lines 322, 442).** "Functional" here means "a function whose argument is a distribution," a measure-theory term of art. A weak-math reader will read it as "function." One clause on first use: "a functional, i.e., a map from distributions to numbers" would clarify.

## Pacing issues

- **The roadmap (lines 20 to 29) is excellent but the chapter does not breathe.** After the roadmap, we go straight into @def-potential-outcome with its full probability-space formalism. There is no gentle "picture first, formalism second" beat. For a Part II opener I wanted one paragraph of intuition (two worlds, one observed) *before* the $(\Omega,\mathcal{F},P)$ machinery.

- **@sec-po-assumptions is the densest section and it is back to back to back.** SUTVA reduction detail, three ignorability forms, the hierarchy lemma with a truncation proof, positivity with weak and strict, plus the Rosenbaum-Rubin closing paragraph. This is easily 120 lines of unbroken formal content with no example interlude. A worked mini-example between @def-ignorability and @def-positivity, or between the hierarchy lemma and positivity, would give the reader a rest and a concrete anchor.

- **@sec-po-identification is short (lines 412 to 494) but packs the per-arm lemma, the ATE theorem, the remark, and the forward-pointer paragraph into one flow.** The forward pointer (lines 476 to 486) lists G-computation, IPW, AIPW, the balancing score, Rosenbaum-Rubin, all by theorem slug from the next chapter. That is seven forward references in ten lines. It reads like a table of contents dropped into the proof discussion. Consider trimming to the two most important (G-computation, IPW) and saving the rest for the next chapter's intro.

- **The worked example @sec-po-example comes too late.** After five sections of formal theorems, the example at line 577 is a relief, but by then I had already struggled through the identification proof without any numerical grip. Moving a *truncated* version of the example (just the ATE-by-formula and the naive contrast) to right after @thm-ate-identification would let readers verify the theorem immediately, then the full selection-bias decomposition could stay where it is.

- **Exercises (lines 717 to 777) are good but the starred ones (★) point to Appendix F** which, per CLAUDE.md status table, is still TODO. So the reader is sent to a chapter that does not yet exist. Flag this or ensure Appendix F is drafted before this chapter is considered DONE.

## What worked well

- **The opening two paragraphs (lines 5 to 18)** are model clarity. The "patient who received $A$ supplies her outcome under $A$ ... her outcome under $B$ is unobserved, and it is unobservable in principle" framing is exactly the right intuition. More of this voice please.

- **The roadmap paragraph (lines 20 to 29)** tells me what is coming and *why each piece is there*. This is rare and valuable.

- **@exm-confounding-gformula is genuinely excellent.** Walking through ATE, naive contrast, selection bias, and standardization in one population with the numbers $9$ vs $4$ made the whole chapter click. The prose is careful and signposted ("True ATE by the adjustment formula," "The naive contrast," etc.). This is the single best teaching moment in the chapter.

- **The consistency identity and its proof (@thm-consistency-identity, lines 168 to 202)** are the cleanest formal passage: a simple case split, explicit use of $T^2=T$. This is the right level of detail for a weak-math reader.

- **The disambiguation of "consistency" (lines 204 to 206)** is a thoughtful touch that prevents a real confusion.

- **The selection-bias decomposition theorem and its corollary (@thm-naive-selection-bias, @cor-naive-unbiased-rct)** are well motivated: they answer the natural question "why not just compare the arm means?" and connect to RCTs concretely.

- **The bridge section @sec-po-bridge**, though too short, correctly names the four things that carry over (overlap, ignorability, effect scale, transportability) and gives honest forward references.

- **The notes section (@sec-po-notes)** is thorough on attribution and on the Coq mapping, which is consistent with the book's stated design.

## Suggestions

1. **Add an intuition paragraph before @def-potential-outcome** (around line 40): one patient, two possible outcomes, only one observed, in plain English with a clinical example (HbA1c, blood pressure). Save the $(\Omega,\mathcal{F},P)$ formalism for the second beat.

2. **Define $P_X$ and $\mathbb{E}_X$ on first use** and add both to notation.qmd. These are used repeatedly and never defined in-text.

3. **Give $\mu_t^{\mathrm{obs}}(x)$ its own named definition** with a sentence contrasting it with $\mu_t(x)$; this pair is the conceptual hinge of identification and deserves to be visible, not buried in a clause.

4. **Inline-label the three steps of @lem-mean-potential-identification's proof** (tower, ignorability, consistency) so the reader can see the chain as it happens, not reconstruct it from prose.

5. **Move a stripped-down version of @exm-confounding-gformula (ATE and naive contrast only) to right after @thm-ate-identification**; keep the full selection-bias decomposition where it is. Readers need a numerical grip before the selection-bias section, not only after.

6. **Add a concrete ITC mini-diagram in @sec-po-bridge**: study $AB$ and study $AC$ with the $A$ arm as common anchor, each identifying its within-study effect, the transfer governed by overlap and ignorability. A figure would be ideal; even a labeled schematic in prose would help.

7. **Soften the non-collapsibility aside (lines 286 to 290)**: either give the one-sentence version or move it to the next chapter where the definitions live. Right now it forward-references two definitions the reader has not seen and warns about a trap they cannot yet picture.

8. **Expand @sec-po-bridge from 17 lines to a full section** with: (a) which estimand the rest of the book targets (ATE? ATT? both, by method?), (b) the overlap failure picture with a concrete study pair, (c) the transportability link stated as "ignorability + positivity, but *across* populations." This is the chapter's reason for existing in an ITC book and it is the shortest substantive section.

9. **Restate the graphoid axioms G1/G2 inline** at their use in @lem-ignorability-hierarchy, and cite the conditional dominated convergence theorem by its Part I reference.

10. **Add a one-sentence health-domain gloss to @def-ignorability and @def-positivity** immediately after each formal statement. The formalism is correct; the missing piece is the clinician's translation.

11. **State *why* we add and subtract $\mathbb{E}[Y(0)\mid T=1]$** in @thm-naive-selection-bias's proof (line 529): one clause explaining that this choice isolates the ATT in the first bracket and confounding in the second.

12. **Check that Appendix F exists** before relying on it for starred exercise solutions (lines 764, 777); per CLAUDE.md it is TODO, so these pointers currently dangle.

13. **Consider reducing in-chapter machine-checked tag density** (e.g., move to footnotes) so the statement text stays readable for beginners; the convention is valuable but the placement is currently disruptive.