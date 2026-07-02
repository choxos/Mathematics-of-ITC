# Feedback: Chapter 30 — Coq Formalization

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation, never used a proof assistant.
**File:** `chapters/part6/30-coq.qmd`

## Overall impression

I came into this chapter knowing only that "Coq" was some computer-math thing, and I leave it genuinely impressed by the honesty and care of the argument, but also fairly lost in the middle. The chapter is well organized at the section level: it tells me what formalization is, what it does and does not guarantee, what axioms it rests on, what is in the tree, and ends with a worked example and build instructions. That architecture is good. The problem is that almost every paragraph in the middle sections (@sec-coq-structure especially) descends into a wall of Coq-specific jargon and file-by-file enumerations that a noob health researcher cannot parse, and the chapter never stops to say, in plain health-research language, why any of this should change how I trust a MAIC estimate or a Bucher indirect comparison. The worked example (@sec-coq-worked) is the one place where I felt the ground under my feet, and even there the Coq syntax blocks are opaque to me. The documentary framing is clear; the execution is written for someone who already knows Coq, not for me.

## What was unclear

- **"Dependently typed proof assistant built on a constructive type theory, the Calculus of Inductive Constructions" (@sec-coq-guarantees, lines 43 to 44).** I have never seen a type theory, I do not know what "constructive" means here versus "classical" (it gets used later), and "Calculus of Inductive Constructions" is a proper noun with zero unpacking. I need one plain sentence: a type is a category things can belong to, a dependent type is a category that depends on a value, and "inductive constructions" is the way the system lets you define data and propositions by recursion. Right now this reads as a gatekeeping sentence.

- **The Curry-Howard correspondence (lines 44 to 46).** "A mathematical proposition is encoded as a type, a proof of that proposition is a term of that type." I sort of get the slogan, but I cannot picture it. An analogy with something I know would help: if a proposition is like a "question on an exam" and a proof is like "a filled-in answer the grader accepts," or even better, a tiny example like "the proposition `1 + 1 = 2` becomes a type, and the term `eq_refl 2` is the proof." Without one concrete instance the correspondence stays abstract.

- **The kernel (lines 47 to 52).** "The component that performs this type-checking is the kernel, a small program (a few thousand lines)." I get the soundness pitch, but I do not actually know what the kernel *is* in operational terms. Is it a separate executable? A function inside Coq? Does it run after my proof script finishes? The phrase "LCF tradition" (line 51) is dropped with no definition; I had to guess it is a family of proof assistants. A footnote or one clause saying "LCF is the Milner et al. interactive theorem prover whose design introduced this trust-kernel pattern" would fix it.

- **"tactics, automation, notation, and the interactive interface" (line 48).** I do not know what a tactic is at this point in the chapter, and the chapter does not define it until much later (and never cleanly). The first time the word "tactic" appears (line 48) it is used to draw the soundness contrast, but I have no referent. This is a forward reference that should be resolved inline.

- **"mathcomp-analysis" and `boolp` module (lines 54 to 58, 139).** The text tells me the development imports real numbers, measure theory, Lebesgue integration, probability measures, transition kernels. It does not tell me what mathcomp is as a project, why I should trust it, or how widely used it is. "widely used, separately maintained" (line 57) is asserted, not shown. For a reader weighing trust, a one-line pointer to the mathcomp project and its pedigree would help me calibrate.

- **"active axioms" vs "named premises" (@sec-coq-axioms versus @sec-coq-boundary).** This is the single most confusing distinction in the chapter. Lines 132 to 139 tell me there are three axioms inherited from `boolp`. Then @sec-coq-boundary tells me there are named hypotheses like `E_linearity`, `E_total`, `Hipw1`. I had to read the table at line 326 three times to grasp that axioms are logical principles (excluded middle, extensionality, choice) while named hypotheses are *mathematical* probability facts (tower property, Jensen) supplied as premises. The chapter should state this contrast explicitly in one sentence near @def-active-axioms, because a noob will conflate "axiom" with "assumption" and think the whole thing is circular.

- **"Diaconescu's argument" (line 163).** This is name-dropped as the reason excluded middle is a theorem rather than a fourth axiom. I have no idea what the argument is. The Notes section (line 562) repeats the name without explaining it. Either a two-sentence sketch ("from extensionality and choice one can decide any proposition by constructing two singleton sets and choosing the element of the one that holds") or an explicit "see the cited reference" would stop me from feeling the chapter is hand-waving on the one claim I most wanted justified.

- **`Print Assumptions` (line 38, 432 to 433, 498 to 499).** The chapter leans heavily on this command as the certificate. I do not know what it prints or what its output means structurally. The example at lines 435 to 443 shows three lines, but I do not know whether "Axioms:" lists only direct dependencies or the transitive closure, whether it would also list `eq_refl` or other type-theory rules, or whether an empty output is possible. One paragraph on what the command does would make the worked example land.

- **"abstract expectation operator `E : (Omega -> R) -> R`" (lines 191 to 195).** This is the spine of the whole formalization pattern, and it gets one sentence. I do not understand what it means to "machine-check the algebra of estimands without committing to a specific integration theory." Why is that good? What is lost by not committing? What does "abstract" buy us, and where does it eventually get filled in? The payoff only becomes clear much later; at first introduction it reads as a cryptic design choice.

- **"cross-multiplied, division-free form" (@eq-coq-dci, lines 343 to 347) and "zero-mass conditioning events handled by marginal monotonicity" (lines 348 to 350).** I can read the equation $q_{XYZ}(x,y,z)\,q_Z(z) = q_{XZ}(x,z)\,q_{YZ}(y,z)$ but I cannot tell why this form needs no positivity assumption while the continuous one does. The phrase "marginal monotonicity" is undefined. A noob reader needs the connection spelled out: in the cross-multiplied form, both sides are products, so if any factor is zero both sides are zero and the equality holds trivially, whereas in the divided form you would be dividing by zero. That is the entire point and it is not stated.

- **"field convention $r/0 = 0$" (line 255).** This is mentioned in passing as a convention. I have never heard of defining division by zero to return zero; I thought it was undefined. Why is it safe here? Is it a mathcomp choice? Does it affect the truth of the theorems or only the statement? This deserves two sentences, not a parenthetical.

- **"the disintegration compatibility as an explicit hypothesis in the interim" (lines 354 to 355).** I do not know what disintegration is. The word appears once with no gloss. A reader without measure theory cannot follow what is being deferred.

## What wasn't elaborated enough

- **@sec-coq-structure (lines 187 to 316) is a 130-line file-by-file walkthrough that reads like a changelog.** Each file gets a paragraph listing lemma names and short fragments of proof technique (`cond_exp_linear from integralD, integralZl`, line 234). For someone who has never opened Coq, these names and tactic fragments are noise. What I needed instead is a *conceptual* map: three or four paragraphs saying "here is the spine of the formalization, here is what is genuinely proved from nothing, here is what is supplied as a premise, here is what is left to paper." The file names belong in an appendix or a table, not in the main narrative flow. As written, this section is the one most likely to make a health researcher put the book down.

- **The proof-status tiers (@def-coq-proof-status, lines 105 to 130).** The five tiers F, P, S, O, E are defined, but the two-level reading ("tier F as a Coq object, tier P as a formalization of the book theorem," lines 126 to 128) is subtle and only one sentence long. I had to re-read it several times. A tiny table with one row per tier showing a concrete example and the two-level reading would have made this stick. The exercise @exr-coq-status-tier does test this, but the chapter itself should teach it more slowly.

- **The four "what the kernel does not guarantee" gaps (lines 71 to 93).** These are excellent and honest, but each is compressed to a few lines. *Statement faithfulness* (line 75) is the most important one for a health researcher and it gets one paragraph. The placeholder trap (defining an assumption as `True`) is mentioned in passing at line 81 and only fully worked out in exercise @exr-coq-faithfulness at the very end. This idea deserves a worked mini-example in the body, because it is exactly the failure mode a skeptical methodologist should learn to watch for. Right now it is the most load-bearing concept given the least airtime.

- **The named-hypothesis table (lines 326 to 336).** The table lists hypotheses and the catalogue identifiers (A.4, B.7, etc.), but I do not know what the catalogue is, where it lives, or how to read the identifiers. Line 101 mentions "the proof catalogue that accompanies the Coq tree" but never tells me where to find it or what its structure is. A pointer to `theories/` or `proofs/` in ITC_Coq and one sentence on the identifier scheme would close this.

- **The build instructions (@sec-coq-build, lines 470 to 501).** I appreciate the reproducibility, but the `grep -nE "Admitted|^Axiom|admit\." theories/*.v` command (line 494) is shown without explanation of what each pattern means. A noob does not know that `Admitted` is the Coq keyword for a skipped proof, that `Axiom` declares a new assumption, or that `admit.` is the tactic that leaves a hole. Telling me "this returns nothing" is reassuring only if I understand what it would have found.

## Missing motivation / "why does this matter?"

- **The single biggest gap: the chapter never connects formalization to a concrete ITC worry a health researcher actually has.** The introduction (lines 7 to 15) says long algebraic derivations "are exactly the places where a human proof can hide an error." That is good as far as it goes, but it stays at the level of principle. I wanted one sentence like: "When a health technology assessment body reads a MAIC reanalysis, the ESS bound is the number that tells it how much the reweighted evidence has shrunk; this chapter certifies that the bound $\mathrm{ESS} \le n$ is not an approximation or a rule of thumb but a logical consequence of arithmetic, so the HTA can rely on it without re-deriving it." That is the bridge from Coq to HTA, and it is missing.

- **Why formalize at all, as opposed to just being careful?** Line 9 to 10 mentions peer review is fallible, but the chapter never quantifies or illustrates the kind of error it is guarding against. A one-paragraph anecdote (even a hypothetical one) about a population-adjustment identity that was published, used in an HTA, and later found to have a sign error or a missing positivity condition would make the case concretely. Without it, the motivation is abstract.

- **Why should a health researcher care, given they will never compile Coq?** The chapter implicitly addresses this in the last paragraph (lines 542 to 546), but only obliquely. The honest answer is: "you do not need to run Coq; you need to know that someone could, and that the result is therefore not a matter of authorial confidence." That sentence is worth stating directly near the top, because otherwise a noob reads the whole chapter wondering why they are reading it.

- **The cost-benefit of the named-hypothesis boundary.** The chapter is proud of the design (lines 320 to 324) but never tells me the downside: the formalized theorems are weaker than the book theorems because they rest on named premises the machine has not checked. I only pieced this together from the two-level reading. The tradeoff should be stated as a tradeoff: "we gain gap-free algebra; we lose full machine certification of the probabilistic steps, which remain paper-proved."

## Missing examples and intuition

- **No worked Coq interaction anywhere.** The chapter shows Coq *source* (lines 402 to 408, 413 to 415, 420 to 423, 596 to 600) but never shows what the *interaction* looks like: a goal state, a tactic applied, the goal change. For a reader who has never used a proof assistant, the most illuminating thing would be one tiny transcript: a goal `x + 0 = x`, the tactic `intros`, the new goal, `apply Nat.add_0_r`, `Qed`. Without this, "tactic" and "proof script" remain words without a picture.

- **The ESS numeric example (@exm-coq-ess-numeric, lines 451 to 459) is the best pedagogical moment in the chapter.** It is the only place a health researcher can compute along. But it is only one example, and it comes after a very dense formal section. I would want two more like it: one for Bucher's identity (showing the subtraction $d_{AB} = d_{AC} - d_{BC}$ with numbers) and one for the effect-modifier separation counterexample (lines 309 to 316), which is currently described as "$\mu_A(x,w) = \mu_C(x,w) = \mathbf{1}\{w\}$" with no numerical instantiation.

- **No diagram of the trust structure.** The chapter describes a stack: tactics produce a proof term, the kernel checks it, axioms sit underneath, mathcomp-analysis sits to the side, named hypotheses sit as premises. A single figure showing this stack with the trust boundary drawn around the kernel would replace three pages of prose. There is no figure in the chapter at all.

- **No "before and after" illustration of what formalization changes about a theorem.** I wanted to see one book theorem stated in prose, then its Coq counterpart, with the two aligned side by side and the differences (named premises, slightly different scope) annotated. The cross-reference table (lines 365 to 379) does this in tabular form but without the side-by-side statement comparison that would make faithfulness concrete.

## Notation and jargon problems

- **Undefined Coq-specific terms used before any glossary:** tactic (line 48), kernel (line 47), LCF tradition (line 51), inductive (implied by "Inductive Constructions," line 44), Ltac (never defined, though `by_contra` and `classical_case` are called tactics at line 202), proof script (implied throughout, never defined), admit (line 167, 494), Admitted (line 167, 494), Axiom (line 167), Qed (implied by the code blocks), `Print Assumptions` (line 38), `boolp` (line 139), mathcomp (line 54), ssreflect (line 475), Hierarchy Builder (line 476), `.vo` object (line 488), `_CoqProject` (line 189, 473). A short "Coq vocabulary" sidebar near the top would let the rest of the chapter refer to these freely.

- **`E : (Omega -> R) -> R` (line 191) versus the book's $\mathbb{E}$.** The chapter says the abstract operator `E` "plays the role of the expectation $\mathbb{E}$." But `E` is a Coq identifier and $\mathbb{E}$ is the book symbol; the chapter does not clarify that the two are deliberately not the same and that the gap is the point. A noob might think the formalization is just typesetting the book symbol.

- **Notation clash risk: `ESS`.** The notation file (line 139) defines $\mathrm{ESS}$ as the effective sample size, and warns (lines 60 to 62) about the clash with $\mathrm{ESS}_{\mathrm{reg}}$. The chapter uses `ESS` as a Coq definition (line 403) and in prose. This is fine, but the chapter never echoes the notation-file warning, and a reader skipping the front matter could be confused.

- **Catalogue identifiers (A.4, A.5, A.6, B.6, B.7, B.9, F.3, F.8, G.6) appear throughout (lines 326 to 336, 400, 565) with no explanation of the scheme.** Are A, B, F, G proof parts? Where do I find them? Line 101 says "the proof catalogue that accompanies the Coq tree" but no path or structure is given. This is a persistent small frustration.

- **"the field convention $r/0 = 0$" (line 255).** Calling a division-by-zero convention a "field convention" is misleading to someone who knows field axioms, where division by zero is simply undefined. It is really a mathcomp-analysis library convention. Naming it accurately would prevent a confused reader from thinking standard field theory sanctions it.

## Pacing issues

- **The chapter front-loads the abstract guarantees and axioms and defers all intuition to the worked example at @sec-coq-worked.** That is roughly 400 lines of dense material before the first concrete computation. For a noob, the right order would be: tiny motivating example first (even a one-line Coq proof of `1 + 1 = 2`), then the guarantee, then the axioms, then the full structure. As written, by the time I reach the ESS example I have been told about eleven files and a dozen named lemmas, and I have no mental model to slot them into.

- **@sec-coq-structure (lines 187 to 316) is too long and too granular for the main text.** Five phases, fifteen files, dozens of lemma names in 130 lines. This is reference material masquerading as narrative. Splitting it into a shorter conceptual overview in the body and moving the file-by-file detail to an appendix (or to a table with one line per file) would dramatically improve readability without losing content.

- **The jump from @sec-coq-guarantees (the four gaps) to @sec-coq-status (the tier vocabulary) is abrupt.** The four gaps end at line 96 and the tier vocabulary begins at line 98 with no transition tying the tiers to the gaps. In fact the tiers are the chapter's *response* to the completeness gap (gap 4), and that connection is never made. One sentence bridging them would help.

- **The exercises (@sec-coq-exercises, lines 583 to 642) vary wildly in difficulty.** @exr-coq-ess-compute is a plug-in arithmetic exercise; @exr-coq-discrete-vs-named and @exr-coq-faithfulness are starred and ask for genuine conceptual synthesis. There is no middle band. A noob who can do the first will be stonewalled by the last two. One intermediate exercise, such as "write in plain English what `mu1_IPW_unbiased` is saying and which named premise corresponds to which book assumption," would bridge the gap.

## What worked well

- **The honesty of @sec-coq-guarantees (lines 60 to 96).** Stating the four gaps explicitly, especially statement faithfulness and model adequacy, is exactly the right tone for a methods audience that has been trained to distrust black boxes. This is the strongest part of the chapter and should be a model for the rest.

- **The worked example @sec-coq-worked (lines 387 to 468).** Tracing one theorem end to end, showing the Coq statement, the lemma chain, and the `Print Assumptions` output, is the clearest passage. The closing remark at lines 461 to 468 ("the kernel has not certified that ESS is the right diagnostic") is a model of precise scope claim. More of the chapter should be like this.

- **The closing scope accounting @sec-coq-scope (lines 503 to 546).** The explicit list of what is machine-checked, what is modulo named premises, and what is paper-only is exactly what a skeptical reader wants. The two-track framing in the last paragraph (lines 542 to 546) is the clearest statement of the chapter's value proposition and should arguably appear earlier.

- **The reproducibility instructions (@sec-coq-build, lines 470 to 501).** Giving the exact toolchain versions, the `make` command, and the grep check for admits and axioms is commendable. A reader who actually wants to verify can do so without hunting.

- **The cross-reference table @sec-coq-map (lines 365 to 385).** Once I understood the tier vocabulary, this table became my anchor. The "Coq status" column with its honest annotations ("complement F," "paper-only") is exactly the right level of precision.

## Suggestions

1. **Add a "Coq vocabulary" sidebar or short subsection right after @sec-coq-intro** defining, in one line each: proof assistant, kernel, tactic, proof script, term, type, inductive, Ltac, admit, Admitted, Axiom, Qed, `Print Assumptions`, mathcomp, ssreflect. Refer back to it instead of leaving these as unexplained jargon.

2. **Insert a tiny motivating Coq interaction before @sec-coq-guarantees**, e.g. a three-line transcript proving `1 + 1 = 2` showing the goal, the tactic, and `Qed`. This gives every subsequent mention of "tactic" and "proof script" a concrete referent. It costs half a page and pays for itself across the whole chapter.

3. **State the axiom-versus-named-premise distinction explicitly and early**, right after @def-active-axioms: "Axioms are logical principles (excluded middle, extensionality, choice) inherited from the library; named premises are *mathematical* facts (tower property, Jensen) supplied as hypotheses. Conflating the two would make the formalization look circular; keeping them separate is what makes the trust claim honest."

4. **Give Diaconescu's argument two sentences** at line 163, or move it to an appendix with a pointer. Name-dropping it twice without any sketch is the most visible hand-wave in an otherwise precise chapter.

5. **Add one figure showing the trust stack**: tactics on top producing a proof term, the kernel as a trust boundary, axioms and mathcomp-analysis underneath, named premises as side inputs. This replaces several paragraphs of prose that currently ask the reader to hold the structure in their head.

6. **Rewrite @sec-coq-structure as a short conceptual overview (about 30 lines) plus a table** with one row per file: file, role, key result, tier. Move the lemma-name and tactic-fragment detail to an appendix or to the proof catalogue. The main text should be readable by someone who will never compile Coq.

7. **Add one or two more numeric examples** in the style of @exm-coq-ess-numeric, especially for Bucher's subtraction and the effect-modifier separation counterexample (lines 309 to 316), which currently stays symbolic.

8. **Bridge the four gaps (lines 71 to 93) to the tier vocabulary** with one sentence: the tiers are the chapter's structured response to the completeness gap, making explicit how much of each book result the machine certifies.

9. **Explain the `grep` verification command (line 494)** in plain terms: `Admitted` is a skipped proof, `Axiom` is a newly declared assumption, `admit.` is a tactic that leaves a hole; the command returning nothing means none of these appear in the fifteen files.

10. **Add a one-paragraph "why a health researcher should care" near the top**, ideally before @sec-coq-guarantees, stating plainly: you will not run Coq, but you should know that the load-bearing algebra behind the ESS bound, Bucher's identity, and double robustness is not a matter of authorial care but of machine verification, and that the probabilistic premises the machine does not check are explicitly named so you can see exactly where trust is still placed in paper proofs.

11. **Add a pointer to the proof catalogue's location and identifier scheme** (lines 101, 326 to 336): a path within ITC_Coq and one sentence explaining that A, B, F, G are proof parts and the numbers index results within them.

12. **Soften "the field convention $r/0 = 0$" (line 255)** to "the mathcomp-analysis library convention that real division by zero yields zero," and add one clause on why it is safe here (both sides of the cross-multiplied equality are zero when a factor is zero, so the convention only resolves the divided form, not the truth of the theorem).