# Revision log: Chapter 04, Probability and Distributions

Pedagogical-accessibility revision of `chapters/part1/04-probability.qmd` per reviewer feedback in
`feedback/chatgpt/ch04-probability.md` and `feedback/glm/ch04-probability.md`. Followed `logs/STYLE.md`
(Sections 10 and 11) and kept notation consistent with `notation.qmd`. File grew from 1247 to 1717 lines.
No existing theorem, proof, or label was removed or renamed; only intuition, examples, tables, signposts,
and warm-up exercises were added, plus a few proof steps were *expanded* (never shortened).

## Verification performed

- All 35 original `def/thm/lem/prp/cor` labels, 14 `eq-` labels, 18 `sec-/exr-` labels still present
  exactly once (scripted check passed).
- Fence balance 94 open / 94 close; display-math `$$` count even (142); pandoc `-f markdown -t native`
  parses with no error.
- PDF safety: no bare `align/equation/gather`; no `\not` on an extensible arrow; no `smallmatrix`; star
  written `$\star$`; all non-ASCII characters are pre-existing prose (accents, section sign), none in math.
- Markdown tables use literal `|` only as cell delimiters; conditional bars inside cells are `\mid`
  (a macro), absolute values are `\lvert/\rvert`, so column parsing is unaffected.
- Cross-references: every `@`-reference resolves in-file except the two expected Chapter 3 externals
  `@thm-spectral-theorem` and `@thm-pd-characterization` (unchanged from the original).

## Highest-priority fixes addressed

ChatGPT 1 / GLM 1 (running clinical example): new section `@sec-prob-running-example` with
`@exm-toy-trial`, a toy two-arm trial (severity `X`, treatment `T`, response `Y`, study `S`) plus a
table of within-stratum risks, introduced *before* the measure theory. Includes an explicit
patient-level vs study-level probability-space distinction (ChatGPT "what is omega" point). The example
is reused at every transition: probability space, random variables, expectation, conditioning, tower,
independence, Jensen.

ChatGPT 2 / GLM 2 (conditional expectation + tower bridge): expanded the discrete-to-measure-theoretic
transition into a full paragraph with the explicit `0/0` reason; added `@exm-cond-exp-strata`, a
finite-strata worked example computing `E[Y|X]` by the elementary ratio AND by the defining property, and
checking the tower identity `E[Y] = 0.32` numerically before the theorem.

ChatGPT 3 / GLM 7 (concrete Jensen / non-collapsibility): added `@exm-jensen-logit` with hand-checkable
arithmetic showing `logit^{-1}(E[eta]) = 0.75` differs from `E[logit^{-1}(eta)] = 0.70`, tied to odds-ratio
non-collapsibility (forward pointer to Chapter 11).

ChatGPT 4 / GLM 5 (graphoid burden): the preserve-proofs hard constraint forbids shortening the proof, so
instead I (a) added a skip signpost, (b) added a `(G1)-(G5)` roadmap table with plain meaning and ITC use,
(c) added `@exm-graphoid-binary`, a three-binary-variable causal illustration of decomposition and
contraction, and (d) added a post-proof remark translating the weak-union `(G3)` step into words. Net
effect: the reader can use the axioms without reading the proof, while the full proof survives intact.

ChatGPT 5 / GLM 3 (earlier worked examples): `@exm-cond-exp-strata`, `@exm-jensen-logit`, and
`@exm-mvn-mini` (a slim bivariate-normal preview after `@thm-mvn-linear`) all land well before the final
worked example, breaking the abstraction wall.

## Other feedback addressed

- Reader translations (`::: {.remark}` with bold `**Reader translation.**`) after the major definitions:
  probability space, random variable, variance/covariance, conditional expectation, independence,
  conditional independence (causal-ignorability story), MGF, Poisson binomial, normal, multivariate normal.
- "Why this matters" remarks tying load-bearing theorems to regression/NMA/ITC after: linearity (why we
  prove it; IPW), tower property (identification, ML-NMR estimand), total variance (hospital-count
  example), graphoid axioms (propensity-score reduction, overlap), Jensen (non-collapsibility),
  Cauchy-Schwarz (MAIC ESS), Fubini-Tonelli (nested averages), covariance PSD (NMA likelihoods),
  conditional MVN (ML-NMR population averaging).
- Jargon glossed in line at first use: `\bigsqcup` (disjoint union), measurable space and the `S'` prime
  (label, not derivative), pushforward, Borel set, `\sigma(X)`, version, `L^1`/`L^2`, "almost surely / a.s.",
  the `\uparrow` arrow, indicator `1_A` / `1{X=x}`, dyadic approximation, generalized inverse / quantile
  function, sigma-finite, Schur complement, and the `N(mu,sigma^2)` variance vs `N_p(mu,Sigma)` covariance
  convention. A "field guide" vocabulary table up front collects the worst offenders.
- Tables added (plain Markdown, not labeled `tbl-` so no caption/cross-ref machinery is needed):
  (1) measure-theory vocabulary field guide; (2) "six words for one random quantity" comparing event,
  random variable, law, CDF, density, expectation (ChatGPT explicit request); (3) the graphoid axiom
  roadmap.
- Radon-Nikodym paragraph softened ("a deep theorem we cite and never use the internals of; take existence
  on faith"), per GLM 9.
- ESS bound spelled out as an explicit instance of Cauchy-Schwarz under the empirical measure (states the
  probability space, the two random variables, and the rearrangement), per GLM.
- Proof steps expanded, never cut: the supporting-line lemma now writes out both displayed inequalities;
  the MGF differentiation derives the constant `C = 1/(e(r''-r'))`; the De Morgan step is glossed; the
  conditional-MVN `U ⊥ X_2` step is annotated as the one place normality is used.
- Limsup/liminf of sets glossed as "occurs infinitely often / for all but finitely many" right where the
  closure lemma introduces them (GLM); concrete countable-union example ("eventually relapses") added.
- Change-of-variables identity now states in words "we never look at Omega again."
- A reading-orientation note added to the introduction: read translations and why-this-matters notes,
  treat the graphoid and MGF-moment proofs as optional on a first pass; links the notation chapter via
  `[Notation](/notation.qmd)`.
- Exercises: added the one-line `$\star$ = solution in Appendix F` convention; prepended four accessible
  warm-up/interpretation/computation exercises (`@exr-reweight-strata`, `@exr-jensen-logit-interpret`,
  `@exr-ignorability-meaning`, `@exr-pobin-count`) before the existing proof-heavy and starred ones.

## New labels introduced (all globally unique; checked against the whole book)

- Section: `sec-prob-running-example`.
- Examples: `exm-toy-trial`, `exm-cond-exp-strata`, `exm-jensen-logit`, `exm-mvn-mini`,
  `exm-graphoid-binary`.
- Exercises: `exr-reweight-strata`, `exr-jensen-logit-interpret`, `exr-ignorability-meaning`,
  `exr-pobin-count`.

No new `eq-` labels; the new display equations inside examples are unlabeled by design.

## Deliberately NOT changed (with rationale)

- The graphoid proof was not shortened or moved to an appendix despite both reviewers asking, because the
  revision contract forbids deleting/shortening proofs. The reader burden is reduced by signpost + table +
  example + post-proof gloss instead.
- Section order kept as MGF -> core distributions -> multivariate normal. GLM suggested moving
  `@sec-distributions` earlier; the current order is the logically necessary one (MGFs are needed to state
  the distributions' MGFs; the univariate normal is needed for the MVN) and reordering risks the build, so
  I added a transition sentence flagging the change of gear rather than reordering.
- `S'` for the target sigma-algebra was glossed, not renamed, to avoid introducing a symbol that conflicts
  with or diverges from `notation.qmd`.
- The MGF subscript is kept unbolded (`M_X`) even for vector `X`, matching the literal `notation.qmd`
  entry, with a one-line clarifying note in the def-mgf reader translation. See proposal below.

## Proposals for the orchestrator (do NOT edit notation.qmd from here)

These symbols are now glossed in-chapter but would be worth folding into `notation.qmd` for book-wide
consistency, since other foundation chapters use them too:

- `\bigsqcup` — disjoint (pairwise non-overlapping) union.
- `\uparrow` (as in `X_n \uparrow X`) — monotone increase to a limit.
- `L^1`, `L^2` — spaces of integrable and square-integrable random variables.
- "a.s. / almost surely" — with probability one (outside a set of measure zero).
- `1_A`, `1{X=x}` — indicator of an event.
- `(\mathcal{S}, \mathcal{S}')` — measurable space; consider documenting the prime so the careful reader
  is not surprised, or switching the book-wide convention to a non-prime label.
- MGF notation: `notation.qmd` writes `M_X(\mathbf{t})` with an unbolded subscript even when `X` is a
  vector, which is inconsistent with the global bold-vector convention (Convention 1). The chapter follows
  the literal notation entry; the orchestrator may wish to reconcile by bolding to `M_{\mathbf{X}}`
  everywhere, or by documenting the exception.

No new bibliography keys were introduced; the chapter still cites only `@billingsley1995`, `@williams1991`,
`@hernan2020whatif`, `@bingham2010regression`. (As noted in `logs/log-ch04.md`, `@billingsley1995` and
`@williams1991` still need to be merged into `references.bib` before the PDF render; that gap is unchanged
by this revision.)
