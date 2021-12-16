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


## US Politcians talking about climate change <a name="climatechangeinuspolitics"></a>

## Quote Similarities <a name="quotesimilarities"></a>

## Topic Detection <a name="topicdetection"></a>

{: style="text-align: justify" }
There are several aspects and subtopics about how one can discuss climate change. To detect underlying topics and affiliate quotes with their dominant topic, we followed a structured workflow to build an insightful model based on the **Latent Dirichlet Allocation (LDA) algorithm**. Before creating the topic model using `gensim's native LdaModel` library, we  cleaned and tokenized the quotes and additionally added bigrams to the model.
<br /> 
<iframe src="/assets/html/climate_change_topics_lda.html" width="100%" height="600px"></iframe>
<br />
{% include pyldavis.html %}
<br /> 
<br /> 

We were able to group the quotations around **three distinct topics**. The word cloud below with the size of the words proportional to the weight gives an overview about the content of each topic. While topics 1 and 3 are closely related to the discussion about climate change, topic 2 is centered around oil and its economic aspects.
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

## Semantic Analysis <a name="semanticanalysis"></a>
#### Are Democrats really more concerned about climate change than Republicans?

{: style="text-align: justify" }
Language is rich in subtle signals and quotes can convey different connotations. Having gained a first understanding about how polarization is motivated by socio-political differences, we dive deeper using semantic analysis. Therefore, we use `Empath`, a tool developed at Stanford that can generate and validate new lexical categories from a set of seed terms. We use `Empath` to validate whether Democrats are really more concerned about climate change than Republicans?

seed termshow  between socio-political subgroups theAs we were faced with an imbalanced dataset containing significantly more quotes for Democrats and Men, we balanced the four socio-political subgroups using [Random Oversampling](https://machinelearningmastery.com/random-oversampling-and-undersampling-for-imbalanced-classification/). Through randomly duplicating examples in the minority class (i.e., Republicans and Women), we obtained four subgroups with the same amount of quotes. Looking now at the representation of each subgroup in the different topics, we gain a deeper understanding in how group divisions manifest themselves in the topics discussed. 


