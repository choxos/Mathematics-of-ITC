# Feedback: Chapter 19 — STC

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part4/19-stc.qmd`

## Overall impression

I came in hoping to understand what "simulated treatment comparison" actually does and why anyone would reach for it instead of MAIC. The chapter eventually answered both questions, but I had to read it twice and keep flipping back to Chapters 10, 11, 14, 16, and 17. The opening (@sec-stc-intro) is dense and front-loads a lot of cross-referenced machinery (Bucher, transitivity failure, non-collapsibility, conditional transportability, convex hull) before I have a single concrete trial in my head. The arc is clear in retrospect: set up the model, prove the MLE works, define the naive plug-in, show it is biased, fix it by integrating, prove that works, isolate non-collapsibility with an example, do a worked numerical example, add a Bayesian layer, fold in the Chapter 17 conditions, and reconcile with MAIC. But on first reading the chapter feels like it assumes I already understand why the plug-in is tempting and why it fails; the "why" arrives only after several pages of "what."

The worked example (@exm-stc-logistic) is the high point for me: three numbers I can check with a calculator, a clear contrast between biased plug-in and correct marginal, and a closing of the triangle via Bucher. If the rest of the chapter had that level of concreteness I would have been much less lost. The lowest point is the introduction and the theorem on MLE asymptotics, which both assume I am comfortable with a long chain of notation and references to earlier chapters that, honestly, I have only half-retained.

## What was unclear

- **The very first paragraph (@sec-stc-intro, lines 7-17).** "MAIC leaves the outcomes untouched and bends the *sample*... STC leaves the *sample* untouched and bends a *model*." I understand the symmetry the author is going for, but as a health researcher I do not have a crisp mental picture of "bending a sample" versus "bending a model." A one-sentence concrete gloss ("MAIC reweights patients so the weighted index population looks like the comparator; STC fits a regression on the index patients and asks that regression what it would predict for the comparator patients") would have saved me a reread.

- **"STC is the analogue of outcome regression, or g-computation, of Chapter 10 (@thm-g-computation-unbiased)" (line 15).** The link to g-computation is the conceptual backbone of the whole chapter and it is stated in a subordinate clause. If I do not remember Chapter 10 in detail, the rest of the chapter's framing ("dual routes to the same estimand," "transported g-computation") is opaque. I needed a two-sentence recap of what g-computation is before it was used as the central analogy.

- **"The bias that this corrects is the transitivity failure of Chapter 16" (lines 28-31).** This is the first mention of *why* we are doing any of this, and it is buried in a long sentence with a cross-reference. The clinical motivation (two trials enroll different patients, so a naive indirect comparison answers the right question in the wrong population) deserves its own short paragraph with a concrete drug pair, not a parenthetical.

- **"conditional transportability of the outcome surface (@thm-conditional-transportability), not on overlap" (lines 36).** Two big terms in one clause, neither defined here. I had to leave the chapter to find out what "transportability of the outcome surface" means operationally. A one-line definition ("the regression you fit in trial AC also describes how covariates drive outcomes in population BC") would keep me inside the chapter.

- **The orientation remark (@sec-stc-outcome-model, lines 111-122).** This sign-convention discussion confused me more than it helped. We have $\Lambda=\eta_A-\eta_C$ here, but Notation and Chapter 14 use $d_{AC}=\eta_C-\eta_A$, so "the marginal version of @eq-stc-cate-link enters Bucher's identity as $d_{AC}=-\Lambda$." I appreciate the honesty, but the remark then says "the overall sign is bookkeeping" and "it changes none of the bias, consistency, or non-collapsibility statements." If it changes nothing, why spend a remark on it before I have seen any theorem? I would move this to an aside after the worked example, where the sign actually shows up in numbers.

- **@eq-stc-loglik and the exponential-family notation (lines 126-143).** The notation $\vartheta_i$, $b(\vartheta_i)$, $a(\phi)$, $V(\mu)=b''(\vartheta)$, and the working weight $W_i=[a(\phi)V(\mu_i)g'(\mu_i)^2]^{-1}$ arrive in a single block with a citation to McCullagh & Nelder. For a reader with "basic calculus, weak math" this is a wall of symbols. I know what a GLM is loosely, but I could not reconstruct the score and information formulas myself. The chapter says "see @mccullagh1989glm, Chapter 2" but offers no worked intuition for why the score has that particular form (residual over variance times $g'$).

- **@thm-stc-outcome-mle and its proof (lines 145-227).** This is the most intimidating block in the chapter. The proof walks through identifiability, score mean zero, information equality, existence/consistency, and asymptotic normality, citing van der Vaart Theorem 5.9 and the M-estimation argument. I followed the words but could not fill in most steps. The sandwich-form remark (lines 229-241) introducing the pseudo-true parameter and misspecification is conceptually important for the chapter's punchline ("STC is only as good as its model") but is presented as a remark, so I almost skipped it. I think this remark deserves to be a stated corollary or at least a callout box, because it is the central vulnerability the chapter returns to.

- **@eq-stc-taylor (lines 314-318).** The second-order Taylor expansion giving $b_k=\tfrac12\mathbb E[(g^{-1})''(\xi_{k,X})(\boldsymbol\beta_{(k)}^\top(X-\bar{\mathbf x}))^2]$ is the technical heart of the bias theorem, and it is written as a single displayed equation with "for some $\xi_{k,X}$ between $\eta_k(X)$ and $\eta_k(\bar{\mathbf x}_{BC})$." I needed the preceding prose to say, in plain words: "the gap between the mean of the response and the response at the mean is, to second order, half the variance of the linear predictor times the curvature of the inverse link." That one sentence would have made the formula readable.

- **"the rate ratio and risk ratio are collapsible in exactly this sense (@def-collapsibility)" (lines 397-398).** This is the first time a health researcher sees the payoff of the log-link example, and it is tucked at the end. I would have liked an explicit clinical sentence: "for a count or rate outcome analyzed on the log link, conditional STC at the mean covariate is actually unbiased for the population rate ratio as long as there is no effect modification; this is a real, usable fact, and it is *not* true for the odds ratio."

- **The Bayesian section (@sec-stc-bayes, lines 724-803).** The functional $\Psi(\boldsymbol\xi)$ and the pushforward $\Psi_\#\pi(\cdot\mid\mathcal D)$ are advanced. "Pushforward" is not in the notation file. I gathered it means "the distribution of $\Psi$ when $\boldsymbol\xi$ has the posterior," but the term is used without definition. The Bernstein-von Mises theorem is cited but not characterized in words; I had to infer what "total variation convergence of the posterior to a Gaussian centered at the MLE" buys me.

## What wasn't elaborated enough

- **Why model outcomes instead of reweight?** The dual framing (MAIC = weighting, STC = outcome regression) is stated, but the *practical* reasons a health researcher would pick one over the other are scattered. Only much later (the "STC against MAIC, assumption for assumption" remark, lines 865-877) do I get the trade-off: STC needs a correct model, MAIC needs overlap. The chapter would be far more motivating if a short "when would you use STC?" paragraph appeared right after the introduction, pointing forward to the trade-off.

- **What exactly is "simulated"?** The name "simulated treatment comparison" implies a simulation, but the core estimator (@eq-stc-marg) is an integral. Only line 434-441 mentions Monte Carlo, and line 440 casually notes that when only AgD summaries are published "$f_{BC}$ is reconstructed from a parametric model, typically a Gaussian copula (Chapter 22)." For a beginner, the phrase "simulated" needs an early, concrete paragraph: "we cannot do the integral analytically for a logistic model, so we draw $M$ synthetic patients from the reconstructed comparator covariate distribution, plug each into the fitted model, and average. That averaging *is* the simulation." Right now the simulation aspect feels like an afterthought.

- **The MLE proof (@thm-stc-outcome-mle).** Each labeled sub-argument (identifiability, score mean zero, information, existence, asymptotic normality) is one paragraph. The asymptotic normality paragraph (lines 211-226) does the Taylor expansion, the CLT, the uniform LLN, Slutsky, and the sandwich-collapse in about 15 lines. This is too fast for the stated audience. At minimum, the step "$-n^{-1}\nabla\mathbf s_n(\tilde{\boldsymbol\xi})\xrightarrow{p}\mathbf M$" deserves a sentence saying this is the observed information converging to the Fisher information.

- **@prp-stc-gcomp and its proof (lines 447-468).** The proposition identifies marginal STC as transported g-computation, which is the conceptual climax of the method. But the proof is four lines and leans entirely on "by @thm-g-computation-unbiased" and the tower property. I would have liked an explicit two-step picture: (1) fit $\mu_k$ in trial AC, (2) use the *same* $\mu_k$ to predict in population BC. The transportability assumption is the bridge, and it deserves a sentence in its own right rather than a parenthetical cross-reference.

- **The anchored vs unanchored distinction in @thm-stc-consistency (lines 813-863).** The theorem states both cases, but the unanchored case is only sketched. As a health researcher I know anchored means "common comparator C" and unanchored means "no common comparator," but the *consequence* (unanchored needs every prognostic variable in the model, not just every effect modifier) is the clinically critical point and is buried in proof prose. A short remark before the theorem contrasting the two data scenarios with a concrete example (e.g., "A vs C trial and a B vs C trial: anchored; an A trial and a B trial with no shared arm: unanchored") would help.

- **The equivalence theorem and its proof (@thm-maic-stc-equivalence, lines 911-957).** The proof's MAIC side (lines 942-953) is the densest in the chapter. The tower-property step and the first-moment balance step are both one line each. I could not reconstruct why first-moment balance is enough without working it out on paper. An intermediate displayed line showing $\mathbb E_{P^\ast_k}[\alpha_k+X^\top\boldsymbol\beta_{(k)}]=\alpha_k+\bar{\mathbf x}_{BC}^\top\boldsymbol\beta_{(k)}$ would make the "same arm limit" claim transparent.

## Missing motivation / "why does this matter?"

- **Why prove the MLE theorem at all (G.1)?** The chapter is about STC, not about GLM asymptotics. The theorem is "Chapter 5 applied to the GLM," which is honest, but I never learned *why* I need the asymptotic normality result to do STC. The answer is presumably that the consistency of marginal STC (@thm-marginal-stc-unbiased) needs $\hat{\boldsymbol\xi}\xrightarrow{p}\boldsymbol\xi_0$, and the delta-method variance in @exr-stc-delta needs the asymptotic distribution. A sentence at the start of @sec-stc-outcome-model saying "we need the fitted coefficients to converge to the truth and to have a known limiting distribution, because every downstream STC estimator is a functional of them; here is the result that guarantees both" would frame the section.

- **Why is the plug-in the historical default?** @def-stc-conditional and line 246 say conditional STC is "the historically the original STC of @caro2010stc." But *why* did Caro propose the plug-in? Because it is one line of arithmetic and needs only the published mean $\bar{\mathbf x}_{BC}$, not the full covariate distribution. That practical reason (you often cannot get the covariance from a published paper) is the whole reason the plug-in exists, and it is never stated. Without it, the plug-in looks like a straw man.

- **Why does non-collapsibility matter for HTA?** The "A legitimate estimand for the wrong question" remark (lines 403-413) is good and almost says it, but I wanted an explicit HTA sentence: a cost-effectiveness model feeds in a single marginal effect and a population; if you hand it a conditional-at-the-mean effect you are silently evaluating the technology for a hypothetical average patient, not for the population the decision covers. That is the stakes, and it would make the bias theorem feel urgent.

- **Why simulate from the posterior rather than use the delta method?** The remark at lines 793-803 gives the answer (asymmetry, curvature, clean composition with Bucher), but it comes after the theorem. I would front-load a one-sentence motivation before @def-stc-bayes: "the marginal STC functional is nonlinear in $\boldsymbol\xi$, so its uncertainty is skewed; simulating from the posterior captures that skew, while the delta method forces a symmetric Gaussian."

## Missing examples and intuition

- **No running clinical scenario.** The introduction mentions $A$, $B$, $C$ abstractly and never names a drug, a disease, or an outcome. A single sentence like "suppose $A$ is a new oncology agent, $C$ is standard of care, and $B$ is a competitor's drug tested against $C$ in a different trial whose patients are older and sicker" would anchor every subsequent formula.

- **The worked example (@exm-stc-logistic) is good but isolated.** It uses a "binary biomarker" with no clinical identity. Giving the biomarker a name (e.g., "high vs low disease burden," or "biomarker-positive vs negative") and the event a name (e.g., "response at 6 months") would cost nothing and would make the four probabilities $\mu_C(0), \mu_C(1), \mu_A(0), \mu_A(1)$ feel like real quantities.

- **No diagram of the triangle.** The anchored triangle ($A$-vs-$C$ trial, $B$-vs-$C$ trial, want $A$-vs-$B$) is referenced repeatedly (lines 19-26, 715-722) with no figure. A simple three-node diagram with the two trials labeled and the STC step and the Bucher step marked would massively help a weak-math reader.

- **No picture of plug-in vs marginal.** The core conceptual move of the chapter is "average then link, do not link then average." A two-panel figure (left: plug the mean in, then contrast; right: average the curves, then contrast) would communicate the whole chapter's point at a glance. The arithmetic in @exm-stc-logistic does it in numbers, but a picture would do it in intuition.

- **No example of the unanchored case.** Every example is anchored. The unanchored theorem (@thm-stc-consistency part 2) and the stronger prognostic-variable requirement are never illustrated. Even a one-sentence hypothetical ("if the $A$ trial and the $B$ trial share no common comparator, STC must model the absolute outcome in each population, so every prognostic factor that differs between trials must be in $\mathbf x$") with a concrete variable would help.

- **No example of misspecification.** The misspecification remark (lines 229-241) is the chapter's most clinically important warning, and it has no example. A short illustrative case (e.g., "if the true model has a quadratic covariate effect but you fit a linear one, the fitted surface is wrong off the index support, and STC's extrapolation inherits that error") would make the abstract "pseudo-true parameter" land.

## Notation and jargon problems

- **$\boldsymbol\xi$ for the full parameter (line 88).** Notation confirms $\boldsymbol\xi$ is the full parameter vector, but the chapter also uses $\boldsymbol\beta_1, \boldsymbol\beta_2, \gamma, \alpha$ as components. The switch between the assembled $\boldsymbol\xi$ and the components is sometimes abrupt (e.g., line 314-316 introducing $\boldsymbol\beta_{(C)}=\boldsymbol\beta_1$, $\boldsymbol\beta_{(A)}=\boldsymbol\beta_1+\boldsymbol\beta_2$ mid-equation). A reminder that $\boldsymbol\beta_{(k)}$ is just "the covariate slope in arm $k$" would help.

- **"link position" (line 277, @eq-stc-armmean).** The term "link position" for $\eta_{k(\mathcal P)}=g(\bar\mu_{k(\mathcal P)})$ is used here and in Chapter 14, but for a beginner it is jargon. "The link of the marginal mean" or "the marginal mean on the link scale" is plainer.

- **"response scale" vs "link scale" vs "natural outcome scale."** The chapter uses all three phrases (e.g., lines 50, 311, 418) to mean the same thing. Pick one and use it consistently; "natural outcome scale" is the most readable for a health researcher.

- **"convex hull of the IPD" (line 38, @thm-maic-no-extrapolation).** The convex-hull phrasing is geometric and will be opaque to a weak-math reader. "The range of covariate combinations actually observed in the index trial" is the plain version.

- **"tower property" (lines 189, 466, 511, 947).** Used four times without definition. A one-line gloss the first time ("the law of iterated expectations: $\mathbb E[\mathbb E[Y\mid X]]=\mathbb E[Y]$") would demystify it for the rest of the chapter.

- **"pushforward" (line 738).** Not in the notation file and not defined. "$\Psi_\#\pi$" is a measure-theoretic shorthand that will stop a health researcher cold.

- **"M-estimator" (line 191).** Used once, undefined. Either define it ("an estimator defined as the zero of an estimating function") or drop the term and say "estimator defined by a score equation."

- **"effective sample size" symbol conflict.** Notation warns that $\mathrm{ESS}_{\mathrm{reg}}$ (explained regression sum of squares) conflicts with $\mathrm{ESS}$ (effective sample size of weighting). This chapter only uses the weighting ESS (line 873), so the conflict does not bite, but the chapter's "small effective sample size" reference at line 873 could briefly remind the reader which ESS it means.

## Pacing issues

- **The introduction does too much too fast.** Lines 33-55 pack in: conditional mean surface, g-computation, integrating measure swap, conditional transportability, interpolation vs extrapolation, MAIC convex-hull limit, correct-specification dependence, non-collapsibility, conditional vs marginal STC, the bias theorem, the consistency theorem, the counterexample, the worked example, and the section roadmap. That is 14 ideas in 23 lines. Slowing the first three paragraphs and deferring the theorem roll-call to its own "roadmap" paragraph would help.

- **The outcome-model section (@sec-stc-outcome-model) front-loads the GLM machinery before any STC happens.** A reader who came for STC sits through a full GLM asymptotics theorem and proof before seeing the first STC estimator (@def-stc-conditional at line 249). Consider stating the plug-in estimator *informally* first ("evaluate the fitted model at the comparator mean"), then doing the MLE rigor, then formalizing.

- **The bias theorem (@thm-conditional-stc-bias) and its proof are the densest sustained block.** Three parts, a Taylor expansion with Lagrange remainder, a Jensen-gap argument, and a contrast-bias regrouping, all in one proof. Breaking the proof into three named sub-proofs with one-sentence summaries at the head of each would help the reader keep orientation.

- **The Bayesian section (@sec-stc-bayes) and the consistency section (@sec-stc-consistency) come after the worked example and feel like add-ons.** They are necessary, but the chapter's emotional climax is the worked example; after it, my attention drops. A one-line signpost at the start of @sec-stc-bayes ("we now handle uncertainty properly, then fold STC back into the Chapter 17 framework") would help.

- **The equivalence section (@sec-stc-maic-equivalence) is the hardest reading and comes last.** By the time I reached the MAIC-side proof (lines 942-953) I was exhausted. This is the chapter's most technical proof and it has no numerical illustration in-line (the supporting exercise @exr-stc-maic-numeric is at the end). A small inline numeric check would sustain a tired reader.

## What worked well

- **The worked example @exm-stc-logistic is excellent.** Three numbers ($1.50000$, $1.44261$, $1.41515$), each computed step by step, with the three lessons called out in named remarks. This is exactly the kind of artifact that turns an abstract bias theorem into something I can show a colleague.

- **The log-link example @exm-stc-loglink** gives a clean closed form and makes the collapsibility boundary concrete. The contrast between "log link: gaps cancel when $\boldsymbol\beta_2=0$" and "logit link: no such cancellation" is the chapter's sharpest conceptual output.

- **The three closing remarks after the worked example (lines 694-722)** are well written and do the clinical translation I wanted elsewhere: the plug-in bias, what population adjustment moves, and closing the triangle via Bucher. If the whole chapter had this voice it would be far more readable.

- **The machine-checked tags and the accompanying remarks** are honest about what the Coq proof does and does not cover (e.g., lines 522-532: "the Coq theorem is the identity-scale skeleton; the link transformation and uniform-convergence step are the pen-and-paper additions"). This is a good model for how to flag formalization scope.

- **The "STC against MAIC, assumption for assumption" remark (lines 865-877)** is the clearest statement in the chapter of when to use which method. It would make a great sidebar near the introduction, not just at the end.

- **The exercises are well designed** and several (@exr-stc-em-shift, @exr-stc-maic-numeric) directly fill gaps the chapter leaves open. The ★ exercises correctly route the harder delta-method and collapsibility material out of the main flow.

## Suggestions

1. **Add a concrete clinical scenario in the first three sentences** of @sec-stc-intro (drug names, disease, outcome). Use it again in @exm-stc-logistic so the example has continuity with the motivation.

2. **Insert a "what is g-computation, in two sentences" recap** at line 15 before relying on it as the central analogy. Cross-reference Chapter 10 is not enough for a weak reader.

3. **Add a one-paragraph "when would you use STC?" box** right after the introduction, summarizing the STC-vs-MAIC trade-off (model correctness vs overlap) that currently appears only at line 865. This gives the reader a reason to keep reading.

4. **Add a figure: the anchored triangle with the STC step and the Bucher step labeled.** Referenced at lines 19-26 and 715-722, never drawn. This is the single highest-value addition for a beginner.

5. **Add a figure: plug-in vs marginal.** Two panels showing "link then average" (wrong) and "average then link" (right) for a curved inverse link. This picture is the chapter.

6. **Rewrite the plug-in motivation at @def-stc-conditional** to say *why* it was the historical default: it needs only the published mean $\bar{\mathbf x}_{BC}$, not the full covariate distribution. Without this the plug-in reads as a straw man.

7. **Expand the MLE theorem's framing** at the start of @sec-stc-outcome-model: state in one sentence why the downstream STC results need $\hat{\boldsymbol\xi}$ to be consistent and asymptotically normal, so the section feels purposeful rather than compulsory.

8. **Break the @thm-conditional-stc-bias proof into three labeled sub-proofs** with a one-sentence summary at the head of each, and add the plain-words gloss of @eq-stc-taylor ("half the variance of the linear predictor times the curvature of the inverse link").

9. **Promote the misspecification remark (lines 229-241) to a callout or corollary.** It is the chapter's central clinical warning and is currently formatted as a skippable remark.

10. **Define "pushforward," "tower property," and "M-estimator" on first use** (one line each), or avoid them. All three are used as if standard and will stop a health researcher.

11. **Standardize the scale vocabulary** to one phrase (suggest "natural outcome scale") and use it everywhere instead of alternating with "response scale" and "link scale."

12. **Add an inline numeric check in @thm-maic-stc-equivalence** (one line of arithmetic with $x$-mean shifted from $0$ to $1$), or at minimum point forward to @exr-stc-maic-numeric in the proof, so the equivalence does not feel purely formal.

13. **Illustrate the unanchored case** with one sentence and one concrete prognostic variable, since @thm-stc-consistency part 2 is otherwise abstract.

14. **Move the sign-orientation remark (lines 111-122) to after the worked example.** It changes nothing technical and confuses a first-time reader who has not yet seen a number.

15. **Add a one-sentence "what is simulated" paragraph near @eq-stc-marg-mean** (line 434): the integral is evaluated by drawing synthetic comparator patients and averaging their predicted outcomes; that is the simulation. This connects the method's name to its mechanism.