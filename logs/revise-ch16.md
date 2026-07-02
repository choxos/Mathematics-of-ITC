# Revision log: Chapter 16, The Limits of Standard Network Meta-Analysis

File revised: `chapters/part3/16-limits-of-nma.qmd`
Feedback addressed: `feedback/chatgpt/ch16-limits-of-nma.md` and `feedback/glm/ch16-limits-of-nma.md`
(both reviewers read as novice health researchers; both "highest-priority fixes" lists were prioritized).

## Summary of approach

The chapter kept all of its rigor: every existing theorem, lemma, corollary, proposition, definition,
example, exercise, equation label, and proof is preserved verbatim or lightly augmented (never shortened
or deleted). All additions are scaffolding: a concrete running example, reader translations, why-matters
lines, jargon signposts, tables, a binary special case, interleaved worked examples, and warm-up
exercises. Chapter grew from ~5.5k to ~10.8k words; no mathematics removed.

## Highest-priority fixes (ChatGPT reviewer)

1. **Concrete health example before the first definition.** Added `@exm-limits-psoriasis` (running
   example): plaque psoriasis, two biologics A and B versus standard care C, effect modifier = prior
   biologic exposure, two trials with different exposure prevalences, target = decision population. It
   states plainly why the shared comparator C does not make the trials exchangeable, and carries the exact
   stratum risks reused in `@exm-limits-bucher-rd`. Reused at each transition.
2. **Estimand and sign-convention table.** Added a **Sign convention** remark early (B relative to A;
   positive risk difference means B worse; lowercase `b` is a bias not treatment B) and a four-row
   **estimand roadmap table** before `@thm-failure-of-bucher` covering `d_{ab(P)}`, `\tilde d_{ab(P)}`,
   `\Delta^{Cond,g}_{AB}(P*)`, `d_AB^Bucher` with columns notation / plain meaning / estimated from / why
   it matters. Added a "no tilde = marginal, tilde = average-conditional" mnemonic and a "where g sits"
   table after `@def-conditional-marginal-contrast`.
3. **Binary-covariate bias before the general integral theorem.** Added proposition
   `@prp-limits-binary-bias` (new) with new equation `@eq-limits-binary-bias`: bias =
   s_AC(p_AC - p*) - s_BC(p_BC - p*), where s_tC is the effect-modification jump. Self-contained proof
   (no forward reference to `@eq-limits-bias`), plus a one-line numeric preview using the psoriasis
   numbers giving -0.06.
4. **Ecological-bias section rebuilt around the failed cure.** Added a bridge paragraph ("the analyst's
   temptation") and a mini aggregate-meta-regression table (trial mean vs trial contrast, slope 0.19)
   that explicitly distinguishes `b_2` (between-trial slope) from `\beta_2` (within-patient interaction)
   BEFORE the probit theorem. Split the coefficient-level ecological bias into its own display equation
   `@eq-limits-coef-eb` inside `@def-ecological-bias`. Added a symbol-map table before
   `@thm-ecological-norecovery`.
5. **Stronger bridge to population adjustment.** `@sec-limits-gap` now opens with the explicit diagnosis
   ("standard NMA averages the wrong conditional effects over the wrong populations"), adds a **What a
   valid indirect comparison must compute** checklist remark, and gives each of MAIC/STC/ML-NMR an
   explicit "Data needed" clause.

## Highest-priority / key items (GLM reviewer)

- **Clinical scenario threaded throughout:** `@exm-limits-psoriasis`, reused in the two-constancies
  section, `@prp-limits-binary-bias`, `@exm-limits-bucher-rd`, and the warm-up exercise.
- **HTA stakes stated:** sign reversal -> wrong reimbursement decision -> NICE TSD 18 (`@phillippo2016tsd18`),
  in the running example.
- **Two key remarks promoted to warnings:** "Warning: the standard error cannot see this bias" and
  "Warning: in the anchored triangle this bias is untestable" now lead with bold **Warning** headers.
  (Used `.remark` blocks with bold leads rather than Quarto callouts: no chapter or appendix in this book
  uses callouts; the only callouts in the repo are in an unrelated reference copy under `documentation/`.
  Kept build-safe per STYLE Section 11. Flagged for possible book-wide callout adoption later.)
- **Worked examples interleaved:** `@exm-limits-bucher-rd` moved to immediately follow the
  failure-of-Bucher discussion inside `@sec-limits-failure-bucher`; `@exm-limits-probit-eco` moved to
  immediately follow `@thm-ecological-norecovery` inside `@sec-limits-ecological`. `#sec-limits-example`
  is preserved as a repurposed synthesis section ("Reading the two failures side by side") with a
  comparison table (label kept, not removed).
- **Disambiguated the two d symbols:** explicit mnemonic + estimand table (did NOT rename, since
  `notation.qmd` lists `d_{ab(P)}`; renaming would conflict with the single source of truth). Noted
  `\tilde d` and `\Delta^{Cond,g}` as proposed notation additions.
- **Non-collapsibility surcharge expanded into a subsection** `#sec-limits-surcharge` (new sec id) with a
  pure-form numeric OR illustration (constant conditional OR = 3, balanced covariate, marginal OR = 7/3)
  and a two-problems table (imbalance bias vs surcharge). Fixed the stale "subject of the next section"
  forward reference.
- **PV-vs-EM table** added next to `@cor-limits-pv-no-bias`, plus a plain-English paragraph on why a
  contrast cancels equal arm shifts.
- **Fubini and measure-zero steps spelled out:** the `W`-integration interchange in
  `@cor-limits-pv-no-bias` is now named as Fubini with its justification; the strict-inequality argument
  in `@thm-ecological-norecovery` now states that a single point has Lebesgue measure zero, and the
  `h'(rho)` numerator simplification `(1+rho^2 sigma^2) - rho^2 sigma^2 = 1` gets its intermediate line.
- **Jargon softened / signposted:** a **Terms carried from earlier chapters** glossary remark defines
  contrast, anchored comparison, effect modifier vs prognostic variable, transitivity/consistency,
  node-splitting, heterogeneity, link/inverse link (logistic and Phi), directly collapsible, and affine.
  "affine" also glossed inline at first use in `@lem-limits-aggregation-jensen`. Standardized
  "pointwise additivity (sometimes called conditional additivity)".
- **SEMA clarified:** conditional constancy is identified with the shared effect modifier assumption
  (`@phillippo2016tsd18`) in the two-constancies section and the added constancy-contrast table.
- **Phi(t) = P(U <= t)** stated explicitly at the top of the `@lem-limits-probit-integral` proof.
- **Jensen applied to eta_t(X), not X**, is now flagged in a reader translation, with the plain sentence
  "the average of the patients' risks is not the risk of the average patient" and a one-line numeric
  check E[Phi(0.5 + X)] = 0.638 vs plug-in 0.691.
- **"same Jensen gap" remark promoted to a labeled proposition** `@prp-limits-eco-noncollapse` with a
  short proof (ecological bias = non-collapsibility of the slope). The original remark content is kept as
  elaborating remarks (constant-term twin).
- **Exercises:** added the `$\star$` -> Appendix F note at the top; added two accessible exercises
  (`@exr-limits-identify-em` warm-up tied to the running example, `@exr-limits-interpret-se`
  interpretation about narrow CIs). Labeled every exercise by type (Warm-up / Interpretation /
  Computation / Proof / Challenge), reordered easy-to-hard, and added hints to the harder ones
  (`@exr-limits-logit-compound`, `@exr-limits-zero-bias-trap`, `@exr-limits-general-attenuation`).

## New labels added (none renamed, none removed)

- `#sec-limits-running` (section: A running clinical example)
- `#exm-limits-psoriasis` (running example)
- `#prp-limits-binary-bias`, `#eq-limits-binary-bias` (binary special case)
- `#sec-limits-surcharge` (subsection: The non-collapsibility surcharge)
- `#eq-limits-coef-eb` (coefficient-level ecological bias display)
- `#prp-limits-eco-noncollapse` (ecological bias = non-collapsibility)
- `#exr-limits-identify-em`, `#exr-limits-interpret-se` (warm-up / interpretation exercises)

## Left unchanged (deliberately)

- Every original label (37 of them) verified present and unique; the machine-checked tag on
  `@cor-limits-pv-no-bias` (`theories/EffectModifiers.v`, `anchored_PV_cancellation`) is intact.
- All proofs preserved; only additive clarifying lines were inserted (no proof shortened).
- The YAML title is unchanged.
- Did not rename `d_{ab(P)}` / `\tilde d_{ab(P)}` / `\Delta^{Cond,g}` (would conflict with `notation.qmd`).
- Did not add any new machine-checked tags (no new Coq counterpart confirmed).

## Proposed notation additions (for the orchestrator to fold into `notation.qmd`)

- `\tilde d_{ab(\mathcal P)}`: average-conditional relative effect of b vs a in population P on scale g.
- `\Delta^{\mathrm{Cond},g}_{AB}(\mathcal P^{*})`: target average-conditional A-vs-B contrast in the
  decision population.
- `s_{tC}` (local to Ch 16): effect-modification jump on a binary covariate,
  tau^g_{tC}(1) - tau^g_{tC}(0).
- `\mathrm{EB}_{\mathrm{coef}} = b_2 - \beta_2`: ecological bias of the effect-modification coefficient.

## New sources

None. All citations use existing bibtex keys (`phillippo2016tsd18`, `phillippo2020mlnmr`,
`phillippo2019thesis`, `chandler2026transport`), each verified present in `references.bib`.

## Build-safety checks run (all pass)

- Pure ASCII in the whole file (no Unicode in math or prose); `$\star$` used, no Unicode star.
- No bare `align`/`equation`/`gather`/`eqnarray`; multi-line displays use `aligned`.
- No `\not` on extensible arrows.
- `$$` delimiters balanced (94, even); `:::` divs balanced (42 open / 42 close).
- Every section heading preceded by a blank line; every div-title heading (15) sits directly after its
  `::: {#...}` opener.
- All cross-references resolve (24 external targets confirmed in `chapters/`/`notation.qmd`; all internal
  targets defined in-file). No dash punctuation used as a connector; American English throughout.
- `[Notation](/notation.qmd)` link used (not `@sec-notation`).
