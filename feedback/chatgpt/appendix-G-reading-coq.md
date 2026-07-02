# Appendix G Feedback: Reading the Coq Proofs
## Overall reaction

Appendix G is valuable because it gives a motivated reader a real path from "machine-checked theorem" to "I can open the file, compile it, and inspect the assumptions." For a health researcher who is new to indirect treatment comparisons and weak in abstract mathematics, the appendix is probably too steep in its current form. It is operationally precise, but it often reads as if the reader is already comfortable with command-line package managers, proof assistant terminology, typed functional programming, and the difference between a theorem's hypotheses and foundational axioms.

The strongest part is the annotated Bucher example. Starting with `Bucher.v` is pedagogically sensible because Bucher's indirect comparison is concrete, central to the book, and less technically loaded than the conditional-independence machinery. The appendix also does a good job making the Chapter 30 claims reproducible through `make`, `grep`, and `Print Assumptions`.

The main weakness is that the appendix does not slow down enough at the exact points where a novice health researcher will need translation: why Coq matters for ITCs, what a Coq statement is saying in ordinary statistical language, what assumptions remain outside the machine, and how to recover when the installation or proof-reading workflow fails.

## What was clear

The opening clearly distinguishes Chapter 30 from Appendix G: Chapter 30 gives the conceptual account, while Appendix G gives the hands-on route for cloning, building, reading, and querying the Coq development. That framing is useful.

The toolchain table is concrete and helpful. Naming Coq or Rocq, mathcomp, mathcomp-analysis, Hierarchy Builder, and the minimum versions gives the reader something checkable rather than a vague instruction to "install Coq."

The `_CoqProject` explanation is one of the clearest technical passages. The sentence explaining that `-R theories ITC` maps `theories/Bucher.v` to `ITC.Bucher` gives the reader a practical key for later `Require Import` commands.

The dependency-order discussion helps a novice choose a first file. The point that `Bucher.v` and `EffectModifiers.v` are placed late for narrative reasons but are lightweight dependencies is useful because it prevents the reader from assuming they must understand every earlier file before starting.

The Bucher walkthrough is the best novice-facing material in the appendix. It translates `Definition transitivity`, `Lemma transitivity_subtract`, `E_linearity`, `E_sub`, and `bucher_unbiased` into mathematical and ITC language. The explanation of `rewrite /transitivity`, `=> H`, `GRing.addrK`, and `by` is exactly the kind of line-by-line bridge a first-time Coq reader needs.

The distinction in "Reading a theorem's premises versus its axioms" is important and mostly clear. It correctly warns that `Print Assumptions` does not show named section hypotheses, which is a common place for a novice to overinterpret the machine's guarantee.

## What was unclear

The appendix assumes too quickly that the reader already understands why they should care about Coq in a health-research setting. The opening says Coq provides a proof assistant guarantee, but it could better connect that guarantee to familiar ITC concerns: hidden transitivity assumptions, fragile algebra in Bucher subtraction, MAIC effective sample size calculations, and model assumptions that are scientific rather than merely algebraic.

The transition from "proof assistant" to "typing shell commands" is abrupt. A novice may not know whether they are expected to become a Coq developer, merely verify that the repository compiles, or learn to read enough Coq to audit a theorem tag. A short "what success looks like" paragraph would help: for example, compile the tree, open `Bucher.v`, identify the hypotheses of `bucher_unbiased`, and run `Print Assumptions`.

The installation instructions are precise but not novice-safe. Terms such as "opam," "switch," "released-packages repository," "transitional alias," and "logical module names" are introduced with little practical context. A health researcher who uses R or Stata more than command-line tools may not know whether `eval $(opam env)` must be run once, in every terminal, or after every switch change.

The Coq to Rocq rename paragraph may confuse the target reader. It is current and useful, but it introduces alternative package names before the reader has a stable mental model. The appendix should tell the novice what command to try first, what error means "use the Rocq package name instead," and whether `coqc`, `rocq`, `coqtop`, and `rocqtop` are interchangeable in this project.

The tables of tactics and notation are useful, but they are dense. A novice may read `R : realType`, `fun omega => e`, `{mfun A >-> B}`, and `R.-pker X ~> Y` as equally important for the Bucher example, even though only some of them matter immediately. The appendix should separate "needed for the first Bucher proof" from "useful later in the larger development."

The phrase "abstract expectation operator" is central but still hard. The appendix says `E` maps `Omega -> R` to `R`, but a novice may not understand why the development chooses this abstraction instead of a normal integral, or what is gained and lost by making linearity a hypothesis. This matters because it is the bridge between statistical expectations and Coq's formal statement.

The connection to Chapter 30 is present through cross-references, but it depends heavily on the reader remembering Chapter 30's vocabulary. Appendix G repeatedly points to proof-status tiers, active axioms, the named-hypothesis boundary, and the theorem map, but it does not give a compact refresher before using those ideas operationally.

## Under-explained details

The appendix should define "compile" in plainer terms before using it as verification. For a novice, it is not obvious that a successful `make` run means Coq has checked every theorem, nor that a `.vo` file is a compiled proof object rather than just a build artifact.

The `grep -nE "Admitted|^Axiom|admit\." theories/*.v` command needs a little more interpretation. The appendix says no output confirms no project axioms and no admitted proofs, but a novice may not know what "no output" looks like, what to do if there is output, or why inherited library axioms are not caught by that search.

The `Print Assumptions` workflow would benefit from a complete scratch-file example. The text says to place a scratch file outside `_CoqProject` and run `coqc -R theories ITC scratch.v`, but it never shows the actual contents of `scratch.v`. A novice would benefit from seeing:

```coq
Require Import ITC.MAIC.
Print Assumptions ESS_upper_bound.
```

The theorem-reading guidance should more explicitly distinguish four things: Coq variables, Coq hypotheses, mathematical assumptions, and foundational axioms. The appendix explains these separately, but a novice may still conflate `E_linearity`, transitivity, unbiasedness premises, and the three `boolp` axioms.

The `Section` mechanism is explained correctly, but it needs a concrete before-and-after example. A novice will not immediately understand "when the section closes, each parameter and hypothesis that a definition or lemma actually used is added to that object's statement." Showing how a hidden-looking section variable becomes an explicit theorem argument would make the point much clearer.

The Bucher theorem explanation should explicitly name the health-research interpretation of `d_AB`, `d_AC`, and `d_BC`: treatment effects for A versus B, A versus C, and B versus C on the book's relative-effect scale. The appendix states they are population relative effects, but the clinical-trial network picture would make the formal symbols less abstract.

The file-by-file reference table is useful as an index, but under-explained as a reading tool. A novice needs a suggested route through it: start with `Bucher.v`, then `MAIC.v` for the ESS bound, then maybe `EffectModifiers.v`, and defer `ConditionalIndep.v` until after Chapter 10 concepts are secure.

Troubleshooting is mostly absent. The appendix should say what to check if `opam install` fails, if `coqc --version` reports an older version, if `make` cannot find `coq_makefile`, if `Require Import ITC.MAIC` fails, or if the reader is on Windows without a Unix-like shell.

## Where a novice may get lost

A novice may get lost before reaching any mathematics because the installation section is long and assumes comfort with opam. The phrase "create an isolated switch" is likely opaque. The reader may not know whether this is like an R library, a Python virtual environment, or a new Coq installation.

The reader may also get lost at the first Coq type signature. `Variable (E : (Omega -> R) -> R)` is concise but alien. For a statistician, it should be translated slowly as "a random variable is represented as a function from possible worlds to numbers, and expectation is a function that takes such a random variable and returns a number."

The tactic table may create the impression that the reader must memorize SSReflect before understanding anything. It would be better to frame the table as a lookup aid and then highlight the five tactics needed for the Bucher example: `rewrite`, `move=>`, `have`, `apply:`, and `by`.

The theorem `bucher_unbiased` is approachable, but the proof's final rewrite may confuse readers because the text says it leaves the goal `d_AC - d_BC = d_AB`, while the hypothesis is written `d_AB = d_AC - d_BC`. Coq's rewrite behavior can handle this, but a novice may wonder why the equality direction works. A short note on rewrite direction, or using `rewrite -H_trans` if that is closer to the displayed goal, would prevent a small but distracting confusion.

The active-axioms section may be misread as saying "the clinical assumptions are only these three axioms." The appendix does warn against this, but the warning should be more prominent near the first `Print Assumptions` example. Health researchers are trained to care about causal assumptions, and they need repeated reminders that the machine verifies algebra conditional on stated modeling premises.

The long file-by-file table at the end may overwhelm rather than orient. It includes many names from Chapters 9 through 19, and a novice who is still learning ITCs may not know which entries are important for understanding Appendix G itself.

## Suggested improvements

Add a short "Reader goal" paragraph after the opening. It should tell the novice that they do not need to become a Coq expert. The realistic goal is to learn how to verify that the development compiles, read the statement of a tagged theorem, identify its assumptions, and understand what `Print Assumptions` does and does not certify.

Add a small clinical-network diagram or verbal setup for the Bucher example before the Coq code: trials compare A with C and B with C, the target is A versus B, and transitivity lets the indirect estimate subtract the two observed contrasts. This would anchor the syntax in a familiar ITC problem.

Insert a "minimal path" box before the full installation details: clone the repository, install the listed packages, run `make`, open `theories/Bucher.v`, run `Check bucher_unbiased`, then run `Print Assumptions bucher_unbiased`. The full opam instructions can remain, but the reader should first see the shape of the journey.

Add troubleshooting bullets after the build section. Include common failures and plain-language fixes: wrong Coq version, missing mathcomp-analysis, shell not using the opam switch, `coq_makefile` not found, module path not found because `-R theories ITC` was omitted, and scratch file accidentally placed in `_CoqProject`.

Reorganize the tactics and notation tables into tiers. First list the tiny subset needed for the Bucher proof. Then list additional notation for later files. This would reduce the cognitive load for a reader who only wants to understand one theorem.

Add a compact refresher from Chapter 30 before `Print Assumptions`: "A theorem has ordinary premises in its statement, and it may also depend on foundational axioms. Coq prints the second kind, not the first." This should be repeated before the example output.

Show the exact contents of a scratch file for `Print Assumptions`, not only the shell command. This is a small addition that would make the workflow much more reproducible.

Turn the file-by-file reference into a guide, not just an index. Add a sentence such as: "If you are reading for ITC intuition, start with `Bucher.v`, then `MAIC.v`, then `STC.v`; leave `ConditionalIndep.v` and `PropensityScore.v` until after Chapters 9 and 10."

Strengthen the Chapter 30 connection by saying explicitly what Appendix G adds: Chapter 30 tells the reader what is machine-checked and why it matters; Appendix G teaches them how to verify that claim on their own machine and how to read one proof script without becoming a formal-methods specialist.

## Highest-priority fixes

1. Add a novice-facing motivation paragraph that connects Coq directly to ITC trust: transitivity, hidden assumptions, algebraic slips, and what the machine can and cannot certify.

2. Add a minimal reproducible workflow with expected success signals: `make` exits cleanly, fifteen `.vo` files are produced, `grep` returns no output, and `Print Assumptions` prints only the three active axioms.

3. Add a complete `scratch.v` example for `Print Assumptions`, plus a note that named modeling premises must be read in the theorem statement because they will not appear in the printed axiom list.

4. Slow down the explanation of `E : (Omega -> R) -> R`, `Hypothesis`, and `Section`, because these are the key bridge from statistical language to Coq syntax.

5. Reduce the first-pass burden of the tactic and notation tables by identifying which entries are needed immediately for the Bucher proof and which can be ignored until later files.

6. Add practical troubleshooting for opam, Coq or Rocq naming, missing libraries, wrong load paths, and failed `make` runs.

7. Add a recommended reading route through the source files so the file reference table does not become a wall of names for someone still learning ITCs.
