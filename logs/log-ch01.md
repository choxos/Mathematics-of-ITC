# Work log: Chapter 01, Linear Algebra I (Vector Spaces, Linear Maps, and Rank)

File authored: `chapters/part1/01-linear-algebra-i.qmd`
Author pass: foundations chapter, Part I. Renders cleanly under Quarto 1.8.26 (standalone render exit 0;
only warnings are the deliberate forward references to sibling chapters listed below).

## Sources used

- `@strang2016` (Strang, *Introduction to Linear Algebra*, 5th ed.). Primary and only citation. Used for:
  the four-fundamental-subspaces organizing picture; the existence and algorithm of (reduced)
  row-echelon form (cited, not reproved, in `@prp-rank-equals-pivots`); and the determinant
  characterization of invertibility (`@thm-invertibility-characterization`, item $\det A\neq 0$), which
  is the single fact taken on citation rather than proved, per STYLE rule 6.
- Everything else is proved in full from `@def-vector-space` upward, relying only on standard real
  arithmetic. No other reference was needed; no new bibliography entry is proposed.

## What is proved in full (load-bearing results)

- Vector-space arithmetic consequences (`@lem-vector-space-basics`).
- Subspace criterion, span as smallest subspace, intersection closure.
- Dependence lemma; **Steinitz exchange / replacement theorem** (`@thm-steinitz-exchange`) with full
  induction, giving dimension well-definedness (`@cor-dimension-well-defined`). I chose to PROVE
  basis-cardinality equality rather than cite it, since rank-nullity and the four-subspace counts rest
  on it; STYLE permitted either. Basis existence/extension proved for the finite-dimensional case
  (`@lem-reduction-to-basis`, `@lem-basis-extension`).
- Linear maps: kernel/image are subspaces; injective iff trivial kernel; map determined by a basis.
- Matrices ARE the linear maps between coordinate spaces (`@prp-matrices-are-maps`); matrix
  multiplication DERIVED from composition (`@thm-matrix-mult-composition`).
- **Rank-nullity** (`@thm-rank-nullity`) in full, both abstract-map and matrix forms.
- Row rank = column rank via rank factorization $A=CF$ (`@thm-row-rank-column-rank`).
- **Four fundamental subspaces** (`@thm-four-subspaces`): all four dimension counts proved in full; the
  orthogonality relations $\mathcal N(A)=\mathcal C(A^\top)^\perp$ and
  $\mathcal N(A^\top)=\mathcal C(A)^\perp$ proved as elementary set-equalities. The deeper projection
  geometry (orthogonal direct-sum decomposition realized by projection operators, least-squares
  geometry) is STATED and deferred to Chapter 2 per the assignment, via `@thm-projection-theorem` /
  `@thm-gram-schmidt`.
- Solvability of $A\mathbf x=\mathbf b$ via the column space (`@prp-system-solvability`), including the
  affine solution-set structure and the identifiability remark.
- Elementary row operations preserve rank and null space (`@lem-invertible-preserves-rank`); rank = number
  of pivots (`@prp-rank-equals-pivots`).
- **Invertibility characterization** (`@thm-invertibility-characterization`): 10 equivalent conditions
  proved via a closed implication loop driven by rank-nullity, plus $A^\top$ invertibility; the
  one-sided-inverse-is-two-sided fact for square matrices is in the trailing remark.

## Worked example and exercises

- Fully worked numerical example (`@exm-design-matrix`): the two-arm design matrix
  $\mathbf X=[\mathbf 1_4\ \mathbf t]\in\mathbb R^{4\times2}$. All four subspaces computed by hand, with
  explicit bases; $\mathbf X^\top\mathbf X=\begin{psmallmatrix}4&2\\2&2\end{psmallmatrix}$, det $=4$,
  inverse $\begin{psmallmatrix}1/2&-1/2\\-1/2&1\end{psmallmatrix}$, all hand-verifiable. A follow-on
  remark works the rank-deficient collinear design $[\mathbf 1_4\ \mathbf t\ \mathbf c]$ (dummy-variable
  trap) to foreshadow identifiability in regression and ITC.
- 10 exercises (`@exr-la1-*`), mix of computation and proof. Two starred for Appendix F:
  - `@exr-la1-dim-sum` ($\dim(U+W)=\dim U+\dim W-\dim(U\cap W)$).
  - `@exr-la1-gram-rank` ($\mathcal N(\mathbf X^\top\mathbf X)=\mathcal N(\mathbf X)$, hence
    $\mathbf X^\top\mathbf X$ invertible iff $\mathbf X$ has full column rank; the OLS precondition).

## Slugs defined (all globally unique, topic-namespaced)

Owned per assignment (all present): `def-vector-space`, `def-subspace`, `def-basis`, `def-linear-map`,
`def-column-space`, `thm-rank-nullity`, `thm-four-subspaces`, `thm-invertibility-characterization`.

Auxiliary definitions: `def-span`, `def-linear-independence`, `def-dimension`, `def-kernel-image`,
`def-rank`, `def-invertible`.

Lemmas: `lem-vector-space-basics`, `lem-subspace-criterion`, `lem-intersection-subspace`,
`lem-span-smallest-subspace`, `lem-dependence`, `lem-unique-representation`, `lem-reduction-to-basis`,
`lem-basis-extension`, `lem-kernel-image-subspace`, `lem-injective-trivial-kernel`,
`lem-map-determined-by-basis`, `lem-invertible-preserves-rank`.

Theorems/propositions/corollaries: `thm-steinitz-exchange`, `thm-matrix-mult-composition`,
`thm-row-rank-column-rank`, `prp-matrices-are-maps`, `prp-system-solvability`, `prp-rank-equals-pivots`,
`cor-dimension-well-defined`, `cor-iso-preserves-dim`.

Examples: `exm-coordinate-space`, `exm-other-spaces`, `exm-standard-basis`, `exm-design-matrix`.

Labeled equations: `eq-matvec`, `eq-matmul`, `eq-rank-nullity`, `eq-rank-factorization`, `eq-four-dims`,
`eq-four-orth`.

Sections (`sec-la1-*`): `intro`, `vector-spaces`, `subspaces`, `basis`, `linear-maps`, `matrices`,
`rank-nullity`, `four-subspaces`, `systems`, `row-ops`, `invertibility`, `design-example`, `notes`,
`exercises`.

Exercises (`exr-la1-*`): `four-subspaces-compute`, `elementary-rank`, `subspace-intersection`,
`design-collinear`, `rank-product`, `rank-one`, `left-right-inverse`, `map-unique-matrix`, `dim-sum` (★),
`gram-rank` (★).

## Cross-references to siblings (by slug map; currently unresolved, will resolve when authored)

- Ch02: `@thm-projection-theorem`, `@thm-gram-schmidt` (orthogonal decomposition completing the four
  subspaces; deferred geometry).
- Ch03: `@thm-spectral-theorem`, `@thm-svd`, `@thm-pd-characterization` (eigenvalue/singular-value views
  of invertibility, in the invertibility remark and notes).
- Ch06: `@def-linear-model`, `@thm-ols-normal-equations`, `@def-hat-matrix` (the regression payoff of the
  design-matrix example and Gram-matrix exercise).

All intra-chapter cross-references resolve with no warnings.

## Notation proposed for `notation.qmd` (did not edit the file myself)

- Orthogonal complement $\mathcal{M}^\perp=\{\mathbf z:\mathbf z^\top\mathbf m=0\ \forall\,\mathbf m\in
  \mathcal M\}$ and the relation $\mathbf x\perp\mathbf y\iff\mathbf x^\top\mathbf y=0$. These are
  consistent with the existing scheme (the table already lists $P^\perp_{\mathcal M}=I-P_{\mathcal M}$,
  which presupposes $\mathcal M^\perp$). I introduced $\mathcal M^\perp$ inline in this chapter without a
  cross-ref slug to avoid colliding with Chapter 2, which owns the orthogonality theory. Recommend the
  orchestrator add one row for $\mathcal M^\perp$ to the linear-algebra block of `notation.qmd`, and let
  Chapter 2 own the formal `def-`. No other new symbols introduced. The rank factorization $A=CF$
  (`@eq-rank-factorization`) is local notation only.

## Decisions and gaps left for review

- Machine-checked tags: none added; the assignment states there is no `ITC_Coq` file for this chapter, so
  per STYLE rule 4 no tags are claimed.
- I proved the four-subspace orthogonality as set-equalities (one-line, elementary) rather than asserting
  them silently, while deferring the projection-operator geometry to Chapter 2. If the harmony pass
  prefers the orthogonality to be merely stated here, the two short paragraphs in the proof of
  `@thm-four-subspaces` and the following remark can be trimmed; I kept them to honor "no silent claims."
- Determinant equivalence in `@thm-invertibility-characterization` is cited to `@strang2016` Ch. 5 rather
  than proved (full determinant theory is out of scope and not otherwise needed in the book). Flag if a
  self-contained determinant treatment is wanted somewhere in Part I.
- Potential cross-chapter naming overlap to watch in the harmony pass: I used `def-rank`, `def-dimension`,
  `def-span`, `def-linear-independence`, `def-kernel-image`, `def-invertible`. These are natural Chapter 1
  introductions and should not collide, but the orchestrator should confirm no later chapter redefines
  them.
