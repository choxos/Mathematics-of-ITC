# Revision log: Appendix G, Reading the Coq Proofs

File: `appendices/G-reading-coq.qmd`. Kind: narrative (hands-on companion to Chapter 30).
Before: 483 lines. After: 1024 lines.

## Source verification done first

Read the actual repository to keep every new snippet faithful (not invented):
- `~/Documents/GitHub/ITC_Coq/theories/Bucher.v` in full (section structure, exact tactics, goal
  evolution for `transitivity_subtract`, `E_sub`, `bucher_unbiased`).
- `~/Documents/GitHub/ITC_Coq/theories/Axioms.v` head (confirmed `fun_ext`, classical axioms, the
  beginner-facing comments).
- Extracted the exact `Require Import` line(s) from all fifteen `theories/*.v` to build the new literal
  dependency table (some files carry two import lines; the prose in the appendix matches them).

## Reviewer points addressed (both files, highest-priority first)

ChatGPT highest-priority fixes:
1. Novice motivation tying Coq to ITC trust: new `#sec-coqread-why` (auditable assumptions, algebra that
   cannot be fudged, reproducible certificate; explicit "what the machine does NOT certify").
2. Minimal reproducible workflow with success signals: new `#sec-coqread-minimal` (six commands, "what
   success looks like": clean `make`, fifteen `.vo`, empty `grep`, three axioms).
3. Complete `scratch.v` shown for `Print Assumptions` (I added the file contents, not just the shell
   command); refresher remark and concrete contrast state that named premises live in the statement, not
   in the axiom list.
4. Slowed down `E : (Omega -> R) -> R`, `Hypothesis`, `forall`, and `Section`: expanded the expectation
   example's type reading; added a worked `Section` discharge before/after in `#sec-coqread-anatomy`.
5. Tiered both reference tables: added a "First pass?" column to `#tbl-coqread-tactics` and
   `#tbl-coqread-notation` marking the Bucher-only rows; lead-in names the five tactic families.
6. Troubleshooting: new `#sec-coqread-trouble` (opam version resolution, wrong Coq version, switch not
   active/`eval $(opam env)`, `coq_makefile` missing, module-not-found load path, scratch file in
   `_CoqProject`, Windows/WSL).
7. Recommended reading route: added a route paragraph after `#tbl-coqread-files` and a "Where to go next"
   close in the notes.

GLM highest-priority/suggestions:
- New conceptual primer `#sec-coqread-primer`: terms/types, propositions-as-types, the kernel as the
  small trusted checker, proof script vs proof term, goal/context proof-state model, and Gallina vs
  Ltac vs SSReflect named explicitly. Includes a hello-world `warmup` proof with goal-state snapshots
  after every tactic.
- Vocabulary table `#tbl-coqread-vocab` glossing term, type, `Prop`, `bool`, `Type`, proof term,
  kernel, tactic, goal, context, hypothesis, Gallina, Ltac/SSReflect, `Definition`,
  `Lemma`/`Theorem`, `Proof.`/`Qed.`/`Admitted.`, `Axiom`, `forall`, `exists`, `fun x => e` (lambda).
- Goal-state traces added to `transitivity_subtract`, `E_sub`, and `bucher_unbiased`.
- Three `Print Assumptions` axioms glossed in place via new `#tbl-coqread-axioms`.
- Second worked `Print Assumptions` on `bucher_unbiased` shown in full (was only asserted identical).
- Section discharge worked before/after example added.
- Concrete premises-vs-axioms contrast on `bucher_unbiased` added inside the existing remark.
- Demonstrated `Check bucher_unbiased` with output.
- Jargon glossed on first use: switch (with R/Python analogy), logical name, `.vo` as compiled
  kernel-checked file, SSReflect = small-scale reflection, the mathcomp library stack + "hierarchy",
  ordinal finite type `'I_n`, lambda, `Prop`/`Type`, `addrK` naming convention, `x ^+ n` vs `x *+ n`
  with numeral examples, `n%:R` coercion.
- Clinical-network setup + `#tbl-coqread-bucher-symbols` mapping `d_AC`/`d_BC`/`d_AB`/hats/`E` to the
  two-trial picture.
- Coq-to-Rocq remark expanded with "try `coqc` first, else `rocq`/`rocqtop`; interchangeable here."
- Build section now defines "compile", "kernel" (forward-ref to the primer), and interprets the `grep`
  output (what "no output" means, why library axioms are not caught, why admits/axioms matter).
- ITC motivation for the abstract-operator pattern added (population adjustment manipulates expectations
  without a fixed measure; Bucher/MAIC/STC unbiasedness hinge on linearity alone).

## Reviewer-flagged math point fixed/clarified

- GLM "rewrite direction" confusion on the last step of `bucher_unbiased`: added an explicit note that
  `rewrite H_trans` uses `H_trans : d_AB = d_AC - d_BC` left to right (pattern `d_AB` -> replacement
  `d_AC - d_BC`), so the goal `d_AC - d_BC = d_AB` becomes `d_AC - d_BC = d_AC - d_BC` and closes by
  reflexivity; `rewrite -H_trans` would go the other way (leading `-` is the SSReflect direction flag,
  not subtraction). No existing identity was wrong; this is a clarification of a correct proof. All
  goal-state traces were checked against `Bucher.v`.

## Skipped / deliberately not done

- No Exercises section exists in this appendix, so per the task scope I added NO `$\star$` convention
  line and NO new exercises.
- Did not move the `Check`/`About`/`Print`/`Search`/`Locate` paragraph out of `#sec-coqread-assumptions`
  (GLM suggested relocating to anatomy); moving risked churn, so instead I demonstrated `Check` there in
  place. Kept all section ordering to avoid disturbing cross-references.
- Left the existing `mu1_IPW_unbiased`/`Hipw1` sentence intact (not verified line-by-line against
  `IPWEstimator.v`); added the concrete contrast using `bucher_unbiased`, whose statement and axioms I
  did verify.

## New labeled environments / tables added (all unique, none renamed)

- Sections: `#sec-coqread-why`, `#sec-coqread-minimal`, `#sec-coqread-trouble`, `#sec-coqread-primer`.
- Tables: `#tbl-coqread-imports`, `#tbl-coqread-vocab`, `#tbl-coqread-bucher-symbols`,
  `#tbl-coqread-axioms`.
- One new `::: {.remark}` (the "two kinds of assumption" refresher) ending in `$\blacktriangleleft$`.

## Preservation confirmed

- All 14 pre-existing IDs kept and unique: `#sec-coqread-{get,install,build,deporder,anatomy,bucher,
  assumptions,files,notes}`, `#tbl-coqread-{toolchain,tactics,notation,files}`, and the four
  `#exm-coqread-{transitivity,subtract,expectation,bucher-thm}` example divs.
- All `theories/*.v` file pointers preserved; `#tbl-coqread-files` rows untouched (only a route
  paragraph appended after its caption). No cross-references removed or renamed.
- The single literal `[machine-checked: ...]` mention (prose, in the files section) preserved. The
  appendix has no self-tags, consistent with its notes.

## Build safety verified

- Zero non-ASCII characters in the file (checked with a Python scan): no em/en dash, no Unicode star,
  no Unicode arrows or minus. All dash-looking hits are math or Coq-code subtraction.
- All code (sh/coq/text) in fenced blocks (76 fence markers, balanced); no code in math mode.
- No bare `align`/`equation`/`gather` inside `$$`; all added math is inline `$...$` with ASCII commands.
- 7 fenced divs open/close balanced; every `#sec-` id unique across the file.
- The only headings without a preceding blank line are the four pre-existing example-div titles
  (`## The theorem` etc. inside `::: {#exm-...}`), which are original and already build in the PDF.
- No `@phillippo2016tsd` without `18` present (0 matches); no new `@bibkey` citations introduced.
