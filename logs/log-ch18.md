# Work log: Chapter 18, Matching-Adjusted Indirect Comparison (MAIC)

File authored: `chapters/part4/18-maic.qmd` (stub overwritten with full chapter).
Catalogue ownership: F.1 through F.12 of `proofs/F_maic.md`.

## Sources consulted

- `logs/STYLE.md` (authoring contract) and `notation.qmd` (notation, single source of truth).
- `chapters/part3/14-bucher.qmd` for voice, div grammar, and the worked-example style.
- Base draft expanded: `~/Documents/GitHub/ITC_Coq/proofs/F_maic.md` (results F.1 to F.12) and
  `~/Documents/GitHub/ITC_Coq/manuscript/08_maic.md`. Every sketch in those files was expanded into a
  complete proof in this book's notation.
- `~/Documents/GitHub/ITC_Coq/theories/MAIC.v` (read in full) to confirm exact Coq names for the
  machine-checked tag, and `~/Documents/GitHub/ITC_Coq/theories/AXIOMS.md` (confirms the ESS/Cauchy-Schwarz
  results are fully proved, no admissions; `H_MAIC` is the MAIC identification hypothesis for F.6).
- `~/Documents/GitHub/ITC_Coq/proofs/00_concepts_index.md` for catalogue wording (B.9 = HT/IPW
  unbiasedness; E.4/E.5 = conditional constancy of relative/absolute effects; E.8 = shared effect
  modifier).
- `~/Documents/GitHub/itc_courses/Unanchored_ITC_and_Bias_Analysis_with_uitc/02_MAIC_Entropy_Balancing_Weights/lesson.yaml`
  for the KL-from-uniform derivation of entropy balancing; my independent derivation (normalized weights,
  I-divergence, convex dual = log-partition minimization) matches it. The course's hand example (ESS
  211.7 from 345, three covariates) corroborates the ESS interpretation.

## Slugs defined (owned)

Definitions: `def-moment-balance` (F.1), `def-entropy-balancing` (F.2). Plus a supporting lemma
`lem-maic-xlogx-convex` and a definition `def-maic-ess` (effective sample size), both chapter-local.

Theorems: `thm-maic-exponential-weights` (F.3), `thm-maic-existence-uniqueness` (F.4),
`thm-maic-logistic-ipw-equiv` (F.5), `thm-anchored-maic-consistency` (F.6),
`thm-unanchored-maic-consistency` (F.7), `thm-maic-ess-bound` (F.8), `thm-maic-variance-inflation` (F.9),
`thm-maic-no-extrapolation` (F.10), `thm-maic-sandwich-variance` (F.11), `thm-maic-bootstrap` (F.12).

Example: `exm-maic-twocov`. Exercises: `exr-maic-onecov`, `exr-maic-secondmoment`, `exr-maic-logit`,
`exr-maic-ess-majorization`, `exr-maic-bias-decomp` (starred), `exr-maic-sandwich-vs-naive` (starred). The
two starred exercises are flagged for Appendix F.

Equation labels (all lowercase, topic-namespaced `eq-maic-*`): moment-balance, moment-centered, entropy,
kl, weights, lagrangian, stationarity, alpha, balance-beta, dual, grad-q, hess-q, feasible-hull, relint,
logit, densityratio, ht, anchored-est, unanchored-est, ess, var-weighted, inflation, nonid, estfun,
sandwich, example-weights. (Two labels were renamed from `eq-maic-gradQ`/`eq-maic-hessQ` to
`eq-maic-grad-q`/`eq-maic-hess-q` to keep slugs lowercase and avoid any crossref ambiguity.)

## Machine-checked tags added

- `thm-maic-ess-bound`: `[machine-checked: theories/MAIC.v, Theorem ESS_upper_bound]`. Confirmed by
  reading `MAIC.v`: `Theorem ESS_upper_bound` (line 303) is proved from `Lemma cauchy_schwarz_n_weights`
  (291), itself from `Lemma cauchy_schwarz_ones` (257) and the elementary `Lemma two_mul_le_sqr` (248);
  `AXIOMS.md` confirms no admissions. The supporting lemma names are also cited in the Notes section.
- No machine-checked tag on F.3 (exponential weights): `MAIC.v` only defines `maic_weight_fn` and proves
  `maic_weight_pos`; the KKT/duality optimization is pen-and-paper, so I cited those Coq names in prose but
  did not tag the theorem. Same reasoning for the consistency theorems (carried by abstract section
  hypotheses in Coq, not formalized probabilistic theorems).

## Cross-references used (all verified to resolve except concurrent-wave siblings)

Resolve now (grep-confirmed): Ch5 `def-sandwich-variance`, `thm-mle-asymptotic-normality`; Ch7
`def-link-function`, `def-non-collapsibility`; Ch9 `thm-ate-identification`; Ch10 `thm-ipw-unbiased`,
`thm-g-computation-unbiased`, `def-balancing-score`; Ch11 `def-effect-modifier`, `def-prognostic-variable`,
`def-collapsibility`, `thm-noncollapsibility-or-hr`; Ch12 `def-transportability`,
`thm-conditional-transportability`, `thm-sema-insufficient`; Ch14 `def-transitivity`, `thm-bucher-unbiased`,
`thm-bucher-variance`, `prp-trial-unbiased`, `lem-relative-effect-algebra`, `prp-baseline-cancellation`;
Ch16 `thm-failure-of-bucher`, `def-ecological-bias`; `@vandervaart1998` (bib) for the bootstrap functional
delta method.

Will resolve once sibling wave lands (intended forward/lateral references): Ch17
`def-conditional-constancy-relative`, `def-conditional-constancy-absolute`, `thm-anchored-paic-consistency`,
`thm-unanchored-paic-consistency`, `def-sema`, `exm-scale-dependence-em`, `thm-shared-em-identifiability`,
`prp-testable-untestable-constancy`; Ch19 `thm-maic-stc-equivalence`. These match exactly the slugs the
orchestrator assigned to Ch17 and Ch19 in this wave.

## Proposed notation / bibliography additions

- None required. All symbols used are already in `notation.qmd`: `w_i`/`w(x)`, `ESS`, `alpha`/`boldbeta`
  for the weight parameters, `\mathbb V` (sandwich variance), `\bar{\mathbf x}_j`, `f_j`, `\mathcal P`,
  `d_{ab(\mathcal P)}`, `g`/`g^{-1}`, `\mu_t(x)`, `\tau(x)`, `SEMA`. Chapter-local symbols introduced
  explicitly in text: `\boldsymbol\Delta_i` (centered covariate), `Q(\boldsymbol\beta)` (log-partition /
  dual objective), `\mathcal P_{AC}`/`\mathcal P_{BC}` (IPD and AgD trial populations, instances of the
  existing `\mathcal P` scheme). No conflicts with existing notation.
- All bibtex keys cited (`signorovitch2010maic`, `phillippo2019thesis`, `phillippo2016tsd18`, `bucher1997`,
  `vandervaart1998`) are already present in `references.bib`. No additions needed.

## Decisions and notes for the harmony pass

- Trial naming: I use `AC` for the IPD (index) trial and `BC` for the AgD (comparator) trial, matching
  the Bucher chapter exactly. The catalogue's `F_maic.md` confusingly labels the IPD trial "AB" while its
  arms are A vs C; I corrected to `AC` for harmony with Ch14 and the notation. Mathematics unchanged.
- Consistency vs unbiasedness: stated explicitly (weights are estimated), following the catalogue's own
  correction of the early-literature "unbiased" language.
- F.6/F.7 proved in full for the affine-mean (identity-scale / matched-higher-moment) case; the
  non-collapsible-scale subtraction step is delegated to Ch17 `thm-anchored-paic-consistency`, as the slug
  map intends ("referencing @thm-anchored-paic-consistency / @thm-unanchored-paic-consistency"). This is by
  design, not a gap.
- Worked example is exact and hand-checkable: a centered unit square with target mean (0.5, 0.5) gives
  beta = (1/2)ln 3 by a tanh identity, weights (2.25, 0.75, 0.75, 0.25), ESS = 2.56 (= 16/6.25),
  inflation 1.5625, SE inflation exactly 1.25; the adjusted A-vs-C benefit moves from 4.0 (index) to 4.5
  (comparator), and the anchored A-vs-B estimate is 1.5 versus the biased unadjusted 1.0.

## Verification performed

- All 12 owned div slugs present; all internal `@eq-maic-*` references match a defined `{#eq-maic-*}` label
  (no danglers). No capital letters remain in any slug.
- Div fences balanced (50 open, 50 close). 11 proof blocks, each ending in `\square`. Stub callout
  removed; YAML title preserved. Two starred exercises present. No dash-as-connector punctuation
  (em/en/spaced-hyphen/double-hyphen) in the chapter; American spelling throughout.
