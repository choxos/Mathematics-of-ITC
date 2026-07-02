# Feedback: Appendix G — Reading Coq

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation, never used a proof assistant.
**File:** `appendices/G-reading-coq.qmd`

## Overall impression

I have never seen Coq before, and I have never done functional programming or type theory. I came to this appendix because the book keeps promising that theorems are "machine-checked," and I wanted to know what that actually means for me as someone who runs meta-analyses in R. The appendix is clearly written by someone who knows the toolchain cold, and it is precise about commands I can type. But it reads like it is addressed to another computer scientist who just happens not to have seen this particular project yet, not to a health researcher who has never touched a proof assistant. The first half (getting, installing, building) is reassuringly concrete. Then at @sec-coqread-anatomy the floor drops out: a tactic table appears with no explanation of what a tactic *is*, what a goal *is*, what the kernel *is*, or why any of this should matter to indirect treatment comparisons. I finished the appendix able to install Coq and type `make`, but I cannot honestly say I could read a new proof script on my own, and I am still not sure why a health researcher should invest the time to learn.

## What was unclear

- **The word "tactic" is never defined.** @tbl-coqread-tactics (lines 207-226) lists eighteen tactics and constructs, but the table is preceded by no sentence telling me what a tactic *is*. I gather from the rows that a tactic is some kind of instruction that manipulates "the goal," but I had to reverse-engineer that. A reader who has never stepped through a proof has no mental model of a tactic as a command that transforms the current proof state (a stack of goals plus a context of assumptions) into a new state. Without that, every row of the table is a definition of a thing I do not yet understand.

- **"The goal" and "the context" are used as if self-evident.** Line 209: "introduce hypotheses and variables `H`, `x`, `y` from the goal into the context." From the goal into the context? I do not know what either of those is. I assume "context" is the list of things I have already assumed or proved, and "goal" is what I am trying to prove right now, but the appendix never says so. This is the single most important concept for reading a Coq proof and it is treated as background knowledge.

- **The kernel.** Line 128 says `.vo` is "the kernel-checked certificate." Line 200 says `Qed.` "submits the constructed proof term to the kernel." Line 369 says `Print Assumptions` "traverses the kernel proof term." I have now read "kernel" four times and I still do not know what it is. Is it a program? A part of Coq? A database? The whole selling point of a proof assistant is "trust the kernel," so I need a paragraph explaining: the kernel is the small trusted core of Coq that type-checks proof terms; everything else (tactics, libraries) is untrusted machinery that *produces* terms the kernel then checks. Without this, "kernel-checked" is just a magic word.

- **Type checking as the mechanism of proof.** I have heard "Coq checks types" but I do not understand how checking types *is* proving a theorem. The appendix never connects the two. A sentence like "in Coq, a proof of proposition P is a term of type P, so 'finding a proof' and 'finding a term of that type' are the same task" would have made everything click. It is nowhere.

- **`Proof.` ... `Qed.` as a script that builds a term.** Line 198-201 tells me a Lemma is followed by `Proof.`, tactics, and `Qed.`, and that `Qed.` submits "the constructed proof term." But I was never told that the sequence of tactics *constructs* a term. I thought tactics were the proof. The distinction between the proof script (what I write) and the proof term (what the kernel checks) is invisible here, and it is exactly the thing a beginner conflates.

- **Gallina versus Ltac versus SSReflect.** These three words never appear in the appendix as a contrast. Line 178 mentions "the SSReflect proof language, the dialect of Coq tactics." Line 243 references `GRing.addrK` and ring scopes. But I am never told that Coq has (a) Gallina, the term language in which definitions and statements are written, and (b) Ltac / SSReflect, the tactic language in which proofs are scripted. The example at lines 273-279 mixes both: the statement is Gallina, the proof is SSReflect. I needed that split named explicitly so I could stop trying to read `d_AC = d_AB + d_BC` as a tactic.

- **`move=>` and `move:`.** Lines 209-210 define these as introducing and generalizing, but I do not understand the arrow notation. Why `=>`? What is it pointing at? And `move: H` putting something *back* into the goal felt backwards to me; why would I ever undo progress? The table gives the mechanic but not the motivation.

- **`rewrite -E` (the minus sign).** Line 211: "rewrite the goal left to right with equation `E`; `rewrite -E` goes right to left." The minus here is not subtraction, it is a direction flag. This will trip up anyone reading the table casually. It deserves to be flagged as "the leading `-` is an SSReflect direction modifier, not arithmetic negation."

- **`by` as a forcing combinator.** Line 214: "run `tac` ... and fail unless the goal is fully closed." Okay, but why would I want a tactic to *fail*? The pedagogy of `by` (it is a discipline device: you assert this step finishes the goal, and Coq complains if you are wrong) is missing. To a beginner `by` looks like noise.

- **`have -> : a = b`.** Line 219: "prove `a = b` and immediately rewrite the goal with it." I read this three times. I think it means: open a subgoal proving the equation, and when it closes, use it as a rewrite. But the `->` syntax is unexplained; is the arrow the same `=>` family? Is it the rewrite direction? The table packs too much into one line.

- **Section variable discharge.** Lines 183-189 explain that section parameters become explicit arguments when the section closes. I think I understand, but I have no example to anchor it. Show me one `Variable (d_AB : R)` inside a section and then the *same* `d_AB` appearing as an explicit argument of the final theorem after `End.`, side by side. Right now it is a rule without a worked instance.

- **@sec-coqread-deporder import edges.** Lines 160-166 say "`Axioms.v` imports only the mathcomp libraries; `BasicTypes.v` imports `Axioms`; ... `ConditionalIndep` adds `CausalAssumptions`." The verb "imports" / "adds" is used loosely and I cannot tell whether "adds" means "imports in addition to everything before" or "imports exactly that one extra." A beginner reading a dependency graph wants a literal `Require Import` line, not a paraphrase.

## What wasn't elaborated enough

- **@tbl-coqread-tactics.** Eighteen tactics in a table is a reference card, not a tutorial. A beginner cannot learn tactics from a one-line gloss each. At minimum the three or four tactics that recur in the Bucher example (`move=>`, `rewrite`, `by`, `have`) each deserve a paragraph with a tiny goal-state illustration: "before this tactic the goal is X and the context is Y; after, the goal is Z." The appendix gives itself permission to be "precise enough to be typed at a shell" (line 11) but does not extend that precision to the proof-reading half, which is the half I most need.

- **@tbl-coqread-notation.** Several rows need a sentence of unpacking for a non-CS reader. `R : realType` (line 231) says "a formal real-closed field, the real numbers"; but I have spent the book learning that $\mathbb{R}$ is a complete ordered field, and now I am told `realType` is a "real-closed field" with no comment on why Coq uses a *structure* rather than a *set*. `x ^+ n` versus `x *+ n` (lines 233-234) differ by one character and mean very different things; one concrete numeral example for each would prevent silent misreading. `n%:R` (line 235) is "the image of the natural number `n` in the ring `R`"; I needed to be told this is the coercion that lets me write `2` where a ring element is expected. `\sum_(i < n) F i` (line 236) over `'I_n` (line 237): the ordinal-finite-type machinery is name-checked but never explained, and a health researcher has never met ordinals as an index set.

- **The proof of `E_sub` (lines 309-319).** The annotation at lines 322-327 is good but compressed. It says `have -> : ...` "discharges the function equality by `apply: fun_ext => omega`." I now have three new things in one clause: `have ->`, `apply:`, and `fun_ext`, plus functional extensionality as a concept. The annotation should slow down here. What does `apply: fun_ext` do to the goal? What is `fun_ext` (it is named once, at line 325, as "functional extensionality from `Axioms.v`")? Functional extensionality is a deep idea ("two functions are equal if they agree on every input") and it gets one parenthetical. For a reader with no type theory this is a place to spend a paragraph.

- **The proof of `bucher_unbiased` (lines 340-344).** The annotation (lines 353-358) is the best one in the appendix, but it still skips the goal-state snapshot. After `move=> H_AC H_BC H_trans`, *what is the goal*? After `rewrite E_sub H_AC H_BC`, *what is the goal*? The whole point of reading a Coq proof interactively (which the appendix itself recommends at line 425) is watching the goal mutate, yet the prose never shows me the goal at any intermediate step. Annotate with the goal after each tactic, in a fenced block, and the example becomes ten times more useful.

- **`Print Assumptions` output (lines 394-402).** The three axioms are pasted verbatim, which is great, but only `boolp.functional_extensionality_dep` is conceptually unpacked (back at line 325, indirectly). `propositional_extensionality` and `constructive_indefinite_description` get no plain-English gloss here. I am told to "see @sec-coq-axioms" (line 404), but the appendix is supposed to be the hands-on guide; a one-line paraphrase of each axiom next to its formal statement would let me keep reading without a tab switch.

- **The remark at lines 412-419 (premises vs axioms).** This is genuinely important and I am glad it is here, but the two-level reading is stated in one sentence. It deserves a concrete worked contrast: "Here is the *statement* of `mu1_IPW_unbiased` with `Hipw1` visible as an argument; here is the `Print Assumptions` output showing only the three classical axioms. The first tells you what the theorem assumes about the world; the second tells you what it assumes about logic." Without the contrast it is abstract.

## Missing motivation / "why does this matter?"

- **No "why should a health researcher read Coq?" anywhere.** The appendix opens (lines 5-13) by saying it is the "operational counterpart" to Chapter 30, and closes (lines 459-466) by pointing back to Chapter 30. But it never answers the question a health researcher actually has: *I run meta-analyses in R and Stan; why should I spend an afternoon installing opam and stepping through `.v` files?* A short motivating paragraph at the top: what does machine-checking buy *me* that a careful paper proof does not? For ITCs specifically, the value is that assumptions like constancy of relative effects, positivity, and no effect modification on the wrong scale are made *explicit* as hypotheses rather than smuggled into prose; a reader can query exactly which assumptions a result rests on. That is a real benefit for someone doing a health technology assessment, and the appendix should say so up front, not bury it in a remark at lines 412-419.

- **No connection from each Coq artifact back to an ITC decision.** The file-by-file table (@tbl-coqread-files, lines 436-455) maps Coq names to book slugs, which is good, but it never says *what would change in my HTA submission* if, say, `bucher_unbiased` failed to check. The whole point for a health researcher is that the assumptions are auditable; the appendix should periodically remind me what is at stake in the domain. Right now the ITC content feels decorative.

- **Why the abstract-operator pattern matters for ITCs.** Lines 303-307 introduce the "abstract-operator pattern" where `E` is a section variable with only linearity assumed. The text says it "lets the algebra of estimands be machine-checked without committing to an integration theory." That is a computer-science motivation. The ITC motivation is stronger and missing: in population adjustment we constantly manipulate expectations and conditional expectations without needing to specify the measure, and the proofs of unbiasedness for MAIC, STC, and Bucher all hinge on linearity alone. Telling me that would make the abstraction feel like it is serving *my* subject, not avoiding work.

- **Why "zero axioms, zero admits" matters.** Lines 16, 139-143, and 404-410 emphasize the zero-admit, three-classical-axiom status. But I am never told why an "admitted" proof is bad or what an axiom costs. A sentence: "an `Admitted` proof is a hole the kernel lets you leave; it means the theorem is not actually checked. A project axiom is an extra unproved assumption everyone downstream must trust. Fewer of both means more of the result is actually verified." Without that, the inventory reads as a badge rather than a guarantee.

## Missing examples and intuition

- **No "hello world" proof.** The first Coq code I see is the Bucher definitions (lines 193-196). The first proof I see is `transitivity_subtract` (lines 273-279). There is no trivial warm-up, no `Lemma easy : 1 + 1 = 2` stepped through with the goal shown before and after each tactic. A one-paragraph, four-line warm-up would let a beginner build the goal-state mental model before hitting real material.

- **No screenshot or text rendering of a goal state.** Line 425 says "watching the goal change after each tactic is, in practice, the fastest way to understand a script." Agreed. So show me one. A fenced block reproducing what VsCoq shows (the context on top, the goal below, after each line of the Bucher proof) would be worth a thousand words of prose. The appendix never does this.

- **No worked `Print Assumptions` walk for a second theorem.** The appendix runs the command once (for `ESS_upper_bound`, lines 380-402) and then asserts (lines 405-410) that five other theorems return "the identical three-line list." It would cost one fenced block to actually show one of those five, so I can see the sameness rather than take it on faith.

- **No example of *reading a statement* with `Check` or `About`.** Lines 421-426 list `Check`, `About`, `Print`, `Search`, `Locate` as useful commands, but none is demonstrated. A single `About bucher_unbiased.` with its output would teach me how to interrogate a lemma I find in the file-by-file table.

- **No example of a Section discharging a variable.** Mentioned above, repeated because it is the same gap: the Section mechanism (lines 183-189) is the device that makes assumptions visible, and it has no worked before/after example.

- **No intuition for `'I_n` and `\sum_`.** The ordinal-finite-type idiom (lines 236-237) is ubiquitous in mathcomp and completely foreign to a statistician. A sentence: "mathcomp indexes finite sums by a finite type `'I_n` of `n` elements rather than by a range `0..n-1`; this makes the index set a first-class object" would at least name the culture shock.

## Notation and jargon problems

- **"Switch"** (line 56). I do not know opam; "switch" is jargon. One clause: "an opam switch is a self-contained OCaml compiler plus a set of packages" would fix it. The parenthetical on line 56 tries but is too terse.

- **"Logical mapping" / "logical module prefix"** (lines 110-112). I gather `theories/Bucher.v` becomes `ITC.Bucher`, but the word "logical" is doing a lot of work. Say "the name Coq uses to find the compiled file" instead.

- **"Object" / "certificate"** (lines 128-129). `.vo` is called an "object" and a "certificate." Both are CS usage. "Compiled, kernel-checked file" is plainer.

- **"SSReflect"** (line 178). The name is introduced as "the dialect of Coq tactics used by Mathematical Components" but I am never told what the name *means* (small-scale reflection) or why it exists as a dialect at all. A beginner will keep wondering whether they are learning "real Coq" or some variant. One sentence on the history and intent would settle it.

- **"mathcomp-analysis"** and the hierarchy-building stack (lines 39-42). The three libraries are named and their contents listed, but I am not told how they relate to each other or what a "hierarchy" is in this context. The dependency is implicit. A one-line diagram (mathcomp-ssreflect at the base, mathcomp-algebra on top, mathcomp-analysis on top of that, Hierarchy Builder as a generator) would orient me.

- **`GRing.addrK` and friends (line 244).** The table helpfully gives the equations, but I still do not know what the *name* encodes. Is `addrK` "add right cancellation K"? Telling me the naming convention (`addrK` = "add, right, K-lemma" or whatever it actually is) would let me decode new names myself instead of looking each one up.

- **`Prop`, `Type`, `R`, `realType`.** These type-level words appear in statements without a glossary entry distinguishing a proposition (`Prop`) from a type (`Type`) from a structured type (`realType`). The notation table at lines 229-244 mentions `realType` but not `Prop` or `Type`, even though `Definition transitivity : Prop := ...` (line 260) is the first code the reader meets.

- **`fun omega => e`** (line 240). Defined as "an anonymous function (a random variable as a map on the sample space)." Good, but the *syntax* `fun x => e` is lambda notation and a health researcher has never seen it. One sentence: "this is Coq's notation for a lambda, the function that maps `x` to `e`."

## Pacing issues

- **The jump from installation to @sec-coqread-anatomy is too steep.** Lines 84-94 carefully walk through verifying the install and choosing a front end. Then @sec-coqread-anatomy (line 176) immediately dives into `Section`, `Variable`, `Hypothesis`, `Context`, and section discharge, with no transition. I went from `coqc --version` to dependent-type jargon in one page turn. A short "what you will see when you open a `.v` file" bridge: definitions, statements, proof scripts, and the cursor that reveals the goal; then the formal mechanics. The current order is tools-first, concepts-never.

- **The tactic table arrives before the example.** @tbl-coqread-tactics (lines 207-226) is a reference dropped before the only annotated proof (lines 273-344). Pedagogically the example should come first, with tactics introduced as they appear, and the table reserved as a recap. As written, I memorize eighteen one-liners, forget them, and only meet them again twenty lines later.

- **@sec-coqread-deporder is too dense too early.** The phase list (lines 153-158) is fine, but the "actual import edges" paragraph (lines 160-166) is a wall of file names for a reader who has not opened any of them yet. This section could be deferred or shortened; a first-time reader does not need the tight import graph before they have read a single proof.

- **The Bucher example packs four numbered examples back to back** (@exm-coqread-transitivity, @exm-coqread-subtract, @exm-coqread-expectation, @exm-coqread-bucher-thm, lines 254-360). Each is well chosen, but they escalate fast: from a one-line definition to a two-tactic lemma to a proof that uses `have ->`, `fun_ext`, and functional extensionality, to the headline theorem. The middle example (`E_sub`) is the steepest step and gets the least commentary relative to its difficulty. Consider splitting the escalation with a goal-state trace at each step.

- **@sec-coqread-assumptions comes after the example but before the file table.** That is reasonable, but the four "further commands" paragraph (lines 421-426) is bunched at the end of that section and feels orphaned. It might belong in @sec-coqread-anatomy as a "how to interrogate what you are reading" box.

## What worked well

- The install instructions (lines 60-89) are concrete, copy-pasteable, and include a verify step. This is the part I felt I could actually do.

- The choice of `Bucher.v` as the worked example (justified at lines 168-174) is excellent: it genuinely depends only on Phase 1, and the math (transitivity and subtractive form) is something I already understand from Chapter 14. Anchoring the Coq tutorial in the simplest ITC theorem is exactly right.

- @tbl-coqread-files (lines 436-455) is a genuinely useful reference. Mapping every Coq name to a book slug means I can navigate from a theorem I care about to the file that checks it. This is the table I will return to.

- The remark on the Coq-to-Rocq rename (lines 76-82) is considerate; a reader following along in 2025-2026 will hit exactly this confusion and the appendix pre-empts it.

- The grep one-liner for "no admits, no project axioms" (line 142) is a lovely piece of operational reproducibility. It turns a claim into a command I can run myself.

- The two-level reading remark (lines 412-419), though under-elaborated, names a real and subtle distinction that I had not seen stated anywhere else in the book.

- The prose is clean, the cross-references are consistent, and the notation matches `notation.qmd` (the `E` / $\mathbb{E}$ bridge at lines 12-13 is correctly flagged).

## Suggestions

1. **Add a "Why read Coq as a health researcher" paragraph at the top**, before @sec-coqread-get. State the domain payoff: assumptions become auditable, results carry a reproducible certificate, and the set of hypotheses a theorem needs is machine-queryable. Tie it to HTA practice.

2. **Insert a short "What is Coq / what is a proof assistant / what is the kernel" primer** between installation and @sec-coqread-anatomy. Cover: terms and types, propositions as types, proofs as terms, the kernel as the small trusted checker, the proof script as a recipe for building a term, and the goal-state model (context + goal stack). One page. This is the missing foundation for everything after it.

3. **Reorder @sec-coqread-anatomy so the example comes first.** Open with a tiny warm-up proof (even `Lemma easy : 1 + 1 = 2`), show the goal before and after each tactic, introduce `move=>`, `rewrite`, `by` in context, *then* give the tactic table as a reference recap.

4. **Annotate the Bucher proofs with goal-state snapshots.** After each tactic line, show a fenced block with the current context and goal. This is the single change that would most help a beginner, and it matches the appendix's own advice at line 425.

5. **Name and separate Gallina vs Ltac vs SSReflect** explicitly, early. A short table: "Gallina = the term language (statements, definitions); Ltac = the built-in tactic language; SSReflect = the mathcomp dialect of Ltac (what this project uses)." Flag that statements are Gallina and scripts are SSReflect.

6. **Expand the three `Print Assumptions` axioms in place** with a one-line plain-English gloss each, so a reader does not have to jump to @sec-coq-axioms to understand the output they just produced.

7. **Add a worked Section discharge example**: one `Variable (d_AB : R)` inside a `Section`, then the post-`End` theorem signature showing `d_AB` as an explicit argument. This is the mechanism that makes ITC assumptions visible, and it deserves a concrete instance.

8. **Add a "hello world" `Print Assumptions` on a second theorem** (one of the five claimed identical at lines 405-410), so the reader sees the sameness rather than trusting the prose.

9. **Gloss every piece of CS jargon on first use**: switch, logical mapping, object, certificate, SSReflect, hierarchy, ordinal finite type, lambda (`fun x => e`), `Prop`, `Type`. One clause each is enough; none is currently given.

10. **Add a closing "where to go next" paragraph** for the health researcher: once you can read `Bucher.v`, try `EffectModifiers.v` (same dependencies, more ITC-central), then `MAIC.v` (first file that uses the abstract `E` and `Var` together). The appendix ends at line 483 by pointing back to Chapter 30; it should also point forward into the tree in increasing difficulty order.