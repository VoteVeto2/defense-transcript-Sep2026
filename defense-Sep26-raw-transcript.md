# Defense Q&A — Raw Transcript (September 2026)

Two-channel transcript from the recording: **Christopher** is the candidate's microphone; **Jury** combines every other participant on the call (the professors, the daily advisor, the APB representative, and the chair) since the source audio does not separate them. Consecutive turns on the same channel are merged into single paragraphs. Timestamps mark minutes:seconds into the recording. Automatic speech recognition (ASR) artifacts — filler words, false starts, mis-heard terms — are kept verbatim; short interjections that are likely ASR noise (stray punctuation, one-word hallucinations picked up during silence) are left as transcribed rather than edited out.

---

## Before the Presentation

**[0:15–0:43] Christopher:** Am I sharing the screen with you now or should I just stop right now? I mean, I'm just doing a test. Okay, I guess... Yes, it's possible. You are sharing your screen. Okay, it's Yeah, it's just like that. Stop sharing.

**[0:55–1:01] Jury:** Good afternoon. Hello. If you link.

**[1:02] Christopher:** Hello everyone.

**[1:06–1:27] Jury:** All right, I think we are complete, right? Yes. Great. Thank you everyone for being here. Um, So Christopher, You know that you have 10 minutes to present your thesis work. And after that, we'll Ask some questions. Ah, Alan's also there. Good afternoon, Alan.

**[1:30] Christopher:** Okay.

**[1:31–1:50] Jury:** Good afternoon. Now you see me probably. Oh, not yet. Wait. We don't see you. We see your background. Wait, wait, wait. Are we waiting for other people? That's better. Alain, are other people joining from APB? No, no, no. Isabel, she's just back from Canada. So I think she is... said jet lag so yeah no that's fine it was just a question so that then i think we are ready for christopher so you can start


## Presentation

**[1:59–12:20] Christopher:** Okay, um... Hello everyone. professors and my daily advisor and good to have you here Today I'm presenting my final thesis defense. In this thesis I crossed the one-year of Belgium Pharmacy dispensing data in collaboration with the Association of Pharmacists in Belgium. Um, The main research question has not changed since the midterm. We still ask, can pharmacist's dispensing data loan refill meaningful subgroups beyond type 1 and 2? One important reference is Selkos et al. here. the edify fly Subtypes using six clinical features. However, we don't have the same feature except for age at our scale. Our data contains pharmacy dispensing records for diabetes-related medications identified through ADC codes, cover off the one in ten people in the Belgian population. Among them, metaforming is the most common one. followed by SOT2 and softener reviews and we will see you later Here's an overview of what has changed since midterm. During March, I presented the K-Mean prototype with seven clusters, mainly selected based on interpretability, but the selection procedure was not sufficiently rigorous. So today, six methods are, if I were under the same selection criteria, then And here's our other changes, starting with restricting the cohorts to type 2 only, I suck for the numerical feature, all the way to adding statistical facilitation tasks and examining regional differences. Our details and motivation one by one later. First, we refine the data pre-processing. We move our layers and restrict cohort to patient classifiers type 2. The rules was followed by APB experts inciting only treatment or defined as type 1 with others or type 2. There are three reasons to do that. The first rule really misses type 1, it has high sensitivity Second is the literature's Some literature, a lot of literature show type 2 diabetes has greater heterogeneity and therefore more suitable for subgroup analysis and on our third, on our earlier photo types Early experiments on the full cohorts, insulin-treated type 1 patients were grouped together with Advanced Type II Fishing Hall already was a requirement thing. This raises concerns about the interpretation of the clusters, so eventually restricts the final cohort to Type 2 only. Next I will explain the feature engineering. On the left is a synthetic table of one patient. In this example you have 10 records and it's compressed to 14 numerical features from four categories designed to summarize all aspects on its dispensing behavior. 11 of them all remain unchanged from the midterm. The main change is we remove out the binary ones in ADC codes directly. There are reasons for this decision and mainly three. The first is we find the ADC codes as the categorical labor, the numerical values doesn't quite represent meaningful distance. For example, a neural difference between two ADZ codes does not mean that corresponding drugs are clinically more or less similar. The second is when we try to use one-hot encoding to mitigate this thing, we found out that this increased dimensions substantially make computation infeasible at our scales. And so even when we use more appropriate methods that serve as the drug distance measures in our earlier experiments, we found out that costs are larger driven by the medication costs to namely patients taking sovereign risk, So we grouped together in where patients taking GLP-1 they form another and that did not add much more new information beyond the medication. itself. And so this is a workflow of our validation. We first use k-means as a benchmark to find the best possible k. among all the matrix. and then I compare six methods listed here All methods need to pass both the permutation test and the stability test. And afterwards, I select Masters with the highest SilverScore to be the final choice. So the main criterion is the SluaScore. And here's the result on the left. You can see a 3x score equals different k Um, in k-means and the highest one is that k equals 5 On the right I compare six Masters. together. and, um, There are two masters of seeing them. are not sufficiently reproducible and is below the thresholds. The remainder of methods that also pass the stability test and select the k-means as the final ones. The reason is mostly because due to the computation constraints, these two methods are actually calculated on a subsample. This brings us to the final five class results and I order these by size. And this is a full result in thesis, it's a bit too dense, so I have a more condensed one, a more simplified one. Each digit represents the proportional patient in the cluster who receive at least one dispensing from that corresponding drug category during the one-year observation. And we give names to all the 5 costs 3 cover size fault. The biggest cluster of one is the largest and is characterized mainly by oral therapy with cardiovascular prevention. There are 79% of patients do smart forming and 79% of patients use lipid low-altering drugs. Closin-2 has the highest treatment burden, there are 63 refills per year, highest of all. There are highest insulin use and highest overall drug classes in the oldest median age. Coster 3 is Inquetin dominant. there are 70% of patients using synchrotin, the highest of all all clusters, among all clusters. And the cluster 4 has the lowest refills. at 10 and 87% only use one single. I come. diabetes-related cost treatment over one year. And cluster 5 is the smallest, but it's also the one I found most difficult to interpret as this. It's pretty close to the global average, and I don't find quite much meaningful signal in there. And given time-constraining, I will only focus on cluster 3 explanation. Within closet tree, monthly incrementing, dispensing increased 2.5 over 2.5x in one year, especially Tisabertit. It goes from near zero to near 32k. The non-reimbursed share also raised from 75 to 87%, indicating that mostly of this prescription is self-paid. This pattern could be compatible with weight management usage for people with high body mass index. However, this alone cannot establish clinical indications, so this requires for the validation in the future. Beyond cost analysis, also examining the regional differences inspired by our cost results, we found two trends in actually opposite directions. On the left, overall around half of the national population dispense only one diabetes related cost over one year. Harvard English and Wallonian region we find it above the average, especially English at 62%. and the damage is below of all we can conclude the Wallonie regions. more monotherapy compared to a farm. and on the right the self-paid incretin Um... It's on the north direction, Flemish's balls, the average and Brussels and Wallon are below them. We also looked closer into Leach and we found Leach has a distinct insulin dispensing pattern. Overall, the dispensing of insulin in lurch is lower compared to the rest of the region. Harvard? when it comes to the pre-mix. in the same pants. They are more common in English. and suggests that Leitch may have the same insulin prescribing patterns. and I come to close this defense. Returning to the swimming, which is a question I asked at the beginning of my thesis. First can dispensing data long identify meaningful dispensing features? Yes, we used the fencing feature alone to give 5 grooves. and there are three or clinically more distinct and we examine it to look at closer and second can the cost ring to scale into one million and this can be done by optimizing memory usage substance categories and power computing and so do we find any regional differences and we find out that we observe geographical variation in monotherapy. Non-wing birds are increasing using semi-dispensing patterns. Several limitations should also be on knowledge. Um There are a lot. Most importantly, the analysis does not also evaluate Cosmic Methods on feature designs. constrained by computational cause and the affiliate project timeline and my intellectual limitation. And that's all. Thank you for listening and welcome questions afterwards. Yeah.


## Q&A — Prof. Molenberghs

**[12:23–12:58] Jury:** Thank you, Christopher. So I'm mainly looking at Professor Molenbergs and Carboni to start asking questions. and I'll start. Yeah. I'll start, Anne, if that's okay, and then I'll give the word to you. Thank you very much for the presentation, and thanks for the opportunity to ask a few questions. You mentioned FUSIK-K means as one of the methods. Now you're the expert, I'm not, so forgive me for asking a naive question. but, uh, What is the fuzzy referring to in fuzzy game? needs.

**[12:59–13:08] Christopher:** Uh... Thee means right. So this method Yes.

**[13:08] Jury:** Yes, indeed.

**[13:09–13:38] Christopher:** Um... It's... So, C-means is just a fancy way to say K-means. it's still K and the FOSCI refers to a software cluster centroid so basically in For these Siemens patients are not assigned to a unique cluster. So instead each patient gets a get sort of like a proportion of how it belongs to each centroid. That's what it stands for.

**[13:46] Jury:** Thank you.

**[13:47] Christopher:** A soft label.

**[13:48–14:18] Jury:** Sure, sure, sure, sure. Let me go to my next question. Now, you have various methods, and we were discussing one, but there are several here, and you presented that nicely. In conclusion, would you say that the big picture, the conclusions that you get, the practical conclusions also for the fields, are robust between clustering methods or does it really depend to a large extent on which clustering methods you exactly choose? Because then, As a practitioner, I would be a bit worried, of course.

**[14:22–14:25] Christopher:** So you're asking is this like a like a database or we have actually have a more general robust methods overall.

**[14:32–14:45] Jury:** I'm talking about the agreement or disagreement between the methods, to put it differently. So I mean robust in the sense of... Yeah, whichever method you use, the main picture that emerges is every time the same or No, the conclusions are very dependent on which clustering method that you choose.

**[14:56–15:12] Christopher:** Overall, we use k-means as a benchmark for reason, it is the most robust one. But it's definitely much more data data center, database, if you have a much more smaller smaller observation of data. So it relies on the structure if you only have 10K patient, if you only have 8K patient, that's most literature that I see.

**[15:20] Jury:** Thank you.

**[15:21–15:24] Christopher:** So my answer is this, if you sell software a lot of records then maybe more plain methods or more robust but if it goes to a much more smaller observation then you need to examine closer of the structure of the data and of course your design of choice.

**[15:42] Jury:** Now, you say that K means is the benchmark. Why is that?

**[15:48–16:03] Christopher:** ehhh... That's a bad one. Personal reason is that... This is the first Cosmic Master I learned a few years ago, but I think in much more Obviously this is in a much more algorithmic sense. K-means just calculate the distance in Ukraine.

**[16:09] Jury:** Mm-hmm.

**[16:12–16:40] Christopher:** Yeah, in my own sense, it's a linear algebra geometrical of way of approaching everything. So yeah, that's just why normal distribution is the most common one in all distribution. I guess that's the reason. Everybody is using it as a benchmark, and it has the most simplest. Sorry, it has the most simplest interpretation in terms of algorithm. Okay.

**[16:40–16:58] Jury:** OK, and then one small final one before I hand over the word to my colleague, Professor Karpone. In figure 5.4, you show pairwise ARI. What is the ARI? And I'm referring to the text, your thesis text. So figure 5.4 in the thesis text, what is the A-R-I?

**[17:03–17:10] Christopher:** It's probably like an agreement run in that or something like that. the alignments between these two things. And if it's closer to one, it's a perfect align, but it never happens.


## Q&A — Examiner 2

**[17:18–17:28] Jury:** Okay. Thank you very much. Over to Professor Kalbon, and then if it's okay. Thank you. Thank you for your presentation. I have also a question about the means. Because indeed, from your study, it seems that OK means is the leading technique as a bit.

**[17:34] Christopher:** But

**[17:36–18:04] Jury:** You have used the k-means to select a number of clusters, and then you came up with five clusters. And then... You have used this said, we try to find five clusters, and then you have used several methods to compare. And then... it comes up that the k-means is the best. So, maybe this could have been influenced. Maybe it's because you already have used the k-means to select a number of clusters, that at the end, the k-means seemed to be the best. Have you tested this?

**[18:07–19:15] Christopher:** the The answer is yes. At first it's, At first I tried to green master, so it's just a... very brutal way of searching the best case for each method. So first, it takes a lot of time. And I think I just run through k equals 3 to 24 for all methods. And they're not just limited to 6. But the problem is this. Most methods return the best result to k equals 3 or 2. And that's just not in a way that it's good enough. And the alternative is that I could compare like maybe this matter at k equals 4 and that one is at k equals 6, but then we lost these same criterians there. And this is a deliberate choice of this sign of me. I restrict the scope to k equals 5. And yes, it will come back to the question you talked about. It's more like a rhetorical one, like, This is flawless. I admit. A flaw. That's a flaw.

**[19:18] Jury:** For integrating the different five clusters, you have used the ATC code.

**[19:24] Christopher:** Uh...

**[19:24–19:32] Jury:** have you you have done this yeah yeah That's okay, you have showed us. But have you thought of maybe using an automatic technique just like cards, classification and regression trees.

**[19:37–20:20] Christopher:** Uh... card regression trees, I don't think it works at my scale. No, it's not... it cannot be wrong i just say uh it maybe it can work on it can work on 10k patients a 100k patient but it cannot work on one million patients i i indeed tried it and uh i had a lot of time fine-tuning these things to to see you know what the what's the limit of my computational. resources can handle you know and I try it and doesn't work along with other methods like db scan and other stuff yeah Yeah, it just I can't

**[20:21–20:27] Jury:** It's been a so-called DB scan is something completely different than the classification and regression trees, That's a completely different technique. The one is supervised and the other is insupervised.

**[20:32–20:34] Christopher:** Oh, yeah, yeah. Oh.

**[20:34–21:12] Jury:** I'm talking about the supervised technique, classification and regression trees. Once you know that this belongs to cluster 1, this belongs to cluster 4, that you can put it in your... card analysis and then he will say okay this is because you obtain cluster one as because of this and these characteristics. So the profiling of your... Cluster membership can be done by classification and regression trees. And that was my question. You have done it by yourself. You just looked at the ATC codes and said, okay, they look there and there. But maybe another way was to let it do automatically. That was my question.

**[21:17–21:26] Christopher:** I believe, thank you, I understand your suggestion right now. I guess I was in the wrong direction a few minutes ago. I didn't try that. It's... yeah.

**[21:29–21:47] Jury:** Did it? At the end. Good. Then another thing... You are working with diabetic patients. For diabetic patients you have years of follow-up information. So hence you have longitudinal data. Have you used clustering on this Lugin longitudinal data?

**[21:55–22:37] Christopher:** Uh... The answer is... Yes, naturally this is I think this is destruction that I first approached. I tried to find information among the one year of data. And the result is that it doesn't work. It's a limitation of the time. Most of the literature I saw are actually done by longitudinal analysis but it has at least five years of patients so you can draw some curved things there but our data is i tried it and it doesn't it doesn't make sense so it's limited let's for example you only have four seasons but you don't have five years of different four seasons right so you can and even not explore some seasonal trends here.

**[22:41] Jury:** And you have tried it, but it didn't work. What was the problem?

**[22:45] Christopher:** Uh...

**[22:45–22:46] Jury:** To... too much data, no trends,

**[22:51–22:58] Christopher:** limited of time. Like if I have Five years of data. This is going to be a longitudinal cluster, but I only have one year of data.

**[23:06–23:21] Jury:** Then maybe my final question, all your clustering techniques are based on distance-based clustering techniques. Um, This is because your data is continuous. What to do in case you have data of mixed type? continuous and also some categorical

**[23:24–24:39] Christopher:** Um... Thank you, Professor, for raising this. This data set is Well, the original one is there is a lot. But you can create as many as you want. And it can include categorical. I guess, actually, you're not at my midterm defense committee. But back at the time, I do a lot of one-hot encoding at that time. And the problem. And I still use a mix of methods there. Like for example, K-Mean is designed for a distant base, but it also worked for categoricals. There are other methods like the Chara, and it is designed for this kind of categorical features. And it actually worked very well with the binary one. This is just for This is for mixed type data. And of course, you have the Random Forests, things like that. you can try this stuff too, but eventually it's due to my design of choice, design of the features I go with all numerical ones. And if I include binary categorical one thing to zero, eventually I need to half of have a different Uh... different cosmic method that's not Euclidean-disant-based.

**[24:45] Jury:** These were my questions. Thank you.

**[24:48] Christopher:** okay thank you thank you for raising thank you for asking


## Q&A — Alain (APB)

**[24:53–25:22] Jury:** All right. Thank you. I see we still have some time for more questions. So Alain, do you want to ask questions to Christopher? Well, thank you for doing the analysis of our data. And then actually you already answered my questions. So because you didn't have time, you didn't do interesting stuff like playing with the features, for example. So my next question is then, if you don't really play with the features, what inspired you to Just take these 14 features and not other features.

**[25:26–26:16] Christopher:** Uh... Thank you for asking the question. There are devices that I received from advisors from the feature design. And one thing we agree that this thesis was lag is that we didn't try We try an exhaustive way of constructing features and use PCAs to reduce one to make it computational. feasible. I guess that's the first thing if I have more time to do. I will just exhaust it all the possible way to construct it and adopt PCA to make it trainable. That's the first thing I will do. and I will explore the mixed type of features and to see if it gives you a better cluster than the one you see right now.

**[26:27–26:33] Jury:** Yeah, because I would expect that Distinct pharmacies visit isn't contributing anything and then I'm missing gender in this feature thing so

**[26:38–26:48] Christopher:** Uh, yes, it's... um I'm sorry. Chandra

**[26:49] Jury:** So you just kicked out gender, you know?

**[26:51–27:42] Christopher:** I... I... indeed... to your... I find it difficult to Uh... I find it difficult to interpret gender. Sorry, it's not interpreted. Wrong word of choice. Um... So, so... I also did like a box of these features importance in the thesis. Maybe it's not that much and I found that if I have a binary outcome, I find it's very hard to measure the contribution of these features. And as you said, the number of physical pharmacists is not that important. I agree. It just... And that's the best I can do to create these stuff like Like, yeah, and this is, I try to, yeah, this maybe is less powerful than the gender, but I didn't go with binary. I want every feature to be numerical, so it fits into the payments. Yeah, it's a distant base.

**[28:01–28:02] Jury:** Okay, thank you. And then I have another question. So I look at your violin plots.

**[28:06] Christopher:** Yeah.

**[28:07–28:16] Jury:** And what worries me is that you have enormous spikes. So I think maybe your cutoff instead of what is it now, you put it to 1000, maybe you should put it

**[28:20] Christopher:** Good.

**[28:20] Jury:** Closer, yes, there.

**[28:22] Christopher:** Thank you.

**[28:24] Jury:** Because...

**[28:38] Christopher:** .

**[28:38] Jury:** Thanks for 10 years.

**[28:40–28:41] Christopher:** Uh... Peace.

**[28:42] Jury:** Isn't he getting poisoned or something?

**[28:50–29:09] Christopher:** But... I have to say this is a good point. Maybe I excluded from... I... I... You're making a good point. I definitely need to go back to check these things. Yeah, it has more of that. than I expect, and this is too conservative. Maybe I should go to the 99.99% of this.

**[29:17–29:31] Jury:** Yeah, something. Well, again, I think really you have to look here what you get in the data. Does this make sense? If some... and I don't know what it is, then you have to look what it is. because Some diabetes medicines can make you that your blood sugar becomes too low and then you even can get into coma.

**[29:31] Christopher:** I'll see you next time.

**[29:39] Jury:** Did you?

**[29:41] Christopher:** This

**[29:41] Jury:** discover something there, somebody's taking too much of medicine, and then he has the risk of becoming, well, in getting into a coma.

**[29:49–29:58] Christopher:** Uh... Thank you for asking, that's a very good point. Unfortunately I didn't thought about it. What I thought about it is Aye, aye.

**[29:59–30:04] Jury:** Well, with metformin, there is no problem, but others, like insulin, for example, maybe that can be a problem.

**[30:07–30:11] Christopher:** Yeah, it's... Um... What I have done in this thesis, I found a very small number of string records. They're absolutely not real patients. It can go way off than this. But I didn't thought about to look at...

**[30:24] Jury:** Yeah, I think these are artifacts because I have difficulties to believe that somebody takes 10 years of his medication.

**[30:33–30:44] Christopher:** Um... But... So to answer your question, no, I did not specifically identify these patients. So the extreme case I believe I did is it's too conservative. I should exclude them in the variable setting.


## Q&A — Felipe & Pedro

**[30:57–31:52] Jury:** Okay, thank you. All right. Felipe. I Yeah, Christopher, I don't have... Big questions to you. I think we talked a lot during the... some time ago. Um. Yeah, I don't know exactly what to ask. Most of the things have been asked already. There's no need to have questions. I had some of them, but they were already... Asked. Yeah, I'm going to think more about it, but I don't think I have questions for the moment. Yeah, Pedro, do you have a question? Yeah, we also discussed a lot between us. Maybe one thing that I could ask is I imagine your variables will have different scales or units of measurements. So,

**[31:52] Christopher:** Thank you.

**[31:53–32:00] Jury:** whole Did you take care of this and how this could affect the approaches that you used. differing between the k-means, the k-means spherical and

**[32:00–32:04] Christopher:** Oops. .

**[32:05] Jury:** The other methods.

**[32:06–32:54] Christopher:** Thank you for asking. I didn't introduce this thing... 20 minutes ago. But yes, they are... Even so, I'm not dealing with mixed type of data, I'm dealing with data at different scales. So did I make, yeah, this is not real. This is inside the data, but you can give a glimpse of like you have 47, you have 10 in here. So what I did is to standardize this thing. And if it's way off the table, I do a log transform. That's it. And I keep it to be the most simplest term of log transform, not like log log or any fencing tactic. But if it's too big, I just log transform it and standardize it to. Oh, yeah. There it is.

**[32:55] Jury:** Mm-hmm.

**[32:56] Christopher:** Yeah. And then I have.

**[32:58] Jury:** I see.

**[32:59] Christopher:** calculatable k-means distance.

**[33:05] Jury:** And what would happen if you hadn't done this standardization stuff?

**[33:10–33:41] Christopher:** Uh... At an earlier experience, I didn't do that, and the... I'm not sure if I did the... did the box plots before, but this thing goes way off the table, all right? It explodes, let's just say. There are features that contributes a lot and features that didn't contribute much. So this will work if we don't do standardization. Thanks.

**[33:41–33:55] Jury:** I see, I see. of Yeah. At some point, you also mentioned that the clustering algorithms also depend, the choice of the clustering algorithms will depend on the distribution of your data, And would there be any limitations of

**[33:59] Christopher:** .

**[33:59–34:05] Jury:** a means regarding this type of distribution that you were detecting or closing?

**[34:07–35:39] Christopher:** Oh Yes, so So I can maybe I can I can give some, let's just say maybe I can give some examples like, let's just take a look at these values. So... K-means just basically want to separate in a high-dimensional Ukraine space and these things, hopefully these things are clustered together, but it doesn't quite work. So that's why spherical K-means comes to the rescue for some structures that I think this just calculates the cosine distance here that it has a you have very well shape that is measured by the angle. Alright, the angle. And the, for example, like, How do I say? And there are also distributions that are scaled. And you need to do some pre-processing. Like it has an extreme outliers there. You can do the vincorization there. So basically just rule out the 99.9 percentile and 0.1 percentile, things like that. And of course, you can do the quadratic log transform mitigate this thing this Avital distribution so K-Mingus is indeed easy to interpret but it's still It can still only work if you actually take care of the data.


## Q&A — Chair

**[35:47–36:02] Jury:** The answers? Let's talk for me. Thank you. All right. Thanks. Um, Yeah, most of my questions have been asked, but maybe I want to ask one final short question. So you obtain these five clusters. And then in your text you find a very good description, you interpret these clusters.

**[36:08] Christopher:** .

**[36:09] Jury:** where you have a very pharmacological description of each of them.

**[36:14] Christopher:** .

**[36:15–36:18] Jury:** And I wonder how did you arrive at that description? Was this with some input from people at APB? Was this with AI assistance?

**[36:25] Christopher:** Yeah

**[36:25–36:30] Jury:** Yeah, like because you use terms like cardiometabolic oral therapy, Basel versus Bones regiment. So I don't think this is...

**[36:35] Christopher:** .

**[36:35] Jury:** yeah your background right so how did you arrive at those descriptions

**[36:39–37:34] Christopher:** Thanks for asking, Professor. No, I don't have this background. I'm a statistic student, but I have a mapper between these codes and the names. So there are a period of time for me is just to Yeah, I go through all the A10 category of these stuff. Yeah, so I map it together and to look which one thing to, you know, outperform the other. There are a lot of dirty works done in there and I just try different methods, Yeah, I tried a lot and tried And I just tried to look which one seemed to separate everyone better and eventually I race to this one. So this is a very clear separation. You have this heat map that is just Well, it's just higher than others.

**[37:36–37:41] Jury:** Yeah, but how did you arrive at these descriptions, like if you... Here, for example, how do you know that C3 is incretin-dominant therapy? How do you obtain this?

**[37:49–37:54] Christopher:** uh... It's indeed the highest and it's absently high

**[37:55] Jury:** Okay, so incretin is one of the...

**[37:58–38:27] Christopher:** And I go to look at the water under the ingratin. I located this stuff. And that actually starts from the very earlier stage of EDA I tried to look what are the most common A10 these diabetes related drugs prescribed to people except for metavermine that's the only one I know before this project and yeah that's how I find it out and I don't yeah I guess it's just mapping the code to its original terms and goes to ask Google. Yeah, that's basically it is. And I didn't quite directly ask for a VB expert on this. But I got the sheets from them. Yeah, I got the data from them.


## Closing

**[38:52–39:00] Jury:** All right. Uh... Gilles, I don't know if you're saying something, but you're mute. Okay, good. Okay. Thank you. If there are no other questions, then I think we are finished with the questioning. And then I will have to ask you to leave the meeting, Christopher.

**[39:09] Christopher:** Yeah.

**[39:10] Jury:** because we need to do an evaluation.

**[39:12] Christopher:** Sure.

**[39:12] Jury:** Okay.

**[39:13] Christopher:** sharing and I will leave right now

**[39:16] Jury:** Yes.

**[39:17] Christopher:** Bye bye.

**[39:17] Jury:** Okay.

**[41:54] Christopher:** I'm so hungry.
