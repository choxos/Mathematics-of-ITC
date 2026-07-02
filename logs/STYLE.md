# Authoring contract (read this before writing any chapter)

Every content agent must read this file and `notation.qmd` before drafting. The purpose of this
contract is harmony: parallel chapters must read as one book, share one notation, and cross-reference
each other without collision. Follow it exactly.

## 1. Mathematical voice and structure

This is a pure-mathematics text. The reader is intelligent but starts naive; lead with motivation, then
make everything precise. Each chapter follows this skeleton:

1. A short motivating introduction (what problem this chapter solves and why it matters for indirect
   comparison).
2. Definitions, then lemmas, then theorems, in dependency order. State every hypothesis explicitly.
3. A proof for every lemma, theorem, corollary, and proposition, unless the result is a cited
   prerequisite (see rule 6). End each proof with `$\square$`.
4. At least one fully worked numerical example per chapter, with concrete inputs and outputs the reader
   can verify by hand or with a calculator.
5. A short "Notes and references" section attributing the material (bibtex keys from `references.bib`)
   and pointing to the proof catalogue and any machine-checked counterpart.
6. A set of exercises at the end (mix of computation and proof). Solutions to starred exercises go in
   Appendix F.

Depth target: these are substantial chapters. Prove things in full. Prefer a complete elementary proof
to a slick one that cites machinery the reader does not yet have.

## 2. Quarto theorem and proof grammar

Use cross-referenceable divs. The label prefix sets the environment type.

```markdown
::: {#thm-gauss-markov}
## Gauss-Markov
Under the linear model with $\mathbb{E}[\boldsymbol\varepsilon]=\mathbf 0$ and
$\mathrm{Cov}(\boldsymbol\varepsilon)=\sigma^2 I$, the OLS estimator $\hat{\boldsymbol\beta}$ is the
best linear unbiased estimator of $\boldsymbol\beta$.
:::

::: {.proof}
Let $\tilde{\boldsymbol\beta}=C\mathbf y$ be any linear unbiased estimator ... $\square$
:::
```

Prefixes: `thm-` theorem, `lem-` lemma, `cor-` corollary, `prp-` proposition, `def-` definition,
`exm-` example, `exr-` exercise. Proofs use `::: {.proof}` (not cross-referenced). Remarks use
`::: {.remark}`. Reference results with `@thm-gauss-markov`, sections with `@sec-...`, equations with
`@eq-...`. Give display equations you will reference a label: `$$ ... $$ {#eq-normal-equations}`.

Slugs are globally unique. Namespace them by topic, not by chapter number, so they survive renumbering:
`@thm-bucher-unbiased`, `@def-effect-modifier`, `@thm-maic-ess-bound`. Never reuse a slug.

## 3. Notation

`notation.qmd` is the single source of truth. Use those symbols and no conflicting ones. If a chapter
genuinely needs a new symbol, choose one consistent with the existing scheme (bold lowercase vectors,
bold uppercase matrices) and add it to your work log so the orchestrator can fold it into
`notation.qmd`.

To point the reader at the notation chapter, write a plain link `[Notation](/notation.qmd)`. Do NOT use
`@sec-notation`: the notation chapter is unnumbered and is not cross-referenceable, so a `@sec-`
reference to it renders as `??`. The same holds for the preface. Reuse symbols silently; you do not need
to cite the notation chapter every time you use a symbol from it.

## 4. Machine-checked tags

When a result has a counterpart in the `ITC_Coq` Coq development, add a tag inside the theorem div,
immediately under the statement:

```markdown
[machine-checked: `theories/Bucher.v`, `Theorem bucher_unbiased`]
```

Only tag results you have confirmed exist in `~/Documents/GitHub/ITC_Coq/theories/`. If unsure, write
the pen-and-paper proof and note the candidate in your log; the orchestrator verifies tags in the
consistency pass.

## 5. Citing sources

Cite with bibtex keys present in `references.bib` (for example `@phillippo2020mlnmr`,
`@hernan2020whatif`, `@strang2016`). If you rely on a source not yet in `references.bib`, add the entry
to your work log with full bibliographic data; the orchestrator merges it. When you adapt a result from
the proof catalogue, add the parenthetical "(corresponds to F.3 in the proof catalogue)".

## 6. What to prove versus cite

- From Chapter 6 (linear regression) onward: prove everything in full.
- Chapters 1 to 5 foundations: state every result precisely; prove the load-bearing ones (orthogonal
  projection theorem, spectral theorem, properties of the multivariate normal, MLE consistency and
  asymptotic normality, Cramér-Rao). Cite Strang (`@strang2016`) or a standard analysis text for
  routine facts (existence of bases, basic limit theorems) rather than reproving them.
- Never assert a result without either a proof or an explicit citation. No silent claims.

## 7. Writing rules

- American English spelling throughout.
- No dash punctuation as a connector or parenthetical: no em dash, en dash, spaced hyphen, or double
  hyphen. Use comma, semicolon, colon, or period. Hyphens inside compound words and acronyms are fine.
- Define every nonstandard term on first use. Expand every acronym on first use, then use the acronym.

## 8. File discipline

- Write only the `.qmd` file(s) assigned to you. Do not edit `_quarto.yml`, `notation.qmd`,
  `references.bib`, or another agent's chapter; record needed changes in your log instead.
- Overwrite the stub at your assigned path with the full chapter (keep the YAML `title`; drop the stub
  callout).
- Write a work log at `logs/part<N>.md` (append if multiple agents share a part, with a clear heading).
  The log records: references and sections consulted (with citations), catalogue theorem identifiers
  covered, new notation or bib entries proposed, decisions, and any gaps left for review.

## 9. Per-chapter theorem assignment (disjoint; from the proof catalogue)

Each chapter owns the catalogue results below. Owning a result means stating and proving it (or marking
it cited per rule 6). Do not duplicate another chapter's results; cross-reference them instead.

| Ch | Topic | Catalogue identifiers | Primary sources |
|---|---|---|---|
| 01 | Linear algebra: spaces, maps, rank | new (rank-nullity, four subspaces) | `@strang2016` |
| 02 | Orthogonality, projection theorem | new (projection theorem, Gram-Schmidt) | `@strang2016` |
| 03 | Spectral theory, quadratic forms, SVD | new (spectral theorem, SVD, PD forms) | `@strang2016` |
| 04 | Probability and distributions | A.1 to A.10 | `@hernan2020whatif`, standard |
| 05 | Statistical inference | A.11 to A.13, plus MLE, Fisher, Cramér-Rao | `@bingham2010regression` |
| 06 | Linear regression from first principles | new (OLS, Gauss-Markov, normal theory) | `@bingham2010regression`, `@strang2016` |
| 07 | Generalized linear models | new (exponential family, IRLS, deviance) | `@mccullagh1989glm`, `@dias2018nma` |
| 08 | Hierarchical and Bayesian | L.1 to L.5, plus random effects, REML | `@dias2018nma` |
| 09 | Potential outcomes and identification | B.1 to B.5 | `@hernan2020whatif` |
| 10 | Adjustment methods | B.6 to B.12 | `@hernan2020whatif`, `@rosenbaum1983` |
| 11 | Effect modification and collapsibility | B.13, E.1, E.2 | `@hernan2020whatif`, `@chandler2026transport` |
| 12 | Transportability | N.1 to N.12 | `@chandler2026transport` |
| 13 | Pairwise meta-analysis | C.1 to C.9 | `@dias2018nma`, `@dersimonian1986` |
| 14 | Bucher indirect comparison | D.1 to D.4 | `@bucher1997` |
| 15 | Network meta-analysis | D.5 to D.14 | `@dias2018nma` |
| 16 | Limits of standard NMA | E.3 | `@phillippo2020mlnmr` |
| 17 | Population adjustment theory | E.4 to E.12 | `@phillippo2019thesis`, `@phillippo2016tsd18` |
| 18 | MAIC | F.1 to F.12 | `@signorovitch2010maic`, `@phillippo2019thesis` |
| 19 | STC | G.1 to G.7 | `@caro2010stc`, `@phillippo2019thesis` |
| 20 | ML-NMR aggregation | H.1 to H.7 | `@phillippo2020mlnmr` |
| 21 | ML-NMR discrete and approximation | H.8 to H.11 | `@phillippo2020mlnmr`, `@lecam1960` |
| 22 | ML-NMR numerical integration | H.12 to H.19 | `@sobol1967`, `@sklar1959`, `@owen1956` |
| 23 | ML-NMR estimands and generality | H.20 to H.23 | `@phillippo2020mlnmr` |
| 24 | Bayesian computation and diagnostics | I.1 to I.6 | `@carpenter2017stan` |
| 25 | General likelihoods | J.1 to J.8 | `@phillippo2025general` |
| 26 | ML-UMR | M.1 to M.12 | `@chandler2025mlumr` |
| 27 | Distance matching | O.1 to O.7 | `@chandler2025mlumr` |
| 28 | Quantitative bias analysis | new (E-value, NORTA, tipping point) | `@lash2021qba`, `@vanderweele2017evalue` |
| 29 | Simulation study theory | K.1 to K.7 | `@morris2019ademp` |
| 30 | The Coq formalization | walkthrough of `theories/` | ITC_Coq |

The catalogue files are at `~/Documents/GitHub/ITC_Coq/proofs/` (one file per Part, named
`A_...md` to `O_...md`), with `00_concepts_index.md` the master list. The companion manuscript chapters
are at `~/Documents/GitHub/ITC_Coq/manuscript/`. Use these as the base draft for Parts II to VI; expand
every sketch into a full proof and add the worked examples and exercises.

## 10. Revision pass: pedagogical accessibility (target reader is a novice health researcher)

Two reviewers read the book as a beginner health researcher with weak mathematics. Their feedback is in
`feedback/chatgpt/` and `feedback/glm/`, one file per chapter. When revising a chapter, address BOTH
files, prioritizing each reviewer's "highest-priority fixes". The recurring requirements:

- **Concrete first, abstract second.** Put a small concrete example (a tiny design matrix, two specific
  vectors, real numbers) EARLY and reuse it; do not leave the only worked example to the end. A running
  health or trial example that reappears at each transition is the single highest-value addition.
- **Intuition after every definition.** After each `def-`, add a one or two sentence plain-language
  "reader translation" (what the object means for a trial, a model, or an estimand). Do the same after
  each major theorem: a short "Why this matters" line tying it to regression, NMA, or ITC.
- **Define or signpost jargon.** Any term a novice will not know (coset, affine subspace, direct sum,
  morphism, the symbol `\oplus`, pivot, row-echelon form) must be defined in line at first use or in
  `notation.qmd`; if it is only needed later, add a short "you do not need this yet" signpost.
- **Fix forward references.** Do not use a symbol or term before it is defined; reorder if needed.
- **Tables and roadmaps.** Where the reviewers ask for one (notation-role table, four-subspaces table,
  implication roadmap for long equivalence theorems), add a Markdown table.
- **Exercises.** Explain the `$\star$` convention in one line at the top of the Exercises section: a
  starred exercise has a full solution in Appendix F. Add at least one or two accessible warm-up or
  interpretation exercises before the proof-heavy ones; you may label exercises (warm-up, computation,
  interpretation, proof, challenge).

HARD CONSTRAINTS during revision (preserve harmony and the build):
- **Never remove or rename an existing `#thm-`, `#lem-`, `#def-`, `#eq-`, `#prp-`, `#cor-`, or `#sec-`
  label.** Other chapters cross-reference them. You may ADD new labeled environments.
- **Preserve every existing theorem and its proof.** This is a rigor book; you are adding scaffolding and
  intuition, not deleting mathematics. Expand and clarify; do not cut proofs.
- Keep American English and the no-dash rule. Keep notation consistent with `notation.qmd`.

## 11. PDF build safety (the book renders with pdflatex; do not break it)

The PDF engine is pdflatex (set in `_quarto.yml`). pdflatex does NOT load unicode-math, so:
- Use only ASCII in math mode. For a star marker use `$\star$`, never the Unicode `★`.
- Do not put a Unicode math operator (for example a multiplication sign, an inequality glyph, or a Greek
  letter as a literal character) in math; write the LaTeX command (`\times`, `\le`, `\beta`).
- Never apply `\not` to an extensible arrow (`\not\xrightarrow` fails); use `\overset{p}{\nrightarrow}`
  or `\nrightarrow`. `\not\to` and `\not\equiv` are fine.
- Inside display math `$$ ... $$` use `aligned`, `cases`, `pmatrix`, `bmatrix`, `array`; never a bare
  `align`, `equation`, or `gather` environment (that double-nests math mode and fails).
- Section labels on UNNUMBERED headers are not cross-referenceable; link with `[Notation](/notation.qmd)`
  rather than `@sec-...`. Keep every `#sec-` id unique across the whole book.
- Non-ASCII letters in prose (accents, the section sign) are fine; keep them out of math mode.
