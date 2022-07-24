---
title: "[NLP] 데이터셋 가져오기"
excerpt: "[NLP] 데이터셋 가져오기"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

- Sentiment Analysis of all Billboard Hot 100 Songs Over Time (1958–2019)
  <https://towardsdatascience.com/sentiment-analysis-of-all-billboard-hot-100-songs-over-time-1958-2019-3329439e7c1a>

- Programming for Cultural Heritage - Demo: Working with Genius.com API
  <https://www.youtube.com/watch?v=CokKFmDnDtw>
  -> 가사를 불러오는데 사용되는 API
  해당 깃헙: <https://github.com/johnwmillr/LyricsGenius>

## Sentiment Analysis of all Billboard Hot 100 Songs Over Time (1958–2019)의 진행 과정

1. LyricsGenius의 API를 바탕으로 가사를 가져온다
2. textBlob.sentiment.polarity를 이용해서 감정을 찾아낸다
3. 이를 바탕을 keywords를 찾는다
   ...

## TextBlob.sentiment.polarity

<https://www.analyticsvidhya.com/blog/2021/10/sentiment-analysis-with-textblob-and-vader/>

TextBlob uses NLTK
The input contains a single sentence.
The output of TextBlob is polarity and subjectivity.

Polarity that is one of the output score lies between -1 to 1 where -1 identifies the most negative words and 1 identifies the most positive words.

Subjectivity score lies between 0 and 1. It shows the amount of personal opinion. So, if a sentence has high subjectivity close to 1, it resembles that the text contains more personal opinion than factual information.

해당 글에 TextBlob은 왜 그런 감정 점수가 나왔는지 정확히 알고 싶어서 **VADER** 을 사용했다고 함.

VADER의 경우는 neg, neu, pos로 구분되고 얼마나 pos, neg, neu인지를 알려준다고 한다.
The output from VADER comes in a Python dictionary in which we have four keys and their corresponding values. => four keys: ‘neg’, ‘neu’, ‘pos’, and ‘compound’ which stands for Negative, Neutral, and Positive respectively.

최종적으로 TextBlob과 vader을 비교해보니까 TextBlob가 좀더 부정적인 경향으로 감정을 분석한다는 것을 알게 됨.
