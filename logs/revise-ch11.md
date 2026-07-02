# Revision log: Chapter 11 (Effect Modification, Interaction, and Collapsibility)

Target reader: novice health researcher with weak mathematics. Both feedback files addressed
(`feedback/chatgpt/ch11-...md` and `feedback/glm/ch11-...md`), prioritizing each reviewer's
highest-priority fixes. All existing labels, theorems, and full proofs preserved; only scaffolding,
intuition, tables, examples, signposts, and warm-up exercises were added, plus proof *expansions* (no
proof was shortened or deleted).

## Highest-priority fixes (both reviewers) and how they were addressed

ChatGPT highest-priority:
1. Plain-language bridge after conditional/marginal definitions with a small "average-then-transform vs
   transform-then-average" numeric example. Done: the order-of-operations idea now appears BEFORE the two
   definitions (two-paths table in `#sec-emcoll-cond-marg`), each definition has a *Reader translation*, a
   notation->plain-meaning table follows `@def-marginal-effect`, and a numeric preview
   ($\log 4.5-\log 6=-0.288$) follows `@lem-emcoll-gap`.
2. Early scale table linking identity/log/logit/log-hazard to RD/RR/OR/HR. Done: new subsection
   `#sec-emcoll-running` with a four-row effect-measure/link/contrast/outcome-range table at first mention
   of $g$; GLM's request for the outcome range is included.
3. Novice-facing summary box distinguishing the five ideas in one place. Done: new "Reader's map: five
   ideas, kept apart" remark in the intro, with a five-term table, a two-question procedure, and the four
   "never conflate" pairs.
4. Prognostic-variable table ambiguity ("not prognostic" = neither arm; EM may be prognostic for only one
   arm). Done: table columns relabeled "prognostic for both" / "prognostic for neither arm," a strict
   reading stated, numeric instances added to every cell, and a new bridge paragraph before
   `@prp-emcoll-em-implies-pv`/`@thm-emcoll-em-pv-distinct` resolves the apparent contradiction (one-arm
   cases live outside the two columns).
5. Intuitive numeric OR non-collapsibility example before the change-of-measure proof. Done: new remark
   "The odds-ratio phenomenon before the proof" ($6\to 4.5$) precedes `@thm-noncollapsibility-or-hr`.
6. At least one low-entry interpretation/classification exercise. Done: added `@exr-emcoll-interpret`
   (interpretation), `@exr-emcoll-order-ops` (warm-up), `@exr-emcoll-classify` (four-table classification,
   exactly the exercise ChatGPT suggested), all before the proof-heavy exercises.

GLM highest-priority (numbered suggestions 1-12):
1. Worked example earlier / numeric preview after the gap lemma. Done: the worked example is now the tail
   of a *running* example introduced at the start (`@exm-emcoll-teaser`, same four risks), forward-pointed
   from the intro and reused at every transition; a 6-vs-4.5 preview and the $-0.288$ gap appear early.
2. "Why this matters" callout at the start of each section in ITC vocabulary. Done: every major section
   (`cond-marg`, `em-interaction`, `pv`, `collapse`, `synthesis`, plus the running subsection) opens with
   an italic *Why this matters (ITC).* line tying to Bucher/NMA/MAIC/STC.
3. Expand `@lem-emcoll-gap` proof term by term + one-line Jensen statement first. Done: added a "Jensen's
   inequality, in one line" remark before the lemma; proof now writes both estimands, the linearity split,
   and an `\underbrace` regrouping into $J_g(\mu_b)-J_g(\mu_a)$; $J_g$ named the "Jensen gap."
4. Break the OR non-collapsibility proof into labeled steps with plain reweighting before Radon-Nikodym.
   Done: proof (a) now has Step 1 (setup) / Step 2 (reweighting) / Step 3 (covariance) / Step 4 (bounds),
   each with a "What we showed" line; the tilt is introduced as "positive weights that sum to one" before
   the Radon-Nikodym phrase; the covariance identity is stated explicitly.
5. Small link-function table at first mention of $g$. Done (see ChatGPT 2).
6. Promote "Non-collapsibility is not confounding." Done: stated plainly and early in the Reader's map
   ("One warning") with a forward pointer; the original well-written remark is kept in place unchanged.
7. Name SEMA and SPFA where the assumption first appears. Done: named in the `#sec-emcoll-pv` opener and
   again after `@lem-emcoll-anchored-cancellation`, with forward reference to Chapter 12 and to Notation.
8. Add a diagram and an HR-vs-time figure. Partially: rendered the "transform-then-average vs
   average-then-transform" commutative square as a two-paths Markdown table (no image, because the book
   builds with pdflatex and figures were out of scope); the HR-over-time shape is given in prose
   (frailty-selection paragraph) and in `@exr-emcoll-hr-limits`. See "Deliberately left / deviations."
9. Standardize $\mu_t^{\mathcal P}(x)$ vs $\mu_t(x)$. Done: intro states the superscript is kept only when
   several populations are in play and dropped within a fixed population.
10. Concrete two-population example for population-dependent EM status. Done: new
    `@exm-emcoll-pop-dependent` (same means, support of $X$ changed).
11. Reword `@thm-emcoll-em-pv-distinct` Part 1 to commit to one construction. Done: committed to the
    pencil construction ($0.3,0.7$); the "or simply take two distinct values" hedge removed; the Coq
    construction moved into a clean parenthetical.
12. Reorder `#sec-emcoll-pv` to lead with the slogan and anchored/unanchored consequence. Done: the
    section now opens with the balancing rule and SEMA/SPFA before any algebra (labels kept in place so
    cross-references are unaffected).

## Other "unclear / under-explained" points addressed

- "Commute with averaging" glossed in the intro. `@def-effect-modifier`, `@def-prognostic-variable`,
  `@def-collapsibility` each gained a *Reader translation*; the collapsibility one gives the exact
  "does the constant survive averaging? vs does a varying effect average correctly?" contrast both
  reviewers wanted.
- "Affine" glossed as "linear plus a constant" in `@lem-emcoll-gap`.
- Dual notation $\tau^g$ / $\psi_g$ / $\psi_g^{\mathrm M}$ reconciled with an explicit note.
- `@lem-emcoll-interaction` proof: cancellation written out, dot product glossed, held-fixed reasoning
  spelled out; a *Why this matters* ties it to NMR/ML-NMR.
- Applied-language paragraph on "when is a nonzero interaction effect modification?" added.
- `@prp-emcoll-scale` numbers framed clinically (younger low-risk vs older high-risk, constant +0.1);
  a *Reader translation* answers "is it wrong to call age an effect modifier?".
- `@prp-emcoll-em-implies-pv` proof: the four evaluations of $g$ written out.
- `@lem-emcoll-anchored-cancellation`: plain A-vs-C / B-vs-C network picture added before it; proof sets
  up $f(x,w)=f(w\mid x)f_X(x)$ and states $\int f(w\mid x)\,dw=1$ explicitly.
- `@prp-emcoll-rr`: mechanism explained in words (why collapsible but not directly collapsible).
- Hazard proof (b): clinical reading of the strata (early vs advanced disease), $\bar S_t$ derived from
  $e^{-hu}$, the marginal hazard $-\bar S'/\bar S$ explained (minus sign, survival-weighted average), and
  a frailty-selection paragraph explains the time drift.
- `@cor-emcoll-or-attenuation`: degeneracy clause expanded ("baseline odds identical for every patient").
- Synthesis-table lead-in reworded to remove the phantom "EM-status scale dependent" column reference; it
  now states the table is only about collapsibility.
- `@prp-emcoll-orthogonal` combination 3: OR arithmetic ($0.60/0.40$ over $0.25/0.75 = 4.5$) shown inline.
- Worked example headed with a pointer back to the running example and a $\mu_0/\mu_1$ reminder.
- Footnote on first `$\blacktriangleleft$` explains both end-marks ($\blacktriangleleft$ and $\square$).
- Exercises section states the $\star$ convention in one line (starred = full solution in Appendix F);
  `@exr-emcoll-or-attenuation` opener clarified so its task (the monotonicity route) is unambiguous
  relative to the theorem's covariance proof.

## New labeled environments added (all slugs verified unique across the book)

- `#sec-emcoll-running` (new subsection under the intro)
- `#exm-emcoll-teaser` (the running trial; same four risks as `@exm-emcoll-worked`)
- `#exm-emcoll-pop-dependent` (population-dependence of EM status)
- `#exr-emcoll-interpret`, `#exr-emcoll-order-ops`, `#exr-emcoll-classify` (three unstarred warm-ups)

## Tables added (Markdown)

- Effect-measure / link / contrast / outcome-range table (`#sec-emcoll-running`).
- Reader's-map five-term table (intro remark).
- Two-paths (commutative-square) table (`#sec-emcoll-cond-marg`).
- Notation->plain-meaning table after `@def-marginal-effect`.
- Numeric instances filled into the four-cell EM/PV table (`#sec-emcoll-pv`).
- Four-table classification grid inside `@exr-emcoll-classify`.

## Deliberately left unchanged / deviations

- Every existing theorem, lemma, proposition, corollary, definition, equation, and exercise LABEL is
  preserved (44 originals, each once; verified). No proof was cut; proofs (a) of
  `@thm-noncollapsibility-or-hr`, `@lem-emcoll-gap`, `@lem-emcoll-interaction`,
  `@prp-emcoll-em-implies-pv`, `@lem-emcoll-anchored-cancellation`, and the hazard proof were only
  expanded.
- The two starred exercises `@exr-emcoll-or-attenuation` and `@exr-emcoll-anchored-unanchored` keep their
  labels and `($\star$)` marks and their (a)/(b) structure, so the existing Appendix F solutions stay in
  sync (I did not edit Appendix F). Only a clarifying clause was added to the OR one.
- The two machine-checked tags in `@thm-emcoll-em-pv-distinct` and `@lem-emcoll-anchored-cancellation`
  were kept verbatim.
- The existing "Non-collapsibility is not confounding" remark was kept in place (well written; reviewers
  liked it); it is now also previewed early rather than moved, to avoid disturbing surrounding text.
- No figures/images were added (GLM suggestion 8): the book builds with pdflatex and image assets were out
  of scope. The requested commutative-square "diagram" is rendered as the two-paths table, and the HR(u)
  behavior is conveyed in the new frailty paragraph plus `@exr-emcoll-hr-limits`.

## Citations / bibliography

- No new `\cite` keys used. Only bibtex keys already in `references.bib` are cited
  (`@dias2018nma`, `@hernan2020whatif`, `@chandler2026transport`, `@phillippo2019thesis`).
- The existing Notes section already flags two out-of-bib historical sources for the orchestrator
  (Greenland-Robins-Pearl 1999; Gail et al. 1984). I did not add them to `references.bib`; they remain
  prose mentions. No further bib additions are proposed by this revision.
- No new notation symbols were introduced; the chapter reuses the `notation.qmd` scheme (including the
  $\mu_t^{\mathcal P}$ vs $\mu_t$ convention, which is now stated explicitly, and SEMA/SPFA, which are now
  named in text).

## Build-safety verification performed

- Pure ASCII in math (Python scan: 0 non-ASCII lines); `$\star$` everywhere, no Unicode star.
- No em/en dash or spaced double-hyphen used as connector (all "spaced hyphen" hits are math minus signs).
- No bare `align`/`equation`/`gather` inside `$$`; brace balance 461/461; `$$` count even (90);
  `:::` divs balanced (44/44); every real section heading has a preceding blank line; the `#eq-...` label
  stayed attached to its display after the proof restage.
- `pandoc -f markdown -t latex` parses the file with exit 0 and no warnings.
- All cross-reference targets used exist in the book (`@thm-jensen`, `@def-link-function`,
  `@def-non-collapsibility`, `@thm-bucher-unbiased`, `@thm-sema-insufficient`,
  `@thm-collapsible-transport`, `@thm-scale-alignment`, `@thm-failure-of-bucher`, etc.).
