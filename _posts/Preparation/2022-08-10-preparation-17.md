---
title: "[NLP] NLP Model"
excerpt: "[NLP] NLP Model"
categories: [Preparation]
tags: [Preparation, Python]
toc: true
toc_sticky: true
---

## 모델 구상

- <https://pseudo-lab.github.io/Tutorial-Book/chapters/NLP/Ch1-Introduction.html>

- <https://velog.io/@7ryean/%EC%9E%90%EC%97%B0%EC%96%B4%EC%B2%98%EB%A6%AC-%EA%B0%90%EC%A0%95%EB%B6%84%EC%84%9D> <br>

## 감정 분석 모델

텍스트 데이터의 종류 <br> <br>

(1) 객관적인 정보 : 뉴스, 백과 사전 같은 텍스트 <br>

(2) 주관적인 평가나 감정 : 리뷰, 소설 같은 텍스트 <br>

### 나이브 베이즈

감정의 발생 확률은 주어진 텍스트 데이터 내 해당 감정을 표현하는 문서의 비율로 추정하는 방법이다.

![download1](https://user-images.githubusercontent.com/96654391/183777735-3166ae0d-e437-4a17-bc3f-50af5c12e9a3.png)

### 평균 임베딩 벡터

텍스트가 주어졌을 때 각 단어의 임베딩 벡터를 평균을 내서 텍스트를 하나의 벡터로 표현하는 방법이다.

### CNN

단어 임베딩 벡터에 필터를 적용하여 CNN 기반으로 감정 분류이다

### RNN

LSTM, GRU를 활용하여 RNN 기반으로 분류 및 예측하는 방법이다.

### BERT

## Sentiment Analysis in 10 Minutes with BERT and TensorFlow

<https://towardsdatascience.com/sentiment-analysis-in-10-minutes-with-bert-and-hugging-face-294e8a04b671> <br>
