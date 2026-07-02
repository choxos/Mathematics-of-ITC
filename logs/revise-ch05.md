# Revision log: Chapter 05, Statistical Inference

Pedagogical-accessibility revision per reviewer feedback in `feedback/chatgpt/ch05-inference.md` and
`feedback/glm/ch05-inference.md`. Target reader: novice health researcher with weak mathematics. All
edits are additive: no existing theorem, proof, definition, equation, or label was removed or renamed.
File grew from 1329 to 1868 lines.

## Constraints honored

- All 70 pre-existing labels verified present after the edit (every `#thm-/#lem-/#cor-/#prp-/#def-/#eq-/#sec-/#exm-/#exr-`).
- Every theorem and full proof preserved; intuition was added only as new sentences inside proofs (never deleting math) and as new `.remark` blocks around them.
- PDF safety re-checked: no Unicode `star` (uses `$\star$`); no `\not` on an extensible arrow; no bare `align/equation/gather` (the one new multiline display uses `aligned`); `$$` count even (136); div fences balanced (97/97); code fences even (4); only non-ASCII are the accented names already in the file (Cramer, Hajek) and all are in prose, none in math. The two ASCII figures are fenced code blocks (render verbatim in pdflatex).
- American English; no dash punctuation as connector (all `" - "` hits are math subtraction; only `--` is the YAML delimiter).
- Notation chapter linked as `[Notation](/notation.qmd)` (added in the new O_p/o_p remark). No `@sec-notation`.
- No new `#sec-` ids introduced (still 12); new structure uses `.remark` blocks and `exm-/exr-` divs only, so no risk of cross-file `#sec-` collision.
- Only existing bibtex keys cited (`@bingham2010regression` reused; no new citations invented). Chapter references kept as plain "Chapter N" text, matching existing convention.

## Highest-priority fixes (both reviewers) and how they were addressed

1. **Thread the Bernoulli/binary example through the chapter (ChatGPT #1, GLM #2).** Added an early running
   example `@exm-running-trial` (n=25, 10 responders, with a patient-level table) immediately after the
   intro, and reused it at every transition: as the estimator p-hat after `@def-estimator`; as the
   log-likelihood after `@def-likelihood`; as the Bernoulli score (with mean-zero check) after
   `@lem-score-mean-zero`; as I(p)=1/[p(1-p)] after `@def-fisher-information`; as I vs I_n numbers after
   `@cor-information-additivity`; as p-hat -> p after `@thm-mle-consistency`; as sqrt(n)(p-hat-p) ->
   N(0,p(1-p)) after `@thm-mle-asymptotic-normality`. The end worked example now opens with a sentence
   pointing back to where each piece already appeared.
2. **Plain-language intuition for score/Hessian/Fisher info/inverse-info SE before the formal proofs
   (ChatGPT #2, GLM #6).** Added "Reader translation" remarks after `@def-statistical-model`,
   `@def-estimator`, `@def-consistent-estimator`, `@def-likelihood`, `@def-score`, `@def-regular-model`,
   `@def-fisher-information`, `@def-mle`, `@def-m-estimator`, `@def-test-statistics`, and a sandwich
   "Reader translation, with a picture". Added "What this means" after `@lem-score-mean-zero` and "Why
   this matters" duality paragraph after `@thm-information-equality`.
3. **Bridge paragraphs after CMT, Slutsky, delta method, MLE asymptotic normality, Wilks (ChatGPT #3,
   GLM #6).** Added "Why this matters" remarks (with one-line examples) after `@thm-continuous-mapping`
   (X-bar^2 -> mu^2), `@thm-slutsky` (z/t ratio), `@thm-delta-method` (effect-measure SEs),
   `@thm-mle-asymptotic-normality` (the estimate +/- 1.96 SE statement, with the slope/curvature picture),
   and `@thm-wilks` (parabola). Also after `@prp-bias-variance-decomposition`, `@thm-cramer-rao`,
   `@cor-mle-efficient`, `@thm-m-estimator-normal`.
4. **Per-observation vs sample information (ChatGPT #4, GLM notation).** New titled remark + two-row table
   after `@cor-information-additivity` giving I, I_n=nI, Var(theta-hat) ~ I_n^{-1} = I^{-1}/n, with the
   Bernoulli numbers, and an explicit warning about the common factor-of-n slip. Also added a roadmap
   table early (preview of score, MLE, per-obs and sample info, observed info, inverse info, each with
   "Defined in").
5. **Strengthen health/ITC examples in delta method, M-estimation, sandwich, tests, exercises (ChatGPT
   #5, GLM #3).** New `@exm-delta-logodds` (numeric log-odds SE) and `@exm-indirect-bucher` (full toy
   Bucher indirect comparison of log odds ratios with delta-method SEs, variances adding across
   independent trials, OR-scale interval) placed in the asymptotic-tools section (previously had zero
   examples). Expanded the sandwich-to-MAIC remark to two paragraphs with the explicit MAIC balancing
   estimating equation and the misspecified working model. Added health-flavored exercises (see below).

## Other GLM "what was unclear" items addressed (in proofs, additively)

- `@def-statistical-model`: glossed "sigma-finite dominating measure" and "injective/identifiable" with a
  concrete non-identifiable example (mu = alpha*beta); distinguished "true parameter" (correct model) from
  "target" (estimating equation), with forward pointer to `@sec-m-estimation`.
- `@prp-bias-variance-decomposition`: the shrunken-mean arithmetic (bias = -mu/(n+1) -> 0, variance -> 0)
  is now shown, not just named (GLM "missing examples").
- `@thm-continuous-mapping` proof (ii): added the subsequence-trick intuition sentence.
- `@thm-slutsky` proof: spelled out the good-event/bad-event split that yields the
  2||h||_inf P(...) bound.
- `@thm-delta-method` proof: justified ||Z_n|| = O_p(1) and the o_p*O_p product via the new O_p/o_p
  remark.
- New `.remark` "The O_p and o_p shorthand": defines O_p(1), o_p(1) and the three calculus rules used
  silently in the delta-method and Wilks proofs (GLM notation, suggestion #5).
- `@def-regular-model`: one-paragraph "what R1-R4 are for" translation (smooth curve, tame tails, locally
  pinned-down parameter), with the Uniform(0,theta) signpost to `@exr-information-equality-fail`.
- `@lem-score-mean-zero` proof: explained why (R1) matters (support does not move, no boundary term).
- `@thm-information-equality` proof: glossed "quotient rule for gradients" (vector version; read one
  component at a time) and defined Hessian = matrix of second partials.
- `@thm-mle-asymptotic-normality` Step 2: explained the integral remainder as componentwise FTC on the
  gradient field (mean-value remainder analogue). Expanded the "Estimating the asymptotic variance"
  remark with when observed vs expected information differ and what software prints as a "standard error".
- `@thm-cramer-rao`: defined the general Loewner order A >= B with its variance-in-every-direction
  reading; in the proof, explained why the vector (v, -I^{-1}v) is chosen (cancels cross terms = Schur
  complement).
- `@thm-m-estimator-normal`: rewrote the local-uniform-law hypothesis in symbols, parallel to (A3); added
  the gloss A^{-T} = (A^{-1})^T = (A^T)^{-1}.
- `@def-sandwich-variance`: ASCII bread/meat/bread schematic and the bread = sensitivity / meat =
  variability reading; "bread"/"meat" defused as mnemonic nicknames in a new remark after
  `@thm-m-estimator-normal`.
- `@thm-wilks` LR part: spelled out that both averaged Hessians converge to the same I.
- Confidence-interval-by-inversion remark: added the "sweep null values, keep the non-rejected ones"
  scalar recipe.
- `@prp-mle-invariance`: explained why it is called the "profile" likelihood (maximize out nuisances,
  trace a ridge).

## Missing-motivation items addressed (section openers)

- `@sec-asymptotic-tools`: new "Why this section, and why now" opener motivating the delta method via the
  log odds ratio, naming it the most-used result, and acknowledging the ordering.
- `@sec-consistency`: "Why prove this?" opener (NMA/MAIC stop being systematically wrong).
- `@sec-cramer-rao`: "Why a lower bound matters for indirect comparisons" opener (optimality yardstick).
- `@sec-tests`: which test to report in health applications, plus a three-test comparison table.
- Efficiency (`@def-efficient-estimator`/`@cor-mle-efficient`): "not leaving precision on the table"
  reassurance.

## Tables added (Markdown)

1. Roadmap / notation-role table of the key quantities (early, after the "one picture").
2. Running-example patient-level data table.
3. Per-observation vs sample information table (after `@cor-information-additivity`).
4. Three-test comparison table (Wald / score / LR: what is evaluated, MLE needed?, null fit needed?,
   intuitive question) in `@sec-tests`.
5. Two-trial 2x2 data table in `@exm-indirect-bucher`.

## Figures added (ASCII, fenced code blocks; pdflatex-safe)

- The promised "one picture": log-likelihood curve with score = slope-zero at the peak and curvature =
  information (GLM suggestion #1, "make the promised picture real"). Chose ASCII over TikZ because TikZ is
  not loaded in the pdflatex template and `_quarto.yml` may not be edited.
- The sandwich schematic A^{-1} B A^{-T} = bread/meat/bread.

## Exercises

- Added a one-line note at the top of `@sec-exercises`: a starred ($\star$) exercise has a full solution
  in Appendix F, and the first warm-up is solved inline.
- New accessible exercises before the proof-heavy ones:
  - `@exr-warmup-2x2` (warm-up, fully solved inline): log odds and CI from one arm (GLM #10; ChatGPT
    "compute a CI for a log odds, transform to OR scale").
  - `@exr-interpret-information` (warm-up/interpretation): where a proportion is hardest to estimate; a
    sample-size feel.
  - `@exr-indirect-se` (interpretation): the cost of going indirect, tied to `@exm-indirect-bucher`.
- Existing exercises (`@exr-poisson-mle` ... `@exr-delta-multivariate`) kept verbatim, in order, after
  the new warm-ups; the starred ones still say "(Solution in Appendix F.)".

## New labels added (all `exm-`/`exr-`, none collide)

`#exm-running-trial`, `#exm-delta-logodds`, `#exm-indirect-bucher`, `#exr-warmup-2x2`,
`#exr-interpret-information`, `#exr-indirect-se`.

## Proposed additions to notation.qmd (NOT edited here; for orchestrator)

These were defined inline on first use in this chapter; consider folding into `notation.qmd`:
- General Loewner order `A \succeq B` / `A \succ B` (the file currently lists only `A \succeq 0`).
- `A^{-\top}` for `(A^{-1})^\top = (A^\top)^{-1}`.
- `\sigma`-finite dominating measure `\nu` (currently absent from the inference table).
- A one-line reminder of the `O_p`, `o_p` calculus (rules), since the notation table only names them.
- Observed information `\mathbf J_n(\boldsymbol\theta) = -\nabla^2 \ell_n(\boldsymbol\theta)`.
- Profile likelihood symbol `L_n^{*}` (orphan symbol used only in `@prp-mle-invariance` and tests).

## Deliberately not changed

- **Section order kept.** Both reviewers flagged `@sec-asymptotic-tools` coming before any estimator.
  Rather than physically reorder labeled blocks (risking forward-reference and build breakage), I took the
  option both reviewers explicitly accept "at minimum": a strong motivating opener plus the early running
  example, so the reader meets a concrete estimator (p-hat) and the delta-method payoff before the tools.
  The tools must still be proved before they are used in the consistency/normality proofs.
- **No real figure (TikZ).** Used ASCII art instead, for pdflatex/build safety (cannot add `\usepackage`
  via `_quarto.yml`).
- All proof content, hypotheses, and numeric worked-example values left intact; the capstone
  `@exm-binomial-inference` and `@exm-sandwich-normal` retained at the end as reviewers praised them.
- Notes and references section left as is (already transparent about proved vs cited vs not
  machine-checked).
