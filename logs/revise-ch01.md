# Revision log: Chapter 01, Linear Algebra I

Revised `chapters/part1/01-linear-algebra-i.qmd` for pedagogical accessibility per the two reviewer
files (`feedback/chatgpt/ch01-linear-algebra-i.md`, `feedback/glm/ch01-linear-algebra-i.md`) and
STYLE.md Sections 10 and 11. All mathematics, theorems, and proofs preserved; only scaffolding added.
File grew from 1241 to 1748 lines.

## Highest-priority fixes (both reviewers) addressed

1. **Early running example, reused throughout.** Added new section `#sec-la1-preview` ("A running
   example: a two-arm trial") immediately after the intro: a patient-level data table, the concrete
   4x2 design matrix with numeric fitted values, the three organizing questions (column space / rank /
   null space) each pointing to the section that makes it precise, the over-parameterized 4x3 design,
   and a notation-role table. The example is reused at transitions in the span, linear-map, four-
   subspaces, systems, identifiability, and design-example sections.
2. **Intuition after every definition.** Added a plain-language "What this means" / "Reader translation"
   paragraph after def-vector-space (plus an 8-row axiom-intuition table), def-subspace,
   lem-subspace-criterion (stated as a labor-saving device), def-span, def-linear-independence,
   def-basis, def-dimension, def-linear-map, def-kernel-image (with the null-space = non-identifiability
   reading and the image = column space identification), def-rank, def-column-space, def-invertible.
3. **"Why this matters" after major theorems.** Added one-line ITC/regression payoffs after
   thm-steinitz-exchange, thm-matrix-mult-composition, thm-rank-nullity (strengthened with residual
   df and the collinear-covariate-steals-a-df point), thm-row-rank-column-rank, thm-four-subspaces,
   prp-rank-equals-pivots, thm-invertibility-characterization, and lem-injective-trivial-kernel.
4. **Four-subspaces table.** Added after thm-four-subspaces, with columns subspace / symbol / lives in
   (outcome space vs coefficient space) / dimension / trial reading, plus a sentence on the orthogonal
   pairings. Directly separates coefficient space from outcome space as both reviewers asked.
5. **Worked elimination example.** Added `#exm-la1-elimination` before prp-rank-equals-pivots: a 3x3
   matrix taken to row-echelon and reduced row-echelon form by hand, reading off rank, the free
   variable and null-space basis, the pivot-column basis of the column space, and the row-space basis.
   In-line definitions of pivot, row-echelon form, reduced row-echelon form, and pivot column added.
6. **Identifiability promoted from remark to subsection.** Added `### Identifiability as a null-space
   condition` (`#sec-la1-identifiability`) inside sec-la1-systems, containing the (relocated) original
   remark plus `#exm-la1-nonidentifiability`, which shows the explicit pair beta = (0,1,0) and
   beta' = (1,0,-1) producing identical fitted values (0,0,1,1), and that the contrast beta_1 - beta_2
   is the estimable functional orthogonal to the null space.

## Other reviewer points addressed

- **Forward reference C(A), N(A) before def-column-space (both reviewers):** the rank-nullity section
  now introduces the symbols C(A) = im T_A and N(A) = ker T_A at first use (legitimate, since im/ker are
  already defined), with a pointer that the row space and left null space are assembled later in
  def-column-space. No symbol is now used before definition.
- **Jargon defined or signposted:** "morphism" glossed in-line as structure-preserving map;
  affine subspace and coset defined in a reader-translation paragraph after prp-system-solvability;
  internal direct sum and the symbol `\oplus` defined in the four-subspaces remark with a "not needed
  until Chapter 2" signpost; pivot / row-echelon / reduced row-echelon / pivot column defined in-line
  in sec-la1-row-ops; 1_n and 0_n introduced in-text in the preview; "nonsingular" kept but the text
  now commits to "invertible" throughout to remove ambiguity. Orthogonal complement glossed in-line.
- **Expanded confusing proofs (no shortening):** lem-vector-space-basics(1) now spells out the
  0 = 0 + 0' = 0' chain term by term and names which zero is which; lem-dependence explains why the
  *largest* index is chosen; thm-steinitz-exchange explains why the mid-proof reindexing is harmless
  and is followed by `#exm-la1-steinitz-micro`, a numeric m=2, n=3 replacement walk-through;
  thm-row-rank-column-rank names the rank factorization as it is built and justifies "r columns =>
  dimension <= r" via lem-reduction-to-basis.
- **Orthogonality step extracted (glm):** the load-bearing "orthogonal to a spanning set" move is now a
  named lemma `#lem-orthogonality-linear-combinations`, cited in the thm-four-subspaces proof rather
  than left as a parenthetical.
- **Invertibility roadmap (both):** before thm-invertibility-characterization, added a grouping table
  (inverse / rank / solution conditions) and an implication-route table listing which arrow the proof
  establishes and its role.
- **Concrete companion examples (glm):** `#exm-la1-span-dependence` (two vectors spanning a plane in
  R^3, a dependent third in the plane, an independent third off it) after def-linear-independence,
  described verbally in lieu of a figure (see "figures" note below).
- **exm-other-spaces** kept; added a sentence explaining the function-space view is what ML-NMR
  integration uses, with a "not needed yet" signpost, rather than dropping it.
- **"Why prove anything / why abstract" (glm, whole-chapter point):** two paragraphs added to the intro
  ("Why prove anything at all?" and a how-to-read note), and a motivating sentence opening
  sec-la1-vector-spaces tying the abstraction to regression, NMA, and ML-NMR.
- **Exercises (both):** added a one-line note that starred exercises ($\star$) have full solutions in
  Appendix F and explaining the warm-up / interpretation / computation / proof / starred-challenge
  tags. Added three accessible exercises first (`#exr-la1-warmup-fitted`, `#exr-la1-warmup-redundant`,
  `#exr-la1-interpret-estimable`); existing exercises reordered after them and given flavor tags in
  their titles. The collinearity remark in sec-la1-design-example now also states the explicit
  non-identifiable coefficient pair with a cross-reference to exm-la1-nonidentifiability.

## New labels added (none removed or renamed)

- Sections: `#sec-la1-preview`, `#sec-la1-identifiability`.
- Examples: `#exm-la1-span-dependence`, `#exm-la1-steinitz-micro`, `#exm-la1-elimination`,
  `#exm-la1-nonidentifiability`.
- Lemma: `#lem-orthogonality-linear-combinations`.
- Exercises: `#exr-la1-warmup-fitted`, `#exr-la1-warmup-redundant`, `#exr-la1-interpret-estimable`.

All slugs were checked for uniqueness across the whole book before use. Every pre-existing label (14
sections, 11 defs, 6 eqs, 4 examples, 12 lemmas, 6 theorems, 2 corollaries, 3 propositions, 10
exercises) is still present; verified by label inventory after editing.

## Deliberately not changed

- **No figures added.** Reviewers requested figures (a span/plane picture; a two-beta picture). The book
  contains no figures, TikZ, or code cells anywhere (verified by grep across `chapters/`), and STYLE.md
  Section 11 stresses pdflatex build safety. To stay consistent with house style and not risk the
  build, the geometric intuition is delivered through concrete numeric examples (exm-la1-span-dependence,
  exm-la1-nonidentifiability) and the four-subspaces and notation-role tables instead. Flagged here for
  the orchestrator in case figures are wanted book-wide later.
- **No new bibliography keys.** Only `@strang2016` is cited, as before; no new sources were needed.
- **No machine-checked tags.** Chapter still has no ITC_Coq counterpart.
- **All proofs kept verbatim and full**, including the long invertibility proof and the Steinitz
  induction; additions are commentary, examples, tables, and signposts only.
- Did not touch `_quarto.yml`, `notation.qmd`, `references.bib`, or any other chapter.

## Build-safety verification performed

- ASCII-only in math; star rendered as `$\star$` (no Unicode star); no `\not` on extensible arrows; no
  bare align/equation/gather inside `$$`; `[Notation](/notation.qmd)` link used (no @sec-notation).
- Zero non-ASCII characters in the file; zero dash-punctuation connectors; American English throughout.
- 86 opening div fences match 86 closing fences; 24 proofs each end in `\square`; 8 examples/remarks end
  in `\blacktriangleleft`; all six added Markdown tables have consistent column counts and header rows.
- `pandoc --from markdown --to native` parses the file without error.

## Notation note for the orchestrator

The chapter uses the symbol `\oplus` (internal direct sum), defined in-line in the four-subspaces
remark. It is not currently in `notation.qmd`. Consider adding a row to the linear-algebra notation
table: `$U \oplus W$ | internal (direct) sum of subspaces`. Chapter 2 also uses it. No action taken in
notation.qmd per file-discipline rules.
