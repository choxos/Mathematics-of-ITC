# Revision log: Chapter 28, Quantitative Bias Analysis for ITC

File: `chapters/part6/28-qba.qmd`. Before/after line count: **930 to 1430** (+500).
Revision pass under STYLE.md Section 10 (pedagogical accessibility) and Section 11 (PDF build safety).

## Running example introduced (single highest-value addition)

`#exm-qba-running`: an unanchored **COPD** comparison. New inhaled therapy $B$ versus published comparator
$A$; binary outcome *severe exacerbation within 12 months* (a bad event, so RR below 1 favors $B$);
reported covariate $x_R$ = standardized age; unreported covariate $u$ = baseline $\mathrm{FEV}_1$ (in
liters, prognostic). Headline: adjusted $\mathrm{RR}=0.50$ ($95\%$ CI $0.30$ to $0.81$). The numbers are
exactly those of the existing Section 6 worked example ($\beta_0=-1.0,\beta_R=0.4,\beta_U=-0.5$,
$m_R=1.0,\sigma_R=0.5,\mu_0=0.47,\bar x_U=2.0,\sigma_U=1.0$), so the example threads coherently:
introduced in the intro, previewed at each instrument ($E\approx3.44$; $E_{\mathrm{ITC}}=+\infty$;
$m^{\dagger}=0.6$; prior $\mathcal{N}(2.0,0.3^2)$), computed in full in `#sec-qba-example` (now named COPD).

## ChatGPT reviewer, highest-priority fixes (all addressed)

1. **E (exposure) vs E-value clash.** Renamed the exposure random variable $E\to A$ (and arm index
   $e\to a$: $f_a,q_a,p_a,r_a$) throughout `#lem-qba-confounding-factor` and the `#sec-qba-evalue` setup.
   Kept the literature-standard subscripts $\mathrm{RR}_{EU},\mathrm{RR}_{UD}$ but added an explicit gloss
   (subscript letters name roles: $E$=exposure/treatment, $U$=covariate, $D$=disease; distinct from italic
   E-value $E$ and expectation $\mathbb{E}$) plus a glossary-table row. Verified zero stray exposure $E$.
2. **Bridge classical->ITC.** New translation table at the top of `#sec-qba-itc-evalue`
   (exposure->trial membership, $\mathrm{RR}_{UD}$->IPD-estimable outcome association, etc.).
3. **Clarify $\mathrm{BF}_{\mathrm{obs}}$.** New preamble before `#def-itc-evalue` (RR $0.50$ needs a
   factor $2.0$ to reach the null; "held at IPD value" = plug-in distribution) and a three-case remark.
4. **Practical workflow.** New `### {#sec-qba-workflow}`: 8 applied steps.
5. **NORTA intuition + correlation-borrowing as a substantive assumption.** New nontechnical intro before
   `#thm-norta-copula` (defines "margin" and "dependence" in plain terms) and a strengthened binary-$U$
   remark (borrowing is an assumption; redo under alternative correlation matrices).
6. **Worked example NORTA.** Section 6 independence now explicitly labeled; added `#exm-qba-norta-correlated`,
   a closed-form correlated NORTA computation (Spearman $-0.3$ -> $\rho^N=-0.313$ -> adjusted RR moves
   $0.497\to0.512$), hand-checkable.
7. **Ranges/priors guidance.** New prior-choice remark after `#def-probabilistic-bias-analysis` (normal
   centered at IPD, Beta from elicited interval, registries) plus workflow step 4.
8. **Applied exercises.** Three warm-up/interpretation exercises added (see below) with a star-convention
   line at the top of `#sec-qba-exercises`.

## GLM reviewer, highest-priority suggestions (addressed, with one correction)

- **Restructure around the example / QBA-in-one-screen table / HTA framing to front:** done (new HTA
  opening paragraph; roadmap table; running example early; per-instrument pointers).
- **Disambiguate E + glossary (crude/adj/obs/true, EU/UD):** glossary table in `#sec-qba-workflow` region.
- **Expand the bias triangle:** new `### {#sec-qba-other-corners}` with selection (`#eq-qba-selection-factor`)
  and misclassification (`#eq-qba-misclass-correction`) corrections, cited to `@lash2021qba`.
- **Scale-specificity of the E-value:** new remark + outcome-scale conversion table (OR rare/common, HR,
  RD/RMST) before `#sec-qba-itc-evalue`.
- **Soften jargon:** "Galois inequality" reworded to "the defining equivalence of a generalized inverse"
  (cross-ref kept); "effect-on-the-exposed standardization" glossed; $EU$/$UD$ subscripts spelled out.
- **Proof-gap fills the reviewer flagged:** added $q_a(1)/q_a(0)=\mathrm{RR}_{UD}$ line; spelled out the
  "ratio of affine functions is monotone, so max over a box is at a vertex" clause; wrote out the $g'(b)$
  cancellation explicitly; added the $v\ge1$ reminder in `#thm-evalue-derivation` Part 2; added the
  common-$\mathbf{Z}$ coupling intuition before `#prp-qba-tipping-monotone`.

### Deliberately adapted / skipped (with reasons)

- **GLM #7, corollary "$E_{\mathrm{ITC}}\ge E$ always":** the reviewer's claim is **mathematically false**
  (as $\mathrm{RR}_{UD}=y\to\infty$, $E_{\mathrm{ITC}}=\rho(y-1)/(y-\rho)\to\rho<E$). I instead added the
  **correct** result `#cor-itc-evalue-monotone` (with proof): $E_{\mathrm{ITC}}(y)$ is strictly decreasing,
  crosses the symmetric $E$ exactly at $y=E$, exceeds it for $y<E$ and is below it for $y>E$. A companion
  remark explains that "sharper" means "better calibrated," not "always larger."
- **GLM #5, a rendered contour figure of $\mathrm{BF}_U(x,y)$:** skipped as an image (cannot add and verify
  a TikZ/matplotlib figure without rendering, and rendering is the orchestrator's job; a bad figure risks
  the pdflatex build). Replaced the pedagogy with a worked numeric instance ($\mathrm{RR}_{EU}=2$,
  $\mathrm{RR}_{UD}=3\Rightarrow\mathrm{BF}_U=1.5$) in the "A number to hold onto" remark and the
  sensitivity table in Section 6.

## New labeled environments and tables (only additions; nothing renamed/removed)

Environments: `#exm-qba-running`, `#exm-qba-norta-correlated`, `#cor-itc-evalue-monotone`,
`#eq-qba-selection-factor`, `#eq-qba-misclass-correction`, `#sec-qba-workflow`, `#sec-qba-other-corners`,
`#exr-qba-interpret-evalue`, `#exr-qba-tipping-plausible`, `#exr-qba-hta-writeup`. All checked unique.

Tables (6, all new): (1) prior-method contrast; (2) five-instrument roadmap; (3) crude/adj/obs/true and
subscript glossary; (4) E-value scale-conversion; (5) classical-confounding to ITC translation;
(6) Section 6 sensitivity sweep ($m$, $\Delta(m)$, RR, verdict).

Intuition remarks added: 13 new `::: {.remark}` (reader translations after most definitions/theorems);
6 original remarks preserved (total 19). "Why this matters" ties to regression/NMA/ITC: E-value remark
(HTA/clinician scale), sharpness remark (exact threshold in practice), three-case + corollary remarks
(dossier claim), PBA remark (NMA random-effects analogy), NORTA translation (workflow role).

## Hard constraints verified

- All **42 original labels preserved** (script-checked: `#thm-/#lem-/#def-/#eq-/#prp-/#cor-/#sec-/#exr-/#exm-`).
- All **8 original proofs preserved in full** (proof-div count 8->9, the one new proof being the corollary);
  edits to `#lem-qba-confounding-factor` and `#lem-qba-sharp-bound` proofs only ADD clarifying lines.
- No `[machine-checked: ...]` tags exist in this chapter (Notes confirms no Coq counterpart); none to touch.
- **Zero non-ASCII characters** in the file (Python scan); no em/en dash, no spaced-hyphen connector, no
  double-hyphen connector; `$\star$` used for the star marker; no bare `align`/`gather`/`equation` inside
  `$$`; all 6 tables column-consistent; every real `#sec-` heading has a blank line before it (the `##`
  titles flagged by the scan are div titles inside `::: {#...}`, the standard STYLE.md grammar).
- No new `@bibkey` citations introduced (Cario/Nelson, Nelsen, Schlesselman, Kruskal, Ren named in prose
  only); `@lash2021qba`, `@vanderweele2017evalue`, `@sklar1959` and all cross-chapter refs unchanged.
- No `@phillippo2016tsd` without the `18` suffix present (chapter does not cite it).
