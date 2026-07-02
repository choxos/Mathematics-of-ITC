# Work log — Chapter 03: Linear Algebra III (Spectral Theory and Quadratic Forms)

File authored: `chapters/part1/03-linear-algebra-iii.qmd` (stub fully overwritten; YAML title kept).
Author pass: single agent, Part I foundations.

## Sources consulted and cited

- `@strang2016` (Strang, *Introduction to Linear Algebra*, 5th ed.): the standing reference for all
  background facts cited without proof — invertibility iff nonzero determinant, multiplicativity of the
  determinant, determinant of a block/diagonal-triangular matrix, $\det(cA)=c^n\det A$, existence and
  extension of bases, and the $LDL^\top$/pivots-as-minor-ratios alternative proof of Sylvester's
  criterion mentioned in the Notes.
- Fundamental theorem of algebra: cited as the single genuinely analytic prerequisite (used once to
  guarantee a complex root of the characteristic polynomial). Standard; no bib entry.
- `ITC_Coq/proofs/` scanned: spectral/PD/pseudoinverse keywords appear only as *downstream uses*
  (Mahalanobis distance in `O_distance_matching.md`, covariance/weights in `F_maic.md`,
  `C_meta_analysis.md`, `00_notation.md`), not as pure linear-algebra theorems. No catalogue identifier
  maps to this chapter (Part I linear algebra is marked "new" in the STYLE assignment table).
- `ITC_Coq/theories/` are causal/statistical (PotentialOutcomes, PropensityScore, MAIC, STC, ...). No
  formalized matrix-factorization theorem exists, so **no `[machine-checked: ...]` tags were added**.

## Cross-references to sibling chapters (used, not defined)

- Ch01: `@thm-rank-nullity` (dimension formula for subspaces; used in spectral-theorem complement, in
  Sylvester, in Courant-Fischer, in `lem-ata-psd`), `@thm-four-subspaces` (SVD subspace reading),
  `@def-basis` (extension of independent sets).
- Ch02: `@thm-projection-theorem` and `@def-projection-matrix` (rank-one spectral projectors;
  `prp-pseudoinverse-projection`), `@thm-gram-schmidt` (extend orthonormal sets; used in the spectral
  theorem and in SVD existence), `@thm-cauchy-schwarz-ip` (remark relating Rayleigh bounds to
  Cauchy-Schwarz).
- Ch04 (forward): `@thm-cov-psd` (covariance is symmetric PSD), referenced in the bridge remark and an
  exercise.

The instruction to "Reference `@thm-projection-theorem` from Chapter 2" is satisfied in
`prp-pseudoinverse-projection` and in the discussion after `eq-spectral-decomposition`.

## Slugs defined in this chapter (all globally unique, topic-namespaced)

Owned (required by assignment):
- `def-eigenvalue`, `thm-spectral-theorem`, `def-quadratic-form`, `thm-pd-characterization`,
  `thm-svd`, `def-pseudoinverse`, `thm-rayleigh`.

Additional definitions: `def-characteristic-polynomial`, `def-diagonalizable`, `def-definiteness`,
`def-rayleigh-quotient`.

Lemmas: `lem-eigen-char-poly`, `lem-geo-le-alg`, `lem-eigvec-independent`, `lem-trace-cyclic`,
`lem-trace-det-eigenvalues`, `lem-sym-real-eigenvalues`, `lem-sym-orthogonal-eigenvectors`,
`lem-ata-psd`.

Theorems/corollaries/propositions: `thm-diagonalization-criterion`,
`cor-distinct-eigenvalues-diagonalizable`, `thm-sylvester-criterion`, `thm-courant-fischer`,
`prp-matrix-square-root`, `prp-pseudoinverse-penrose`, `prp-pseudoinverse-projection`,
`prp-pseudoinverse-lstsq`.

Equations: `eq-char-poly`, `eq-spectral-decomposition`, `eq-quadratic-diagonalized`,
`eq-rayleigh-bounds`, `eq-courant-fischer`, `eq-svd`, `eq-pseudoinverse`.

Sections: `sec-la3-intro`, `sec-la3-eigen`, `sec-la3-diag`, `sec-la3-trace-det`, `sec-la3-spectral`,
`sec-la3-quadratic`, `sec-la3-rayleigh`, `sec-la3-svd`, `sec-la3-pseudoinverse`, `sec-la3-covariance`,
`sec-la3-example`, `sec-la3-notes`, `sec-la3-exercises`.

Exercises (two starred): `exr-diagonalize-symmetric`, `exr-definiteness-test`,
`exr-svd-pseudoinverse`, `exr-matrix-power-eigenvalues`, `exr-inverse-pd`, `exr-rayleigh-max`,
`exr-ata-aat-spectrum` (**starred**, Appendix F), `exr-weyl-inequality` (**starred**, Appendix F),
`exr-frobenius-singular`, `exr-correlation-psd`.

Starred-exercise note: solutions to `exr-ata-aat-spectrum` (shared nonzero spectrum of $A^\top A$ and
$AA^\top$; Frobenius norm = sum of squared singular values) and `exr-weyl-inequality` (Weyl's
inequality and eigenvalue perturbation bound via Courant-Fischer) are intended for Appendix F.

## Proofs given in full (load-bearing results, per STYLE rule 6)

Spectral theorem (inductive, via real eigenvector + invariant orthogonal complement); real eigenvalues
of symmetric matrices; orthogonality of eigenvectors; diagonalization criterion; trace/det as symmetric
functions of the spectrum (general, via Leibniz fixed-point degree argument); eigenvalue
characterization of definiteness; Sylvester's criterion (eigenvalue + dimension-count contradiction);
existence and uniqueness of the PSD matrix square root; Rayleigh extreme-eigenvalue characterization;
Courant-Fischer min-max; SVD existence and singular-value uniqueness via the spectral theorem of
$A^\top A$; the four Penrose equations and uniqueness of the pseudoinverse; pseudoinverse as orthogonal
projection and the full-column-rank formula $(A^\top A)^{-1}A^\top$; minimum-norm least-squares
property. Every proof div closes with `$\square$` (21 proofs, 21 squares; verified).

Worked example (`sec-la3-example`): $A=\begin{psmallmatrix}2&1\\1&2\end{psmallmatrix}$ carried through
eigenvalues $\{1,3\}$, orthonormal eigenbasis, spectral decomposition, definiteness (both tests),
Rayleigh bounds attained at the eigenvectors, and a hand-checkable square root; plus rank-1
$C=\begin{psmallmatrix}1&2\\2&4\end{psmallmatrix}$ for SVD ($\sigma_1=5$) and pseudoinverse
$C^{+}=C/25$ with a hand verification of Penrose (P1) using $C^2=5C$.

## Proposed notation additions (for the orchestrator to fold into `notation.qmd` if desired)

These are used in the chapter, are consistent with the bold/Greek scheme, and are reusable downstream.
`notation.qmd` already fixes `lambda_i(A)`, `sigma_i(A)`, `A=Q\Lambda Q^\top`, `A=U\Sigma V^\top`,
`A^+`, `A\succeq 0`, `A\succ 0`, `\|x\|_A`. I introduced, and recommend listing:

| Symbol | Meaning | First used |
|---|---|---|
| `A \prec 0`, `A \preceq 0` | negative definite, negative semidefinite (mirror of existing `\succ,\succeq`) | `def-definiteness` |
| `A^{1/2}`, `A^{-1/2}` | symmetric PSD matrix square root and its inverse (whitening, Mahalanobis) | `prp-matrix-square-root` |
| `\chi_A(t) = \det(tI-A)` | characteristic polynomial | `def-characteristic-polynomial` |
| `E_\lambda = \mathcal N(A-\lambda I)` | eigenspace; `\mathrm{spec}(A)` for the spectrum | `def-eigenvalue` |
| `\Delta_k` | $k$-th leading principal minor | `thm-sylvester-criterion` |
| `\|A\|_2`, `\|A\|_F` | operator (spectral) 2-norm and Frobenius norm | Rayleigh/SVD remarks, `exr-frobenius-singular` |
| `\mathbf{x}^* = \bar{\mathbf{x}}^\top` | conjugate transpose (used only to prove real eigenvalues) | `sec-la3-eigen` |

The matrix square root `A^{1/2}` is the highest-priority addition: it recurs in covariance whitening
and the Gaussian-copula / distance-matching machinery of Parts IV–V.

## Proposed bibliography entry (optional; not cited in text, so `references.bib` left untouched)

If the consistency pass wants a dedicated matrix-analysis reference beyond Strang for the deeper facts
(Weyl, Courant-Fischer, pseudoinverse), the standard choice is:

```bibtex
@book{hornjohnson2013,
  author    = {Horn, Roger A. and Johnson, Charles R.},
  title     = {Matrix Analysis},
  edition   = {2nd},
  publisher = {Cambridge University Press},
  year      = {2013}
}
```

The chapter currently cites only `@strang2016`, per the assignment ("Sources: Cite @strang2016"), so
adding this is discretionary.

## Gaps / items for the consistency pass

1. **Operator-norm identities stated in remarks, not in a labeled proposition.** The Rayleigh remark
   asserts $\|A\|_2 = \max_i|\lambda_i|$ for symmetric $A$, and the SVD remark asserts $\|A\|_2 =
   \sigma_1$. Both are immediate (apply `thm-rayleigh` to $A^2$, resp. read off `thm-svd`) but are
   not proved in a `.proof` div. If the editorial standard wants every asserted identity inside a
   proved environment, promote these to a short proposition. Left as remarks to control length;
   `exr-frobenius-singular` exercises the related Frobenius identity.
2. **Cited prerequisites (STYLE rule 6):** determinant algebra (multiplicativity, triangular/block
   determinants, `det(cA)=c^n det A`, invertibility iff nonzero determinant), existence/extension of
   bases, and the fundamental theorem of algebra are cited to Ch01/`@strang2016` rather than reproved.
   These are the standard Ch01 results; the consistency pass should confirm Ch01 actually states them
   under referenceable slugs (I leaned on `@thm-rank-nullity`, `@def-basis`, `@thm-four-subspaces`,
   and `@def-column-space`; I did not need a determinant slug, citing Strang for those facts).
3. **Sibling slugs assumed live:** `@thm-projection-theorem`, `@def-projection-matrix`,
   `@thm-gram-schmidt`, `@thm-cauchy-schwarz-ip` (Ch02) and `@thm-cov-psd` (Ch04). These match the
   provided cross-chapter slug map; verify they resolve after all chapters render.
4. **No machine-checked tags** in this chapter by design (no Coq counterpart). Recorded here so the
   verification pass does not look for one.

## Mechanical checks run

- No em dash, en dash, or spaced/double-hyphen connector anywhere (grep clean).
- All 7 owned slugs present exactly once; div open/close balanced 65/65; 21 proofs each ending in
  `$\square$`.
- American spelling throughout.
