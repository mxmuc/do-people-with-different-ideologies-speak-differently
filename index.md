---
layout: home
title: Do People With Different Ideologies Speak Differently?
subtitle: How group divisions manifest themselves in language analyzed using the example of climate change
cover-img: "/assets/img/bigimg-dem-rep.jpeg"
full-width: false
---

## Introduction <a name="introduction"></a>
{: style="text-align: justify" }
One of the most pressing problems facing our society today is animosity across political and social lines. It causes tensions between family and friends, politicians, and the public at large. The acrimony between political groups makes it challenging for people and the government that serves them to solve societal problems.

{: style="text-align: justify" }
Using the example of climate change, we aim to provide evidence that the discussion around this phenomenon is highly polarized and that this polarization is motivated by differences between socio-political subgroups. To achieve this, we extract quotations related to climate change that have been uttered by Democrats and Republicans between 2015 and 2020 from the quotebank dataset. We then propose to enrich these quotations with socio-demographic data and cluster the quotation embeddings as a means to identify prominent topics. Measuring within-topic and between-topic group affiliation, our work aims to contribute to a deeper understanding of how group divisions manifest themselves in language.


## US Politcians talking about climate change <a name="climatechangeinuspolitics"></a>

## Quote Similarities <a name="quotesimilarities"></a>

## Topic Detection <a name="topicdetection"></a>

{: style="text-align: justify" }
There are several aspects and subtopics about how one can discuss climate change. To detect underlying topics and affiliate quotes with their dominant topic, we followed a structured workflow to build an insightful model based on the **Latent Dirichlet Allocation (LDA) algorithm**. Before creating the topic model using `gensim's native LdaModel` library, we  cleaned and tokenized the quotes and additionally added bigrams to the model.

{% include pyldavis.html %}


## Semantic Analysis <a name="topicdetection"></a>



