# Feedback: Chapter 05 — Inference

**Reviewer perspective:** Beginner health researcher, basic calculus, weak math foundation.
**File:** `chapters/part1/05-inference.qmd`

## Overall impression

I'll be honest: I got about a third of the way through this chapter before I felt like I was drowning. The opening paragraph (@sec-models, lines 5-14) promised me that this machinery is what makes indirect treatment comparisons trustworthy, and that got me excited. But by the time I hit the regularity conditions (@def-regular-model, line 349) and the proof of the information equality (@thm-information-equality, line 415), I was reading symbols I could not parse and trusting the author on faith. The chapter is clearly written *for someone who already knows this material*, not for a naive researcher being taken from basics to mastery. The ITC motivation is front-loaded in the intro and then almost completely disappears for 900 lines, only returning in the M-estimation section (line 900) and the worked example (line 1124). I kept waiting for "and here is why a log odds ratio in a network meta-analysis is just a delta-method transformation," and it only came briefly at line 241-243. The worked example at the end saved my understanding of the Bernoulli case, but by then I had already suffered through the general theory with no concrete anchor. The proofs are rigorous, which I respect, but they are also terse in a way that assumes I can fill gaps I cannot fill.

## What was unclear

- **@def-statistical-model (line 41-59).** "A $\sigma$-finite dominating measure $\nu$ (Lebesgue measure for continuous data, counting measure for discrete data)." I had to look up what a "dominating measure" means. As a health researcher I have never heard the word "dominating" used this way. You tell me it is Lebesgue or counting measure, but you never tell me *why* I need this abstraction. A one-sentence intuition ("we need a reference measure so that 'probability density' means something; for continuous data it is area, for counts it is a tally") would have saved me fifteen minutes of confusion.

- **@def-statistical-model, identifiability (line 50-53).** "the map $\boldsymbol\theta \mapsto f(\cdot\,;\boldsymbol\theta)$ is injective." I had to recall what "injective" means. I think I get it: two different parameters cannot give the same distribution. But you never give a concrete example of a *non-identifiable* model, so the concept stays abstract. A two-line example ("if two $\theta$ values give the same normal curve, you can never tell them apart from data") would lock it in.

- **@prp-bias-variance-decomposition, the vector statement (line 90-93).** The scalar proof is fine, but then the vector case is dispatched in one sentence: "The vector statement is identical with $\mathbf m = \mathbb E_{\boldsymbol\theta}[\mathbf T_n]$..." It is *not* identical to me; I had to expand the outer product myself and I was not sure the cross terms vanish because of the same argument. This is a jump.

- **@def-consistent-estimator (line 115-121).** Weak vs. strong consistency. You define both but never tell me which one matters for the rest of the chapter, or in practice. "Almost sure" convergence was covered in Chapter 4, I assume, but a one-line reminder ("strong consistency means the estimator converges for almost every possible dataset, not just in probability") would help.

- **@thm-continuous-mapping proof, part (ii) (line 189-195).** "a standard fact: convergence in probability implies almost-sure convergence along a subsequence." You cite this to @bingham2010regression. For me this is a nontrivial claim and the proof by contradiction via subsequence-of-subsequence made my head spin. A sentence saying *why* this subsequence trick works (the idea that "if it fails to converge in probability, some subsequence stubbornly stays away, but inside that subsequence we can always find a further one that converges almost surely") would help the naive reader.

- **@thm-slutsky proof (line 215-238).** The modulus of continuity $\omega_h(\delta)$ and the bound on line 220-223 lost me. I understand the *goal* (joint convergence $(X_n, Y_n) \to (X, \mathbf c)$), but the inequality on line 222 appears with no derivation. Where does the $2\|h\|_\infty\, P(\|Y_n - \mathbf c\| > \delta)$ term come from? I can see it is a "bad event" bound but it is not spelled out. This is the kind of step a weak-math reader cannot reconstruct.

- **@thm-delta-method proof (line 262-297).** The step "$\|\mathbf Z_n\| = O_p(1)$" on line 287-288 is asserted, not justified. I think it is because $\mathbf Z_n$ converges in distribution and hence is bounded in probability, but that fact is not stated anywhere I could find. Also the line "$\rho(\mathbf T_n) \xrightarrow{p} 0$ and $\|\mathbf Z_n\| = O_p(1)$, so the product is $o_p(1)$" uses a rule about products of $o_p$ and $O_p$ that is never stated as a lemma. For a beginner this is a hidden gap.

- **@def-regular-model (line 349-368).** The four conditions R1-R4 are stated precisely but with zero intuition. R3 "differentiation under the integral" with "integrable envelopes" is pure measure-theory jargon. I had to trust that this is "the conditions under which you can swap derivative and integral," but a health researcher has never swapped a derivative and an integral. A one-paragraph aside with a picture ("the log-likelihood is smooth enough that its slope and curvature are well-behaved, and the tails are light enough that expectations exist") would make R1-R4 feel like safety checks rather than incantations.

- **@lem-score-mean-zero proof (line 379-391).** The chain of equalities on line 384-387 is presented as one line. I had to read it four times. The step "multiply and divide by $f$ on the set $\{f > 0\}$, which carries all the mass by (R1)" is the conceptual heart, and it gets one clause. Why does R1 matter here? Because if the support depended on $\theta$, the set $\{f > 0\}$ would move and the trick would break. Say that.

- **@thm-information-equality proof (line 426-448).** "the quotient rule for gradients" on line 430. I know the quotient rule for scalars but "for gradients" threw me. The expansion on line 432-435 is correct but I could not reproduce it. A note that this is the vector quotient rule (or just showing one component) would help. Also the step "the first term integrates to zero" (line 438-444) uses (R3) again, silently.

- **@lem-kl-information-inequality (line 529-543) and its proof (line 545-569).** Jensen's inequality is invoked (@thm-jensen, presumably from Chapter 4), but the *form* used here, $\mathbb E[-\log r(X)] \ge -\log \mathbb E[r(X)]$, is the "negative log" version, and I had to sit and convince myself which direction the inequality goes because $\varphi(u) = -\log u$ is *decreasing* and convex. A one-line reminder of the exact statement being invoked would prevent a sign error in the reader's head.

- **@thm-mle-asymptotic-normality proof, Step 2 (line 713-725).** The integral form of the remainder in the multivariate Taylor expansion. I have only seen the scalar mean-value-form remainder. The expression on line 719 with the integral of the Hessian along the segment is stated without derivation. Is this the fundamental theorem of calculus applied componentwise to the gradient field? Say so. I worked it out but a beginner will not.

- **@thm-cramer-rao, the vector case proof (line 841-863).** The Schur-complement trick on line 856-860. I have never seen a Schur complement. You say in one parenthetical "This is precisely the Schur-complement positivity of the block matrix." For me that is a name, not an explanation. Two sentences on *why* evaluating the quadratic form on $(\mathbf v, -\mathcal I^{-1}\mathbf v)$ is the right move would make this feel like a technique I could reuse, not a magic trick.

- **@thm-m-estimator-normal (line 925-943).** "the local uniform law of large numbers holds for $\nabla_{\boldsymbol\theta}\boldsymbol\psi$." This is a hypothesis stated in words, not symbols, and I could not tell what I am allowed to assume. Contrast with (A3) in @thm-mle-asymptotic-normality, which is written out fully. Make this parallel.

- **@thm-wilks proof, likelihood-ratio part (line 1089-1104).** The second-order Taylor expansion with the Hessian at $\tilde{\boldsymbol\theta}_n$ on the segment. I followed the structure but the final substitution "$\Lambda_n = \mathbf Z_n^\top\mathcal I^{-1}\mathbf Z_n + o_p(1)$ by the same substitution" hides a lot. The "same substitution" is not obvious to me because the matrices are at different points ($\hat{\boldsymbol\theta}_n$ vs $\tilde{\boldsymbol\theta}_n$). Spell out that both converge to $\mathcal I$.

## What wasn't elaborated enough

- **The picture promised on line 30-34.** "the log-likelihood is a random function of $\boldsymbol\theta$; its slope (the score) vanishes at the MLE; its curvature (the information) determines how sharply the data pin down the parameter; and asymptotic normality is the statement that, viewed through a magnifying glass of width $1/\sqrt n$, this random function looks like a parabola whose vertex is Gaussian." This is a *beautiful* sentence. But it is never turned into an actual figure. A diagram of a log-likelihood curve with the score as tangent and the curvature as the parabola at the peak would make the whole chapter click. I kept wanting that figure and it never came.

- **Why the score has mean zero (@lem-score-mean-zero, line 373).** The proof is correct but the *meaning* is barely explained. The intuition is: "the true parameter makes the data look most likely on average, so the average slope of the log-likelihood at the truth is zero." That sentence is missing. Without it, the lemma feels like algebra rather than the cornerstone the author says it is on line 370-371.

- **The information equality (@thm-information-equality, line 415).** This is described as tying score curvature to score variance, but the *why* is thin. The deep fact is that "how wiggly the log-likelihood is on average" (curvature) equals "how variable the slope is across samples" (score variance). That duality deserves a paragraph of plain English, because the entire Cramér-Rao bound and MLE efficiency rest on it.

- **Observed vs. expected information (line 778-784).** The remark distinguishes $\mathcal I(\hat{\boldsymbol\theta}_n)$ (expected) from $\mathbf J_n(\hat{\boldsymbol\theta}_n)$ (observed). I gathered that software reports the observed one, but I do not know *when* they differ in practice or *why* one might prefer one. A sentence ("in small samples or non-Gaussian models they differ; the observed form uses the actual curvature at the estimate, the expected form averages over hypothetical data") would help.

- **The sandwich estimator (@def-sandwich-variance, line 973-994).** The bread-meat-bread metaphor is named but not *shown*. A tiny schematic of the three matrices multiplied together, with labels, would make "sandwich" literal rather than a nickname. And the connection to MAIC (line 1017-1023) is the single most important applied sentence in the chapter for me, and it gets one remark. Expand it: what *is* the estimating equation in MAIC? What is the "working model" that is misspecified? I have to wait until Chapter 18 to find out, and I am not sure I will remember the sandwich by then.

- **Profile likelihood (@prp-mle-invariance part (ii), line 498-501).** The induced profile likelihood $L_n^{*}(\boldsymbol\eta) = \sup\{L_n(\boldsymbol\theta) : h(\boldsymbol\theta) = \boldsymbol\eta\}$ is defined and then barely used until the confidence-interval remark on line 1117-1119. I did not understand from the definition *why* it is called "profile." A sentence ("you maximize out the nuisance parameters and look at the likelihood as a function of the target parameter alone, which traces a profile through the full likelihood surface") would make the name mnemonic.

- **Loewner order (line 810, 814, 874).** "In the Loewner (positive-semidefinite) order." This is defined in one clause: "$\mathrm{Cov} - \mathcal I^{-1}$ is positive semidefinite." But I have no intuition for what it means for one covariance matrix to be "bigger" than another. A sentence ("$\Sigma_T \succeq \mathcal I^{-1}$ means every scalar linear combination of the estimator has variance at least as large as the bound; the estimator is more spread out in every direction") would make this tangible.

## Missing motivation / "why does this matter?"

- **@sec-asymptotic-tools (line 133).** The three tools (continuous mapping, Slutsky, delta method) are proved *before* I have seen a single estimator. I had no reason to care about them yet. The remark on line 240-243 says the delta method is "the single most-used result of this chapter in later applications, because every effect measure in the book (log odds ratio, log hazard ratio, risk difference) is a smooth function of fitted parameters." That is the *whole* motivation for a health researcher, and it comes after the theorem, in a remark, in two sentences. Move that motivation *before* the section, and give a one-line preview: "when you fit a logistic regression and then compute an odds ratio, the odds ratio is a nonlinear function of the coefficient, and the delta method is what tells you its standard error."

- **@sec-consistency (line 522).** Why do I need to *prove* the MLE converges to the truth? As a practitioner I assumed it did. The motivation "this is what guarantees that with enough data, NMA and MAIC estimates stop being wrong" is implicit, never stated. Say it.

- **@sec-cramer-rao (line 787).** Why does a lower bound on variance matter for ITC? The answer is: it tells you the best possible precision you could ever achieve, so when a method like MAIC reports a standard error you can ask whether it is close to optimal. That framing is absent. The section opens with "How small can the variance of an unbiased estimator be?" which is a math question, not a health question.

- **@sec-tests (line 1026).** The three tests are introduced as "the three classical large-sample tests." For a health researcher the question is: which one should I use when I report an indirect comparison? The remark on line 1120-1121 ("the likelihood-ratio and score intervals are generally preferred" near a boundary) is the only practical guidance, and it is buried. A short "in health applications..." sentence in the section intro would orient the practitioner.

- **Efficiency (@def-efficient-estimator, line 868-876).** I never learned *why* I should care that the MLE is asymptotically efficient. The remark on line 890-898 cites Hájek-Le Cam but does not say what is at stake. The practical stake is: "no regular estimator can beat the MLE in large samples, so when a systematic review uses MLE-based methods, you are not leaving precision on the table." That sentence is nowhere.

- **M-estimation (@sec-m-estimation, line 900).** This is the section with the most ITC motivation (it mentions MAIC, Chapter 18, robust standard errors), and it is the best motivated in the chapter. But even here, the *specific* estimating equation of MAIC is never shown. I understand the author wants to defer to Chapter 18, but a one-line preview ("in MAIC the estimating equation says the weighted covariate mean equals the target population mean") would make the sandwich feel real rather than abstract.

## Missing examples and intuition

- **No example anywhere near @sec-asymptotic-tools.** Three theorems, three proofs, zero examples. A tiny numeric illustration of the delta method (e.g. "if $\hat p$ has variance $0.01$, then $\log(\hat p/(1-\hat p))$ has variance approximately $1/\hat p + 1/(1-\hat p)$ times that") would have made the abstraction land. The Bernoulli example at the end (line 1124) does this, but it is 900 lines away.

- **No example for the continuous mapping theorem or Slutsky.** These are the easiest to illustrate and the most useful. One sentence each: "$\bar X_n^2 \to \mu^2$ by continuous mapping; $\bar X_n / S_n \to \mu/\sigma$ by Slutsky." Missing.

- **No graphical intuition anywhere.** No figure of a log-likelihood, no figure of a parabolic approximation, no figure of the sandwich, no figure of the three test statistics as nested surfaces. For a chapter that *says* "keep one picture in mind" (line 30) and then never draws it, this is a real gap.

- **No ITC-flavored example until the very end, and even then only Bernoulli.** @exm-binomial-inference (line 1129) is a proportion. @exm-sandwich-normal (line 1188) is a mean with wrong variance. Neither is an indirect comparison. Even a *toy* ITC example, e.g. two studies estimating a log odds ratio with the delta method, would connect the chapter to the book's spine. The book is about ITCs and the worked examples are not about ITCs.

- **No example of an estimator that is biased but consistent, or unbiased but inconsistent.** The remark on line 124-131 mentions $T_n = X_1$ and the shrunken mean $\tfrac{n}{n+1}\bar X_n$, but these are named, not *shown*. One line of arithmetic on the shrunken mean (its bias is $-\mu/(n+1)$, which vanishes) would make the abstract claim concrete.

## Notation and jargon problems

- **$\sigma$-finite dominating measure $\nu$** (line 43). Undefined jargon on first use. Not in the notation file's inference table.

- **$O_p$, $o_p$** (line 287-289). These appear in the delta-method proof and the Wilks proof but are only in the notation table (line 80) as "stochastic and deterministic order symbols." A reader who does not already know the calculus of $O_p/o_p$ will be lost in the last two proofs. Define them where they are first used, or add a short aside.

- **$\nabla_{\boldsymbol\theta}$ vs $\nabla^2_{\boldsymbol\theta}$** (line 332-336, 432). Gradient and Hessian. I think these are standard, but the jump from $\nabla$ to $\nabla^2$ in the information-equality proof is fast. A health researcher who has only seen scalar derivatives needs a moment.

- **"$\mathbf A^{-\top}$"** (line 941, 979). Inverse transpose. This notation appears without explanation. I guessed it meant $(\mathbf A^{-1})^\top = (\mathbf A^\top)^{-1}$ but it should be stated.

- **Loewner order $\succeq$, $\succ$** (line 810, 874). In the notation file (line 42) only $A \succeq 0, A \succ 0$ are defined, for positive (semi)definite. The general $A \succeq B$ order used on line 812 is *not* in the notation file. It should be, or it should be defined on first use.

- **"bread" and "meat"** (line 933, 936). Cute but introduced as quoted jargon inside the theorem statement. A beginner reads "the bread" and wonders if this is a technical term. A footnote saying "these are conventional nicknames; $\mathbf A$ is called the bread and $\mathbf B$ the meat because of the sandwich form of the variance" would defuse the jargon.

- **$\mathcal I_n$ vs $\mathcal I$** (line 406-407, 1032). Per-observation vs sample information. The distinction is stated but I had to flip back to remember which is which. A consistent typographic cue (e.g. always $n$ subscript for sample) helps, and the text does use it, but a reminder in the tests section would be good since the formulas on line 1041-1052 mix both.

- **Profile likelihood symbol $L_n^{*}$** (line 499). The star is used only here and in the proof. It does not appear in the notation file. Minor, but a beginner notices orphan symbols.

## Pacing issues

- **The chapter front-loads three hard asymptotic theorems (@sec-asymptotic-tools) before defining the likelihood.** I found this disorienting. I was proving Slutsky's theorem before I had any estimator to apply it to. Reordering to introduce likelihood, score, MLE, *then* the asymptotic tools, *then* consistency and asymptotic normality, would give the reader a reason to care about each tool as it arrives. The author notes (line 136-137) "We will use them constantly, so we prove them here, near the front." That is a mathematician's reason; a learner wants motivation first.

- **The jump from @def-regular-model (line 349) to @lem-score-mean-zero (line 373) to @thm-information-equality (line 415) is three heavy results in three pages.** No breathing room, no example, no figure. I had to read this stretch twice. Insert even a one-paragraph Bernoulli aside ("for the Bernoulli, the score is $(x-p)/(p(1-p))$, its mean is zero, and the information is $1/(p(1-p))$") and the abstraction would be anchored.

- **@sec-consistency (line 522) and @sec-asymptotic-normality (line 674) are the densest sections and they run back-to-back with no example.** The Bernoulli example at line 1129 is 450 lines after the consistency theorem. By the time I got there I had forgotten the statement of @thm-mle-consistency. A micro-example immediately after @thm-mle-consistency ("for the Bernoulli, $\hat p_n \xrightarrow{p} p_0$ by this theorem, since $\Theta = [0,1]$ is compact and the envelope holds") would have consolidated the result.

- **The worked example @exm-binomial-inference (line 1129) is excellent but comes too late.** It should be threaded through the chapter: likelihood and score when those are defined, information when that is defined, delta method when that is defined, tests when those are defined. The current structure, where all theory is abstract and all concreteness is dumped at the end, is the single biggest pacing problem.

- **The exercises (line 1262-1328) are good but several are starred ★ and reference Appendix F for solutions.** A beginner cannot self-check the unstarred ones either, since no solutions are provided in-chapter. At least one fully solved exercise inline would model how to approach the rest.

## What worked well

- **The opening paragraph (line 5-14)** is the best motivator in the chapter. It names NMA, MAIC, and ML-NMR and says exactly what each needs from inference (curvature, robust variance, Fisher inversion). I wish the rest of the chapter kept that thread.

- **The "one picture" sentence (line 30-34)** is a gorgeous summary and the right mental model. It just needs to be an actual picture.

- **@prp-bias-variance-decomposition (line 83-94)** and its scalar proof are clear and well-paced.

- **@lem-argmax-consistency (line 596-630)** and its proof are the cleanest in the chapter: the $\delta$-argument is spelled out step by step, and I followed it completely. This is a model for how the other proofs could read.

- **@exm-binomial-inference (line 1129-1186)** is genuinely illuminating. Computing the MLE, the information, the delta-method variance for the log-odds, and all three test statistics on the same dataset made the abstract machinery click. The observation that the delta-method algebra collapses to $1/\#\text{success} + 1/\#\text{fail}$ (line 1166) was an "aha" moment.

- **@exm-sandwich-normal (line 1188-1219)** made the sandwich concrete. The concrete numbers ($n=40$, $\widehat{\mathbf B}_n = 4.0$, robust SE $0.3162$ vs naive $0.1581$) are exactly what a beginner needs.

- **The cross-references to the proof catalogue (A.11, A.12, A.13)** and the ITC chapters (Chapter 18 for MAIC) are helpful signposts. The remark on line 1017-1023 connecting sandwich to MAIC is the kind of bridge I wanted more of.

- **The Notes and references section (line 1221-1260)** is honest about what is proved, what is cited, and what is not machine-checked. This transparency is welcome.

## Suggestions

1. **Add a figure of the log-likelihood, score, and curvature** right after the "one picture" paragraph (line 30-34). Make the promised picture real.

2. **Thread the Bernoulli example through the chapter** instead of dumping it at the end. When the score is defined, show the Bernoulli score; when information is defined, show $1/(p(1-p))$; when the delta method is proved, show the log-odds variance. Keep the full worked example at the end as a capstone.

3. **Add one ITC-flavored toy example**, e.g. two binary-outcome studies and a Bucher-style indirect comparison of log odds ratios, with the delta method producing the standard error of the indirect effect. This is the book's subject; the chapter should touch it.

4. **Reorder @sec-asymptotic-tools to after the MLE is introduced**, or at minimum add a one-paragraph "why we need these" before the section with a concrete teaser (odds ratio standard error).

5. **Spell out the $O_p/o_p$ calculus** in a short lemma or aside before the delta-method and Wilks proofs, since both rely on it silently.

6. **Add intuition sentences** after each major proof: what the score-mean-zero lemma *means*, what the information equality *means*, what Cramér-Rao *means* for a practitioner. One plain-English sentence each.

7. **Define Loewner order and $\mathbf A^{-\top}$ on first use**, and add them to `notation.qmd`.

8. **Expand the sandwich-to-MAIC remark (line 1017-1023)** to two paragraphs: state what the MAIC estimating equation is in one line, and why the working model is misspecified in one line, so the reader carries the application into Chapter 18.

9. **Soften the jargon on first use** ($\sigma$-finite dominating measure, profile likelihood, Schur complement, "bread"/"meat") with a parenthetical gloss. The rigor can stay; just add a sentence of translation.

10. **Add at least one fully solved exercise inline** so beginners can calibrate their attempted solutions against a worked one before tackling the rest.