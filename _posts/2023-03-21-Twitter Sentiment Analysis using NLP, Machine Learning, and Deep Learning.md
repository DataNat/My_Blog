---
layout: post
title: 'Twitter Sentiment Analysis using Twitter, Machine Learning, and Deep Learning'
tags: [Twitter, Machine Learning, and Deep Learning']
featured_image_thumbnail:
featured_image: /assets/images/posts/2019/cover.png
featured: true
hidden: true
---
## Introduction

The advent of social media, review sites, and other online platforms has given customers an amplified voice that can greatly impact businesses. As a result, companies are increasingly aware of the significance of customer feedback and its potential for brand improvement and product enhancement.

To better understand their customers' opinions, attitudes, and emotions, companies turn to sentiment analysis. This powerful technique enables businesses to monitor their brand reputation, identify potential issues, and find areas for improvement.

## Purpose

Our goal is to build a machine-learning model to predict if a given tweet is positive or negative.

## Data and Methodology

Our data was taken from Kaggle ([source link](https://www.kaggle.com/datasets/kazanova/sentiment140)). It contains 1,600,000 tweets extracted using the Twitter API. First, we used the machine learning model to analyze 30,000 tweets. Then, we used the deep learning model for 1,000,000 tweets.

We focused on the following columns: Tweets and Target Variables (negative or positive).
- `target`: the polarity of the tweet (0 = negative, 2 = neutral, 4 = positive)
- `text`: the text of the tweet ("Lyx is cool")

**Wordcloud** can be used to create a visual representation of the most frequently used words and phrases in a given text. We highlighted the keywords used in positive and negative tweets.

 <img src="/assets/images/posts/2019/wc.png" alt="WC">

In the positive wordcloud, tweets such as "good", "lol", "nice", "hope", "thank", and "love" were the most frequently used words. This might suggest that many of the positive tweets express positive sentiment, with a focus on feelings of hope, appreciation, and love. On the other hand, the words "want", "wish", "today", "work", "still", and "need" were the most frequent in negative tweets, possibly expressing frustration, dissatisfaction, and unfulfilled needs.

## Machine Learning

First, we ran the 30,000 tweets through the following machine-learning models used for classification and regression tasks:
- Naive Bayes: an algorithm based on Bayes' theorem
- XGBoost (Extreme Gradient Boosting): a powerful algorithm that uses gradient boosting to train decision trees
- Random Forest: an ensemble learning algorithm that combines the predictions of multiple decision trees

For each model, we used three different vector-type techniques for text representation:
- TF-IDF (Term Frequency-Inverse Document Frequency): a statistical measure reflecting the importance of a term in a document
- Vector Count: representing each document as a vector of word frequencies
- Word2Vec: a neural network-based technique that learns continuous vector representations of words

 <img src="/assets/images/posts/2019/twitter_r.png" alt="twitter_r">

## Deep Learning

We felt the machine learning results were inadequate, so we implemented the LSTM (Long Short-Term Memory) model, a type of Recurrent Neural Network (RNN) used to process sequential data, learn complex patterns, and make predictions about future events. LSTM is capable of handling a larger data set, so we increased our data to 1 million tweets.

Using Keras, here is an explanation for the main part of the code used:

```python
# The maximum length of the tweet:
SEQUENCE_LENGTH = 300
# Number of times it passes through the training data:
EPOCHS = 10
# Number of training examples to process at once during each training iteration:
BATCH_SIZE = 1024

Tokenization is the process of splitting each word in the tweet into a sequence of integer tokens that correspond to the words in each tweet in the sequence. We tokenized the tweets in the `X_train` using the tokenizer object, which was created earlier, and achieved the following results:

```
tokenizer.texts_to_sequences(X_train)

We then created an embedding layer using the Embedding class from Keras. The vocab_size parameter set the number of unique words in the vocabulary, the W2V_SIZE parameter set the dimensionality of the pre-trained word embeddings, and the weights parameter set the initial weights of the embedding layer to the pre-trained word embeddings. Finally, the trainable parameter was set to False to ensure that the pre-trained word embeddings would not be updated during the time the model was training.
```
embedding_layer = Embedding(vocab_size, W2V_SIZE, weights=[embedding_matrix], input_length=SEQUENCE_LENGTH, trainable=False)
```

```
KERAS_MODEL = Sequential()
# Adding pre-trained embedding layer to the model:
KERAS_MODEL.add(embedding_layer)
# Dropout is an input unit for each training iteration that can prevent overfitting.
KERAS_MODEL.add(Dropout(0.5))
# We added an LSTM layer to the model with 100 hidden units. The dropout and recurrent_dropout parameters indicate the rate for the input and recurrent connections, respectively. That captures long-term dependencies in the data.
KERAS_MODEL.add(LSTM(100, dropout=0.2, recurrent_dropout=0.2))
# We added a dense output layer to our model with a single unit and a sigmoid activation function. The outputs help with the labeling to better indicate the likelihood that the input sequence belongs to the positive tweet.
KERAS_MODEL.add(Dense(1, activation='sigmoid'))
# We printed the summary of the model with these parameters:
KERAS_MODEL.summary()
# We compiled the model, then specified the binary cross-entropy loss function, the Adam optimizer, and the accuracy metric.
KERAS_MODEL.compile(loss='binary_crossentropy', optimizer="adam", metrics=['accuracy'])
# ReduceLROnPlateau reduces the learning rate when the validation loss stops improving, and EarlyStopping stops training when the validation accuracy stops improving.
callbacks = [ReduceLROnPlateau(monitor='val_loss', patience=5, cooldown=0), EarlyStopping(monitor='val_acc', min_delta=1e-4, patience=5)]
# We trained the model on the training data, using a batch size of BATCH_SIZE and a maximum of EPOCHS epochs. The validation_split argument specifies the fraction of the training data to use for validation. The verbose argument controls the amount of output printed during training.
history = KERAS_MODEL.fit(x_train, y_train, batch_size=BATCH_SIZE, epochs=EPOCHS, validation_split=0.1, verbose=1, callbacks=callbacks) ```

Accuracy: 0.7863839864730835
Loss: 0.4514560103416443

#### Classification Report

 <img src="/assets/images/posts/2019/tva.png" alt="TVA">

  <img src="/assets/images/posts/2019/tvl.png" alt="TVL">


## Training and Validation Accuracy

We plotted the accuracy and loss values over the epochs of the model training in order to observe how the model performs in the neural network setting.

As the training accuracy increases, so does the validation accuracy. The same occurs with the training loss graph: the loss decreases, and so does the validation loss. This suggests that the model learns the patterns in the data and adapts to new data. In both graphs, when the epochs pass 6, the training and the validation approach one another. With more than 10 epochs, the model will overfit the training data and not make accurate predictions.

 <img src="/assets/images/posts/2019/cp.png" alt="CP">
 <img src="/assets/images/posts/2019/cp.png" alt="CP">



## Conclusion
Based on the results of the model, the binary classification model appears to be performing fairly well. The overall accuracy of the model is 79%, which suggests that the model is predicting both positive and negative tweets correctly for a large portion of the instances in the dataset.
Overall, the model's performance provides confidence that it may be useful in predicting positive and negative tweets in similar scenarios. Further analysis will be useful to determine the model's limitations and areas for improvement.





For the complete code, you can visit my [GitHub repository](https://github.com/DataNat/General-Twitter-Sentiment-Analysis).
