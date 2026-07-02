# Appendix A Feedback: Notation Glossary

## Overall reaction

Appendix A is valuable as a lookup index, especially because the tables repeat the main notation and add the chapter and definition slug where each item is introduced. For a novice health researcher, though, it currently feels more like an author-facing concordance than a reader-facing glossary. It helps me find where a symbol was defined, but it does not always help me understand why that symbol matters for an indirect treatment comparison, how to say it in clinical or trial terms, or how nearby symbols differ from one another.

The appendix would be most useful after I already know the book's mathematical structure. If I am still learning ITCs, I need more bridge text between "this is the symbol" and "this is the thing I recognize from health research." The strongest parts are the clear topic grouping, the "Introduced" column, and the alphabetical glossary. The weakest parts are the lack of novice orientation, the sparse explanation of overloaded symbol families, and the limited practical connection to trials, populations, treatments, contrasts, and effect scales.

## What was clear

The introductory paragraph sets expectations well: this appendix is not trying to prove anything, and it is meant to be a place to look up symbols and defined terms. That is helpful because it prevents me from expecting a tutorial.

The topic structure in "Symbols by topic" is easy to scan. The sequence from linear algebra, regression, probability, causal inference, studies and populations, outcome models, and population adjustment mirrors the journey of the book. That gives the appendix a sense of order instead of being a random list of symbols.

The "Introduced" column is genuinely useful. Seeing that $w_i$ belongs to Chapter 18, $\eta_{ijk}$ belongs to Chapter 20, and $d_{ab(\mathcal{P})}$ belongs to Chapter 14 gives me a way to go back to the right part of the book. The slugs are also useful for precise navigation if the rendered links work.

The abbreviation table is one of the most novice-friendly pieces. It collects ITC, PAIC, NMA, MAIC, STC, ML-NMR, ML-UMR, IPD, AgD, EM, PV, and HTA in one place. A health researcher can recognize these as the practical vocabulary of the field.

Some one-sentence term definitions are especially helpful. "Individual patient data and aggregate data," "Anchored and unanchored setups," "Effect modifier," "Prognostic variable," "Transitivity," and "Transportability" are short enough to be usable and close enough to applied ITC language to make sense without rereading a whole chapter.

## What was unclear

The appendix does not yet explain how a novice should use it. If I encounter a symbol in Chapter 20, should I search the symbol table, the alphabetical glossary, or the main Notation chapter? If I know the clinical term "effect modifier" but not the symbol, should I start in "Causal inference," "Studies, treatments, and populations," or "Population adjustment"? A short usage guide would make the appendix much more approachable.

The "Introduced" column sometimes gives chapter numbers without chapter names or conceptual reminders. For example, "Ch. 17" appears often, but a novice may not remember that this is population adjustment theory. "Ch. 14" may not immediately mean Bucher indirect comparison. The column is useful for precision, but weak for orientation.

Several symbol rows are mathematically correct but too compressed for a novice health researcher. The row for $d_{ab(\mathcal{P})}$ says "marginal relative effect of $b$ versus $a$ in $\mathcal{P}$," but I would want one plain-language cue such as "the target treatment contrast in a named population." The row for $\delta_{j,\,t_1 t_k}$ says "study-$j$ contrast of treatment $t_k$ versus $t_1$," but it does not say how this differs from $d_{ab(\mathcal{P})}$ or when the book uses one notation rather than the other.

The terms "marginal," "conditional," "link scale," "linear predictor," and "relative effect" carry a lot of burden. The appendix uses them repeatedly, but it does not give enough novice-level reminders. These are exactly the words a health researcher moving from clinical papers to mathematical ITC would struggle to keep straight.

The alphabetical glossary is useful but very dense. It mixes basic terms such as "Basis" and "Probability space" with advanced topics such as "Hardy-Krause variation," "Pareto-smoothed importance sampling LOO," and "Active classical axioms." Without a difficulty marker or chapter-part marker, a novice cannot tell which terms are central for understanding ITC and which are specialized later tools.

## Under-explained details

The appendix should say more about repeated Greek letters and reused symbols. For example, $\boldsymbol{\beta}$ appears in regression, matching weights, prognostic effects, and effect modification. $\mu$ can mean a mean, a study baseline, or part of an outcome model. $\tau$ appears in causal estimands and also survival contexts elsewhere in the book. A novice needs reassurance that reuse is controlled by context.

The distinction between $X$, $x$, $\mathbf{x}$, and $\mathcal{X}$ is under-explained for this appendix. The main Notation chapter states conventions, but Appendix A says those conventions are not repeated. For a novice using Appendix A as a lookup tool, that is a missed opportunity. Baseline covariates are central to ITC, so the appendix should make the random variable, realized value, vector, and covariate space distinction especially explicit.

The studies and treatments table needs more bridge text. The symbols $i$, $j$, $k$, $a$, $b$, $t_1$, and $t_k$ are the indexing grammar for the whole book, but the table does not give a small clinical-trial example. A reader would benefit from a sentence like: in an AB trial and a BC trial, $j$ names the study, $a,b,c$ name treatments, and $i$ names a patient.

Population notation deserves more explanation. $\mathcal{P}$, $\mathcal{P}^{*}$, $f_j(x)$, $F_j(x)$, $\bar{\mathbf{x}}_j$, and $\boldsymbol{\Sigma}_j$ are central to population adjustment, but the table gives them as isolated rows. A novice needs the connection: these symbols describe who is in a trial, who the target population is, and why covariate imbalance can change an indirect comparison.

The glossary gives many definition slugs but does not explain what kind of object the slug points to. The introduction says slugs are exact cross-references an author would use. That phrase is accurate, but it sounds author-facing. A novice reader may need simpler wording: these links take you to the formal definition in the chapter.

## Where a novice may get lost

A novice may get lost at the transition from general mathematics to ITC-specific notation. The linear algebra, regression, and probability tables are clear enough as mathematical references, but there is not much signposting that says when the appendix has moved from general tools to the notation of indirect comparisons. The "Studies, treatments, and populations" table is the real conceptual turning point and should be introduced as such.

The reader may also get lost when similar concepts appear in different rows without cross-links. "Effect modifier," "Prognostic variable," "Statistical interaction," "Shared effect modifier assumption," "Shared prognostic factor assumption," $\boldsymbol{\beta}_1$, and $\boldsymbol{\beta}_{2,k}$ are all related, but they are scattered across the symbol tables and glossary. A novice would need a cluster or "see also" pointers to understand how they fit together.

The marginal versus conditional distinction is likely the biggest stumbling point. The glossary includes "Conditional effect," "Marginal effect," "Marginal and average-conditional relative effects," "Marginal STC," and "STC estimands," but these entries do not form a single novice-readable explanation. Since marginalization, non-collapsibility, and target populations are central to ITC, this deserves more than one-line definitions.

The outcome-model notation may be intimidating. The row for $\eta_{ijk}$ and the row for $\theta_{ijk}$ use three indices immediately, and the individual-level model glossary entry contains $\mu_j+\mathbf{x}^\top\boldsymbol{\beta}_1+\mathbf{x}^\top\boldsymbol{\beta}_{2,k}+\gamma_k$. That is concise, but a novice health researcher may need a plain-language unpacking of each piece: baseline risk in study $j$, prognostic covariate effects, effect modification, and treatment main effect.

The appendix may be hard to use when the reader remembers a concept but not the exact term. For example, a reader might look for "common comparator," "published aggregate data," "target population," "trial imbalance," or "odds ratio scale." Some of those ideas are present, but the labels are formal. A synonym index would help.

## Suggested improvements

Add a short "How to use this appendix" paragraph after the introduction. It should tell readers to use the symbol tables when they see a mathematical symbol, the alphabetical glossary when they see a term, and the "Introduced" column when they need the full formal definition.

Add chapter names or part labels to the "Introduced" and "Defined in" columns. For example, "Ch. 14, Bucher indirect comparison" is much more useful to a novice than "Ch. 14" alone. This would improve reference usability without changing the mathematics.

Add a small worked notation key for one anchored ITC example. Use treatments A, B, and C, an AB trial, a BC trial, a target population $\mathcal{P}^{*}$, one patient $i$, one covariate vector $\mathbf{x}_i$, and one contrast such as $d_{AB(\mathcal{P}^{*})}$. This would give readers a concrete map from symbols to the health-research story.

Add "see also" pointers for concept clusters. The most important clusters are population and covariate distribution notation, marginal versus conditional effects, effect modifiers and prognostic variables, MAIC weights and effective sample size, and IPD versus AgD likelihood notation.

Repeat the most important notation conventions in a compact key, even if they already appear in the Notation chapter. In particular, repeat bold vector versus plain scalar, capital random variable versus lowercase realization, and subscript index roles. Appendix users often arrive here while confused, so repeating the key conventions is helpful rather than redundant.

Add a plain-language scale guide. It should explain that many ITC effects are on a link or linear-predictor scale, that odds ratios, risk ratios, risk differences, and hazard ratios are not interchangeable, and that the book will state the scale when it matters. This would make rows involving $g$, $\eta$, $d_{ab(\mathcal{P})}$, marginal effects, and collapsibility much easier to use.

Consider adding a novice priority marker to glossary terms, such as "core ITC," "mathematical background," "computation," and "formalization." This would prevent a new reader from treating "Hardy-Krause variation" and "Potential outcomes" as equally immediate learning priorities.

## Highest-priority fixes

1. Add one concrete anchored ITC notation example that maps $i$, $j$, treatments A, B, C, $\mathbf{x}_i$, $\mathcal{P}^{*}$, $d_{ab(\mathcal{P})}$, and $\hat d_{ab(j)}$ to a realistic trial setting.

2. Add chapter names or part labels next to chapter numbers in the "Introduced" and "Defined in" columns.

3. Add a compact novice key for overloaded notation, especially $X/x/\mathbf{x}/\mathcal{X}$, $\mu$, $\tau$, $\boldsymbol{\beta}$, $d$, $\delta$, and the patient, study, and treatment indices.

4. Add bridge text for the marginal versus conditional distinction and for link-scale versus outcome-scale effects.

5. Add "see also" links among related ITC concepts, especially effect modification, prognostic variables, population adjustment, MAIC weights, STC estimands, and ML-NMR likelihood notation.
