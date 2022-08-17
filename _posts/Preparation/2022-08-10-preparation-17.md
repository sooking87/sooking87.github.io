---
title: "[NLP] NLP Model"
excerpt: "[NLP] NLP Model"
categories: [Preparation]
tags: [Preparation, Python]
toc: true
toc_sticky: true
---

## VADER

compound 점수가 0.1 이상이면 긍정 감성, 그 이하면 부정 감성으로 판단하나 상황에 따라 이 임계값을 적절히 조정해 예측 성능을 조절할 수 있다.

## 모델 구상

- <https://pseudo-lab.github.io/Tutorial-Book/chapters/NLP/Ch1-Introduction.html>
- <https://velog.io/@7ryean/%EC%9E%90%EC%97%B0%EC%96%B4%EC%B2%98%EB%A6%AC-%EA%B0%90%EC%A0%95%EB%B6%84%EC%84%9D> : 자연어 처리 / 감정 분석
- <https://analyticsindiamag.com/nlp-models-bert-state-of-the-art-glue-baseline-language/> : Top 8 Baselines For NLP Models
- <https://towardsdatascience.com/sentiment-analysis-in-10-minutes-with-bert-and-hugging-face-294e8a04b671> :
  Sentiment Analysis in 10 Minutes with BERT and TensorFlow

## BERT

<https://www.techtarget.com/searchenterpriseai/definition/BERT-language-model> <br>

BERT is different because it is designed to read in both directions at once. This capability, enabled by the introduction of Transformers, is known as bidirectionality. <br>

근데 얘는 감정 분석이 아니라 뭔가,, 텍스트 분석에 특화되어 있는 거 같음!

## Deep Learning Models for Sentiment Analysis

<https://underthehood.meltwater.com/blog/2019/08/22/deep-learning-models-for-sentiment-analysis/>

### Bayesian Sentiment

![download1](https://user-images.githubusercontent.com/96654391/183996849-1fd261bb-485e-4161-b830-53eab1767945.png)

특정 단어 개수 / 전체 나온 개수 형식으로 진행되는 방식 => Bag of Words 모델을 사용하겠지? => 단점: 문맥 파악 불가, 희소 행렬이 생성됨.

### Sentence-level Training and Classification

we are now training and classifying at sentence level. <br>

근데 여기서 Bayseian Sentiment를 발전시켜서 문장 단위로 훈련할 수 있게끔 모델을 만들었다고 한다.

### Improvement: New Deep Learning Models

그리고 CNN, RNN, LSTM의 새로운 딥러닝 기술들 중에서 CNN을 바탕으로 해결책을 짰다고 했다. CNNs are mostly used for Computer Vision but they have been shown to perform really well for NLP as well.

<br>

It consists of an embedding (input) layer, followed by a single convolution layer, then max-pooling and softmax layers

![download2](https://user-images.githubusercontent.com/96654391/183999560-a8f44b9a-ab36-4607-89ae-de83ee9ae1e7.png)

그리고 그 다음 글에는 해당 층마다 어떤 역할을 하는지 적혀있었다.

## entiment Analysis: A Definitive Guide

<https://monkeylearn.com/sentiment-analysis/>

## Using Machine Learning for Sentiment Analysis: a Deep Dive

<https://www.datarobot.com/blog/using-machine-learning-for-sentiment-analysis-a-deep-dive/>

### Sentiment analysis, a baseline method

we can define something called a tf-idf score. This stands for term frequency-inverse document frequency, which gives a measure of the relative importance of each word in a set of documents. In simple terms, it computes the relative count of each word in a document reweighted by its prevalence over all documents in a set. <br>

- t: term
- d: document
- D: a set of documents <br>

> tf(t, d) = count(t) in document d <br>
> idf(t, d, D) = -log(P(t | D))

### Sentiment analysis models

Other good model choices include SVMs, Random Forests, and Naive Bayes. These models can be further improved by training on not only individual tokens, but also bigrams or tri-grams. Of course, the process of creating and training on n-grams increases the complexity of the model

### More advanced models

These embeddings are sometimes trained jointly with the model, but usually additional accuracy can be attained by using pre-trained embeddings such as Word2Vec, GloVe, BERT, or FastText. a deep learning model is constructed using these embeddings as the first layer inputs:

- **_Convolutional neural networks_** : those convolutions in the embedded feature space of **the words in a sentence**
- **_LSTMs and other recurrent neural networks_** : they can be used to repeatedly predict the sentiment as each token in a piece of text is ingested.
- **_Recursive neural networks_** : these models take a tree-based representation of an input text and create a vectorized representation for each node in the tree.
- **_Multi-task learning_**

## Project Report Twitter Emotion Analysis

<https://www.cse.ust.hk/~rossiter/independent_studies_projects/twitter_emotion_analysis/twitter_emotion_analysis.pdf> <br>

We use the **Multinomial Naive Bayes** as learning algorithm with the Laplace smoothing representing the classic way of doing text classification.

- **Naive Bayes** : Naive Bayes classifiers are highly scalable, requiring a number of parameters linear in the number of variables (features/predictors) in a learning problem.
- **The Multi­variate Bernoulli Model** : Also called binomial model, useful if our feature vectors are binary (e.g 0s and 1s). An application can be text classification with bag of words model where the 0s 1s are "word does not occur in the document" and "word
  occurs in the document" respectively.
- **The Multinomial Model**: Typically used for discrete counts. In text classification, we extend the Bernoulli model further by counting the number of times a word $w_i$ appears over the number of words rather than saying 0 or 1 if word occurs or not.
- **the Gaussian Model** : We assume that features follow a normal distribution. Instead of discrete counts, we have continuous features.

<br>

<https://scikit-learn.org/stable/modules/naive_bayes.html> -> Naive Bayes에 대한 설명과 이를 활용한 다양한 모델에 대한 설명
<br>

<https://m.blog.naver.com/laonple/220867768192> -> 한국어 ver + 자세한 예시

1. Firstly, we divide the data set into two parts, the training set and the test set + validation set
2. We use the **Multinomial Naive Bayes**
3. We can now train the naive bayes classifier with the training set, validate it using the hold out part of data taken from the training set, the validation set, repeat this 10 times and average the results to get the final accuracy which is about 0.77.

### Bayes example

- <https://www.analyticsvidhya.com/blog/2021/07/performing-sentiment-analysis-with-naive-bayes-classifier/>
- <https://www.youtube.com/watch?v=hp2ipC5pW4I> : youtube
- <https://towardsdatascience.com/sentiment-analysis-introduction-to-naive-bayes-algorithm-96831d77ac91> : 구체적이 방법이 순서와 코드가 같이 잘 나와있다.
- <https://web.stanford.edu/~jurafsky/slp3/4.pdf> : 코드는 안나와있지만 구체적인 원리, 모델링 과정에 필요한 것들에 대한 설명이 나와있다.
- <https://medium.com/analytics-vidhya/document-sentiment-analysis-using-naive-bayes-8911f25f7c95> : 간단한 모델이지만 나와있는 순서를 바탕으로 모델을 구상해도 될듯
  <br>

  ![download3](https://user-images.githubusercontent.com/96654391/184104649-2df10a37-35b3-4038-87cb-2949e1f9cbe7.png)

## BOW VS TFIDF

<https://www.analyticsvidhya.com/blog/2021/07/bag-of-words-vs-tfidf-vectorization-a-hands-on-tutorial/>
