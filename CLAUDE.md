# CLAUDE.md — project context for *The Mathematics of Indirect Treatment Comparisons*

This file is the durable context for any future Claude Code session on this repository. Read it first.

## What this project is

A graduate-level **pure-mathematics textbook**:

> **The Mathematics of Indirect Treatment Comparisons**
> *Population Adjustment, Transportability, and Comparative Effect Estimation*
> Sole author: Ahmad Sofi-Mahmudi (git handle `choxos`, `ahmad.pub@gmail.com`).

Goal: take a **naive researcher to mastery**. Start from the very basics (linear algebra, why OLS, the
mathematics behind regression) and build through evidence synthesis to the frontier methods
NMA, MAIC, STC, ML-NMR, ML-UMR, plus the transportability theory that unifies them. **Every result is
proved in full or explicitly marked as cited or assumed.** Definition, lemma, theorem, proof style.

## Confirmed design decisions

1. **Build:** Quarto book; one `.qmd` per chapter; native theorem and proof environments with
   auto-numbering and cross-references; renders to PDF (via LaTeX) and HTML into `docs/`.
2. **Base material:** the author's own repo `ITC_Coq` (see below) is adapted as the base draft for
   Parts II to VI; the new Part I (foundations) is written from scratch.
3. **Rigor scope:** everything from linear regression onward is proved in full. Prerequisite linear
   algebra and real analysis are stated rigorously, with the load-bearing results proved (projection
   theorem, spectral theorem, Cramér-Rao, and so on) and routine results cited to Strang or Rudin.
   Parts II to VI are 100 percent proved.
4. **Formal companion:** major theorems are tagged with their machine-checked status, and a dedicated
   chapter (30) plus appendix (G) explain the Coq formalization.

## Source inventory (verified absolute paths)

Reference texts, under `documentation/refs/` (copyrighted; gitignored; local only):

- `linear_algebra/` — Strang *Introduction to Linear Algebra*; Greub *Linear Algebra*; Bingham and Fry
  *Regression: Linear Models in Statistics*.
- `whatif_book/full_book.md` and `markdown/` — Hernán and Robins *Causal Inference: What If*.
- `nma/...Network-Meta-Analysis-for-Decision-Making.pdf` — Dias, Ades, Welton, Jansen, Sutton.
- `qba/qba_book.pdf` and `markdown/` — Lash, Fox, MacLehose *Quantitative Bias Analysis*, 2nd ed.
- `phillippo_phd_thesis/David_Phillippo_PhD_Thesis.md` — the ML-NMR mathematical backbone.
- `paic/arXiv-2606.20341v1/mlumr.tex` — Chandler and Ishak, ML-UMR ("Anchors Away").
- `paic/arXiv-2602.17041v2/Transportability_PAIC.tex` — Chandler and Ishak, transportability reframing.

Reference software repositories (outside this repo):

- `~/Documents/GitHub/ITC_Coq` — **the spine.** Three layers:
  - `manuscript/` — 16 pedagogical chapters (`00_preface` to `16_coq`, `99_references`).
  - `proofs/` — numbered catalogue, Parts A to O, about 150 results. Key files:
    `00_notation.md` (seed for our `notation.qmd`), `00_concepts_index.md` (the theorem checklist),
    `00_coverage_matrix.md`.
  - `theories/` — machine-checked Coq: `Bucher.v`, `PropensityScore.v`, `MAIC.v`, `STC.v`,
    `DoublyRobust.v`, `EffectModifiers.v`, and others. Build with `make` (zero axioms, zero admits).
- `~/Documents/GitHub/multinma` — ML-NMR reference implementation (Stan per outcome family; vignettes
  `example_plaque_psoriasis`, `example_ndmm`). Workflow: `set_ipd` / `set_agd_arm` / `set_agd_surv` →
  `combine_network` → `add_integration` (Sobol QMC + Gaussian copula) → `nma`.
- `~/Documents/GitHub/mlumr` — ML-UMR reference implementation. Models `mlumr_<family>_{spfa,relaxed}.stan`;
  `naive()` and `stc()` frequentist benchmarks; four outcome-family vignettes.
- `~/Documents/GitHub/itc_courses` — three swirl courses (mlumr-unanchored, transportability, uitc+bias)
  with hand-derivations: entropy-balancing KL proof, sandwich variance, E-values, NORTA copula.
- `~/Documents/GitHub/uitc` — MAIC/STC/doubly-robust/QBA umbrella package (source for Chapters 27, 28).

Note: copies of `multinma` and the example PDFs also exist under `~/Downloads`; the `~/Documents/GitHub`
copies are canonical.

## The ITC_Coq map (chapter to proofs to Coq)

Our chapters map to ITC_Coq proof Parts. Promote each catalogued result to a stated and proved theorem.

| Book chapters | ITC_Coq `proofs/` Parts | ITC_Coq `manuscript/` | Coq `theories/` |
|---|---|---|---|
| 01 to 08 (Part I) | new; draws on A, L | new (not in ITC_Coq) | (foundational) |
| 09 to 12 (Part II) | B, E.1 to E.2, N | 02, 07 | PotentialOutcomes, PropensityScore, IPWEstimator, OutcomeRegression, DoublyRobust |
| 13 to 16 (Part III) | C, D, E.3 | 04, 05 | Bucher, EffectModifiers |
| 17 to 19 (Part IV) | E, F, G | 06, 08, 09 | MAIC, STC, Comparison |
| 20 to 26 (Part V) | H, I, J, M | 10, 11, 13, 14 | (computation, general likelihoods) |
| 27 to 30 (Part VI) | O, K, plus Coq | 12, 15, 16 | all of `theories/` |

The catalogue identifiers (for example `F.3`, `H.10`) are the theorem checklist. Each chapter owns a
disjoint set; see `logs/STYLE.md` for the exact per-chapter assignment.

## Repository layout

See `README.md` for the tree. Key points: front matter is `index.qmd` (preface) and `notation.qmd`
(single source of truth for symbols); chapters live in `chapters/part1` to `part6`; appendices A to G in
`appendices/`; `references.bib` is the shared bibliography; `logs/` holds the authoring contract and the
per-part work logs.

## Conventions (enforced everywhere: prose, comments, commits, UI)

- **American English** spelling (color, behavior, standardize, modeling, summarize).
- **No dash punctuation.** Never use an em dash, en dash, spaced hyphen, or double hyphen as a connector
  or parenthetical. Use a comma, semicolon, colon, or period. Hyphens inside compound words and
  acronyms (Matching-Adjusted, ML-NMR, machine-checked) are fine.
- **Theorem and proof style.** Use Quarto cross-referenceable environments:
  `::: {#thm-slug}` ... `:::` for theorems (also `lem-`, `cor-`, `prp-`, `def-`, `exm-`, `exr-`), and
  `::: {.proof}` ... `:::` for proofs, ending a proof with `$\square$`. Reference with `@thm-slug`,
  `@sec-slug`, `@eq-slug`.
- **Machine-checked tag** format, placed in the theorem statement where applicable:
  `[machine-checked: theories/Bucher.v, Theorem bucher_unbiased]`.
- **Cross-reference to the proofs catalogue** when adapting a result:
  write "(corresponds to F.3 in the proof catalogue)".
- Notation must match `notation.qmd`. Do not introduce a symbol that conflicts with it.

## Build commands

```bash
quarto render            # PDF + HTML into docs/
quarto preview           # live preview
quarto render chapters/part1/06-linear-regression.qmd  # single chapter, fast check
```

## Authoring workflow (multi-agent, in harmony)

- Chapters are drafted by **multiple Opus 4.8 agents at max effort**, coordinated through
  `logs/STYLE.md` (the authoring contract) and `notation.qmd`. Agents run in coordinated waves: Part I
  first (later parts cite it), then Parts II and III, then IV, then V, then VI, then appendices.
- **Every content agent writes a work log** to `logs/part<N>.md` (or `logs/<topic>.md`) recording: every
  reference and section adopted with citations, the catalogue theorem identifiers covered, decisions
  made, and gaps left. The orchestrator maintains `logs/orchestrator.md`.
- The orchestrator owns `_quarto.yml`, `notation.qmd`, `references.bib`, and the final consistency pass
  (cross-references resolve, bibliography deduped, every machine-checked tag points at a real Coq lemma).

## Git policy

- Sole author: choxos / ahmad.pub@gmail.com. **Never** add a `Co-Authored-By: Claude` trailer, a
  "Generated with Claude" line, or any other co-author or attribution.
- Never mention the code-review process, "audit" (except the `npm audit` tool), or "ChatGPT" in commit
  messages, PR titles, PR bodies, or branch names. Describe the change itself.
- Commit or push only when the author asks. The repo currently has no commits; the first commit
  initializes `main`, after which feature work goes on branches. `documentation/refs/` is gitignored
  (copyrighted), as is the rendered `docs/`.

## Chapter status

Legend: TODO (stub only), DRAFT (agent draft written), REVIEWED (consistency pass done), DONE.

| Ch | File | Status |
|---|---|---|
| Preface | `index.qmd` | DRAFT |
| Notation | `notation.qmd` | DRAFT |
| 01 | `chapters/part1/01-linear-algebra-i.qmd` | REVISED |
| 02 | `chapters/part1/02-linear-algebra-ii.qmd` | REVISED |
| 03 | `chapters/part1/03-linear-algebra-iii.qmd` | REVISED |
| 04 | `chapters/part1/04-probability.qmd` | REVISED |
| 05 | `chapters/part1/05-inference.qmd` | REVISED |
| 06 | `chapters/part1/06-linear-regression.qmd` | REVISED |
| 07 | `chapters/part1/07-glm.qmd` | REVISED |
| 08 | `chapters/part1/08-hierarchical-bayes.qmd` | REVISED |
| 09 | `chapters/part2/09-potential-outcomes.qmd` | REVISED |
| 10 | `chapters/part2/10-adjustment-methods.qmd` | REVISED |
| 11 | `chapters/part2/11-effect-modification-collapsibility.qmd` | REVISED |
| 12 | `chapters/part2/12-transportability.qmd` | REVISED |
| 13 | `chapters/part3/13-pairwise-meta-analysis.qmd` | REVISED |
| 14 | `chapters/part3/14-bucher.qmd` | REVISED |
| 15 | `chapters/part3/15-network-meta-analysis.qmd` | REVISED |
| 16 | `chapters/part3/16-limits-of-nma.qmd` | REVISED |
| 17 | `chapters/part4/17-population-adjustment-theory.qmd` | REVISED |
| 18 | `chapters/part4/18-maic.qmd` | REVISED |
| 19 | `chapters/part4/19-stc.qmd` | REVISED |
| 20 | `chapters/part5/20-mlnmr-aggregation.qmd` | REVISED |
| 21 | `chapters/part5/21-mlnmr-discrete.qmd` | REVISED |
| 22 | `chapters/part5/22-mlnmr-integration.qmd` | REVISED |
| 23 | `chapters/part5/23-mlnmr-estimands.qmd` | REVISED |
| 24 | `chapters/part5/24-computation.qmd` | REVISED |
| 25 | `chapters/part5/25-general-likelihoods.qmd` | REVISED |
| 26 | `chapters/part5/26-ml-umr.qmd` | REVISED |
| 27 | `chapters/part6/27-distance-matching.qmd` | REVISED |
| 28 | `chapters/part6/28-qba.qmd` | REVISED |
| 29 | `chapters/part6/29-simulation.qmd` | REVISED |
| 30 | `chapters/part6/30-coq.qmd` | REVISED |
| A,B,C,D,E,G | `appendices/` | REVISED |
| F | `appendices/F-solutions.qmd` | REVISED |

**Build status:** renders to HTML and PDF. PDF is 1111 pages, ~264k words, 399 theorem-type
environments, 400 proofs, 165 definitions, 223 exercises, 99 machine-checked tags. Output in `docs/`.
PDF engine is `pdflatex` (set in `_quarto.yml`); do NOT switch to xela/lualatex, which load unicode-math
and conflict with the book's traditional `\mathbb`, `\mathcal`, and `\boldsymbol` usage.
