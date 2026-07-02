# Work log: Chapter 27, Aggregate-Level Covariate-Distance Matching

Author pass: Opus 4.8. File written: `chapters/part6/27-distance-matching.qmd` (full chapter, stub
callout dropped, YAML title kept).

## Sources consulted

- `~/Documents/GitHub/ITC_Coq/proofs/O_distance_matching.md` (catalogue O.1 to O.7): base draft for all
  seven catalogue results. Adapted and expanded every sketch into a complete proof in this book's
  notation, adding equality conditions, metric-property proofs, and the Wasserstein lower bound.
- `~/Documents/GitHub/ITC_Coq/manuscript/12_distance_matching.md`: companion manuscript chapter. Matched
  its section order and worked from its statements; expanded its one-line proofs and added a full worked
  example and exercises.
- `logs/STYLE.md` and `notation.qmd`: authoring contract and notation (followed).
- `chapters/part4/18-maic.qmd`: voice/structure model; reused its Cauchy-Schwarz/ESS framing and the
  `ESS_upper_bound` Coq cross-reference accurately.
- Verified the exact statements of all cross-referenced siblings before citing them: `@thm-cov-psd`,
  `@thm-jensen` (Ch4); `@thm-unanchored-paic-consistency`, `@eq-pat-unanchored-bias`,
  `@def-conditional-constancy-absolute`, `@def-sema`, `@thm-anchored-maic-consistency` (Ch17/Ch18);
  `@def-spfa` (Ch26); `@def-transportability` (Ch12); `@def-effect-modifier`, `@def-prognostic-variable`
  (Ch11); `@thm-maic-ess-bound` (Ch18); `@def-gaussian-copula` (Ch22). All confirmed present.

## Catalogue identifiers covered

O.1 (comparator-selection problem), O.2 (Euclidean + standardized Euclidean), O.3 (Mahalanobis whitening
equivalence), O.4 (Manhattan/Minkowski/Gower/mean-SMD), O.5 (scale dependence and invariance), O.6 (linear
and Lipschitz bias bounds), O.7 (non-identification caveat). Each section ends with a "corresponds to O.n"
note as required.

## Slugs defined

Owned (from the slug map), all present and unique:
- `def-comparator-selection` (O.1)
- `def-euclidean-distance` (O.2, covers raw + standardized)
- `thm-mahalanobis-whitening` (O.3; proved via `@thm-cov-psd` symmetric square root, general invertible
  factorization, with Cholesky and diagonal reductions)
- `def-distance-variants` (O.4)
- `thm-distance-scale-invariance` (O.5, positive result; standardized/Minkowski/mean-SMD/Gower invariance
  plus full affine invariance of Mahalanobis)
- `thm-lipschitz-bias-bound` (O.6, nonlinear/Wasserstein via coupling + Kantorovich-Rubinstein)
- `prp-distance-diagnostic-not-validity` (O.7; two-part proposition: nonlinearity and unmeasured imbalance)

Auxiliary slugs I introduced (namespaced `distance-`; confirmed no collision anywhere in `chapters/`):
- `def-mahalanobis-distance` (definition split out from the whitening theorem)
- `prp-distance-metric-properties` (which distances are metrics; q>=1 vs 0<q<1; Gower via truncation)
- `prp-distance-scale-dependence` (O.5 negative result: raw Euclidean ranking reversal counterexample)
- `thm-distance-linear-bias-bound` (O.6 linear case; Cauchy-Schwarz, both SE and Mahalanobis, with
  equality conditions; connects to `@thm-unanchored-paic-consistency`)
- `prp-distance-wasserstein-lower-bound` (mean distance <= Wasserstein, via vector `@thm-jensen`; makes O.7
  unavoidable)
- `exm-distance-comparator-ranking` (worked example)
- Exercises: `exr-distance-rescale-ranking`, `exr-distance-chebyshev`, `exr-distance-minkowski-metric`,
  `exr-distance-affine-invariance` (★), `exr-distance-secondmoment` (★), `exr-distance-wasserstein`,
  `exr-distance-ess-tradeoff`.

Labeled equations: 16, all namespaced `eq-distance-*` except references to the existing
`@eq-pat-unanchored-bias` (Ch17). No internal duplicate labels.

Starred exercises for Appendix F: `exr-distance-affine-invariance` (full affine invariance of Mahalanobis;
nondiagonal reparameterization reverses standardized-Euclidean ranking but not Mahalanobis) and
`exr-distance-secondmoment` (two distributions matching in mean and variance with different quartic-contrast
effects; hint and solution numbers verified: P0 = +/-1 each 1/2 gives E[x^4]=1; P1 = 3/4 at 0 and 1/8 at
+/-2 gives mean 0, var 1, E[x^4]=4, bias 3).

## Worked example: numerical verification

The four-comparator example was checked exactly with a script before writing. Index
`x0=(60,0.5,10)`, `s=(10,0.5,4)`, `Sigma=[[100,0,20],[0,0.25,0],[20,0,16]]` (PD; eigenvalues
0.25, 11.48, 104.52), `beta=(0.1,2,0.5)`, `S beta=(1,1,2)`, `Sigma beta=(20,0.5,10)`,
`beta' Sigma beta = 8`. Results (all confirmed):
- raw Euclidean winner C (C<B<D<A); standardized Euclidean winner A (A<D<B<C); Mahalanobis winner D
  (D<A<B<C); mean-SMD winner A. Three distinct winners across raw/std/Mahalanobis.
- exact biases A=1.8, D=3.2, B=3.6, C=4.0; bias ranking matches standardized Euclidean. Raw winner C has
  the largest bias.
- exact Cauchy-Schwarz equality: study B is SE-tight (z_B = 0.6 * S beta, bound = sqrt(12.96) = 3.6); study
  D is Mahalanobis-tight (delta_D = 0.4 * Sigma beta, bound = sqrt(10.24) = 3.2).

## Machine-checked tags

None added. There is no `theories/DistanceMatching.v` in the Coq development (confirmed by listing
`~/Documents/GitHub/ITC_Coq/theories/`). The chapter includes a "Connection to the Coq formalization"
section stating accurately that distance matching is not mechanized, and that the load-bearing inequality
(Cauchy-Schwarz) is the same one formalized as `Theorem ESS_upper_bound` in `theories/MAIC.v` (which does
exist and is already tagged on `@thm-maic-ess-bound`). No claim of formalization is made for any O.x result.

## Proposed bibliography additions (could not edit references.bib)

Cited inline from existing keys: `@phillippo2019thesis`, `@chandler2025mlumr`, `@chandler2026transport`.
Referenced by name in prose, with entries proposed here for the orchestrator to merge:

- `compassblog2024mlnmr` (misc/online): Bristol Compass student blog, "Extending multilevel network
  meta-regression," 2024-09-20,
  https://compass.blogs.bristol.ac.uk/2024/09/20/extending-multilevel-network-meta-regression/ . Source of
  the aggregate-level matching rule.
- `uitc` (software/manual): the `uitc` R package, https://github.com/choxos/uitc . Implements the
  standardized-Euclidean default and the full distance toolkit (Euclidean, Mahalanobis, Manhattan,
  Minkowski, Gower, mean-SMD).
- `mahalanobis1936` (article): P. C. Mahalanobis, "On the generalised distance in statistics,"
  Proc. Natl. Inst. Sci. India 2(1):49-55, 1936.
- `gower1971` (article): J. C. Gower, "A general coefficient of similarity and some of its properties,"
  Biometrics 27(4):857-871, 1971.
- `villani2009ot` (book): C. Villani, "Optimal Transport: Old and New," Springer, 2009. For
  Wasserstein-1 distance and Kantorovich-Rubinstein duality.

All five are referenced only in prose / "Notes and references" and as a named-theorem citation
(Minkowski's inequality, Kantorovich-Rubinstein duality), so the chapter renders without these keys; they
are enhancements, not blockers.

## Proposed notation additions (could not edit notation.qmd)

Symbols introduced in-chapter, consistent with the existing scheme; propose folding into notation.qmd:
- `d_E, d_{SE}, d_M, d_1, d_q, d_\infty, d_{\mathrm{SMD}}, d_G`: the covariate-summary distances (raw and
  standardized Euclidean, Mahalanobis, Manhattan, Minkowski, Chebyshev, mean-SMD, Gower).
- `\boldsymbol{\delta}_j = \bar{\mathbf{x}}_j - \bar{\mathbf{x}}_0`: covariate gap of candidate j.
- `\mathbf{z}_j = S^{-1}\boldsymbol{\delta}_j`: standardized gap; `S = diag(s_1,...,s_p)` reference-scale
  matrix; `s_\ell` reference scales; `r_\ell` Gower ranges.
- `W_\rho(P,Q)`: Wasserstein-1 distance with ground metric rho (Kantorovich-Rubinstein duality).
- `B_j`: transport bias `E_{P_j}[tau] - E_{P_0}[tau]`.
Reused existing notation: `\bar{\mathbf{x}}_j`, `\boldsymbol{\Sigma}_j`, `\|\cdot\|_A` quadratic-form norm,
`\boldsymbol{\Sigma}^{1/2}` symmetric square root, `\mathcal{P}, \mathcal{P}^{*}`.

## Decisions and notes

- Split O.5 into a positive theorem (`thm-distance-scale-invariance`) and a negative proposition
  (`prp-distance-scale-dependence`) for cleaner statements; the catalogue bundled both.
- Split O.6 into the linear bound (`thm-distance-linear-bias-bound`, Cauchy-Schwarz, exact) and the
  nonlinear bound (`thm-lipschitz-bias-bound`, Wasserstein), and added `prp-distance-wasserstein-lower-bound`
  (mean distance <= Wasserstein) because it is the precise reason O.7 holds: mean distance is a floor, not
  a ceiling, on distributional distance.
- Proved the Lipschitz bound by the elementary coupling argument (needs only vector Jensen, `@thm-jensen`)
  rather than invoking Kantorovich-Rubinstein duality as a black box; duality is noted as the dual view.
- Proved `thm-mahalanobis-whitening` for a general invertible factorization `Sigma = B B^T` (covers both
  Cholesky and the symmetric square root of `@thm-cov-psd`), strengthening the catalogue's Cholesky-only
  statement, and added the affine-invariance strengthening to the scale theorem.
- Added `prp-distance-metric-properties` (rigor: which "distances" are metrics; q<1 fails triangle
  inequality; Gower via truncation + averaging) because STYLE requires every stated claim to be proved or
  cited; proved q in {1,2,infinity} directly and cited Minkowski's inequality for general q.

## Gaps / for the harmony pass

- references.bib needs the five proposed keys above if the orchestrator wants the prose attributions
  (Compass blog, uitc, Mahalanobis, Gower, Villani) to resolve to formal citations; currently they are
  by-name mentions and the chapter compiles without them.
- notation.qmd could absorb the distance symbols and `\boldsymbol{\delta}_j`, `\mathbf{z}_j`, `W_\rho`,
  `B_j` (listed above).
- No `[machine-checked]` tags claimed; if a `theories/DistanceMatching.v` is ever added, the whitening
  identity, the two Cauchy-Schwarz bounds, and the finite counterexamples are the natural targets, and
  Chapter 30's "active axioms / proof status" tables should then be updated.
- Cross-references into Ch28 (QBA: E-value, tipping point) and Ch29 (ADEMP/MSE) are made in prose only and
  assume those chapters land with the slugs implied; no hard `@`-references to unwritten siblings were used,
  so nothing breaks if they slip.
