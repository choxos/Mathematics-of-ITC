# Revision log: Chapter 30 — Machine-Checked Foundations: The Coq Formalization

File: `chapters/part6/30-coq.qmd`. Before: 643 lines. After: 1103 lines.

This is a documentary chapter (few new theorem environments by design). Per the chapter-specific
guidance I did NOT fabricate mathematics; all additions make the formalization narrative accessible to a
novice health researcher. No `thm-/lem-/prp-/cor-` environments were invented. New environments are only
`exm-` (illustrations of results already in the chapter) and `exr-` (warm-ups), plus tables and prose.

## Running example introduced (single highest-value addition)

An HTA body compares drugs A and B for relapse via common comparator C. Trial 1 (A vs C, aggregate)
reports log-OR $-0.80$; Trial 2 (B vs C, IPD) reports $-0.50$. Trial 2 is reweighted (MAIC) to Trial 1;
toy $n=4$, weights $(2,1,1,0)$, so $\mathrm{ESS}=8/3\approx2.67$ and patient 4 (weight 0) has no overlap.
Indirect $d_{AB}=d_{AC}-d_{BC}=-0.30$. Reused at every transition: Bucher subtraction (@sec-coq-twin,
@exm-coq-bucher-numeric), ESS bound (@sec-coq-worked, @exm-coq-ess-numeric), MAIC-practice paragraph, and
the double-robustness motivation. The toy weights match the pre-existing ESS example exactly, so the two
are genuinely the same running example.

## Reviewer points addressed

### ChatGPT highest-priority fixes
1. Early health-research motivation for why machine-checking matters for ITC: new `@sec-coq-why` with the
   running example, sign-slip vs vacuous-safeguard, and what Coq cannot check.
2. Plain-language Coq glossary + side-by-side book-to-Coq translation: new `@sec-coq-vocabulary`
   (13-term glossary table + 1+1=2 transcript + trust-stack figure) and `@sec-coq-twin` (Bucher
   book-vs-Coq table with token-by-token gloss).
3. Proof-status tiers clarified: added a tier table and the two-level "what Coq proves / still supplied
   outside Coq / practical reading" template table after `@def-coq-proof-status`, plus a
   confidence-interval analogy.
4. Statement faithfulness with a concrete nontechnical example in the body: new `@exm-coq-vacuous`
   (the `True`-placeholder / assume-the-conclusion trap), moved out of the exercises into the main text.
5. `theories/` walkthrough tied to ITC questions: added a "how to read this section" bridge, a per-file
   table (file / what it protects for ITC / key result / status), and a one-line ITC bridge before each
   of the five phases.
6. More intuition around named hypotheses, active axioms, discrete model: added the
   axiom-vs-named-premise distinction (in `@sec-coq-vocabulary` and after `@def-active-axioms`),
   per-axiom ITC translations, the named-hypothesis cost/benefit tradeoff, and the zero-stratum
   discrete-model explanation + `@exm-coq-zero-stratum`.
7. Scaffolded exercises: star-convention line + difficulty-gradient note; three new accessible exercises
   (`@exr-coq-why-care`, `@exr-coq-vocab-match`, `@exr-coq-ipw-plain`) before the Coq-parsing ones;
   difficulty labels on all exercises.

### GLM suggestions
1. Coq vocabulary sidebar: `@sec-coq-vocabulary` glossary table.
2. Tiny motivating Coq interaction: the `one_plus_one : 1 + 1 = 2` transcript with goal-state comments.
3. Axiom-vs-named-premise distinction stated explicitly and early: done in vocabulary and after the
   axioms definition.
4. Diaconescu's argument given a two-sentence sketch inline.
5. Trust-stack figure: provided as a build-safe ASCII/text fenced diagram (cannot generate a raster
   image; text figure renders under pdflatex verbatim).
6. Rewrite `@sec-coq-structure`: see "deliberately not done" below; addressed via overview + table +
   bridges without deleting the file-by-file detail.
7. More numeric examples: `@exm-coq-bucher-numeric` and `@exm-coq-em-separation` (the effect-modifier
   separation now has numbers).
8. Bridge the four gaps to the tiers: added at the top of `@sec-coq-status` (tiers are the response to
   the completeness gap).
9. Explain the grep command: `Admitted` / `Axiom` / `admit.` glossed in `@sec-coq-build`.
10. "Why a health researcher should care" near the top: `@sec-coq-why` ("you do not need to run Coq...").
11. Proof-catalogue location + identifier scheme: added after the named-hypothesis table (`proofs/`,
    Parts A-O, numbered within Part).
12. Softened "field convention $r/0=0$" to the mathcomp-analysis library convention, with the safety
    clause.

Also handled from the review bodies: mathcomp/ssreflect pedigree (four-color, Feit-Thompson);
`Print Assumptions` semantics (transitive closure, empty possible); abstract-operator `E` vs book
$\mathbb{E}$ bridge; disintegration gloss; LCF gloss; Curry-Howard concrete instance; type-theory plain
sentence; ESS-to-MAIC-practice paragraph (uneven weights -> poor overlap -> variance inflation -> less
stable transport, and the HTA "hard ceiling" reading); build-section novice reassurance; parenthetical
reminders of referenced theorems and a reader guide for the status column in `@sec-coq-map`.

## New labeled environments and tables added

- Sections: `#sec-coq-why`, `#sec-coq-vocabulary`, `#sec-coq-twin` (all confirmed unique across the book).
- Examples: `#exm-coq-bucher-numeric`, `#exm-coq-vacuous`, `#exm-coq-em-separation`, `#exm-coq-zero-stratum`.
- Exercises: `#exr-coq-why-care`, `#exr-coq-vocab-match`, `#exr-coq-ipw-plain`.
- Tables (5 Markdown): Coq vocabulary glossary; Bucher book-vs-Coq side-by-side; tier-definition table;
  two-level "what Coq proves / what remains" table; per-file summary of `theories/`.
- Figures (2 fenced, build-safe): trust-stack ASCII diagram (```text); the 1+1=2 Coq transcript (```coq).

## Deliberately not done, with reason

- GLM #6 asked to MOVE the file-by-file `theories/` detail to an appendix and shorten `@sec-coq-structure`
  to ~30 lines. Not done: the hard constraints forbid deleting content and require preserving every
  `#sec-` label, and this agent may not edit the appendices. Instead the spirit was met by ADDING a
  conceptual overview, a per-file table, a "how to read this section" bridge, and per-phase ITC bridges,
  so a reader who will never open Coq gets the conceptual map first while the detailed inventory (with all
  lemma names) is retained.
- GLM #5 figure delivered as text art rather than a rendered image (no image-generation path; text is
  pdflatex-safe).

## Preservation confirmation

- All original `#sec-` ids preserved: intro, guarantees, status, axioms, structure, foundations, core,
  estimators, methods, bucher, boundary, map, worked, build, scope, notes, exercises.
- All original `#def-` (def-coq-proof-status, def-active-axioms), `#eq-` (eq-coq-dci, eq-coq-ess), the
  original `#exm-coq-ess-numeric`, and all six original `#exr-` ids preserved.
- The cross-reference map (`@sec-coq-map`) preserved verbatim: all 14 book-to-Coq rows intact, including
  every Coq file name, lemma name, and status annotation. No mapping cut.
- No `[machine-checked: ...]` inline tag existed in this chapter to remove; the machine-checked mappings
  live in the `@sec-coq-map` table and are untouched.
- Every existing proof/statement expanded or left intact; nothing shortened or deleted.

## Build safety checks (all pass)

- No em dash, en dash, or double-hyphen connector; American English throughout.
- No Unicode star; `$\star$` used in exercises (existing two preserved).
- No non-ASCII characters anywhere in the file (math or prose).
- No bare `align`/`equation`/`gather` inside `$$...$$` (only the two pre-existing single-line displays).
- All Coq/shell/diagram code in fenced blocks (```coq / ```sh / ```text), never in math mode.
- All new `## {#sec-}` headings preceded by a blank line; environment `## Title` lines correctly follow
  their `:::` opener (verified against the pre-existing pattern).
- No citation change needed (`@phillippo2016tsd` not present; no new bibkeys introduced).

## Counts

- Before/after line count: 643 -> 1103.
- Intuition / plain-language additions: ~10 (glossary table; tier reader-translation; per-axiom ITC
  translations; abstract-operator explanation; type-theory + Curry-Howard + LCF glosses; disintegration
  gloss; field-convention plain rewrite; discrete-model elementary reason).
- "Why this matters" additions: ~11 (value-proposition in `@sec-coq-why`; Bucher-twin why-matters; tier
  practical-reading line; ESS-to-MAIC-practice; EM anchored-vs-unanchored; named-hypothesis
  visibility+tradeoff; map status reader guide; five per-phase ITC bridges).
