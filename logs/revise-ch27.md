# Revision log: Chapter 27, Aggregate-Level Covariate-Distance Matching

File: `chapters/part6/27-distance-matching.qmd`. Before: 1026 lines. After: 1493 lines.
Reviewers addressed: `feedback/chatgpt/ch27-distance-matching.md` and `feedback/glm/ch27-distance-matching.md`.

## Running example introduced

A single-arm oncology (relapsed/refractory large B-cell lymphoma) Phase II index trial described by two
aggregate covariate means (age, severity biomarker), with two external Phase III candidate comparators
$P$ and $Q$. Labeled `@exm-distance-two-trials`. Numbers are the age-biomarker sub-block of the existing
four-study example (index means $(60,10)$, scales $s=(10,4)$, $\boldsymbol\Sigma=[[100,20],[20,16]]$,
corr $0.5$; $\boldsymbol\delta_P=(10,4)$ concordant, $\boldsymbol\delta_Q=(6,-4)$ discordant). Raw and
standardized Euclidean both pick $Q$ ($d_{SE}(Q)=1.166<1.414$); Mahalanobis picks $P$ ($d_M(P)=1.155<
1.617$), because $P$'s move respects the correlation and $Q$'s fights it. Reused at each transition:
raw/std computation after `@def-euclidean-distance`, Mahalanobis reversal after `@thm-mahalanobis-whitening`,
exact bias $B_P=3.0,\,B_Q=-1.4$ with both Cauchy-Schwarz bounds in the bias section. The existing
four-study `@exm-distance-comparator-ranking` now reads as an extension of this toy.

## ChatGPT highest-priority fixes

1. Novice workflow before the formal definitions: new `## A practical workflow` section
   (`#sec-distance-workflow`) with a 6-step list and `@tbl-distance-workflow`.
2. Reference-scale and covariate-selection guidance: new "Choosing the covariates and the reference scales"
   remark (index IPD SD vs pooled/comparator SD vs Bernoulli SD; missing SDs; scale-vs-unit distinction).
3. Wasserstein plain-language: "piles of sand / holes" coupling paragraph before `@thm-lipschitz-bias-bound`.
4. ESS/bias tradeoff into main text: "Bias against variance" remark with `@tbl-distance-ess` and the
   MSE = bias^2 + variance framing.
5. Worked example interpretation: "Reading the four rankings" remark with `@tbl-distance-interpretation`
   (winner / why / HTA meaning) and a note on where the sensitivity vector beta comes from.
6. Scope caveat: added clinical-comparability clause to the "what matching is/is not good for" remark; the
   entropy-balancing/individual-level locator is a new remark.

## GLM highest-priority fixes

- Concrete clinical framing in the opening paragraph (CAR-T single-arm trial vs external Phase III arms;
  stakes stated: a wrong choice can flip the reported effect).
- Entropy-balancing locator: new "Where entropy balancing and individual-level reweighting live" remark
  (Hainmueller / MAIC weights are individual-level, downstream of selection; named in prose only, no bibkey).
- Why not run MAIC on every candidate: new "Why a cheap pre-analysis screen" remark.
- Conditional constancy and affine contrast restated in plain terms; affine contrast tied to a logit-link
  linear predictor $\eta=\mu+\beta_1^\top x+(\gamma+\beta_2^\top x)T$ with $\tau(x)=\gamma+\beta_2^\top x$,
  so beta = effect-modifier slopes.
- Coupling/Wasserstein intuition; Kantorovich-Rubinstein remark rewritten for the reader (worst-case bias
  over 1-Lipschitz contrasts) with Lip norm defined in words.
- "Coherent rescaling" preceded by the concrete months-vs-years-with-SD example and a regulatory framing.
- Whitening defined at first use; `$\|\mathbf v\|_A$` and `$\succ0$` glossed in prose at first heavy use.
- Spectral-theorem square-root existence recalled explicitly in the whitening proof.
- Minkowski general-$q$ step signposted to `@exr-distance-minkowski-metric`.
- Caveat Part 1 expanded: explicit optimal coupling and `|B_j|=1 <= L*W = 2` stated; Part 2 names ECOG
  performance status as the concrete unmeasured prognostic variable.
- Coq section reframed as an intentional non-target (design heuristic) with a schematic certifying
  `Theorem distance_linear_bias_bound` in a fenced ```coq block.
- Exercises: `$\star$` convention line added; two accessible warm-ups (`#exr-distance-warmup-compute`,
  `#exr-distance-warmup-memo`) before the proof-heavy ones; all exercises tagged by type.
- Roadmap `@tbl-distance-roadmap` and "if you read only one distance" signpost added; variants section
  flagged as reference material.

## Notation collision (deliberately not renamed)

GLM flagged `$\boldsymbol\delta_j$` (bold covariate gap) versus notation.qmd's `$\delta_{j,t_1t_k}$`
(plain scalar treatment contrast). Renaming the gap symbol would touch dozens of labeled equations and
proofs and risk the build, so I PRESERVED `$\boldsymbol\delta_j$` and instead added a clarifying sentence
at first use: the boldface marks the vector, the plain italic the scalar, per the book's convention; they
never co-occur. This is the reviewer's stated acceptable minimum ("or at minimum flag it").

## New labeled environments and tables added

- Section: `#sec-distance-workflow`.
- Example: `#exm-distance-two-trials`.
- Exercises: `#exr-distance-warmup-compute`, `#exr-distance-warmup-memo`.
- Tables: `#tbl-distance-roadmap`, `#tbl-distance-workflow`, `#tbl-distance-ess`, `#tbl-distance-interpretation`.
- Numerous unlabeled `::: {.remark}` intuition/motivation blocks (not cross-referenced).

## Preservation confirmation

- All pre-existing labels intact: 14 `#sec-`, 4 `#def-`, 4 `#thm-`, 4 `#prp-`, 16 `#eq-`, 1 original
  `#exm-`, 7 original `#exr-`. None removed or renamed (verified by inventory grep).
- Every existing theorem, proposition, and proof preserved; edits to proof bodies only EXPANDED them
  (whitening square-root recall, Minkowski signpost, caveat Part 1 coupling detail, caveat Part 2 naming).
- This chapter carries NO `[machine-checked:]` tags (the Coq section states distance matching lies outside
  `theories/`); none added, none removed.
- No new `@bibkey` citations introduced. Entropy balancing / Hainmueller and Villani / optimal transport
  are named in prose only; the Bristol Compass blog and `uitc` package remain "citation forthcoming" as
  before. Bib entries still owed to the orchestrator: the Bristol Compass blog, the `uitc` package,
  Mahalanobis (1936), Gower (1971), Villani optimal transport, and Hainmueller entropy balancing.
- `@phillippo2016tsd` fix: not applicable; the chapter does not cite that key.

## Build-safety checks run

- `:::` divs balanced (56 openings / 56 closings).
- No bare `align`/`equation`/`gather` inside `$$`; new displays use `pmatrix`, `smallmatrix`, `cases`.
- ASCII-only in math; `$\star$` marker used; only non-ASCII is "Hölder" in prose (allowed).
- No dash punctuation (no em/en/spaced-hyphen/double-hyphen connectors).
- No `\not` on extensible arrows. Coq in a fenced ```coq block, not math.
- Table captions on single physical lines matching house style; blank lines around every table and every
  `{#sec-}`/`###` heading.
