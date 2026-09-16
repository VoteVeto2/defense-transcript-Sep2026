# Defense Q&A, September 2026: independent question-by-question review

Second pass, done from the raw transcript without reusing the first file. For each question: what was asked, what you said (condensed from the raw ASR), what went wrong, a better answer, and what to prepare before January. Timestamps refer to the raw transcript.

Ground rule for reading this: an examiner's question is an invitation to show you understand your own method. Every answer below that failed did so in one of four ways: (a) answered a different question, (b) gave a personal or time-based reason where a technical one was needed, (c) guessed at something in your own thesis, or (d) joked.

---

## Prof. Molenberghs

### Q1 [12:42] "What does the fuzzy in fuzzy c-means refer to?"

He prefaced it with "you're the expert, forgive a naive question." That is a courtesy; it calls for a careful, respectful answer.

**You said [12:59–13:47]:** "C-means is just a fancy way to say k-means... fuzzy refers to soft cluster centroids... each patient gets a proportion of how it belongs to each centroid. A soft label."

**Problem:** The substance (soft membership) is right, but "a fancy way to say k-means" is flippant and inaccurate. Fuzzy c-means (Bezdek, 1981) is a different algorithm with its own objective and a fuzzifier parameter m; the "c" is only the number of clusters. You also never said how you turned soft memberships into the hard labels you compared against the other methods.

**Better:**
> "Fuzzy c-means is the soft-assignment counterpart of k-means. Instead of one label, each patient gets a membership degree in every cluster, summing to one, and a parameter m controls how soft the memberships are; I used m = [value]. For comparison with the other methods I assigned each patient to the cluster with the highest membership. Its interest for this data is that patients between two profiles, for example moving from oral therapy to insulin, get an intermediate membership rather than a forced label."

**Prepare:** one sentence per method in your comparison: what it optimizes, its main parameter, and the value you used.

### Q2 [13:53, restated 14:32] "Are the practical conclusions robust across clustering methods, or do they depend on the method?"

**You said [14:56–15:40]:** k-means is the benchmark because it's the most robust; it depends on data size; the literature uses 8 to 10k patients; with many records simpler methods are more robust.

**Problem:** You never answered. He asked about agreement between your methods, and you have the number in your own thesis (the pairwise ARI figure). The answer about sample size is unrelated to his question.

**Better:**
> "Partly. Figure 5.4 gives the pairwise ARI between the methods that passed the stability test; it ranges from [x] to [y]. The high-burden insulin cluster, the incretin cluster and the low-refill monotherapy cluster are recovered by every method, with cluster-level overlap of [z]. The two smaller clusters are not stable across methods, and I would not base practice recommendations on them. So the practical picture, three distinct profiles plus a large average group, is robust; the exact partition of the remainder is method-dependent."

**Prepare:** a backup slide with the ARI matrix and a per-cluster overlap table (for each k-means cluster, the share of its patients that land together under each other method).

### Q3 [15:42] "Why is k-means the benchmark?"

**You said [15:48–16:35]:** "That's a bad one. Personal reason is that this is the first clustering method I learned... it's like why the normal distribution is the most common... everybody uses it as a benchmark... simplest interpretation."

**Problem:** "That's a bad one" sounds like you are rating his question. "The first method I learned" is not a scientific justification. The normal-distribution analogy is not an argument.

**Better:**
> "Three reasons. First, scale: k-means is linear in the number of patients per iteration, so it runs on the full 1.1 million patients on GPU, whereas the medoid-based and density methods needed subsampling. Second, comparability: the diabetes-subtyping literature I build on clustered with k-means on standardized variables [check exactly what your reference did before saying this], so results are comparable. Third, it optimizes within-cluster variance on Euclidean distance, which is the natural criterion for standardized numerical features, and with k-means++ initialization and multiple restarts it is reproducible. Its weaknesses, spherical equal-variance clusters and outlier sensitivity, are why I included the other five methods and the stability test."

### Q4 [16:46] "In Figure 5.4 you show pairwise ARI. What is ARI?"

**You said [17:03–17:17]:** "It's probably like an agreement rate... or something like that... if it's closer to one it's a perfect alignment, but it never happens."

**Problem:** This is a figure in your own thesis and you answered with "probably". This alone can decide a grade. "It never happens" is also wrong; two identical partitions give ARI = 1.

**Better:**
> "The Adjusted Rand Index. The Rand index is the fraction of patient pairs on which two partitions agree, either grouped together in both or separated in both. ARI corrects it for chance, so two random labelings score around zero, identical partitions score one, and it can be slightly negative. I use it to compare each pair of methods at k = 5, and also in the stability test between bootstrap resamples."

**Prepare:** be able to define every metric that appears in your thesis (silhouette, ARI, permutation p-value, your stability statistic) in two sentences each, without notes.

---

## Examiner 2

### Q5 [17:24] "You used k-means to select k = 5, then compared methods at k = 5, and k-means won. Could the outcome be influenced by that? Have you tested it?"

This is the "hyperparameter optimization" question in the written feedback.

**You said [18:07–19:15]:** Yes; ran a grid search k = 3 to 24 for all methods; most methods peak at k = 2 or 3, "not good enough"; comparing methods at different k loses a common criterion; "deliberate choice" to fix k = 5; then "it's more like a rhetorical one, like, this is flawless. I admit. A flaw. That's a flaw."

**Problem, in three layers:**

1. You opened with "yes, I tested it" and then described a grid search that showed the opposite: other methods preferred a different k, and you overrode that. So the honest answer was "no, and the comparison is biased in favor of k-means", which you only conceded at the end.
2. Silhouette on Euclidean distance rewards compact convex clusters, which is what k-means optimizes. Choosing k by k-means silhouette and then ranking methods by silhouette at that k favors k-means twice.
3. The closing ("rhetorical", "flawless", "that's a flaw") sounds sarcastic, whatever you meant. Calling an examiner's question rhetorical says you think it didn't need asking.

Note: the written feedback says you deflected with "how k-means creates spherical clusters". In the transcript that explanation comes at 34:07, in answer to Pedro. Either the ASR dropped it here, or the jury merged the two exchanges. It doesn't change the fix.

**Better (say this before being asked, in the presentation):**
> "Yes, the comparison is conditional on k-means. I chose k = 5 with the k-means silhouette and then compared all methods at that k with the same silhouette score, which favors k-means on both counts. I did run every method over k = 3 to 24; most peaked at k = 2 or 3, which is clinically uninformative, so I fixed k = 5 for comparability. That makes this a comparison of methods at a fixed k, not a fair model-selection contest. A fair protocol would choose k with a method-agnostic criterion, such as consensus or bootstrap stability or prediction strength, then compare each method at its own optimum and report cross-method ARI. I list this as a limitation, and I also report how the five clusters behave at k = 4 and k = 6, where [result]."

**Prepare:** actually run it: (a) k chosen by a method-agnostic stability criterion, (b) each method at its own optimum, (c) sensitivity of the five clusters to k = 4 and 6. Put it in a chapter, not a footnote.

### Q6 [19:18] "For interpreting the clusters you used the ATC codes. Have you considered an automatic technique, like CART?"

**You said [19:39–20:20]:** "CART doesn't work at my scale... maybe on 10k or 100k patients, not one million... I tried it... along with DBSCAN and other stuff." After she explained supervised vs unsupervised [20:21–21:12]: "I understand your suggestion now. I didn't try that."

**Problem:** You answered before understanding the question, dismissed it ("doesn't work"), and confused a supervised tree with a density clustering method. For a statistics examiner, the supervised/unsupervised mix-up is worse than not having done it. A depth-limited tree on 1M × 14 rows takes seconds to minutes; "doesn't work at scale" was also factually wrong.

**Better:**
> "No, I profiled the clusters by hand from per-cluster drug-class prevalence and feature distributions. A tree with the cluster label as outcome and the 14 features as inputs would give explicit decision rules, for example 'insulin refills > x and drug classes ≥ 3 → cluster 2', and its accuracy would quantify how separable the clusters are. It's cheap at this size, so it's a straightforward addition, and I'd use it to check that my hand-written labels match what actually separates the groups."

If you don't understand a question, say "Do you mean using the cluster labels as the outcome of a supervised model?" before answering.

**Prepare:** fit the tree, report accuracy and the top splits, and use its rules to justify the cluster names.

### Q7 [21:41, followed up 22:41] "Do you have longitudinal data? Have you used longitudinal clustering? What was the problem?"

**You said [21:56–23:05]:** "Yes... it doesn't work... limitation of the time... literature has at least five years... you only have four seasons." On follow-up: "Limited of time. If I have five years of data..."

**Problem:** "Limitation of time" is ambiguous; she may have heard "I ran out of time" when you meant "the observation window is one year." She asked a concrete follow-up (too much data? no trends?) and got a repeat. You never said what you tried, what it produced, or why it failed.

**Better:**
> "The data covers 12 months, so each patient has at most 12 monthly observations, and the median patient has about [n] dispensings in the year. I built monthly refill trajectories per drug class and clustered them with [method]; the groups separated on refill timing and number of dispensings rather than on any treatment change, and they were unstable across bootstrap samples. With one year you can't distinguish progression from refill scheduling, so I collapsed to yearly aggregates and kept only [any trend features you have, e.g. first-half vs second-half difference] as within-year information. With multi-year APB data, trajectory clustering would be the first thing I'd do."

**Prepare:** one backup slide with what you tried and the ARI/stability numbers. If you didn't try it properly, say so in one sentence rather than "it doesn't work."

### Q8 [23:06] "All your techniques are distance-based on continuous data. What would you do with mixed-type data?"

**You said [23:25–24:44]:** the original data has categorical fields; "you're not at my midterm defense committee, back then I did one-hot encoding"; "k-means also worked for categoricals"; CLARA "is designed for this kind of categorical feature"; random forests; in the end all-numerical by design.

**Problem:** Two incorrect statements to a statistics professor: k-means is not appropriate for categorical variables, and CLARA is a subsampling scheme for k-medoids, not a categorical method. Random forests are unrelated. "You weren't on my midterm committee" implies she lacks context; don't reference what she missed.

**Better:**
> "Two families. Distance-based: Gower distance, which handles continuous, binary and nominal variables together, with PAM or CLARA k-medoids; or k-prototypes, which combines Euclidean distance for numerical and matching distance for categorical variables. Model-based: latent class or finite mixture models with Gaussian and multinomial components. I chose all-numerical features so k-means and the silhouette score were appropriate, and I moved the categorical information, drug class and sex, to post hoc description of the clusters. With Gower plus CLARA I could include them directly, at the cost of a less interpretable distance."

### Alain (APB)

### Q9 [25:10] "If you didn't experiment with the features, what led you to these 14 and not others?"

**You said [25:28–26:26]:** advice from advisors; we agree the thesis lacks an exhaustive feature construction with PCA; would do that with more time; would explore mixed features.

**Problem:** "Advice from advisors" hands the design to someone else; you should own it. The PCA idea is weak: PCA on hand-crafted features doesn't fix feature design, and the components are hard to interpret clinically. He asked for the reasoning behind these 14; you gave a plan for different ones.

**Better:**
> "The 14 features cover four aspects of a year of dispensing that could separate patients: treatment intensity (refills, number of drug classes, insulin share), regularity (interval between refills and its variability, as a proxy for adherence), cost and reimbursement (self-paid share), and age. Each was chosen because it is computable for every patient from dispensing alone and has a clinical reading. What I did not do is a systematic sensitivity analysis: dropping each feature and measuring the ARI against the full solution. That, rather than an exhaustive feature search, is what I'd add."

**Prepare:** the leave-one-feature-out ARI table. It also answers his next point about distinct pharmacies.

### Q10 [26:27] "I'd expect distinct pharmacies visited contributes nothing. And I'm missing gender."

**You said [26:38–27:59]:** "I'm sorry. Gender?"; "I find it difficult to interpret gender, sorry, wrong word"; binary variables are hard to measure the contribution of; agree distinct pharmacies isn't important; wanted every feature numerical for k-means.

**Problem:** A visible fumble on a simple point. The reason for excluding sex is fine (binary variables distort Euclidean distance) but was buried under apologies. You conceded distinct pharmacies contributes nothing and offered nothing in its place.

**Better:**
> "Sex was excluded from the clustering because a binary variable in Euclidean k-means acts as a fixed offset that dominates or is ignored depending on scaling. I use it instead as a validation variable: the sex ratio per cluster is [values], which is [informative / not]. Keeping sex out of the inputs also makes any sex difference between clusters a finding rather than an artifact. On distinct pharmacies: its leave-one-out ARI is [value], so you're right that it adds little, and I would drop it."

### Q11 [28:02–30:57] "Your violin plots have enormous spikes; maybe your cutoff should be lower. Someone taking 10 years of medication, isn't he getting poisoned? Did you find people at risk of hypoglycemic coma?"

**You said [28:50–30:56]:** good point; go to the 99.99th percentile; the extreme records are "absolutely not real patients"; "unfortunately I didn't think about it"; did not identify these patients; cutoff too conservative.

**Problem:** You asserted "not real patients" with no evidence, to the person who owns the data and who was raising a patient-safety concern. Moving a percentile cutoff is arbitrary and doesn't answer him. "I didn't think about it" is honest but should be followed by what you will do.

**Better:**
> "I applied a cutoff at [1000 / value] annual units, which left records that are implausible for a single patient. I haven't yet characterized them. Likely explanations are institutional dispensing through one patient ID, pack-size or quantity coding errors, or genuine overuse. The right check is clinical rather than statistical: convert quantities to defined daily doses and flag patients above, say, 3 DDD per day, then inspect them by drug class. For metformin an excess is a data-quality issue; for insulin and sulfonylureas it would be a hypoglycemia risk and worth reporting back to APB separately. I'll do that before rerunning the clustering."

**Prepare:** do the DDD-based check, report how many patients it affects and what they look like, and rerun with a plausibility cap instead of a percentile cap.

---

## Pedro

### Q12 [31:46] "Your variables have different scales. Did you take care of it, and how could it affect the methods?"

**You said [32:06–33:00]:** standardized; log-transformed the heavily skewed ones; nothing fancier.

**Problem:** Adequate but thin, and you didn't answer the second half (how it affects the different methods).

**Better:**
> "Log(1+x) for the skewed count and cost features, then z-scoring. All the distance-based methods are scale-dependent, so without it the features with the largest variance, total refills and cost, would dominate the distance. Standardization makes every feature contribute equally, which is itself a weighting choice. Spherical k-means is the exception: it normalizes each patient vector, so it is insensitive to scale but sensitive to the relative pattern across features."

### Q13 [33:05] "What would happen without standardization?"

**You said [33:10–33:40]:** "It goes way off the table, it explodes... some features contribute a lot."

**Better:** "The partition becomes a binning of the single highest-variance feature, total annual quantity, so the clusters are just low/medium/high volume." Say the concrete outcome, not "it explodes."

### Q14 [33:46] "Are there limitations of k-means regarding the distributions you observed?"

**You said [34:07–35:45]:** k-means separates in Euclidean space; spherical k-means uses cosine distance; skewed distributions need pre-processing; winsorize at 99.9/0.1; log-transform.

**Problem:** A tour of pre-processing, not an answer about k-means's assumptions. This is possibly the "spherical clusters" answer the jury remembered as a deflection.

**Better:**
> "K-means assumes roughly spherical clusters of similar spread, uses hard assignments, and is sensitive to outliers and skew. My features are right-skewed counts with many zeros, so even after the log transform there are mass points at zero, for example patients with no insulin refills. That can produce clusters defined by which features are zero rather than by a gradual profile, and it tends to split large clusters into equal-sized pieces. That is a plausible reason cluster 5 sits near the global mean. A Gaussian mixture with unequal covariances or k-medoids would relax those assumptions; I compared [which] and found [result]."

---

## Chair

### Q15 [35:59] "How did you arrive at the pharmacological descriptions, e.g. 'cardiometabolic oral therapy', 'basal versus bolus regimen'? With APB input? With AI assistance?"

**You said [36:39–38:50]:** statistics student; had a code-to-name mapping; went through the A10 category; "a lot of dirty work"; heat map shows the separation; "mapping the code to its original term and asking Google, that's basically it"; did not ask APB experts.

**Problem:** He asked a direct yes/no question about AI assistance and you didn't answer it. He named the terms because they are not a statistics student's vocabulary, so he already suspected the answer. Evasion here costs more than an honest yes. "Asking Google" also sounds careless.

**Better:**
> "The class groupings come from the WHO ATC A10 index. The wording of the cluster labels I drafted [with the help of an LLM / from the pharmacology references listed in Section X] and checked against the ATC definitions and [source]. I did not have them validated by APB, which is a gap; I'd like APB to review the labels before the final version, and I've noted the AI use in the thesis's declaration."

KU Leuven's [guidelines on authorised GenAI use](https://www.kuleuven.be/english/education/student/educational-tools/guidelines-for-students-on-the-authorised-use-of-genai) expect disclosure. Whatever the truth is, state it in one sentence.

---

## Laughter and disrespect: second, independent pass

Two signals, checked separately.

### Signal 1: ASR hallucination markers on your channel

Speech recognizers produce filler phrases or lone punctuation on your channel when they pick up non-speech sound: laughter, a sigh, an exhale. Your channel shows this at these points, all while an examiner was talking:

| Time | ASR output on your line | What the examiner was saying |
|---|---|---|
| 28:38, 28:41, 28:50 | ".", "Peace.", "But..." | Alain: 10 years of medication, "isn't he getting poisoned" |
| 29:31 | "I'll see you next time." | Alain: blood sugar too low, risk of coma |
| 31:52, 32:00, 32:04 | "Thank you.", "Oops.", "." | Pedro setting up the scaling question |
| 36:08, 36:14, 36:35 | ".", ".", "." | Chair asking about the cluster descriptions and AI |

Treat this as a hypothesis. But 28:38–29:31 is the strongest candidate for laughter in the whole recording, and it is the worst place for it: the pharmacists' representative was raising a patient-safety point. Even if you were laughing at his phrasing ("poisoned"), the jury will have read it as laughing at the concern.

### Signal 2: wording

Ranked by how likely each is to be what the jury meant by "disrespectful."

1. **19:02–19:15**, "it's more like a rhetorical one... this is flawless... I admit, a flaw." Sarcastic concession on the key methodological question.
2. **15:48**, "Ehh... that's a bad one. Personal reason is..." Rating a professor's question, then a personal reason.
3. **23:39**, "you're not at my midterm defense committee." Telling an examiner she lacks context.
4. **19:39–20:20**, dismissing CART as "doesn't work at my scale" before understanding it, then "it cannot be wrong, I just say..."
5. **38:27**, "asking Google, that's basically it." Flippant, and dodges the AI question.
6. **13:13**, "C-means is just a fancy way to say k-means." Flippant to the most senior examiner after he'd been courteous.
7. **22:51**, "limited of time," repeated after the examiner had rephrased and offered options. Together with 12:07, 25:10 (his words, but you agreed), 26:00: four times you attributed gaps to time.
8. **17:03**, "probably like an agreement rate or something like that," on a figure in your own thesis.
9. **12:07**, "my intellectual limitation." Self-deprecating joke in the limitations slide; jury may read it as not taking the limitations seriously.
10. **26:45–27:07**, "I'm sorry. Gender? ... difficult to interpret gender. Sorry, wrong word." Fumbled, probably with a nervous laugh.
11. **33:24**, "It explodes, let's just say." Casual.

### The pattern behind all of it

Every flagged moment is the same reflex: when a question exposes a weakness, you defuse the tension with a joke, a personal aside, or a concession delivered lightly. In a defense that reads as not taking the jury seriously. Replace the reflex with a fixed routine:

1. Two-second pause. No laugh, no "thank you for asking."
2. Restate the question in one sentence.
3. Direct answer first: yes/no, a definition, or a number.
4. One sentence of reason or limitation.
5. Stop. Let them ask the follow-up.

If you don't know: "I don't know. I'll check and add it." Nothing after that.

---

## Before January, in priority order

1. Fair method comparison (Q5): method-agnostic choice of k, each method at its own optimum, cross-method ARI, sensitivity at k = 4 and 6.
2. Definitions: ARI, silhouette, permutation test, stability statistic, and each of the six methods with its parameters (Q1, Q4).
3. CART profiling of cluster membership (Q6).
4. DDD-based plausibility check of extreme records and rerun (Q11).
5. Leave-one-feature-out ARI; drop distinct pharmacies if it adds nothing (Q9, Q10).
6. Sex and age per cluster as validation variables (Q10).
7. A backup slide on what the longitudinal attempt produced (Q7).
8. Cluster labels validated by APB; AI-use declaration written (Q15).
9. Rehearse every answer above aloud, recorded, until none contains "I guess", "probably", "limited time", or a laugh.
