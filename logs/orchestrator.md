# Orchestrator log

Running log of the book build, maintained by the orchestrating session.

## Session 1 (2026-06-25)

**Goal set by author.** Pure-mathematics textbook *The Mathematics of Indirect Treatment Comparisons*.
Naive to mastery; every result proved or marked cited/assumed. Start from linear algebra and OLS, build
to NMA, MAIC, STC, ML-NMR, ML-UMR, with transportability as the unifying thread. Quarto book, one
`.qmd` per chapter. Chapters drafted by multiple Opus 4.8 max-effort agents in harmony.

**Exploration.** Three Explore agents mapped the sources. Key findings:

- The author's `ITC_Coq` repo is already titled identically and contains a 16-chapter `manuscript/`, a
  numbered proof catalogue `proofs/` (Parts A to O, about 150 results), and a machine-checked Coq
  development `theories/`. It begins at probability and assumes undergraduate linear algebra. The book
  therefore equals ITC_Coq expanded downward (new Part I foundations) and outward (full proofs, worked
  examples, Quarto build, formal companion).
- `multinma` and `mlumr` are the reference implementations of ML-NMR and ML-UMR; `itc_courses` and
  `uitc` carry hand-derivations (entropy-balancing KL proof, sandwich variance, E-values, NORTA).
- Foundations sources: Strang (linear algebra), Bingham and Fry (OLS to GLM), Hernán and Robins
  (causal, transport), Dias et al. (NMA), Lash et al. (QBA), Phillippo thesis (ML-NMR), Chandler and
  Ishak (ML-UMR, transportability).

**Decisions (confirmed with author).** Quarto book; adapt ITC_Coq as base for Parts II to VI; prove
everything from linear regression onward, cite routine LA/analysis; integrate the Coq formal companion.

**Scaffolding done.** Directory tree; `_quarto.yml` (parts, chapters, appendices, theorem crossref,
pdf+html); `.gitignore` (refs and rendered output excluded); `references.bib` seed; `index.qmd`
preface; `notation.qmd` (single source of truth, seeded from ITC_Coq `00_notation.md` and extended with
Part I symbols); 37 chapter and appendix stubs; `README.md`; `CLAUDE.md`; this log; and `logs/STYLE.md`
(the authoring contract with the disjoint per-chapter theorem assignment).

**Next.** Smoke-render the skeleton, then launch the Part I authoring wave (Opus 4.8, max effort).

### Notation additions proposed by agents
(none yet)

### Bibliography additions proposed by agents
(none yet)

### Part I result (8 Opus 4.8 max agents, ~1.04M tokens)
All 8 chapters written, 1000 to 1400 lines each (~63k words total), 68 theorem environments, 154
proofs, all stubs replaced. Clean HTML render after two fixes: added bib keys `billingsley1995` and
`williams1991`; replaced `@sec-notation` (unnumbered, not cross-referenceable) with `[Notation](/notation.qmd)`
in 10 places and patched STYLE.md so later waves avoid it. Spot-checked the Gauss-Markov proof in
Chapter 6: correct A+D decomposition and Loewner-order argument with equality case. Part I status: DRAFT.

### Wave 2 result (Parts II and III, ch 09 to 16)
Hit the session token limit mid-wave (resets 2am America/Toronto). Six chapters were fully written
before the limit (09 to 14; each has theorems, proofs, a worked example, exercises, and notes), but only
ch09 returned its summary and log; ch10 to 14 died after writing the file (no per-chapter log yet).
Ch15 and ch16 remained stubs. Recovery: added 7 missing bib keys used by the causal chapters
(horvitzthompson1952, robins1986, robins1994, bangrobins2005, hahn1998, tsiatis2006, vandervaart1998);
launched a 2-agent fill workflow for ch15 and ch16. Remaining cross-ref warnings point into ch15/ch16
(will resolve once written) plus a few slug mismatches for the consistency pass (@sec-transportability,
@def-reference-treatment-param order).

### Wave 3 result (Part IV, ch 17 to 19)
All three written cleanly (population adjustment theory 1118 lines; MAIC 1401 lines, 10 theorems; STC
1101 lines). Many machine-checked tags into theories/MAIC.v, STC.v. Fixed a recurring citation typo
`@phillippo2016tsd` to `@phillippo2016tsd18`.

### Wave 4 result (Part V, ch 20 to 26)
ch20 to 25 written in the first pass (947 to 1122 lines each); ch26 ML-UMR hit a fresh session limit
(reset 12pm America/Toronto) and was filled by resuming the same workflow (cached agents returned
instantly). ch26 is 1379 lines, 9 theorems. Added bib keys guyot2012 (Kaplan-Meier reconstruction) and
chandler2026survival; fixed the tsd typo in Part V.

### Wave 5 result (Part VI, ch 27 to 30)
All four written cleanly: distance matching 1026 lines; QBA 930 lines; simulation theory 1154 lines;
Coq formalization 643 lines (documentary, 14 machine-checked mappings, no new theorems). No missing bib
keys. Fixed the last cross-chapter ref (@sec-transportability) in ch11 by naming the chapter in prose.
ALL 30 CHAPTERS NOW DRAFTED.

### Wave 6 result (appendices A to G)
A, B, C, D, E, G written; F (solutions) hit the session limit (resets 5pm America/Toronto) and is still a
stub. F is the only outstanding content; it must scan all chapters for starred exercises, so it needs an
agent after reset.

### Consistency pass
- Fixed a stray closing fence in ch13 (orphan `:::` before the Notes section) found by a `:::` balance
  check; this cleared the generic "fenced div" render hint.
- Fixed the last cross-reference, `@sec-coqread-build` in appendix G, by escaping the leading underscore
  in the `_CoqProject` header so Pandoc attaches the section id.
- Machine-checked tags VERIFIED: every `[machine-checked: theories/X.v, ...]` tag points to an existing
  file and an existing lemma. The only flagged names (`DistanceMatching.v`, `conditional_constancy`) are
  honest prose (ch27 says distance matching is not yet formalized; ch30 uses a deliberate bad-practice
  example), not false claims.
- HTML render is clean: zero missing citations, zero unresolved cross-references across 30 chapters and
  6 appendices.
- Optional, deferred (low value, render already clean): fold the by-name prose citations proposed in
  logs/log-appB.md and log-appE.md into references.bib, and the optional notation additions proposed in
  several chapter logs into notation.qmd. None create broken `@keys`.

### Final render
PDF builds successfully with pdflatex: `docs/The-Mathematics-of-Indirect-Treatment-Comparisons.pdf`,
1111 pages, 4.25 MB. LaTeX fixes required: (1) switched pdf-engine off lualatex/xelatex to pdflatex,
because Quarto loads unicode-math under the unicode engines and it conflicts with the book's traditional
`\boldsymbol`, `\mathbb`, `\mathcal` usage (errors `\mitbeta` "Improper alphabetic constant" and
`\__um_group_begin:` "Missing {"); (2) dropped unused `bm` and `bbm` packages; (3) converted the `★`
exercise markers in 24 files to `$\star$` (Latin Modern lacks the glyph); (4) replaced an invalid
`\not\xrightarrow{p}` with `\overset{p}{\nrightarrow}` in ch05; (5) deduped `#sec-poisson` (ch21 to
`#sec-poisson-aggregate`). Math environments scanned clean (agents used `aligned`, never bare `align`).

### Whole-book totals
35,945 lines of .qmd, ~264k words, 399 theorem-type environments, 165 definitions, 400 proofs, 223
exercises, 99 machine-checked tags. 36 of 37 content files complete.

### Remaining
- Appendix F (solutions to starred exercises): still a stub; blocked by the session limit (reset 5pm
  America/Toronto). Resume with a single agent that scans the chapters' starred exercises and solves
  them, then re-render.
- Optional polish: fold by-name prose citations (logs/log-appB.md, log-appE.md) into references.bib and
  optional notation additions from chapter logs into notation.qmd. None block the build.

### Revision pass on Part I (reviewer feedback)
Two reviewers (`feedback/chatgpt/`, `feedback/glm/`) read the book as a novice health researcher. Added
their requirements to STYLE.md as Section 10 (pedagogical accessibility) and Section 11 (pdflatex build
safety). Ran a revision wave: 8 Opus agents rewrote ch01 to 08 to add early concrete examples, intuition
after each definition, "why this matters" lines, jargon definitions, fixed forward references, tables,
the starred-exercise note, and warm-up exercises, while preserving every label and proof. All 8 chapters
grew substantially (for example ch01 1240 to 1748, ch06 1201 to 1789).

Appendix F was deliberately NOT done (author asked to defer it); the workflow was stopped before its
phase. ch07 and ch08 agents were cut off by that stop AFTER writing their revised chapters but BEFORE
writing their logs (so `logs/revise-ch07.md` and `revise-ch08.md` are absent); the chapter content is
complete and renders. ch07 was missing the starred-exercise note, which was patched by hand.

Post-revision consistency: fixed prose-preceded section headings across Part I (a missing blank line
before a heading folds it and drops its `{#sec-}` id; this had broken `@sec-la1-vector-spaces`). After
the fix the HTML render is fully clean (no missing citations, no unresolved cross-references) and the PDF
rebuilds. Part I status: REVISED.

### Appendix F authored
After the author lifted the hold, a single Opus agent wrote Appendix F (solutions to selected
exercises): 2254 lines, 61 solutions, covering all 30 chapters, build-safe (no Unicode star, balanced
fences, no folded headings), no missing citations. The book is now complete: all 30 chapters plus all 7
appendices drafted. Appendix F status: DRAFT.

### Section 1 finished + Section 2 revised
Completed the ch07/ch08 revisions (they had been cut off in the earlier pass; a completion agent filled
the gaps without duplication, and both now have revision logs; ch07 6/4 to 8/10 why/intuition, ch08 1/3
to 6/9). Revised Part II (ch09 to 12) per both reviewers; all grew substantially and carry the intuition,
why-this-matters, jargon, table, and warm-up-exercise additions. All 12 Part I + Part II revision logs
now present (`logs/revise-ch01.md` to `revise-ch12.md`). Build-safe throughout; fixed the recurring
`@phillippo2016tsd` typo again. Parts I and II status: REVISED.

Revision progress: Parts I and II done.

### Section 3 revised (Part III, ch13 to 16)
Revised pairwise MA, Bucher, NMA, and limits of NMA per both reviewers; all 4 logs present; build-safe;
render clean (PDF 5.34 MB, zero cross-ref or LaTeX errors). Part III status: REVISED.

Revision progress: Parts I, II, III done. Remaining feedback to apply: Parts IV to VI (ch17 to 30) and
the appendices.

### Section 4 and Section 5 revised (Part IV, ch17 to 19; Part V, ch20 to 26)
Two parallel waves, 10 Opus 4.8 max agents, one chapter each, addressing both reviewers.

Part IV: ch17 population-adjustment theory 1118 to 1474, ch18 MAIC 1401 to 1927, ch19 STC 1101 to 1469.
Part V: ch20 aggregation 948 to 1261, ch21 discrete 942 to 1278, ch22 integration 1069 to 1564, ch23
estimands 1020 to 1201, ch24 computation 1122 to 1610, ch25 general likelihoods 1080 to 1497, ch26
ML-UMR 1379 to 1786. All additive: every existing label and every proof preserved (each agent verified
its own label and proof inventory), each chapter gained a running clinical example threaded through the
theorems, intuition after each definition, why-this-matters after each major theorem, contrast and
roadmap tables, and warm-up exercises with the starred-exercise note.

All 10 revision logs present (`logs/revise-ch17.md` to `revise-ch26.md`). Combined build-safety scan
clean: no Unicode star, no `\not` on extensible arrows, no bare align/equation/gather, all `:::` fences
balanced, no folded headings, no `@phillippo2016tsd` missing its `18`, no genuinely missing bib key.
Full render exit 0: zero missing citations, zero unresolved cross-references, zero LaTeX errors. PDF
grew to 5.80 MB. Parts IV and V status: REVISED.

Revision progress: Parts I, II, III, IV, V done. Remaining feedback to apply: Part VI (ch27 to 30) and
the appendices.

### Section 6 revised (Part VI, ch27 to 30)
Wave of 4 Opus 4.8 max agents, one chapter each, addressing both reviewers. ch27 distance matching
1026 to 1493, ch28 QBA 930 to 1430, ch29 simulation 1154 to 1533, ch30 Coq 643 to 1103. All additive:
every label, proof, and machine-checked tag preserved; each chapter gained a running clinical example,
intuition after each definition, why-this-matters after each theorem or claim, contrast/roadmap/glossary
tables, and warm-up exercises with the starred-exercise note. ch30 (documentary) added a Coq vocabulary
glossary, a Bucher book-vs-Coq side-by-side, and plain-language accounts of what machine-checked, zero
axioms, and zero admits guarantee, while keeping all 14 book-to-Coq map rows in full.

Two agent judgment calls worth recording: ch28 declined to prove the GLM reviewer's requested corollary
"E_ITC >= E always" because it is false (E_ITC to rho falls below E as RR_UD grows without bound) and
proved the true monotone relationship instead; ch29 renamed the working-model target symbol theta_0 to
theta_work in the misspecification section to remove a clash with the null theta_0 of the power section,
renaming no label.

All 4 revision logs present (`logs/revise-ch27.md` to `revise-ch30.md`). Combined build-safety scan
clean (no Unicode star, no bad arrows, no bare align/equation/gather, balanced `:::` and code fences, no
folded headings, no missing bib key). Full render exit 0: zero missing citations, zero unresolved
cross-references, zero LaTeX errors. PDF grew to 6.00 MB. Part VI status: REVISED.

Revision progress: ALL SIX PARTS (ch01 to 30) revised per both reviewers. Remaining feedback to apply:
the appendices (A to G) only.

### Appendices revised (A to G)
Wave of 7 Opus 4.8 max agents, one appendix each, addressing both reviewers, with kind-specific scope
(reference glossary and distributions and code map get navigability and cross-links rather than a forced
narrative example; the proved appendices get per-identity reader translations and small worked instances;
the solutions file gets clarity and correctness passes; the Coq guide gets a syntax walkthrough). The
author stopped the first launch (`wr7vqqkht`) before any file changed, then asked to continue; the second
launch (`wb1e46e23`) completed all seven.

Line growth: A 366 to 526, B 786 to 1324, C 311 to 616, D 845 to 1087, E 413 to 819, F 2254 to 3258,
G 483 to 1024. All additive: every label, proof, solution, machine-checked tag, and `theories/*.v`
pointer preserved (each agent verified its own inventory).

Four genuine mathematical errors in Appendix F solutions were found and fixed (not merely clarified):
(1) `@exr-graphoid-counterexample` the original construction did not actually break the intersection
axiom, replaced with a correct witness; (2) `@exr-glm-noncollapse` a false "strictly convex" claim (the
function is concave for positive argument) corrected, with concavity reattributed to Jensen; (3)
`@exr-james-stein-sure` "weakly smaller loss pointwise" corrected to risk dominance; (4)
`@exr-qba-norta-margins-star` Gaussian-parameter identification separated from Sklar copula
non-uniqueness and a degenerate correlation case fixed. Appendix A additionally rejected a false reviewer
claim (that the determinant uses a permutation symbol Pi; Chapter 3 uses det(A - lambda I)) and Appendix
E added the missing derivation chain for the adjusted-binomial moments (a clarification, not a
correction).

All 7 revision logs present (`logs/revise-appA.md` to `revise-appG.md`). Combined build-safety scan
clean (the only "folded heading" hits were R comments inside a fenced code block in Appendix E, not
markdown headings). Full render exit 0: zero missing citations, zero unresolved cross-references, zero
LaTeX errors. PDF grew to 6.36 MB.

REVISION COMPLETE: all 30 chapters and all 7 appendices revised per both reviewers. The only status-table
rows still marked DRAFT are the front matter (Preface `index.qmd`, Notation `notation.qmd`), which the
reviewers did not cover.

Deferred polish (non-blocking, noted by agents during the wave): mirror the new Bayesian and computation
symbols catalogued in Appendix A into `notation.qmd`; fold the optional per-chapter notation and
by-name-citation additions from the `logs/log-*.md` files into `notation.qmd` and `references.bib`.

### Open review items
- Notation/bib additions proposed in per-chapter logs `logs/log-ch0*.md` to be folded in during the
  consistency pass.
- Keep Linear Algebra I as Chapter 1: notation and preface must stay unnumbered (agents reference
  chapters by number in prose).
