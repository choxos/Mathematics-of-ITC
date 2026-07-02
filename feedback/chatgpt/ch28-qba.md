# Chapter 28 Feedback: Quantitative Bias Analysis for Indirect Comparisons

## Overall reaction

This chapter is valuable and timely for a health researcher learning indirect treatment comparisons. The opening motivation is strong: methods like MAIC, STC, ML-NMR, and ML-UMR can only adjust for variables that are measured or reported, so residual bias from an unreported comparator covariate needs to be quantified rather than ignored. That is exactly the kind of practical problem a novice ITC reader will recognize from published trial reports.

The main difficulty is that the chapter quickly becomes a mathematical proof chapter rather than a guided explanation of how a health researcher should think through the bias problem. The reader is told that E-values, indirect-comparison E-values, NORTA, tipping points, and probabilistic bias analysis are tools for one coherent task, but the transitions among those tools are often too abrupt. A motivated novice can follow parts of the intuition, especially in the introduction, the E-value interpretation remark, and the worked example, but may not understand when to choose each tool, what assumptions each tool adds, or how the output should change their confidence in an ITC.

The chapter would work better for its stated audience if it added more bridge paragraphs, plain-language interpretations of the symbols, and a practical workflow before the more formal derivations. The mathematical content can stay, but the reader needs more orientation before being asked to process bias factors, copulas, rank-correlation transforms, stochastic dominance, and prior propagation.

## What was clear

The introduction clearly explains why unmeasured or unreported covariates are a special problem for unanchored indirect comparisons. The contrast between "adjusting for a covariate by using it" and being unable to adjust for a covariate that the comparator publication did not report is effective.

The definition of quantitative bias analysis gives a useful organizing idea: name the bias parameters, write the bias as a function, then invert that function to see how the adjusted estimate changes. This is a good conceptual anchor for the chapter.

The simple binary-confounder bias factor is one of the clearer mathematical parts. The statements that bias disappears when the confounder is balanced, $p_1=p_0$, or inert, $\mathrm{RR}_{UD}=1$, are exactly the kind of sanity check a novice needs.

The E-value interpretation remark is helpful. It tells the reader what the number means in words, why the confidence-interval limit nearest the null matters, and why the E-value is useful but not enough by itself.

The indirect-comparison E-value section has a strong core idea: in an unanchored ITC, the analyst may know the association between the unreported covariate and outcome from IPD, even though the comparator distribution is unknown. That distinction is important and potentially very useful for applied researchers.

The tipping-point definition is intuitive because it talks in natural covariate units: the comparator mean or prevalence at which the conclusion reverses. This is probably the most accessible sensitivity-analysis output for a clinical or HTA reader.

The worked example is useful because it keeps the calculations hand-checkable. The linear sensitivity curve, the E-value calculation, the tipping point, and the probabilistic interval calculation all help make the abstract machinery feel less mysterious.

## What was unclear

The chapter says in the introduction that the plain italic $E$ is reserved for the E-value, but the E-value section immediately uses $E$ as the binary exposure variable in the confounding setup. This is a serious readability issue for novices because the same symbol appears to mean both exposure and E-value in the part of the chapter where the E-value is being introduced.

The bridge from classical unmeasured confounding to unreported effect modification in ITC is not explicit enough. A novice may understand confounding as "treatment groups differ in a risk factor," but may not see how that maps to "trial populations differ in an unreported effect modifier or prognostic variable." The text needs a short translation table that maps exposure, unexposed, treatment assignment, outcome association, and confounder distribution into the ITC setting.

The term "observed bias factor" in the indirect-comparison E-value definition is likely confusing. It is defined as $\exp(|\Delta_{\mathrm{IPD}}|)$, but a novice may read $\Delta_{\mathrm{IPD}}$ as the estimated treatment effect rather than as the amount of bias needed to nullify the result. The chapter should explain in words why a risk ratio of 0.50 requires a bias factor of about 2.0 to move it to the null.

The phrase "with the unreported covariate held at its IPD value" is not clear enough. If $U$ is a covariate with a distribution in the IPD, the reader needs to know whether this means the IPD mean, the full IPD distribution, a representative value, or an outcome-model plug-in value.

The infinite indirect-comparison E-value is mathematically interesting, but the interpretation needs more care. A novice may think "infinite" means "no bias is possible," when the actual claim is narrower: no amount of imbalance in this single covariate can explain away this result under the assumed bias-factor model with the IPD-estimated outcome association treated as fixed.

The NORTA section is technically precise but conceptually hard. Terms like generalized inverse, Gaussian copula, Spearman matching, positive semidefinite projection, and Sklar's theorem arrive before the reader has a practical sense of what problem NORTA solves in the ITC workflow. The chapter says NORTA glues margins to a dependence structure, but it needs a more applied explanation of what the analyst actually has from the comparator publication and what must be borrowed or assumed from the IPD.

The probabilistic bias analysis section explains systematic and total intervals well, but it under-explains where priors come from. A novice health researcher will need guidance on how to choose a beta prior for a binary prevalence, a normal or truncated normal prior for a continuous mean, and how to justify those choices in a report.

## Under-explained details

The three classical QBA threats, uncontrolled confounding, selection bias, and misclassification, are named in the framework section, but only uncontrolled confounding is developed. Since the chapter is about ITC, it would help to say explicitly that the rest of the chapter focuses on the unreported-covariate version of uncontrolled confounding or residual imbalance, while selection and misclassification are included mainly to locate QBA in the broader epidemiologic tradition.

The distinction between an effect modifier and a prognostic variable needs more applied explanation in this chapter. The introduction says unanchored PAIC requires balance of every imbalanced prognostic variable, not merely effect modifiers, while later parts call the unreported covariate an effect modifier. A novice may not know which type of covariate each method is addressing, especially because anchored and unanchored comparisons have different vulnerability patterns.

The ratio-scale restriction for E-values deserves a fuller explanation. The chapter says E-values apply to binary and count outcomes and not continuous or time-to-event effects, but a novice may need to know what to do for hazard ratios, odds ratios, log-risk ratios, mean differences, and RMST differences. A small table of outcome scale, valid QBA tool, and interpretation would help.

The sharp-bound proof is rigorous, but the health meaning of $\mathrm{RR}_{EU}$ and $\mathrm{RR}_{UD}$ gets buried. Before the proof, the chapter should give a small numerical story: for example, a biomarker is twice as common in one population and triples baseline risk, then show how these two facts combine into a maximum possible bias factor.

The NORTA correlation assumption needs a stronger warning. Borrowing the IPD dependence structure for the comparator population is not a harmless technical detail. It is a substantive assumption that the relationship among covariates in one trial population resembles the relationship in another. A novice should be told how sensitive conclusions may be to alternative correlation matrices.

The discrete-margin caveat in the NORTA section is too compressed. The statement that the copula is not unique for a binary covariate is mathematically accurate, but the applied consequence is not stated plainly. The reader needs to know whether this affects the simulated prevalence, the pairwise correlations, the adjusted effect, or just the formal uniqueness claim.

The positive semidefinite repair for the transformed correlation matrix is mentioned as benign and standard, but not explained. A novice may not understand why a matrix can fail to be a valid correlation matrix or how much the repair can change the assumed correlations.

The probabilistic bias analysis definition says structurally invalid draws are discarded and the retained fraction is reported. The chapter should give examples of invalid draws in this ITC setting, such as a normal prior producing impossible prevalences below 0 or above 1, or a covariance structure that cannot be made compatible with the chosen margins.

## Where a novice may get lost

A novice may get lost in the E-value proof because the chapter moves from a binary confounder to a finite-valued confounder, then to a sharp optimization argument, before showing enough applied examples of what the sensitivity parameters mean. The vertex argument and two-cell reduction are mathematically elegant, but they are likely too abstract without a preceding diagram or numeric example.

The transition from the standard E-value to the indirect-comparison E-value is a major conceptual jump. The reader needs to stop thinking about exposure groups inside one observational study and start thinking about population membership or trial membership in an ITC. That translation is essential, but currently it is mostly implicit.

The unanchored estimand formula in the indirect-comparison E-value section may be intimidating. It combines the outcome model, the comparator covariate distribution, the inverse link, integration, and the comparator outcome $\mu_0$ in one display. A novice would benefit from a line-by-line explanation of what each piece represents in a real ITC dataset.

The NORTA construction is probably the hardest section for the target reader. The novice may ask: Why do we start with normal variables if the target covariates are not normal? Why do we transform through $\Phi$? Why is rank correlation used instead of ordinary correlation? Why is the IPD correlation acceptable for the comparator population? These questions are answerable from the text, but not in the order a novice is likely to need.

The tipping-point monotonicity proposition is more formal than many health researchers will need on a first pass. The key applied idea is simple: if higher values of $U$ always move the effect in one direction, then there is at most one tipping point. That intuition should be stated before the stochastic-dominance and coupling language.

The worked example says it carries one comparison through every instrument, but the NORTA part is effectively simplified away by assuming independence and normality. That makes the arithmetic easier, but it means the most difficult method in the chapter is not actually demonstrated in a way a novice can imitate.

The exercises skew heavily toward proofs and advanced probability. Exercises on the sharp bound, discrete NORTA copulas, and nonmonotone surfaces are useful for mathematically strong readers, but they may discourage the health researcher who mainly needs to learn how to interpret and report QBA for an ITC.

## Suggested improvements

Add a short "practical workflow" subsection after the framework definition. It could list the applied steps: identify the unreported covariate, estimate or assume its outcome association, choose plausible comparator marginals, decide whether dependence with reported covariates matters, compute a sensitivity curve, locate a tipping point, optionally place a prior on the bias parameter, and report systematic and total uncertainty.

Add a translation table between classical QBA and ITC. For example, classical exposure groups could correspond to trial or population membership; the unmeasured confounder could correspond to an unreported comparator covariate; $\mathrm{RR}_{EU}$ could correspond to the cross-population imbalance of that covariate; $\mathrm{RR}_{UD}$ could correspond to the covariate-outcome association estimated in the IPD model.

Rename the exposure variable in the E-value derivation from $E$ to something else, such as $A$ or $T$, so it does not conflict with the E-value itself. This is a small notation change with a large readability payoff.

Add a boxed plain-language interpretation after @def-itc-evalue. It should explain the three cases: no meaningful bias factor needed, finite imbalance required, and impossible to explain away under the one-covariate model. The infinite case especially needs careful wording.

Expand the NORTA section with a small nontechnical example before the theorem. For instance, the comparator reports age mean and standard deviation but not biomarker prevalence; the analyst assumes a biomarker prevalence, borrows the age-biomarker rank correlation from IPD, and simulates a pseudo-population whose age and biomarker distributions match those assumptions.

Include a simple sensitivity plot or table in the worked example. Even a small table with assumed $m$, adjusted $\Delta(m)$, risk ratio, and conclusion would make the tipping point and probabilistic prior easier to understand.

Either show a minimal correlated NORTA calculation in the worked example or state clearly that the example uses an independence simplification and that a full NORTA example would add correlation borrowing. As written, the chapter introduces NORTA as central but does not give the reader a usable worked NORTA template.

Give more practical guidance for choosing plausible ranges and priors. Suggested sources could include external registries, baseline tables from related trials, expert elicitation, epidemiologic cohort studies, or broad conservative ranges. The chapter should also warn that the prior is a sensitivity assumption, not new observed evidence.

Make the exercises more accessible by adding applied interpretation exercises. Examples: compute and interpret an E-value from a trial report, decide whether a tipping point is plausible from clinical knowledge, write a one-paragraph HTA interpretation of a probabilistic bias analysis, or compare two priors for an unreported prevalence.

## Highest-priority fixes

1. Fix the notation conflict where $E$ is both the exposure variable and the E-value.

2. Add an explicit bridge from classical unmeasured confounding to unreported covariates in ITC, ideally with a translation table.

3. Clarify the definition and interpretation of $\mathrm{BF}_{\mathrm{obs}}$ in the indirect-comparison E-value section.

4. Add a practical workflow for how a health researcher would run QBA in an unanchored ITC.

5. Expand NORTA intuition before the theorem and explain the correlation-borrowing assumption as a substantive sensitivity assumption.

6. Rework the worked example so it either demonstrates NORTA or clearly labels the independence simplification.

7. Add guidance on selecting plausible ranges and priors for tipping-point and probabilistic bias analyses.

8. Add more applied, interpretation-focused exercises alongside the proof exercises.
