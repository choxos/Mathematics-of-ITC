# Revision log: Chapter 3, Linear Algebra III (Spectral Theory and Quadratic Forms)

Revised `chapters/part1/03-linear-algebra-iii.qmd` in place to address both reviewer files
(`feedback/chatgpt/ch03-linear-algebra-iii.md` and `feedback/glm/ch03-linear-algebra-iii.md`),
following `logs/STYLE.md` Sections 10 and 11. All existing labels and all theorems/proofs are
preserved; the changes add intuition, examples, tables, and signposting only.

## Hard constraints honored

- No existing `#thm-/#lem-/#cor-/#prp-/#def-/#eq-/#sec-/#exm-/#exr-` label was removed or renamed
  (verified: all 58 original labels still present).
- Every existing theorem, lemma, corollary, proposition, and its full proof is preserved. The only
  proof reformatted is the Penrose-equations uniqueness chain, which was re-laid-out step-by-step with
  per-line justifications; no algebra was removed.
- Build safety verified: ASCII-only math, no Unicode anywhere in the file, no em/en/spaced-hyphen
  dashes, no bare `align/equation/gather` inside `$$` (uses `aligned`), `$\star$` used for the math
  star, `[Notation](/notation.qmd)` link (not `@sec-notation`). The new math constructs were
  test-compiled under pdflatex, and the chapter renders cleanly to HTML and PDF with no warnings.
- American English throughout. Only citation used is `@strang2016` (already in `references.bib`); no
  new bib keys invented.

## Highest-priority fixes addressed

ChatGPT reviewer:
1. Applied covariance + contrast-variance example. Added a running example
   (`@exm-la3-contrast-covariance`): covariance `[[2,1],[1,2]]` of two correlated log-OR estimates
   sharing comparator A, with the indirect contrast `a=(1,-1)`. This is the same matrix as the
   end-of-chapter worked example, so the threads connect. Contrast variance `a^T Sigma a = 2` is
   computed in the quadratic-form section, the Rayleigh section, and the worked example, where the
   contrast direction is shown to be the minimum-variance eigen-axis.
2. Plain-language interpretation after spectral theorem, definiteness, SVD, pseudoinverse. Added
   "Why this matters" lines after every major result and a "Reader checkpoint" remark after the
   spectral theorem; promoted the projection interpretation to `@prp-spectral-projections`.
3. Rebalanced the middle with signposting: added a "core vs supporting" learning-priorities table in
   the intro and marked Sylvester and Courant-Fischer as supporting both in that table and in their
   own "Why this matters"/skip-on-first-reading notes.
4. Rayleigh/Courant-Fischer made less abrupt: added the "variance/curvature in a chosen direction"
   framing, a PCA aside (`Var(x^T X) = x^T Sigma x` maximized by the top eigenvector), a numeric
   `R_Sigma(e_1)=2` check, a plain-English reading of the min-max formula, and a skip signpost.
5. Exercises: added the `$\star$` = Appendix F convention line, plus three accessible warm-up/
   interpretation/applied exercises before the proof-heavy ones (`@exr-la3-eigen-warmup`,
   `@exr-la3-contrast-variance` a health covariance/contrast-variance problem, `@exr-la3-collinear-design`
   a condition-number/collinearity problem) and a computational ramp exercise
   (`@exr-la3-penrose-rank-one`) before the starred proofs.

GLM reviewer (suggestions 1-10):
1. Threaded the `[[2,1],[1,2]]` running example through eigenvalues, spectral decomposition,
   quadratic forms, Rayleigh, square root, and the covariance bridge with one-line numeric checks.
2. Figures: not added as images (build-safety risk under pdflatex; see "Deliberately not changed").
   Substituted a build-safe "geometry in numbers" table (unit circle to ellipse) and explicit verbal
   geometry for the spectral and SVD pictures.
3. Front-loaded the ITC motivation: added a notation-role table mapping each object to its statistical
   role, a "why care about eigenvalues" lead-in, an up-front spectral-theorem payoff paragraph, and
   per-section anchors.
4. Slowed the Leibniz-expansion proof: worked the `n=2` case explicitly and added the bijection
   parenthetical for "no permutation has exactly n-1 fixed points".
5. Defined the conjugate transpose and the complex inner product in a "complex-number refresher"
   remark at the start of the eigenvalue section, with reassurance that symmetric matrices have real
   eigenvalues.
6. Promoted the projection interpretation of the spectral decomposition to `@prp-spectral-projections`
   (statement + proof).
7. Added a condition-number definition (`@def-condition-number`) and a paragraph connecting
   `sigma_1/sigma_r` to collinearity and variance inflation in the SVD section.
8. Split-vs-thread decision: instead of physically moving the end worked example, I threaded numeric
   micro-checks at each section and reframed/extended the end example (see "Deliberately not changed").
9. Formal definitions added: `@def-defective`, `@def-principal-minor` (principal vs leading principal
   minor), and the binary Loewner order flagged inline; the conjugate transpose, operator 2-norm, and
   Frobenius norm defined inline in the body.
10. Added intermediate exercises bridging computation and the starred proofs.

## Other specific reviewer points addressed

- Pulled "geometric multiplicity" out of `@def-eigenvalue` into its own `@def-geometric-multiplicity`.
- Clarified the block-upper-triangular step in `@lem-geo-le-alg` (showed the first g columns of
  `S^{-1}AS`), with a "why care" note on geometric vs algebraic multiplicity.
- Spectral-theorem proof broken into named bold steps (Base case; first eigenvector; invariant
  complement; shrink; assemble) with a proof-roadmap table; restated `dim W = n-1` at the point of use;
  added an intuition sentence for "A-invariant".
- `A^* = bar(A)^T` explained in the real-eigenvalues proof (reduces to the transpose for real A).
- "Functions of a matrix" remark expanded with the worked instance
  `A = Q diag(4,9) Q^T => A^{1/2} = Q diag(2,3) Q^T` and a legitimacy explanation.
- Indefinite `2x2` example added in the definiteness section; zero eigenvalues tied to collinearity/
  no-variation.
- Sylvester: motivation (eigenvalues hard, small determinants easy), plan-of-proof, and reassurance
  that the subspace `V` choice is not special to the last coordinate.
- Mahalanobis distance given a one-sentence plain meaning and tied to whitening in the covariance bridge.
- `N(A)`, `C(A)` reminded in-body with a `[Notation](/notation.qmd)` link; "direct sum" and the symbol
  glossed inline.

## New labeled environments added (all unique book-wide; verified no collisions)

- `@exm-la3-contrast-covariance` (running example)
- `@def-geometric-multiplicity`
- `@def-defective`
- `@prp-spectral-projections` (promoted from a plain paragraph; statement + proof)
- `@def-principal-minor`
- `@def-condition-number`
- `@exr-la3-eigen-warmup`, `@exr-la3-contrast-variance`, `@exr-la3-collinear-design`,
  `@exr-la3-penrose-rank-one`

Also added (unlabeled): a notation-role table and a learning-priorities table in the intro; a
spectral-theorem proof-roadmap table; a four-subspaces table and a unit-circle-to-ellipse table in the
SVD section; many "Reader translation." and "Why this matters." paragraphs.

## Notation proposed for the orchestrator to fold into `notation.qmd`

(`notation.qmd` was not edited per file discipline. Each symbol is also defined inline in the chapter
so the chapter is self-contained.)

- `\mathbf{x}^* = \bar{\mathbf{x}}^\top`, conjugate transpose (currently only `\top` appears in
  notation.qmd). Linear-algebra table.
- `A \succeq B`, `A \succ B`, the binary Loewner order (notation.qmd lists only `A \succeq 0`,
  `A \succ 0`). Linear-algebra table.
- `\|A\|_2`, operator 2-norm (largest singular value); `\kappa(A) = \sigma_1/\sigma_r`, condition
  number; `\|A\|_F`, Frobenius norm; `\bigoplus`/`\oplus`, direct sum. Linear-algebra table.

## Deliberately not changed (with rationale)

- No figures/TikZ. The PDF engine is pdflatex and STYLE Section 11 warns against build-breaking
  constructs; a TikZ figure would also not appear in HTML. Instead I added a build-safe "geometry in
  numbers" table (unit input directions mapped to the output ellipse) and explicit verbal geometry.
  A future illustrator could add the unit-circle-to-ellipse and eigen-axes-of-the-quadric figures;
  flagged here as the one remaining reviewer request not satisfied with text.
- The end worked example (`@sec-la3-example`) was kept in place (its `#sec-` and the contained
  references are cross-referenced) rather than physically split across the chapter. Instead I threaded
  the identical matrix as numeric micro-checks after the relevant theorems and reframed/extended the end
  example as the running covariance with an "indirect-comparison reading" (contrast variance,
  eigen-interpretation, condition number, whitening, Mahalanobis) plus a conditioning reading of the
  rank-deficient matrix. This satisfies "concrete first, reuse at transitions" without moving labeled
  content.
- All proofs kept at full length. The spectral-theorem and Sylvester proofs were annotated and
  signposted but not shortened; the lemma `@lem-eigvec-independent` (which the reviewer praised) was
  left as-is.

## Verification performed

- All 58 original labels present; 10 new labels added; no label collisions book-wide.
- Div open/close balance: 79/79.
- All `@`-cross-references resolve to a definition in the book.
- No Unicode, no dash punctuation, no bare `align/equation/gather`.
- pdflatex test-compile of the new `aligned` chains, `\bigoplus`, `\kappa`, `\approx`, and rank-one
  projection sum: OK.
- `quarto render` to HTML: clean (no warnings). PDF render attempted via pdflatex in the project.
