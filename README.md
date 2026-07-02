# The Mathematics of Indirect Treatment Comparisons

**Population Adjustment, Transportability, and Comparative Effect Estimation**

A graduate-level, pure-mathematics textbook that develops indirect treatment comparison from first
principles. It starts at linear algebra and probability, builds ordinary least squares and the
generalized linear model with full proofs, develops the causal-inference and transportability theory
that frames the field, and then derives the modern population-adjustment methods: network meta-analysis,
matching-adjusted indirect comparison (MAIC), simulated treatment comparison (STC), multilevel network
meta-regression (ML-NMR), and multilevel unanchored meta-regression (ML-UMR).

Every substantive result is either proved in full or explicitly marked as cited or assumed. Many of the
central theorems carry a tag pointing to a machine-checked counterpart in a companion Coq development.

## Structure

The book is a [Quarto](https://quarto.org) book. Each chapter is a separate `.qmd` file.

```
.
├── index.qmd                 preface
├── notation.qmd              notation and conventions (single source of truth)
├── chapters/
│   ├── part1/  Mathematical Foundations            (ch 01 to 08)
│   ├── part2/  Causal Inference and Estimands       (ch 09 to 12)
│   ├── part3/  Meta-Analysis and Network MA         (ch 13 to 16)
│   ├── part4/  Population Adjustment: MAIC and STC   (ch 17 to 19)
│   ├── part5/  Multilevel Network Meta-Regression   (ch 20 to 26)
│   └── part6/  Bias, Comparator Selection, Rigor    (ch 27 to 30)
├── appendices/               A to G
├── exercises/                problem sets
├── code/                     minimal reference R and Stan
├── figures/                  diagrams
├── references.bib            bibliography
└── logs/                     authoring contract and per-part work logs
```

## Building

Requirements: Quarto, a LaTeX engine (for example TinyTeX), and pandoc (bundled with Quarto).

```bash
quarto render            # build PDF and HTML into docs/
quarto render --to html  # HTML only
quarto render --to pdf   # PDF only
quarto preview           # live preview while editing
```

## Reference material

The book draws on reference texts and four reference software repositories. The copyrighted source
texts live under `documentation/refs/` and are excluded from version control. See `CLAUDE.md` for the
full source inventory and the mapping from chapters to sources.

## License and attribution

Sole author: Ahmad Sofi-Mahmudi. The copyrighted reference texts under `documentation/refs/` are not
redistributed with this repository.
