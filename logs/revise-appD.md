# Revision log: Appendix D — Special Functions for Numerical Integration

File: `appendices/D-special-functions.qmd`. Kind: proved. Agent: Opus 4.8 revision pass.
Line count before: 845. Line count after: 1088.

## Scope of pass

Addressed BOTH reviewers (`feedback/chatgpt/appendix-D-special-functions.md`,
`feedback/glm/appendix-D-special-functions.md`), prioritizing each reviewer's "highest-priority fixes."
Applied Section 10 accessibility requirements as they fit a proved reference appendix: reader translations,
jargon glosses, navigability tables, bridge/intuition text before hard machinery, reproducible numeric
instances, and cross-links back to the consuming chapters. Every existing theorem, lemma, proof, definition,
example, equation label, and remark preserved; nothing cut or shortened. No Exercises section exists in this
appendix, so no star-convention line or warm-up exercises were added (correct per instructions).

## New labeled environments and tables

- `## How to use this appendix {#sec-sf-guide}` — NEW section (heading with blank line before). Contains:
  - Scope note (acknowledges gamma/digamma/beta/log-gamma are out of scope and points to Chapters 21, 25).
  - **Master "where each function is used" table** (function | section | feeds chapter+result | what it does).
  - A concrete AgD/health motivating task that anchors the whole appendix, plus a difficulty roadmap.
- `::: {#exm-sf-digital-2d}` — NEW worked example: a four-point (0,2,2)-net in two dimensions with explicit
  generating matrices `C_1=I_2`, `C_2=[[1,1],[0,1]]`, the four points, and a box-by-box balance check.
  Numerics verified by hand (points `(0,0),(1/2,1/2),(1/4,3/4),(3/4,1/4)`; all three box shapes hold one point).
- **Health-statistics erf task table** inside a new `.remark` in @sec-sf-erf (task -> function used).

Only two new cross-referenceable labels added: `#sec-sf-guide`, `#exm-sf-digital-2d`. Both ids unique
across the book. Several unlabeled `.remark` divs and inline "*Reader's translation.*" / "*Roadmap for the
proof.*" / "*Why ...*" paragraphs were added as scaffolding (not cross-referenced, so no label collision).

## Reviewer points addressed

ChatGPT highest-priority:
1. Bridge before Owen's T and the bivariate identity — added a "picture / purpose / analytic signpost"
   bridge BEFORE `def-owens-t`; added a "why differentiate in rho" bridge before `lem-bivariate-normal-pde`;
   added a proof roadmap before `thm-owens-t-identity`.
2. Why erf/erfc/erf^{-1} matter for Chapter 22 Phi/Phi^{-1} — added pipeline paragraph in the erf opener
   (every Sobol' node passes through Phi^{-1} = sqrt(2) erf^{-1}(2u-1)) plus the health task table.
3. "What to retain vs what software handles" before the Sobol' generating-matrix algebra — added.
4. Chapter 25 cross-links (same QMC machinery integrates general likelihood kernels) — added in the Sobol'
   "what to retain" paragraph and reinforced in the closing rank remark (survival h^delta S, ordinal probs).
5. Reproducible numeric instances — erf: Phi(1.96) from erf(1.3859)=0.9500 and the 1-Phi(10)~7.6e-24 tail
   underflow example; Owen's T: Simpson's rule on the definition integral (and `sn::T.Owen`) reproduces
   T(0.3536,0.5774)=0.0778.

GLM highest-priority / suggestions:
1/11. Scope mismatch and missing gamma/digamma/beta/log-gamma — added an explicit scope note (not a rename;
   see skipped items) acknowledging absence and pointing to Chapters 21, 25.
2. "Where each function is used" table — added (master table in @sec-sf-guide).
3. Intuition-first — added bridge/picture/roadmap paragraphs before the hard definitions and proofs.
5. MGF motivation — added a paragraph: differentiating k times at 0 gives the k-th moment (name), but we use
   it at t=1 because the log link makes the aggregate mean literally E[e^W]; explains why log link is the
   closed-form case.
6. "Complete the square" — spelled out the full expansion in the MGF proof.
7. Asymptotic vs convergent — added a `.remark` interlude after `prp-erf-expansions` (convergent improves
   forever; asymptotic improves to the smallest term then worsens; truncate at the smallest term).
8. Domain-connection per section — health task table (erf), probit-second-moment purpose (Owen's T),
   why-QMC and Chapter 25 integrands (Sobol'), AgD anchor (guide).
10. QMC jargon — inline glosses added: F_2 (field with two elements, addition is XOR), radix point (base-b
    decimal point), direction numbers, primitive polynomial, star discrepancy; (t,m,s)-net already glossed
    in-statement.
12. Softened differentiate-in-rho proof — roadmap remark before the proof with the checkpoint
    1+a(rho)^2 = 2/(1+rho).
GLM specifics also fixed: expit synonym (logistic sigmoid) note; "(positive semidefinite)" gloss on
Sigma >= 0; explicit Sigma^{1/2} symmetric with Sigma^{1/2}Sigma^{1/2}=Sigma line; Mills ratio defined as
(1-Phi)/phi plus the ~ notation glossed; scale-mixture clarified (motivation for the shape only, w(s) never
needed, numbers come from Taylor matching not quadrature); two-probit solution flagged as a numerical
construction (nonlinear system, Newton seed, unique up to label swap); expected-squared-probit roadmap
("square, condition, correlate"); why probit needs the second moment (binomial variance p(1-p)); why QMC up
front (N^{-1/2} vs (log N)^d/N).

Reader translations added after: `thm-normal-mgf`, `def-error-function`, `def-radical-inverse`; plus applied
"where used / where not" remark after `thm-owens-t-identity`, and a "two error scales" remark after
`exm-sf-probit-logit`.

## Mathematical errors fixed

None. The reviewers flagged no incorrect proved identity or worked solution; their concerns were pedagogical
and about reproducibility. I independently recomputed the load-bearing numerics and all are correct as
printed: erf(1.96/sqrt2)=0.9500 so Phi(1.96)=0.9750; 1-Phi(10)=7.62e-24; T(0.3536,0.5774)=0.0778;
E[Phi(0.5+Z)^2]=0.4826 and Phi(0.3536)=0.6382; one-probit J(0.5,1)=0.6047, two-probit=0.6021 (printed 0.6022,
within display rounding, left untouched). No numeric value in any existing example was changed.

## Deliberately skipped (with reason)

- Actual diagrams/plots (ChatGPT "figures", GLM suggestion 4): not added. pdflatex build safety and the fact
  that figure assets are out of scope for a text revision; replaced with detailed verbal geometry (the Owen
  wedge, the radical-inverse digit reflection, the 2D-net box listing). Both reviewers stated a figure is
  "not necessary" if a geometric description is given.
- Physical reordering of the Owen's T section (GLM suggestion 9): not done as a move, to preserve the exact
  order and integrity of every labeled div. Achieved the "meaning first" goal by inserting the wedge picture
  and purpose BEFORE `def-owens-t` instead.
- Retitling the appendix / adding a full gamma-digamma-beta-log-gamma catalog (GLM suggestion 1): not done.
  Adding brand-new proved sections on unrelated functions exceeds the "preserve every result; add
  scaffolding" remit and would introduce unreviewed mathematics; the YAML title was left unchanged to avoid
  any cross-reference/running-head churn. Instead an explicit scope note names the gap and where those
  functions actually arise (Chapters 21, 25 likelihood normalizers).

## Labels I was tempted to touch but PRESERVED

Considered relabeling `thm-normal-mgf`/`eq-sf-normal-mgf` region while reformatting the MGF motivation, and
considered folding the general-Owen-reduction remark; preserved both untouched. No `#thm-`, `#lem-`, `#def-`,
`#eq-`, `#prp-`, `#cor-`, `#sec-` id, no `phillippo2016tsd18` citation, and no `theories/*.v` pointer was
renamed or removed. (Appendix D carries no machine-checked tag; the Notes section states none is claimed, and
that statement was preserved.)

## Build-safety verification (ran locally, orchestrator renders)

- Dash punctuation: 0 occurrences of em/en dash or spaced-hyphen connector.
- Non-ASCII characters in the file: 0.
- Div fences balanced: 44 openers / 44 closers.
- No bare `align`/`equation`/`gather` inside `$$...$$`; new displays use `pmatrix`/`smallmatrix`/plain.
- No unicode star; no `\not` on an extensible arrow.
- All 56 labels resolve; every original label present; +2 new unique ids.
