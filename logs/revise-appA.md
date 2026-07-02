# Revision log: Appendix A, Notation Glossary

File: `appendices/A-notation-glossary.qmd`
Before: 366 lines. After: 526 lines. Net +160.
Kind: reference glossary. Accessibility target here is navigability and completeness, not narrative.

## Reviewer points addressed

### ChatGPT (highest-priority fixes)
1. Concrete anchored ITC notation example: added `## A worked notation key: one anchored comparison`
   (`#sec-gloss-worked-key`, table `#tbl-gloss-worked-key`) mapping $j$, $i$, $\mathbf{x}_i$,
   $\mathcal{P}^{*}$, $\hat d_{ab(j)}$, $d_{AB(\mathcal{P}^{*})}$, and the Bucher step onto an
   $AC$-versus-$BC$ comparison. Note: framed as a compact reference key, not a narrative running
   example (scope rule), and corrected to the proper anchored triangle ($AC$ + $BC$ sharing $C$),
   since ChatGPT's literal "AB trial and BC trial" is not an anchored setup.
2. Chapter names for orientation: added a chapter legend table (`#tbl-gloss-chapters`) mapping every
   chapter number to its subject and Part. Chose a legend over inline names in the ~90 symbol rows and
   ~160 term rows to avoid PDF table-column overflow and 250 transcription points; the legend decodes
   "Ch. 14" as "Bucher indirect comparison" for both the Introduced and Defined-in columns at once.
3. Compact novice key for overloaded notation: added `## A compact key to the conventions`
   (`#sec-gloss-conventions`) covering bold-vector vs scalar, capital RV vs lowercase realization, the
   $X/x/\mathbf{x}/\mathcal{X}$ family, and the $i,j,k,a,b,c$ index roles; plus a full
   `## Overloaded symbols at a glance` table (`#tbl-gloss-overloaded`) for $\perp$, $\Pi$, $S$, ESS,
   $\tau$, $\mu$, $\sigma$, $\boldsymbol{\beta}$, $\alpha$, $d$ vs $\delta$, $D$.
4. Marginal-vs-conditional and link-vs-outcome bridge: added `## A note on effect scales`
   (`#sec-gloss-scales`) stating both distinctions plainly and warning OR/RR/RD/HR are not
   interchangeable.
5. See-also links among ITC concepts: added `## Finding related terms: clusters by role`
   (`#sec-gloss-clusters`, table `#tbl-gloss-clusters`) grouping the defined terms into 12 role
   clusters (causal foundations, effect modification and scale, evidence synthesis, transportability
   and population adjustment, MAIC/STC/ML-NMR/ML-UMR, Bayesian and computation, etc.), with the
   core-ITC clusters flagged. Also added a `## How to use this appendix` (`#sec-gloss-howto`) orientation
   section.

### GLM (suggestions and unclear items)
1. Missing Bayesian and computation symbols: added new subsection `### Bayesian computation and model
   comparison` (`#sec-gloss-bayes`, table `#tbl-gloss-bayes`) between inference and causal, covering
   $\pi(\boldsymbol{\xi})$, $\pi(\boldsymbol{\xi}\mid\mathbf{y})$, $p(\mathbf{y}\mid\boldsymbol{\xi})$,
   $\Pi$, $\tau^2$, $\hat R$, $N_{\mathrm{eff}}$, $\bar D$/$D(\bar{\boldsymbol{\theta}})$/$p_D$,
   $\mathrm{lppd}$/$\widehat{\mathrm{elpd}}$, WAIC/LOO, PSIS/$\widehat k$. Symbol forms verified against
   Chapters 8, 15, 24 (MCMC ESS is $N_{\mathrm{eff}}$ with a capital N; PSIS tail index is $\widehat k$).
2. One-line plain-language gloss per symbol row: added a second clause to the terse rows across the
   linear algebra, regression, probability, inference, causal, studies, outcome, and adjustment tables
   (for example $A\succeq 0$, $\lambda_i/\sigma_i$, $\mathcal{C}/\mathcal{N}$, $P_{\mathcal{M}}$,
   $M_X$, the convergence arrows, the order symbols, $H$, $e(x)$, $w_i$, $C_\Omega$, $\boldsymbol{\xi}$).
3. Flag glyph collisions: done via `#tbl-gloss-overloaded` plus inline notes on the $\perp$, $S$, and
   ESS rows.
4. Restore detail dropped from `notation.qmd`: re-added the explicit norm formula
   $\lVert\mathbf{x}\rVert_2=\sqrt{\mathbf{x}^\top\mathbf{x}}$, "generalized inverse (quantile)" for
   $F_X^{-1}$, and "on a stated scale" for $d_{ab(\mathcal{P})}$.
5. Paraphrase jargon in alphabetical entries: glossed "natural parameter" (Canonical link),
   "dispersion" (Exponential dispersion family), "measurable function" (Random variable and its law),
   "$\sigma$-algebra" (Probability space), and "idempotent" (Orthogonal projection matrix).
6. Group the term glossary: delivered via the role-cluster index (`#tbl-gloss-clusters`) placed before
   the alphabetical table, rather than physically splitting the alphabetical table (which would risk
   the ordering the appendix advertises); every existing row and slug is kept.
7. Worked mini-examples in rows: added concrete cues, e.g. $\mathbf{e}_1=(1,0,\dots,0)^\top$, "$e(x)=0.3$
   means 30 percent of patients with covariates $x$ were treated", and $\hat{\mathbf{y}}=H\mathbf{y}$.
8. How-to paragraph: added (`#sec-gloss-howto`), explaining symbol table vs term table vs the slug.

## Reviewer asks deliberately skipped or redirected (with reason)
- Per-row difficulty/priority marker on the 160-row alphabetical table (ChatGPT and GLM): not added as a
  column (noisy, 160 fragile edits); the same signal is delivered by the role-cluster index, which flags
  the core-ITC clusters. Kept the alphabetical table intact.
- Inline chapter names in every Introduced/Defined-in cell (ChatGPT #2): redirected to the chapter
  legend table to protect the PDF build (column-width overflow) and avoid transcription risk.
- Mirroring the new Bayesian symbols into `notation.qmd` (GLM #1): out of my file scope (file
  discipline). RECOMMENDATION FOR ORCHESTRATOR: add a "Bayesian computation" section to `notation.qmd`
  mirroring `#tbl-gloss-bayes` ($\pi$, $\Pi$, $\tau^2$, $\hat R$, $N_{\mathrm{eff}}$, $\bar D$, $p_D$,
  lppd, elpd, WAIC, LOO, PSIS, $\widehat k$).
- $\kappa^2$ (GLM wish-list item): omitted from the Bayesian table. Verified it is not a durable
  book-wide symbol; it appears only as a local prior variance in one Chapter 15 DIC exercise
  ($\theta\sim\mathcal N(0,\kappa^2)$). Including it as core notation would misrepresent it.

## Reviewer-flagged error checked / corrected
- GLM claimed $\Pi$ is "the permutation group in the determinant formula (Ch. 3)." Verified against
  `chapters/part1/03-linear-algebra-iii.qmd`: the determinant there is developed via $\det(A-\lambda I)$
  and the characteristic polynomial, not a $\Pi$ permutation sum. I therefore did NOT assert that
  meaning; the overloaded-$\Pi$ row lists only the two verified meanings (prior measure, Ch. 8; coupling
  set, Ch. 27). This prevents introducing a false claim.
- No proved identity or worked solution exists in this appendix, so no mathematics was rewritten; the
  fixes were restorations of dropped `notation.qmd` detail and faithful symbol forms.

## New labeled environments and tables added (all globally unique, verified)
Sections: `#sec-gloss-howto`, `#sec-gloss-conventions`, `#sec-gloss-worked-key`, `#sec-gloss-overloaded`,
`#sec-gloss-scales`, `#sec-gloss-bayes`, `#sec-gloss-clusters`.
Tables: `#tbl-gloss-chapters`, `#tbl-gloss-worked-key`, `#tbl-gloss-overloaded`, `#tbl-gloss-bayes`,
`#tbl-gloss-clusters`.

## Preservation confirmed
- All 10 original `#tbl-gloss-*` ids kept (linalg, regression, probability, inference, causal, studies,
  outcome, adjustment, abbrev, terms); all 12 original `#sec-gloss-*` ids kept.
- All 158 backticked `@def-*` slug pointers kept; every existing glossary row kept (only cell text
  enriched on the five jargon rows).
- No `[machine-checked: ...]` tags exist in this appendix (0), so none were touched.
- Every existing symbol-table row retained; new rows only added (the Bayesian table).

## Build-safety verification
- ASCII-only in math mode confirmed; the sole non-ASCII byte is the pre-existing "Cramér" (prose, not
  math), which Section 11 permits.
- No em dash, en dash, spaced hyphen, or double hyphen used as a connector.
- Blank line before every heading; every table caption followed by a blank line (checked with awk).
- No `$$` display blocks added, so no bare `align`/`equation`/`gather` risk; no `\not` on extensible
  arrows; no code in math mode.
- Cross-reference discipline: `@def-*` pointers stay backticked literal text (the appendix convention,
  zero live-ref breakage); only intra-appendix `@sec-gloss-*` and `@tbl-gloss-*` are live, and each
  target id is defined exactly once (verified). Appendix A is a numbered chapter, and other appendices
  already use live `@sec-`/`@tbl-` refs, so the pattern builds.
- `@phillippo2016tsd18` is already correct throughout the book; this appendix does not cite it, so no
  fix was needed.
