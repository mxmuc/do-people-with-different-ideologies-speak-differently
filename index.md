---
layout: home
title: Do People With Different Ideologies Speak Differently?
subtitle: How group divisions manifest themselves in language analyzed using the example of climate change
cover-img: "/assets/img/background-us-congress-inside.jpeg"
full-width: false
---

## Introduction <a name="introduction"></a>

{: style="text-align: justify" }
One of the most pressing problems facing our society today is animosity across political and social lines. It causes tensions between family and friends, politicians, and the public at large. The acrimony between political groups makes it challenging for people and the government that serves them to solve societal problems.

{: style="text-align: justify" }
Using the example of climate change, this data story aims to provide evidence that the discussion around this phenomenon is highly polarized and that this polarization is motivated by differences between socio-political subgroups. To achieve this, we extracted quotations related to climate change that have been uttered by Democrats and Republicans between 2015 and 2020 from the quotebank dataset. We then enriched these quotations with socio-demographic data and clustered the quotation embeddings as a means to identify prominent topics. Measuring within-topic and between-topic group affiliation, our work aims to contribute to a deeper understanding of how group divisions manifest themselves in language.
<br />
<br />

## Climate Change in US Politics <a name="climatechangeinuspolitics"></a>

{: style="text-align: justify" }
Starting from an initial preprocessing and filtering phase, which consists in discarding quotes delivered from speakers not affiliated with either Republicans or Democrats together with quotes from speakers who changed political parties between 2015 and 2020, we focus on a remodeled dataset containing **5,286,461 quotations**. Out of these, **2,528,204** are from **Republicans** and **2,758,257** from **Democrats**.

![Quotes Per Party](/assets/img/quotes_per_party_initial.png){:class="displayed"}

{: style="text-align: justify" }
Grouping by speaker for further analysis, we obtained quotations from **15,826 different speakers (7,899 of which are Republicans and 7,972 Democrats)**. Hence, the two sets are balanced.

![Quotes Per Speaker](/assets/img/quotes_per_speaker_rep_dem.png){:class="displayed"}

{: style="text-align: justify" }
Analyzing the gender ratio, it is noticeable that female speakers are significantly less quoted than the male speakers, but they are more frequent in the Democrats than in the Republican party.
In particular, only 16.56% of the Republican quotes are delivered by women, whereas the percentage raises to 34.50% in the Democratic party.

#### Climate Change Topic Selection

{: style="text-align: justify" }
In order to better focus on the wide reasearch question, we decided to concentrate our exploration on **climate change** related quotations only. Here the division between the two parties visibly changes. The dataset becomes unbalanced, as shown below. There are significantly more quotes from Democrats compared to Republicans. This is a first indication that Democrats discuss climate change more than Republicans.

![Climate Change Quotes Per Party](/assets/img/climate_change_quotes_per_party.png){:class="displayed"}


#### How Often Do Republicans and Democrats Talk About Climate Change ?

{: style="text-align: justify" }
By analyzing the time series of the ratio of climate change related quotes over the total number of quotes, we can observe how often the topic was covered by these politicians throughout 2015-2020.

{: style="text-align: justify" }
The following plot visualizes the share of climate change quotes as a time series on a day-by-day base. The ratio is shown in log-scale.

![Quotes Per Day](/assets/img/time_series_day.png){:class="displayed"}

{: style="text-align: justify" }
We can now confirm that Democrats talk more often about climate change than Republicans. To better display this difference, we decided to change the granularity from day to month, being the most reasonable choice. The difference is now clearly visible.

![Quotes Per Month](/assets/img/time_series_month.png){:class="displayed"}

{: style="text-align: justify" }
The Republicans have talked more about climate change only during three short time periods. Diving deeper into these three points could be an interesting starting point for future research.
Furthermore, the peak for Democrats i.e., the period where the ratio is at its maximum value, corresponds to the minimum for Republicans. This fact already suggests that some way of polarization in topic selection occurred.
<br />
<br />

## Quote Similarity <a name="quotesimilarity"></a>

{: style="text-align: justify" }
Getting a deeper understanding of how polarization manifests itself in language, we use `BERT’s pre-trained Sentence Transformer` to embed the quotations into numerical arrays of the same length (768 digits). With these embeddings as a vantage point, we could now use similarity metrics such as the cosine similarity to investigate within-party and between-party polarization. The evaluated cosine similarity yields a continuous number between 0 and 1, with a higher value indicating a higher similarity. It's worth noticing that the similarity metric presented is more precisely a semantic similarity between 2 sentences (i.e., how similar is their meaning).

{: style="text-align: justify" }
Our first step along the NLP path yielded the following results:

- On average quotations uttered by _Democrats_ have a higher similarity with each other than with any other socio-political subgroup. We therefore conclude a **low within-party polarization within the _Democratic party_ when looking at climate change**

- The average quote similarity within the _Republican party_ is even lower than the similarity between the two parties. This indicates that **discussions around climate change are highly polarized amongst _Republicans_**
<br />
<br />
<br />

:-------------------------:|:-------------------------:
![Similarity Distribution](/assets/img/similarity_frequency.png){:class="displayed"}  |  ![Similarity Between Within](/assets/img/similarity_between_within.png){:class="displayed"}

<br />

{: style="text-align: justify" }
Making everything more tangible, we look at the top three speakers for each party, whose quotes have the highest within-party and between-party similarity. Looking at the Democrats - interestingly - **high-ranking politicians** such as the former president Bill Clinton, US representative Adam Schiff and senator Richard Blumenthal **lead the similarity ranking - both within their own party and between parties**. We can only hypothesize about this effect being linked to an overwhelming amount of quotes for these politicians and their mediator role. Even the top three Republicans, former governor of Ohio John Kasich, US representative Fred Upton and governor of New Hampshire Chris Sununu have a higher between-party similarity than within-party similarity. This again underlines the **high polarization within the Republican party**.
<br />
<br />

![Top 3 Speakers Similarity](/assets/img/top_3_similarities.png){:class="displayed"}
<br />
<br />

{: style="text-align: justify" }
The second step instead consisted in looking at quote similarities at **person level**. Again using cosine similarity, we are able to construct a similarity matrix storing similarities for all possible speaker-to-speaker combinations. Considering that at this point the number of speakers was of exactly 5,442, still very high, plotting them is neither useful nor pretty. We instead present an interactive undirected network graph, showing the **top-3 similarities for the 50 most talkative persons from each party**. [Play around with it](https://mxmuc.github.io/do-people-with-different-ideologies-speak-differently/assets/html/person_lvl_similarity.html) for as long as you want. The network was created using `pyvis` library and some good ol' `javascript`.
<br />
<br />

## Topic Detection <a name="topicdetection"></a>

{: style="text-align: justify" }
There are several aspects and subtopics about how one can discuss climate change. To detect underlying topics and affiliate quotes with their dominant topic, we followed a structured workflow to build an insightful model based on the **Latent Dirichlet Allocation (LDA) algorithm**. Before creating the topic model using `gensim's native LdaModel` library, we  cleaned and tokenized the quotes and additionally added bigrams to the model.
{: style="text-align: justify" }
We were able to group the quotations around **three distinct topics**. The word cloud below with the size of the words proportional to the weight gives an overview about the content of each topic. While topics 1 and 3 are closely related to the discussion about climate change, topic 2 is centered around oil and its economic aspects.
{: style="text-align: justify" }
If the charts below are not yet enough for you, feel free to play around with our [interactive topic visualization](https://mxmuc.github.io/do-people-with-different-ideologies-speak-differently/assets/html/climate_change_topics_lda.html) using `pyLDAvis`.
<br /> 
<br /> 

![Topic Word Cloud](/assets/img/topic_word_cloud.png){:class="displayed"}
<br /> 

![Topic Word Count and Importance](/assets/img/topic_word_count_important_keywords.png){:class="displayed"}

![Cluster Topics](/assets/img/topic_cluster_bokeh.png){:class="image-box"}

<br /> 
<br /> 

#### What Are the Most Discussed Topics Among Democrats and Republicans?

{: style="text-align: justify" }
As we were faced with an imbalanced dataset containing significantly more quotes for Democrats and Men, we balanced the four socio-political subgroups using [Random Oversampling](https://machinelearningmastery.com/random-oversampling-and-undersampling-for-imbalanced-classification/). Through randomly duplicating examples in the minority class (i.e., Republicans and Women), we obtained four subgroups with the same amount of quotes. Looking now at the representation of each subgroup in the different topics, we gain a deeper understanding in how group divisions manifest themselves in the topics discussed. 

- The _gender_ of the speaker has no relevant impact on which aspect of climate change is discussed

- The _party_ _affiliation_ of a speaker has a strong impact on the way they discuss climate change

- _Democrats_ tend to be more worried about the effect of climate change on our future. Whereas _Republicans_ tend to center their discussions around fossil fuels (e.g., oil and coal) and the economic impact of an energy transition 

- _Democrats_ discuss climate change more frequently than _Republicans_

Below figure visualizes the share of quotes by party affiliation and gender for each topic after oversampling. If all topics would be equally frequent discussed between the different socio-political subgroups, all slices would be of same size (i.e., 25%)

<br />

![Topic Pie Chart Oversampled by Party and Gender](/assets/img/topic_pie_party_gender_oversampled.png){:class="displayed"}
<br /> 
<br /> 
<br /> 

## Semantic Analysis <a name="semanticanalysis"></a>
#### Are Democrats Really More Concerned About Climate Change Than Republicans?

{: style="text-align: justify" }
Language is rich in subtle signals and quotes can convey different connotations. Having gained a first understanding about how polarization is motivated by socio-political differences, we dive deeper using semantic analysis. Therefore, we use `Empath`, a tool developed at Stanford University that can generate and validate new lexical categories from a set of seed terms. We use `Empath` to validate whether Democrats are really more concerned about climate change than Republicans?

<br />

![Empath Bar Chart by Party](/assets/img/empath_topics_1_3.png){:class="displayed"}

<br />
{: style="text-align: justify" }
As topic 2 is focussed around oil and its economic impact, we have excluded it for this analysis. We can not directly confirm our above hypotheses, that Democrats are more concerned about climate change than Republicans. However, we could observe the following: 

- _Democrats_ are more likely to use extreme vocabulary when talking about climate change. Way more quotations of Democrats fall into categories such as _crisis_, _war_ and _help_

- Quotations of _Democrats_ convey far more negavtively associated connotations than the ones of Republicans

- _Republicans_ do not get tired of speaking about oil
<br />
<br />
<br />

## Final Words

{: style="text-align: justify" }
Even if our project only touched the surface of understanding the causes and consequences of media polarization, we learned a lot about how climate change is discussed in US media among Democrats and Republicans. We could validate common hypotheses, such as that Republicans mainly focus their thoughts around fossil fuels when speaking about climate change. Our analysis further showed that Democrats do not just speak more about climate change; they are also more worried about the effects of it on our future. This is expressed through the usage of extreme vocabulary with negative connotations. We were able to show that climate change is a highly polarized topic - especially within the Republican party. Finally, we could not find that the gender of a speaker influences neither the way nor the frequencies one speaks about climate change.
<br />
<br />

{: style="text-align: center" }
This project was realised in 2021 as part of the course ["Applied data analysis" (CS-401)](https://dlab.epfl.ch/teaching/fall2021/cs401/) at the [Swiss Federal Institute of Technology in Lausanne (EPFL)](https://www.epfl.ch/en/)







