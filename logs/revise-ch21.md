# Revision log: Chapter 21 (ML-NMR II: Discrete Outcomes and Approximation Theory)

File: `chapters/part5/21-mlnmr-discrete.qmd`. Revised per Section 10 (pedagogical accessibility) against
both reviewer files. Before: 942 lines. After: 1278 lines (+336). No proof shortened; no existing label
removed or renamed. All 52 original labeled environments/equations verified present exactly once; div
fences balanced 52/52; no unicode in math, no dash punctuation, no bare align/equation/gather.

## Running example introduced (single highest-value addition)

A hypothetical oncology responder arm (`@exm-running-oncology`, in the introduction): study AB reports
responders out of patients on drug A; the ML-NMR model gives each covariate profile a response probability
`p = expit(eta(x))`; frail patients near 0.1, fit patients near 0.7. The concrete five-profile risk vector
`p = (0.1,0.3,0.4,0.5,0.7)`, `pbar = 0.4` is the same vector the terminal worked example
`@exm-aggregate-binomial` uses, so the example now threads the whole chapter: intro -> two-patient
conditional/marginal microexample -> two-Bernoulli PGF expansion -> five-profile worked example (Step 7).

## New labeled environments and tables (11 added; all originals preserved)

- `#exm-running-oncology` : clinical running example + `expit` definition, in the introduction.
- `#exm-two-patient-conditional` : two-patient (0.1, 0.7) conditional-vs-marginal computation by hand,
  placed immediately after the conditional/marginal remark (moves worked numbers up ~600 lines, per both
  reviewers).
- `#sec-discrete-roadmap` : new subsection resolving the integrated-vs-adjusted tension and closing the
  copula loop.
- `#tbl-aggregate-laws` : five-row decision table (data representation -> exact law -> tractable? ->
  surrogate -> what it matches). Directly answers both reviewers' "add a decision/roadmap table."
- `#exm-count-overdispersion` : two-profile hospitalization count mini-example (n=40, rates 1 and 3;
  mean 80, variance 120, dispersion 1.5), inline after `@thm-poisson-aggregate`.
- `#exm-two-bernoulli-pgf` : two-Bernoulli generating-function expansion (health framing), placed before
  `@thm-poisson-binomial-pgf`; includes the `binom(400,120) > 10^100` concrete number.
- `#tbl-lecam-regime` : Le Cam / Barbour-Hall bounds across pbar = 0.02, 0.05, 0.20, 0.50 (n=100), the
  "what this means for 5%, 20%, 50% event rates" diagnostic table.
- `#tbl-worked-comparison` : four-law side-by-side likelihood table (PoBin / adjusted Bin / integrated Bin
  / Le Cam Poi) over y = 0..5 plus mean/variance, replacing the requested "diagram" with a build-safe
  table at Step 6.
- `#exr-why-not-binomial`, `#exr-choose-likelihood`, `#exr-two-patient-warmup` : three accessible warm-up
  / interpretation / likelihood-selection exercises added before the proof-heavy ones. Not starred (no
  Appendix F solution created), so no dangling solution promise.

## ChatGPT reviewer, highest-priority fixes

1. Integrated-vs-adjusted tension (their #1). Resolved with `#sec-discrete-roadmap` + `#tbl-aggregate-laws`
   plus explicit prose: the two are not rivals but the correct laws for two covariate representations
   (exchangeable sample -> integrated binomial; fixed integration nodes -> Poisson binomial / adjusted
   binomial). Reprised in the worked example's "Patients or profiles?" paragraph and the existing "Which
   likelihood to report" remark.
2. Patient-vs-integration-node distinction (their #2). New "Patients or profiles?" paragraph inside
   `@exm-aggregate-binomial`; flagged in the running example and roadmap.
3. Health interpretation of approximation error, TV, moment matching, overdispersion (their #3). Added
   "Reader translation" for TV distance (worst-case likelihood error that scales the arm's pull on the
   estimate); inference tie in "What is guaranteed" ("lets the arm speak too softly"); count-overdispersion
   example ("would pull the network estimate too hard"); ESS reader-translation.
4. Non-integer N* practical status (their #4). New passage in the "Non-integer N*" remark: Gamma
   interpolation makes sense of Bin(3.7,0.45); support {0..N*}; observed y can exceed N* (y=5 vs N*=4 in
   the example); integrated binomial (integer n, full support) is the safe fallback.
5. Smaller count example + easier selection exercise (their #5). `#exm-count-overdispersion` and
   `#exr-choose-likelihood`.

## GLM (beginner) reviewer, key asks

- Clinical motivation up front: `@exm-running-oncology`.
- Move worked numbers up: `@exm-two-patient-conditional` (setup) and `@exm-two-bernoulli-pgf` (pobin).
- One-line glosses at first use: "mixed Poisson" (intro), `expit` (running example, + pointer to
  `@def-link-function`), `beta_tot` (in `@thm-poisson-aggregate` statement), law of total variance /
  tower property (prp proof gloss), W scalar-vs-vector-space note.
- Strategy paragraph at head of `@sec-lecam`: added, listing the four ingredients and the plan.
- Motivate `@lem-poisson-convolution` and its second proof before giving them: added "the reason to dwell"
  sentence and strengthened the second-proof signpost.
- Expand Gaussian-covariate Part 3: added the MGF argument for affine-image-of-normal-is-normal and the
  log-normal moment identity `E[W^r] = M(r)`.
- Diagram: supplied as `#tbl-worked-comparison` (build-safe substitute for a figure).
- Close the copula loop: roadmap sentence tying the per-node p_i to the Gaussian copula `C_Omega` of
  Chapter 22.
- Coupling construction motivation, coupling-inequality direction gloss, numerical single-pair coupling
  (p=0.2 -> 0.0363), Barbour-Hall lambda^{-1} intuition: all added.
- Underdispersion surprise (risks near 0/1 are more predictable): added to the binomial-special-case
  remark.
- ESS parallel unpacked: new "Why a weighting quantity reappears here" remark (Cauchy-Schwarz "effective
  number of equal-information units"; likelihood-ESS vs weighting-ESS disambiguation).
- Easier exercises + star convention line: added.

## Intuition / why-this-matters tally

- 4 blocks explicitly titled "Reader translation" (after `@prp-marginal-binomial`, `@def-pgf`,
  `@def-total-variation`, `@thm-adjusted-binomial`), plus ~10 further inline glosses/intuition insertions
  (mixed-Poisson, tower property, beta_tot, W scalar, asymmetry plain-language, 3-layer theorem priming,
  affine/log-normal scaffolding, near-0/1 predictability, coupling motivation, inequality direction).
- ~7 explicit "why this matters" ties to NMA/ITC/regression (naive Bin(n,pbar) failing; count example
  pulling the network estimate; TV feeding the arm's pull; Le Cam bound as a trust ruler; wrong-surrogate
  mis-scaling the likelihood; ESS bridge to MAIC Chapter 18; roadmap as a modeling choice).

## Deliberately skipped / judgment calls

- Intro length trim (GLM #9, low priority): I added the running example rather than cutting the preview
  paragraphs, because the ADD-don't-cut constraint dominates and the concrete example is what the "too
  abstract" complaint actually wants. Net intro is longer but now concrete-first.
- Did not split the terminal worked example into subexamples (GLM pacing note): would have required
  renumbering/relabeling risk; instead added the consolidating `#tbl-worked-comparison` and the
  "Patients or profiles?" framing to make it easier to navigate.
- New warm-up exercises left unstarred: starring them would promise Appendix F solutions I am not editing.

## Labels I was tempted by but preserved

- The introduction asserts the adjusted binomial "is the surrogate used in practice," while
  `#prp-marginal-binomial` calls the integrated binomial "the likelihood ML-NMR uses by default." Tempted
  to rewrite the intro claim to remove the apparent contradiction; instead I preserved both statements
  verbatim and reconciled them with `#sec-discrete-roadmap` + `#tbl-aggregate-laws` (they are correct for
  different covariate representations). No prose deleted, no label touched.
- Preserved every equation label (`#eq-integrated-binomial` ... `#eq-ex-poisson`) and every theorem/lemma
  even where new scaffolding was inserted into the proof body (e.g. the Part 3 affine/log-normal lines were
  added, the original chain untouched).

## Notes for orchestrator

- Three new cross-referenceable tables use the standard multi-line-caption `: ... {#tbl-...}` form (matches
  `chapters/part5/25-general-likelihoods.qmd`). `\lesssim` used in two spots (amssymb, already loaded).
- No new `@bibkey` citations introduced. Barbour-Hall (1984) and Chen (1975) remain prose attributions as
  in the original; still flagged as proposed bib additions in the Notes section (unchanged).
