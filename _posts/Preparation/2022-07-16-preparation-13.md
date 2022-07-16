---
title: "[NLP] 감정 분석 Sentiment Analysis"
excerpt: "[NLP] 감정 분석 Sentiment Analysis"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

📌 <https://www.youtube.com/watch?v=7GUoDHxN5NM&list=PL7ZVZgsnLwEEoHQAElEPg7l7T6nt25I3N&index=12>

## 💎 파이썬으로 감정 분석하는 방법

1. 감정 어휘 사전을 이용한 감정 상태 분류
   - 미리 분류해둔 감정어 사전을 통해 분석하고자 하는 텍스트의 단어들을 사전에 기반해 분류하고, 그 감정가를 계산
2. 기계학습을 이용한 감정 상태 분류
   - 분석 데이터의 일부를 훈련 데이터로 사용해 그로부터 텍스트의 감정 상태를 분류
   - 이때 사용되는 훈련 데이터는 사용자가 분류한 감정 라벨이 포함되어 있어야 한다.
   - 이를 인공 신경망, 의사 결정 트리 등의 기계 학습 알고리즘을 사용하여 분류

## 💎 진행 과정

### 1️⃣ 감정 사전 라이브러리 설치

afinn 라이브러리를 설치했다. 이 라이브러리는 영어에 대한 긍정, 부정에 관한 감정 사전을 제공한다.

```python
!pip install afinn

from sklearn.datasets import fetch_20newsgroups

newsdata = fetch_20newsgroups(subset='train')
newsdata.data[0]

>>>
From: lerxst@wam.umd.edu (where's my thing)
Subject: WHAT car is this!?
Nntp-Posting-Host: rac3.wam.umd.edu
Organization: University of Maryland, College Park
Lines: 15

 I was wondering if anyone out there could enlighten me on this car I saw
the other day. It was a 2-door sports car, looked to be from the late 60s/
early 70s. It was called a Bricklin. The doors were really small. In addition,
the front bumper was separate from the rest of the body. This is
all I know. If anyone can tellme a model name, engine specs, years
of production, where this car is made, history, or whatever info you
have on this funky looking car, please e-mail.

Thanks,
- IL
   ---- brought to you by your neighborhood Lerxst ----
```

데이터를 가져왔고, 첫 번째 데이터를 출력한 텍스트이다.

- sklearn.datasets ?
- ❓fetch_20newsgroups는 뭘까?
- ❓subset='train'은 무엇을 의미하는 걸까?

### 2️⃣ 감정 상태 분류 및 시각화

```python
from afinn import Afinn
import numpy as np
import matplotlib.pyplot as plt

afinn = Afinn()

plt.style.use('seaborn-white')

positive = 0
neutral = 0
negative = 0

for i in newsdata.data:
  score = afinn.score(i)
  if score > 0:
    positive += 1
  elif score == 0:
    neutral += 1
  else:
    negative += 1

print('postive', positive)
print('neutral', neutral)
print('negative', negative)

plt.bar(np.arange(3), [positive, neutral, negative])
plt.xticks(np.arange(3), ['positive', 'neutral', 'negative'])
plt.show()

>>>
postive 6923
neutral 809
negative 3582
```

![download1](https://user-images.githubusercontent.com/96654391/179365831-9daaa603-1fb2-4373-b568-28b2af879f44.png)

- _afinn.score(newsdata.data[i])_ 를 통해서 감정 점수를 각각 출력할 수 있다.

```python
plt.bar(np.arange(3), [positive, neutral, negative])
plt.xticks(np.arange(3), ['positive', 'neutral', 'negative'])
```

를 통해서 막대 그래프의 막대 부분을 개수로 정의했고 xticks를 통해서 x 라벨이 들어갈 단어를 정의했다.
