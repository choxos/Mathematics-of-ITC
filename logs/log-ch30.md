# Work log: Chapter 30 — Machine-Checked Foundations: The Coq Formalization

## Scope and character

Documentary chapter (Part VI) describing the companion **ITC_Coq** Coq/Rocq formalization. Per the
authoring brief, this chapter does not reprove the mathematics (Chapters 9-19 do that); it describes
accurately what the `theories/` files contain, what a proof assistant certifies and what it does not,
and maps the book's tagged theorems to their Coq lemmas. Two reference items are defined and owned by
this chapter.

## Slugs defined (owned)

- `def-coq-proof-status` — the five proof-status tiers F / P / S / O / E (adapted from the catalogue
  status legend in `proofs/00_coverage_matrix.md`).
- `def-active-axioms` — the three active classical axioms inherited from mathcomp-analysis `boolp`
  (propositional extensionality, dependent functional extensionality, constructive indefinite
  description), plus the no-project-axioms / no-admissions statement.

Other new labels introduced (all namespaced, chapter-internal): sections `sec-coq-intro`,
`sec-coq-guarantees`, `sec-coq-status`, `sec-coq-axioms`, `sec-coq-structure` (+ `-foundations`,
`-core`, `-estimators`, `-methods`, `-bucher`), `sec-coq-boundary`, `sec-coq-map`, `sec-coq-worked`,
`sec-coq-build`, `sec-coq-scope`, `sec-coq-notes`, `sec-coq-exercises`; equations `eq-coq-dci`,
`eq-coq-ess`; example `exm-coq-ess-numeric`; exercises `exr-coq-ess-compute`, `exr-coq-read-statement`,
`exr-coq-status-tier`, `exr-coq-print-assumptions`, `exr-coq-discrete-vs-named` (★),
`exr-coq-faithfulness` (★).

Starred exercises for Appendix F: `exr-coq-discrete-vs-named`, `exr-coq-faithfulness`.

## Sources consulted and verified

All read directly from `~/Documents/GitHub/ITC_Coq/`:

- `manuscript/16_coq.md` — base draft / file-by-file walk-through (adapted and condensed here).
- `proofs/00_coverage_matrix.md` — source of the five-tier status legend (`def-coq-proof-status`).
- `theories/AXIOMS.md` — canonical assumption inventory; named-hypothesis table reproduced (compactly)
  in `sec-coq-boundary`.
- `theories/Axioms.v`, `_CoqProject`, `Makefile`, `README.md` — build config, dependency list, phase
  grouping.
- All 15 `.v` files read (or grepped for exact declaration names): `Axioms`, `BasicTypes`,
  `PotentialOutcomes`, `CausalAssumptions`, `ConditionalIndep`, `BalancingScore`, `PropensityScore`,
  `IPWEstimator`, `OutcomeRegression`, `DoublyRobust`, `MAIC`, `STC`, `Comparison`, `Bucher`,
  `EffectModifiers`. Every Coq name cited in the chapter (e.g. `ESS_upper_bound`, `cauchy_schwarz_ones`,
  `two_mul_le_sqr`, `bucher_unbiased`, `double_robustness`, `AIPW1_pointwise`, `STC_collapse_linear`,
  `not_EM_does_not_imply_not_PV`, `propensity_score_is_balancing`,
  `propensity_score_sufficiency_discrete`, `transfer_independence`, `mu1_IPW_unbiased`,
  `MAIC_variance_inflation_ge1`, `maic_weight_fn`/`maic_weight_pos`, `methods_agree_when_correct`) was
  confirmed against the source `Definition`/`Lemma`/`Theorem` lines.

## Machine verification actually run (not quoted)

The local toolchain is the Rocq Prover 9.1.0 (`/Users/choxos/.opam/default/bin/coqc`), and the
development's `.vo` objects are present and load. I ran, against the compiled tree
(`coqc -R theories ITC chk.v`):

- `Print Assumptions` on `ESS_upper_bound`, `cauchy_schwarz_ones`, `bucher_unbiased`,
  `not_EM_does_not_imply_not_PV`, `propensity_score_is_balancing`, `double_robustness`. **All six**
  report exactly the three `boolp` axioms (propositional_extensionality,
  functional_extensionality_dep, constructive_indefinite_description) and nothing else. The verbatim
  three-line output is reproduced in `sec-coq-worked` and is the basis for `def-active-axioms`.
- Inventory greps: `grep -nE "Admitted" theories/*.v` → none; `^Axiom` → none; `admit\.` → none.
  15 `.v` files; ~137 `Theorem`/`Lemma`/`Corollary`/`Proposition` declarations.

So the chapter's axiom-closure and "zero admissions / zero project axioms" claims are verified on this
machine, not merely taken from `AXIOMS.md`.

## Catalogue identifiers referenced

D.2/D.3 (Bucher), B.6/B.7/B.8/B.9 (g-formula, IPW tower, OR identification, DR mean-zero residual),
A.4/A.5/A.6 (expectation linearity/total/L2 Jensen), E.1/E.2/E.6/E.7 (EM/PV), F.3 (MAIC weights),
F.8 (ESS bound), F.6/G.5/G.6 (MAIC/STC consistency, comparison). The chapter's mapping table tags each
book result with its Coq object and a two-level status reading.

## Accuracy decisions (things I was careful NOT to overclaim)

- `@thm-stc-noncollapsibility-counterexample`: the Coq tree does **not** formalize a non-collapsibility
  counterexample. What is machine-checked is the complementary positive result `STC_collapse_linear`
  (collapsibility of the linear model). Mapped as "complement F" with an explicit note; the nonlinear
  counterexample is paper-only.
- `@thm-maic-stc-equivalence`: not formalized as the linear-model equivalence; the closest Coq object is
  the abstract `methods_agree_when_correct` (Comparison.v). Mapped as tier S with a note.
- `@thm-maic-exponential-weights`: only the weight form and positivity (`maic_weight_fn`,
  `maic_weight_pos`) are formalized; the KKT/duality derivation is paper-only (tier P).
- IPW/G-comp/AIPW unbiasedness: presented as "fully proved Coq objects" but tier **P** *as
  formalizations* because the probabilistic step is a named premise (B.6-B.9). The two-level reading is
  spelled out in `def-coq-proof-status` and `sec-coq-boundary`.
- Excluded middle is stated as a derived lemma (Diaconescu), not a fourth axiom; confirmed by the
  Print Assumptions runs (classical case analyses add no axiom).
- Build requirements: I reported the versions declared in `_CoqProject`/`README` (Coq/Rocq ≥ 9.1,
  mathcomp-ssreflect ≥ 2.0, mathcomp-analysis ≥ 1.9, Hierarchy Builder ≥ 1.6) and noted the actual
  check used Rocq 9.1.0. NB: `manuscript/16_coq.md` says analysis ≥ 1.13, which disagrees with the
  build files; I followed the build files as authoritative. Flag for the harmony pass.

## Cross-references used (all confirmed against the slug map / references.bib)

Sibling slugs @-referenced: `@thm-jensen`, `@thm-cramer-rao`, `@thm-mle-asymptotic-normality`,
`@def-sandwich-variance`, `@def-non-collapsibility`, `@thm-ipw-unbiased`, `@thm-aipw-double-robust`,
`@def-effect-modifier`, `@def-prognostic-variable`, `@def-collapsibility`, `@def-transportability`,
`@thm-sema-insufficient`, `@thm-bucher-unbiased`, `@def-sema`, `@thm-unanchored-paic-consistency`,
`@thm-maic-ess-bound`, `@thm-maic-exponential-weights`, `@thm-stc-noncollapsibility-counterexample`,
`@thm-maic-stc-equivalence`, `@thm-aggregation`, `@thm-aggregation-bias`, `@thm-koksma-hlawka`,
`@def-gaussian-copula`, `@def-spfa`, `@thm-pseudo-ipd-reconstruction`. Part VI siblings (Ch 27, 28, 29)
referred to in prose only (their slugs are being authored in this wave). Bib keys cited (all present in
`references.bib`): `@phillippo2019thesis`, `@hernan2020whatif`, `@rosenbaum1983`, `@robins1994`,
`@bangrobins2005`, `@bucher1997`, `@signorovitch2010maic`, `@caro2010stc`.

## Proposed bibliography additions (could not edit references.bib)

The ITC_Coq development and the tools are cited in prose; no bibtex key exists for them. Suggested
entries for the orchestrator to merge if a formal citation is wanted:

- `itccoq` — @misc{itccoq, title={ITC_Coq: Formal Proofs of Indirect Treatment Comparisons},
  author={Chandler, Christopher}, year={2026}, howpublished={\url{https://github.com/choxos/ITC_Coq}},
  note={GPL-3 licensed Coq/Rocq development}}. (Author/year is my best inference from the repo
  README's citation block; please confirm.)
- `rocqprover` — @misc{rocqprover, title={The Rocq Prover (Coq)}, author={{The Rocq Development Team}},
  year={2025}, howpublished={\url{https://rocq-prover.org}}}.
- `mathcompanalysis` — @misc{mathcompanalysis, title={Mathematical Components Analysis Library
  (mathcomp-analysis)}, author={{The MathComp-Analysis Development Team}},
  howpublished={\url{https://github.com/math-comp/analysis}}}.

If these are added, replace the in-prose mentions in `sec-coq-notes` (and the ITC_Coq mentions
throughout) with the corresponding `@key`. Until then the prose citations stand and are sufficient.

## Proposed notation additions

None. The chapter reuses `$\mathbb{E}$`, `ESS`, MAIC/STC/IPW/AIPW abbreviations, and the
`[machine-checked: ...]` tag convention already defined in `notation.qmd`. Coq identifiers are set in
monospace and are clearly distinguished from book notation; no new mathematical symbol was introduced.

## Style/compliance checks performed

- American English; no dash punctuation as connector/parenthetical (verified by grep; only matches are
  `->` and subtraction inside Coq code blocks). Table "not applicable" cells use `n/a`, not an em dash.
- Quarto grammar: `def`/`exm`/`exr` divs with `## Name` headers; equations labeled `{#eq-...}`;
  `[Notation](/notation.qmd)` plain link used (not `@sec-notation`).
- Stub callout dropped; YAML `title` preserved.
- Structure: motivating intro; full development; worked example with hand-checkable numbers
  (`exm-coq-ess-numeric`, plus the verbatim `Print Assumptions` output); Notes and references;
  Exercises (6, two starred).

## Gaps / items for the harmony pass

1. The analysis-library version discrepancy noted above (`_CoqProject` 1.9 vs `manuscript/16_coq.md`
   1.13).
2. If the orchestrator wants `[machine-checked: ...]` tags added in the *home* chapters for the results
   this chapter maps (Ch 10 IPW/AIPW, Ch 14 Bucher, Ch 18 ESS, Ch 19 STC/EM-PV), the confirmed
   file+name pairs are in the `sec-coq-map` table and can be lifted directly.
3. ITC_Coq author/year for the proposed `itccoq` bib entry should be confirmed (README citation block
   lists Phillippo 2019 and Chandler & Ishak posters but does not state the repository's own
   author/year explicitly).
