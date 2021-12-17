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


## US Politicians talking about climate change <a name="climatechangeinuspolitics"></a>
#### Exploratory Data Analysis

After an initial preprocessing and filtering step, which included discarding quotes delivered from speakers not affiliated with either Republicans and Democrats, and discarding the quotes from speakers who changed political parties between 2015 and 2020, the dataset contains 5286461 quotations (2528204 from Republicans' speakers and 2758257 from Democrats).

![Quotes Per Party](/assets/img/quotes_per_party_initial.png){:class="displayed"}

Furthermore, the quotations comes from 15826 different speakers (7899 of which are Republicans and  7972 Democrats)


![Quotes Per Speaker](/assets/img/quotes_per_speaker_rep_dem.png){:class="displayed"}


Analizing the gender ratio, it is noticeable that female speakers are significantly less quoted than the male speakers, but they are more frequent in the Democrats than in the Republicans party.
In particular, only 16.56 % of the republican quotes are delivered from women, whereas they are the 34.50 % in the Democrats party.


#### Climate change topic selection

However the situation is very different when we consider only the quotes related to climate change
In fact, there are significantly many more quotes from Democrats.

![Climate Change Quotes Per Party](/assets/img/climate_change_quotes_per_party.png){:class="displayed"}


#### How often do Republicans and Democrats talk about climate change ?

Analyzing the time series of the ratio of climate change related quotes over the total number of quotes, we can observe how often does the topic came out in the normal flow of topics that the quotes capture.

The following plot shows the time series with granularity on days, dividing the quotes according to the party. The ratio is shown in log-scale.
![Quotes Per Day](/assets/img/time_series_day.png){:class="displayed"}
It looks like the Democrats talk more often about it, and changing the granularity from day to month, which is more reasonable, the difference results even more evident.
![Quotes Per Month](/assets/img/time_series_month.png){:class="displayed"}
The Republicans have talked more than Democrats about climate change only during three short time periods, but besides that, Democrats ratio dominate significantly over the Republicans.
Furthermore, the maximum peak for Democrats i.e. the period where the ratio is at its maximum value, correspond to the minimum peak for Republicans. This fact suggest that some form of polarization might occur. However, without taking into account the attidutes that the different parties have toward the topic by conducting a deeper analisys, we cannot make any conclusion about it.

## Quote Similarities <a name="quotesimilarities"></a>

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

#### What are the most discussed topics among Democrats and Republicans?

{: style="text-align: justify" }
As we were faced with an imbalanced dataset containing significantly more quotes for Democrats and Men, we balanced the four socio-political subgroups using [Random Oversampling](https://machinelearningmastery.com/random-oversampling-and-undersampling-for-imbalanced-classification/). Through randomly duplicating examples in the minority class (i.e., Republicans and Women), we obtained four subgroups with the same amount of quotes. Looking now at the representation of each subgroup in the different topics, we gain a deeper understanding in how group divisions manifest themselves in the topics discussed. 

- The _gender_ of the speaker has no relevant impact on which aspect of climate change is discussed.

- The _party_ _affiliation_ of a speaker has a strong impact on the way they discuss climate change.

- _Democrats_ tend to be more worried about the effect of climate change on our future. Whereas _Republicans_ tend to center their discussions around fossil fuels (e.g., oil and coal) and the economic impact of an energy transition. 

- _Democrats_ discuss climate change more frequently than _Republicans_.

Below figure visualizes the share of quotes by party affiliation and gender for each topic after oversampling. If all topics would be equally frequent discussed between the different socio-political subgroups, all slices would be of same size (i.e., 25%).

<br />

![Topic Pie Chart Oversampled by Party and Gender](/assets/img/topic_pie_party_gender_oversampled.png){:class="displayed"}
<br /> 
<br /> 
<br /> 

## Semantic Analysis <a name="semanticanalysis"></a>
#### Are Democrats really more concerned about climate change than Republicans?

{: style="text-align: justify" }
Language is rich in subtle signals and quotes can convey different connotations. Having gained a first understanding about how polarization is motivated by socio-political differences, we dive deeper using semantic analysis. Therefore, we use `Empath`, a tool developed at Stanford that can generate and validate new lexical categories from a set of seed terms. We use `Empath` to validate whether Democrats are really more concerned about climate change than Republicans?

<br />

![Empath Bar Chart by Party](/assets/img/empath_topics_1_3.png){:class="displayed"}

<br />

As topic 2 is focussed around oil and its economic impact, we have excluded it for this analysis. We can not directly confirm our above hypotheses, that Democrats are more concerned about climate change than Republicans. However, we could observe the following: 

- _Democrats_ are more likely to use extreme vocabulary when talking about climate change. Way more quotations of Democrats fall into categories such as _crisis_, _war_ and _help_

- Quotations of _Democrats_ convey far more negavtively associated connotations than the ones of Republicans

- _Republicans_ do not get tired of speaking about oil




