# Work log: Appendix B, Matrix Calculus

File authored: `appendices/B-matrix-calculus.qmd` (stub overwritten with the complete appendix; YAML
`title: "Matrix Calculus"` retained, stub callout dropped).

## Scope and purpose

A proved reference for the matrix calculus invoked in the foundations and meta-analysis chapters. Every
formula is derived from the definition of the derivative; this is reference material with full proofs, per
the brief (appendices B and D must prove or derive their results).

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (single source of truth) read in full before
  drafting.
- Chapter 6 (`chapters/part1/06-linear-regression.qmd`, lines ~155-195): confirmed the **gradient
  convention** is denominator layout, $\nabla S(\mathbf b)=-2\mathbf X^\top\mathbf y+2\mathbf X^\top
  \mathbf X\mathbf b$ (a column vector), with Hessian $2\mathbf X^\top\mathbf X$. The appendix's
  @thm-quadratic-form-derivative reproduces exactly this, so Chapter 6 can cite it.
- Chapter 5 (`chapters/part1/05-inference.qmd`): @thm-delta-method fixes the **Jacobian convention** as
  the $q\times p$ matrix $\mathbf D=[\partial g_a/\partial\theta_b]$; @def-score defines the score as a
  gradient (column vector). The appendix matches both.
- Chapters 8 and 13 (`08-hierarchical-bayes.qmd` line ~695; `13-pairwise-meta-analysis.qmd` line ~491):
  the **restricted likelihood** uses $\log\det\mathbf V$ and $\mathbf V^{-1}$ quadratic forms. This
  motivated @thm-logdet-derivative, @thm-inverse-derivative, and the compound-symmetry worked example.
- Chapter 3 (`03-linear-algebra-iii.qmd`): @def-quadratic-form, @def-definiteness, @thm-spectral-theorem.
- Chapter 1 (`01-linear-algebra-i.qmd` line ~934): @thm-invertibility-characterization, used to justify
  "a square matrix with a right inverse is invertible" in the Sherman-Morrison and Woodbury proofs.
- `@strang2016` (in `references.bib`) for the cited prerequisites: determinant, cofactor expansion,
  adjugate and Cramer's rule, multiplicativity and block-triangular determinant. `@dias2018nma` for the
  restricted-likelihood reference.

## Results stated and proved (all owned by this appendix; globally unique slugs, namespaced `mc`)

Definitions: `def-mc-gradient`, `def-mc-jacobian`, `def-mc-matrix-derivative`.
Engine lemmas: `lem-mc-identification` (derivative from differential via the trace form),
`lem-mc-differential-rules` (sum, product, transpose, trace), `lem-mc-trace-properties`.
Forms: `thm-linear-form-derivative`, `thm-quadratic-form-derivative`, `thm-bilinear-form-derivative`.
Trace/inverse/determinant: `thm-trace-derivative`, `thm-inverse-derivative`, `lem-mc-jacobi` (Jacobi's
formula), `thm-logdet-derivative`.
Low-rank updates: `lem-sherman-morrison`, `thm-woodbury`, `lem-mc-schur-det`,
`cor-mc-matrix-determinant-lemma`.
Chain rule: `thm-chain-rule` (vector composition; scalar parameter through a matrix).
Worked example `sec-mc-example`: compound-symmetry covariance $\mathbf V=\sigma^2 I+\tau^2\mathbf 1
\mathbf 1^\top$, inverted by Sherman-Morrison, determinant by the matrix determinant lemma, and
$\partial\log\det\mathbf V/\partial\tau^2$ by both direct and chain-rule routes, verified numerically at
$n=3,\sigma^2=1,\tau^2=2$ ($\det=7$, $\mathbf V^{-1}=I-\tfrac27\mathbf 1\mathbf 1^\top$, derivative
$=3/7$). This is the REML kernel for balanced designs (ties to Chapters 8 and 13).
A summary table of identities closes the body (`sec-mc-summary`).

## Proof-catalogue identifiers

None. Matrix calculus has no entries in `~/Documents/GitHub/ITC_Coq/proofs/` (checked) and no counterpart
in `theories/`; accordingly no result carries a `[machine-checked: ...]` tag.

## New notation introduced (proposed for folding into `notation.qmd`)

All introduced inline in the appendix; flagged here per STYLE rule 3.

- Frobenius inner product and norm: $\langle A,B\rangle_F=\operatorname{tr}(A^\top B)$,
  $\|A\|_F=\sqrt{\sum_{ij}A_{ij}^2}$. (Extends the vector inner product already in `notation.qmd`.)
- Standard basis matrix $E_{ij}=\mathbf e_i\mathbf e_j^\top$.
- Inverse-transpose shorthand $X^{-\top}=(X^{-1})^\top=(X^\top)^{-1}$.
- Matrix derivative $\partial f/\partial X$ (denominator/same-shape layout) and the differential
  $dF(X)[H]$ with free increment $dX:=H$.

## New bibliography entries proposed (NOT yet in `references.bib`)

Cited in the Notes section by author name only, since no bibtex key exists. Proposed keys and data for the
orchestrator to merge if desired:

- `magnus2019matrix`: Magnus, J. R. and Neudecker, H. *Matrix Differential Calculus with Applications in
  Statistics and Econometrics*, 3rd ed., Wiley, 2019. (Primary source for the differential method.)
- `petersen2012cookbook`: Petersen, K. B. and Pedersen, M. S. *The Matrix Cookbook*, Technical
  University of Denmark, version 20121115, 2012. (Identity catalogue, no proofs.)
- `harville1997matrix`: Harville, D. A. *Matrix Algebra from a Statistician's Perspective*, Springer,
  1997.
- `sherman1950adjustment`: Sherman, J. and Morrison, W. J. "Adjustment of an inverse matrix corresponding
  to a change in one element of a given matrix", *Annals of Mathematical Statistics*, 21(1):124-127,
  1950.
- `woodbury1950inverting`: Woodbury, M. A. "Inverting modified matrices", Memorandum Report 42,
  Statistical Research Group, Princeton University, 1950.
- (Optional) `horn2012matrix`: Horn, R. A. and Johnson, C. R. *Matrix Analysis*, 2nd ed., Cambridge
  University Press, 2012.

If these are not added, the prose already attributes the results correctly by name; only `@strang2016`
and `@dias2018nma` are cited with keys, both present in `references.bib`.

## Decisions

- Adopted the **differential** as the organizing tool (Magnus-Neudecker style): expand to first order,
  write the linear term as $\operatorname{tr}(G^\top dX)$, identify $\partial f/\partial X=G$ via
  `lem-mc-identification`. This keeps every proof short and index-free while fully rigorous.
- Stated the log-determinant derivative in the unconstrained layout ($X^{-\top}$) and added a remark on
  the symmetric-layout factor-of-two subtlety ($2X^{-1}-\operatorname{diag}(X^{-1})$), noting that the
  REML applications differentiate with respect to a scalar variance parameter and so avoid it.
- Proved Sherman-Morrison and Woodbury by direct verification (self-checking) rather than by block
  elimination; gave the matrix determinant lemma via a Schur-complement determinant lemma
  (`lem-mc-schur-det`) since the REML log-determinant needs it.
- Included a fully numerical worked example so the reader can verify by hand.

## Validation performed

- Standalone `quarto render` of the file succeeded (HTML produced). Only warnings were the expected
  cross-chapter crossrefs (`@def-quadratic-form`, `@def-score`, `@thm-delta-method`,
  `@def-definiteness`, `@thm-invertibility-characterization`), which resolve in the full book build; no
  internal slug warned.
- Verified all six external slugs cited exist in the chapters; verified every `@`-reference in the file
  resolves to an internal or chapter definition; verified all internal slugs are unique.
- Checked: no dash punctuation as connector (no em/en dash, double or spaced hyphen); American spelling
  ("cataloged"); div balance (35 open / 35 close) and display-math balance (54 `$$` blocks).

## Gaps left for review

- The six matrix-calculus references above are cited by name only; orchestrator may fold the proposed
  bibtex entries into `references.bib` and convert the Notes prose to `@key` citations.
- The new notation (Frobenius inner product/norm, $E_{ij}$, $X^{-\top}$, $\partial f/\partial X$) is
  introduced locally; orchestrator may add it to `notation.qmd` for global consistency.
