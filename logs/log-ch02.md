# Work log: Chapter 02, Linear Algebra II (Orthogonality and the Projection Theorem)

File authored: `chapters/part1/02-linear-algebra-ii.qmd` (overwrote stub; YAML title kept).
Author pass: single agent, Part I harmony.

## Sources consulted
- `@strang2016` (Strang, *Introduction to Linear Algebra*, 5th ed.): orthogonality, Gram-Schmidt,
  projections, least squares, QR factorization, conditioning of the normal equations. Used as the sole
  external citation; all load-bearing results are proved in full rather than cited, per STYLE.md rule 6.
- `logs/STYLE.md` and `notation.qmd` read in full before drafting.
- Confirmed there is **no** linear-algebra file in `~/Documents/GitHub/ITC_Coq/proofs/` (catalogue starts
  at `A_probability_foundations.md`) and that `~/Documents/GitHub/ITC_Coq/theories/` formalize the causal
  and population-adjustment layers, not linear algebra. Therefore **no `[machine-checked: ...]` tag** is
  attached to any result in this chapter. Noted in the chapter's Notes and references.

## Slugs defined (all globally unique, topic-namespaced)
Required (owned per assignment), all present exactly once:
- `thm-cauchy-schwarz-ip` Cauchy-Schwarz inequality (full proof, with equality case)
- `def-orthogonal-complement` orthogonal complement
- `thm-gram-schmidt` Gram-Schmidt orthonormalization (full strong-induction proof)
- `thm-projection-theorem` projection theorem / best approximation (full proof)
- `def-projection-matrix` orthogonal projection matrix
- `thm-normal-equations-geometry` normal equations from the projection viewpoint (full proof)
- `thm-qr` QR factorization (existence via Gram-Schmidt, uniqueness with positive diagonal)

Additional supporting slugs I created (none collide with the cross-chapter map):
- `def-inner-product`, `def-norm`
- `cor-triangle-inequality`, `thm-pythagoras`
- `def-orthogonality`, `lem-orthonormal-independent`, `prp-orthonormal-coordinates`, `cor-onb-exists`
- `lem-complement-subspace`, `thm-orthogonal-decomposition`, `cor-complement-dimension`,
  `prp-fundamental-orthogonality`
- `lem-projection-linear`, `prp-projection-from-onb`, `thm-projection-matrix-characterization`,
  `cor-projection-trace-rank`
- `lem-gram-nullspace`, `prp-ls-by-qr`
- Exercises: `exr-gram-schmidt-r3`, `exr-projection-plane`, `exr-line-fit`, `exr-qr-backsub`,
  `exr-double-complement`, `exr-bessel`, `exr-trace-idempotent`, `exr-parallelogram` (starred),
  `exr-oblique-vs-orthogonal` (starred).

Two starred exercises whose solutions belong in Appendix F: `exr-parallelogram` (parallelogram law,
polarization, and the failure of the ℓ¹ norm to come from an inner product) and
`exr-oblique-vs-orthogonal` (four-way equivalence: symmetric ⇔ orthogonal projection ⇔ norm-contractive
⇔ range ⟂ kernel for an idempotent).

Labeled referenceable equations: `eq-cauchy-schwarz`, `eq-pythagoras`, `eq-parseval`, `eq-gram-schmidt`,
`eq-orth-complement`, `eq-orth-decomp`, `eq-double-complement`, `eq-fundamental-orth`,
`eq-orthogonality-condition`, `eq-best-approx-pythag`, `eq-projection-onb`, `eq-proj-sym-idem`,
`eq-proj-trace-rank`, `eq-gram-spaces`, `eq-normal-equations`, `eq-hat-matrix`, `eq-qr`,
`eq-qr-projection`, `eq-qr-solve`.

## Cross-references to sibling chapters (by slug, per the map)
- Ch01: `@def-vector-space`, `@def-basis`, `@def-column-space`, `@thm-rank-nullity`, `@thm-four-subspaces`.
- Ch03: `@thm-pd-characterization` (weighted/Mahalanobis inner product example), `@thm-svd` (numerics remark).
- Ch06: `@thm-ols-normal-equations`, `@def-hat-matrix`, `@thm-ols-blue` (the remark stating this chapter
  is the geometric foundation reused there). Spellings match the cross-chapter slug map exactly.

## Notation: no conflicts introduced; one rendering decision recorded
- All symbols are drawn from `notation.qmd`: `⟨x,y⟩`, `‖x‖`, `‖x‖_A`, `C(·)`, `N(·)`, `P_M`,
  `P_M^⊥ = I − P_M`, `H`, `M`, `I_n`, bold lowercase vectors, bold uppercase data/factor matrices.
- **Decision (for the harmony pass):** `notation.qmd` writes the operator matrices `P_M`, `H`, `M`,
  `I_n`, `J_n` *without* bold, while data/parameter matrices (`X`, `Σ`) are bold. I followed that realized
  convention: data and factor matrices are bold (`A`, `Q`, `R`, `X`), and projection/identity operators
  are non-bold (`P`, `P_M`, `I_n`). A one-line statement of this convention appears at the end of the
  chapter introduction. No new symbol was introduced.
- The weighted inner product `⟨x,y⟩_A := xᵀA y` (for `A ≻ 0`) is used only as an example; it is the inner
  product whose induced norm is the already-defined `‖x‖_A` of `notation.qmd`. **Optional addition the
  orchestrator may fold into `notation.qmd`:** the row `⟨x,y⟩_A = xᵀA y | weighted (A-)inner product,
  A ≻ 0; induces ‖·‖_A`. Not required; the chapter is self-contained without it.

## Bibliography
No new bib entries needed. Only `@strang2016` (already in `references.bib`) is cited externally.

## Worked example (numbers verified independently with numpy)
4-point line fit: A = [[1,1],[1,2],[1,3],[1,4]], b = (1,3,4,4)ᵀ. Verified end to end:
Gram-Schmidt → Q, R = [[2,5],[0,√5]]; AᵀA = [[4,10],[10,30]], Aᵀb = (12,35); x̂ = (1/2, 1);
ŷ = (3/2,5/2,7/2,9/2); residual r = (−1/2,1/2,1/2,−1/2) with ⟨r,a₁⟩ = ⟨r,a₂⟩ = 0; RSS = 1, TSS = 6,
R² = 5/6; QR back-substitution reproduces x̂; trace(H) = 2 = p with H diagonal (0.7,0.3,0.3,0.7).
Every figure is exact and hand-checkable.

## Gaps / items for the consistency pass
1. This chapter relies on three facts that Chapter 1 must supply by the indicated slugs: existence of a
   basis for a finite-dimensional space (`@def-basis`), the column space (`@def-column-space`),
   rank-nullity (`@thm-rank-nullity`), and **row rank = column rank** (used inside `lem-gram-nullspace`
   and attributed to `@thm-four-subspaces`). If Ch01 places "rank(A) = rank(Aᵀ)" under a different slug,
   update the single citation in the proof of `lem-gram-nullspace`.
2. The forward references to Ch06 (`@thm-ols-normal-equations`, `@def-hat-matrix`, `@thm-ols-blue`) and
   Ch03 (`@thm-pd-characterization`, `@thm-svd`) assume those chapters define exactly those slugs (they
   match the map). Verify in the harmony pass.
3. `def-projection-matrix` and the symbol `P_M` are introduced here; Ch06 reuses `H = P_{C(X)}`. The
   chapter explicitly ties `eq-hat-matrix` to the `notation.qmd` hat matrix so the two read consistently.
4. Mechanical checks run: 60 opening fenced divs / 60 closers balanced; 20 `.proof` blocks each closing
   with `$\square$`; no em/en dash or double-hyphen connectors in prose (only YAML `---` fences match);
   all 7 owned slugs present exactly once.
