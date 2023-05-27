---
layout: post
title: 'Analyzing Customer Sentiment for Major US Airlines on Twitter'
tags: [Airlines, Twitter, Transfer Learning]
featured_image_thumbnail:
featured_image: /assets/images/posts/2019/al_cover.png
# featured: false
# hidden: true
---

## Introduction

In today's digital age, social media has transformed the way people interact with airlines, allowing customers to share their travel experiences instantly. In this blog post, we analyze a dataset from Kaggle consisting of tweets about major US airlines, and leverage Hugging Face's advanced natural language processing tools to gain valuable insights into customer sentiment. Our aim is to help airlines improve their services and enhance the overall customer experience.

## Data

The dataset we will be working with is available on Kaggle at [this link](https://www.kaggle.com/datasets/crowdflower/twitter-airline-sentiment). We used 7,089 tweets about six major U.S. airlines: United, American, Southwest, Delta, US Airways, and Virgin America. The tweets are labeled as positive, negative, or neutral.

## Data Preprocessing

This code defines a preprocessing function for cleaning and processing text data. The function removes URLs, non-alphanumeric characters, and English stopwords. It also stems words using the PorterStemmer to reduce words to their root form. This function can be applied to text data to improve the accuracy of sentiment analysis and other natural language processing tasks.

 <img src="/My_Blog/assets/images/posts/2019/clean.png" alt="Clean">

## Visualization

The `wc` function generates a WordCloud visualization based on a given dataset, mask, and filename. Positive tweets such as 'great', 'thank', 'flight', 'amazing', and 'airport' indicate customers' satisfaction with the airlines and their positive experiences at airports. On the other hand, negative tweets with words like 'hour', 'time', 'customer service', 'bag', 'canceled', and 'waiting' reveal issues like delays, poor service, and problems with baggage handling and cancellations.

 <img src="/My_Blog/assets/images/posts/2019/al_wc_code.png" alt="al_wc_code">
 <img src="/My_Blog/assets/images/posts/2019/al_wc.png" alt="al_wc">

## Model Evaluation

During our analysis, we prioritized accuracy as our data was balanced. We evaluated multiple models to predict customer sentiment accurately and measured their accuracy, precision, recall, and F1 scores. Among the models tested, the BERT-based model had the highest accuracy score of 75.07%, followed by the XGBoost model using TF-IDF (71.81%). For our pre-trained model, we used Hugging Face's pre-trained Twitter RoBERTa model, available at [this link](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment).

While some models performed well in predicting customer sentiment accurately, others struggled to provide meaningful results. The worst performer in our analysis was the Word2Vec with LSTM model, which had an accuracy score of only 32.88%. This low accuracy score may be due to the complex nature of LSTM models and the relatively small size of our dataset. Nonetheless, this highlights the importance of selecting the appropriate model and approach for the task at hand to achieve the best results.

<img src="/My_Blog/assets/images/posts/2019/al_results.png" alt="al_results">
## Conclusion

We explored a dataset of tweets about major airlines to perform sentiment analysis. By analyzing the top words and evaluating different models, we gained valuable insights into customer sentiment, which airlines can use to improve their services and enhance customer satisfaction. By continuing to monitor and analyze social media sentiment, airlines can stay ahead of the competition and provide an even better travel experience for their customers.

For more details on the code used in this project, please visit [my GitHub page](https://github.com/DataNat/Twitter-Sentiment-US-Airways).
