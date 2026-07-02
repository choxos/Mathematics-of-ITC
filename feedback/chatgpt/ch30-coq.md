# Chapter 30 Feedback: Machine-Checked Foundations: The Coq Formalization

## Overall reaction

This chapter is valuable because it explains exactly what has been machine-checked, what has not, and what kind of trust Coq adds to the book. I appreciated the honesty about statement faithfulness, model adequacy, truth of hypotheses, and completeness. Those limits are essential for a health researcher, because they prevent the reader from thinking "machine-checked" means "clinically true" or "methodologically appropriate for my data."

For a novice health researcher, though, the chapter often reads more like a formal-methods inventory than a teaching chapter. It gives a very precise map of the Coq development, but it does not always slow down to explain why each formal detail matters for indirect treatment comparisons. I understood the broad message that Coq catches hidden algebraic and logical mistakes, but I had to work hard to connect phrases such as "kernel-level facts," "rectangle factorization," "constructive indefinite description," "abstract expectation operator," and "tier P as a formalization" back to the practical question of whether an ITC method is being used correctly.

The chapter would be stronger for its intended novice audience if it repeatedly translated the formalization claims into the language of health evidence synthesis: what this protects against, what it does not protect against, and how much confidence it should give a researcher comparing treatments across trials.

## What was clear

The opening motivation is clear about why machine-checking is useful. The examples of Bucher's subtraction, ML-NMR aggregation, and scale-specific population-adjustment results make it plausible that small algebraic slips could matter.

The distinction between what the kernel guarantees and what it does not guarantee is one of the strongest parts of the chapter. The four gaps, especially statement faithfulness and model adequacy, are important and are stated candidly.

The proof-status tiers are useful in principle. The chapter makes clear that not every theorem has the same level of formal support, and that a compiled Coq theorem can still be only a partial formalization of a book theorem if a key probability fact is supplied as a named premise.

The active-axioms section is careful and reassuring. It clearly says that the project does not add treatment-effect assumptions as hidden axioms, and that the active axioms are generic foundations for classical mathematics.

The effective sample size worked example is the most accessible part of the chapter. The hand calculation with weights `(1,1,1,1)` and `(2,1,1,0)` helps connect the formal theorem to a quantity a health researcher might already recognize from MAIC.

The final scope section is helpful because it prevents overclaiming. It is clear that the Coq development covers an algebraic and discrete-probabilistic core, not the entire book.

## What was unclear

The practical reason for formalization in ITC needs more explanation. The chapter says Coq checks algebra and discrete probability, but a novice may still ask: "How would this change my confidence in a MAIC, STC, Bucher, or IPW result?" The opening could use a concrete health-technology-assessment scenario where a small sign error, missing assumption, or vacuous theorem would change an interpretation.

"Machine-checked" is defined precisely, but the reader may not understand the difference between checking a proof, checking a statement, checking a model, and checking an analysis. The chapter says the kernel checks that `P` follows from hypotheses, but it would help to state in plain words that Coq does not check whether the trial populations are comparable, whether the model is correctly specified, whether covariates were measured well, or whether the data analysis code was run correctly.

The term "statement faithfulness" is important but still abstract. The placeholder example appears later in an exercise, but the main text would benefit from a simple example much earlier. For instance, show how a theorem could be made formally true but scientifically empty by adding an assumption that already contains the conclusion.

The proof-status tiers are cognitively heavy. The definitions of F, P, S, O, and E are clear individually, but the two-level interpretation is hard: "F as a Coq object but P as a formalization of the book theorem" is likely to confuse a novice. This needs a compact table with one row for "what Coq proved" and one row for "what remains as a mathematical or scientific premise."

The named-hypothesis boundary is under-motivated for nontechnical readers. I eventually understood that named hypotheses make assumptions visible instead of hidden, but the chapter should explain why this is a good thing for health research: it lets the reader see exactly where exchangeability, positivity, tower-property steps, or mean-zero residual assumptions enter.

The discrete-model discussion is too compressed. The cross-multiplied conditional-independence equation is probably correct and elegant, but a novice may not understand why avoiding division helps with zero-mass covariate points, or why that matters for propensity-score balancing. A short numerical example with a zero-count stratum would make this much more teachable.

The cross-reference map is useful but intimidating. Statuses such as "complement F" and "P (weight form and positivity formalized; KKT and duality are paper-only)" require the reader to already know which part of the original theorem carries the clinical or methodological content.

## Under-explained details

Coq itself needs a gentler first explanation. The Curry-Howard correspondence, kernel, type-checking, tactics, proof terms, mathcomp-analysis, and Rocq rename are introduced quickly. A novice health researcher does not need all of that at once. A short analogy would help: a theorem is like a claim with a required checklist of logical steps, tactics help fill the checklist, and the kernel accepts only a complete checklist.

The chapter should say more plainly what "relative to a small and explicit logical foundation" means. A novice may hear "axioms" and worry that the results are assumed rather than proved. The text explains this later, but it could earlier distinguish logical axioms from causal or statistical assumptions.

The "abstract expectation operator" pattern needs a bridge. The chapter says `E : (Omega -> R) -> R` plays the role of expectation and that linearity is supplied as a hypothesis. A novice may wonder whether this is a shortcut that weakens the result. It would help to say that this isolates the algebraic part of the argument from the measure-theory part, so the proof is honest about which part has been checked.

The theorem faithfulness safeguards need more detail. The chapter says the development avoids `True`-valued placeholder definitions and makes modeling hypotheses explicit, but it does not show enough of what the dangerous alternative would look like in the main text.

The active axioms are listed in their kernel form before the reader has much intuition for them. The prose explanations are useful, but each one could use a concrete ITC-adjacent example. For example, functional extensionality could be tied to proving two predicted-outcome functions equal because they give the same value for every covariate profile.

The effective sample size example is accessible, but it could do more work. It shows the arithmetic of the bound, but it only briefly explains why ESS matters for MAIC uncertainty. A novice would benefit from one paragraph connecting uneven weights to poor overlap, less information, larger variance, and less stable population adjustment.

The build instructions are clear for a technical reader but not for a novice. The chapter could explain that most health researchers are not expected to understand every Coq script, but can still inspect the status table, run the build if they have the toolchain, and rely on the absence of `Admitted` and project-specific axioms as part of the assurance story.

## Where a novice may get lost

The file-by-file walkthrough of `theories/` is dense. It names many Coq files, lemmas, tactics, and technical choices in quick succession. A novice reader may lose the main thread: which pieces matter for ITC interpretation, which are infrastructure, and which are formal proof engineering.

The chapter assumes high familiarity with earlier theorem labels. References such as `@thm-ipw-unbiased`, `@def-collapsibility`, `@thm-aggregation`, and `@thm-maic-stc-equivalence` are useful for navigation, but a novice may not remember what each result says. A few parenthetical reminders would reduce friction.

The distinction between algebraic checking and scientific adequacy is easy to forget after the guarantee section. Later sections list many machine-checked results, and the reader may drift back into thinking those results are fully validated methods rather than conditional mathematical results.

The status table may cause overconfidence or underconfidence. A reader might see "F" and think the whole clinical claim is settled, or see "P" and think the theorem is weak. The table needs a short reader guide explaining how to interpret each status in practice.

The phrase "no project-specific axioms and no active admissions" is important, but a novice may not know why this is impressive. The chapter should say that an admitted proof would be a hole the system accepts on trust, whereas this project has no such holes.

The exercises become difficult quickly. The ESS computation exercise is accessible, but the Coq statement reading, `Print Assumptions`, discrete-versus-named premise, and placeholder-trap exercises require substantial comfort with formal notation. They are good exercises, but novices may need hints, worked starts, or labels indicating which are conceptual and which require Coq literacy.

## Suggested improvements

Add a short opening clinical example. For instance, describe an indirect comparison where a Bucher contrast, MAIC ESS bound, or AIPW cancellation is used to support a treatment comparison. Then show what kind of mistake Coq can catch and what kind it cannot catch.

Add a novice-facing glossary box for Coq terms: proof assistant, theorem statement, hypothesis, conclusion, kernel, tactic, axiom, admission, named premise, and statement faithfulness. Keep the definitions informal before giving the formal details.

Add a side-by-side translation of one theorem before the ESS example. Use a small table with "book statement," "Coq statement," "hypotheses," "conclusion," "what is checked," and "what remains scientific judgment." The Bucher theorem or ESS theorem would work well.

Clarify the two-level proof-status idea with one repeated template:

| Result | Coq proves | Still supplied outside Coq | Practical reading |
|---|---|---|---|
| ESS bound | arithmetic inequality | whether ESS is the right diagnostic | strong algebraic check |
| IPW unbiasedness | estimator algebra from named premise | tower-property identification step | conditional check |

Add bridge sentences before the `theories/` walkthrough. The reader should be told how to read that section: not as a list to memorize, but as an inventory of which ITC concepts have machine support.

Reduce or scaffold the most formal prose in the active-axioms and discrete-model sections. The current text is precise, but a novice needs more "why this matters" sentences after each technical claim.

Strengthen the ESS example by connecting it directly to MAIC practice: uneven weights imply poor overlap, smaller effective information, larger variance inflation, and less stable transported estimates.

Make the exercise set more accessible by adding one or two low-barrier conceptual exercises before asking readers to parse Coq statements or predict `Print Assumptions`. The current exercises are useful but steep.

## Highest-priority fixes

1. Add an early health-research motivation that explains why machine-checking matters for ITC decisions, not just for mathematical trust.

2. Add a plain-language Coq glossary and a side-by-side translation of one book theorem into a Coq statement.

3. Clarify the proof-status tiers, especially the idea that a theorem can be fully proved as a Coq object but only partially formalize a book theorem.

4. Expand the explanation of statement faithfulness with a concrete nontechnical example in the main text, not only in the exercises.

5. Rework the `theories/` walkthrough so each file is tied to the ITC question it protects, rather than mainly listing internal Coq objects.

6. Add more intuition around named hypotheses, active axioms, and the discrete-model restriction, with explicit statements of what a novice should and should not conclude.

7. Make the exercises more scaffolded so the first-time reader can build from ESS arithmetic to Coq literacy gradually.
