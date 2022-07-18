---
title: "[NLP] 감정 분석 Sentiment Analysis"
excerpt: "[NLP] 감정 분석 Sentiment Analysis"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

📌 <https://www.youtube.com/watch?v=7GUoDHxN5NM&list=PL7ZVZgsnLwEEoHQAElEPg7l7T6nt25I3N&index=12>

## 파이썬으로 감정 분석하는 방법

1. 감정 어휘 사전을 이용한 감정 상태 분류
   - 미리 분류해둔 감정어 사전을 통해 분석하고자 하는 텍스트의 단어들을 사전에 기반해 분류하고, 그 감정가를 계산
2. 기계학습을 이용한 감정 상태 분류
   - 분석 데이터의 일부를 훈련 데이터로 사용해 그로부터 텍스트의 감정 상태를 분류
   - 이때 사용되는 훈련 데이터는 사용자가 분류한 감정 라벨이 포함되어 있어야 한다.
   - 이를 인공 신경망, 의사 결정 트리 등의 기계 학습 알고리즘을 사용하여 분류

## 감정 어휘 사전을 이용한 감정 상태 분류 => Eng ver.

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

- sklearn.datasets ? : 데이터셋
- ❓fetch_20newsgroups는 뭘까? : 사이킷런에서 제공하는 데이터셋 중 하나
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

## 기계학습을 이용한 감정 분석 => Kor ver.

여기서부터 다시 임포트부터 시작!

- 한국어 자연어 처리 konlpy와 형태소 분석기 MeCab 설치
  ```python
  !set -x \
  && pip install konlpy \
  && curl -s https://raw.githubusercontent.com/konlpy/konlpy/master/scripts/mecab.sh | bash -x
  ```
- default

  ```python
  import re
  import urllib.request
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  plt.style.use('seaborn-white')

  from konlpy.tag import Mecab
  from tensorflow.keras.preprocessing.text import Tokenizer
  from tensorflow.keras.preprocessing.sequence import pad_sequences
  ```

### 1️⃣ 데이터 로드: `urllib.request` 사용

```python
train_file = urllib.request.urlopen('https://raw.githubusercontent.com/e9t/nsmc/master/ratings_train.txt')
test_file = urllib.request.urlopen('https://raw.githubusercontent.com/e9t/nsmc/master/ratings_test.txt')

train_data = pd.read_table(train_file)
test_data = pd.read_table(test_file)
```

### 2️⃣ 중복 및 결측치 처리

- 데이터 중복 및 null 제거

  ```python
  print(train_data['document'].nunique())
  print(train_data['label'].nunique())

  train_data.drop_duplicates(subset=['document'], inplace=True) # 중복 제거

  print(train_data.isnull().sum())
  train_data = train_data.dropna(how='any')

  >>>
  146182
  2

  id          0
  document    1
  label       0
  dtype: int64
  ```

  - unique(): 데이터에 고유값들이 뭐가 있는지 알고 싶을 때
  - nunique(): 데이터에 고유값들의 수를 출력해주는 함수
  - value_counts(): 값별로 데이터의 수를 출력해주는 함수
  - drop_duplicates(): 중복된 열의 값을 제거
  - dropna(): any -> 1개라도 Nan이 존재시 drop, all -> 모두 NaN값이 존재시 drop

### 3️⃣ 데이터 정제

이 과정을 통해서 한글(?) 만 남겨놓는다. 콤마, 온점 등은 제외시킴.

```python
train_data['document'] = train_data['document'].str.replace("[^ㄱ-ㅎㅏ-ㅣ가-힣 ]", "")
train_data[:10]
train_data = train_data.dropna(how='any')

test_data.drop_duplicates(subset=['document'], inplace=True)
test_data['document'] = test_data['document'].str.replace("[^ㄱ-ㅎㅏ-ㅣ가-힣 ]", "")
test_data = test_data.dropna(how='any')
```

### 4️⃣ 토큰화

`'의','가','이','은','들','는','좀','잘','걍','과','도','를','으로','자','에','와','한','하다'` 를 기준으로 단어를 분리하고, 불용어는 제거한다.

```python
stopwords = ['의','가','이','은','들','는','좀','잘','걍','과','도','를','으로','자','에','와','한','하다']

mecab = Mecab()

X_train = []
for sentence in train_data['document']:
  X_train.append([word for word in mecab.morphs(sentence) if not word in stopwords])

print(X_train[:10])

>>>
[['아', '더', '빙', '진짜', '짜증', '나', '네요', '목소리'], ['흠', '포스터', '보고', '초딩', '영화', '줄', '오버', '연기', '조차', '가볍', '지', '않', '구나'], ['너무', '재', '밓었다그래서보는것을추천한다'], ['교도소', '이야기', '구먼', '솔직히', '재미', '없', '다', '평점', '조정'], ['사이몬페그', '익살', '스런', '연기', '돋보였', '던', '영화', '스파이더맨', '에서', '늙', '어', '보이', '기', '만', '했', '던', '커스틴', '던스트', '너무나', '이뻐', '보였', '다'], ['막', '걸음마', '뗀', '세', '부터', '초등', '학교', '학년', '생', '인', '살용', '영화', 'ㅋㅋㅋ', '별반', '개', '아까움'], ['원작', '긴장감', '을', '제대로', '살려', '내', '지', '못했', '다'], ['별', '반개', '아깝', '다', '욕', '나온다', '이응경', '길용우', '연기', '생활', '몇', '년', '인지', '정말', '발', '로', '해도', '그것', '보단', '낫', '겟', '다', '납치', '감금', '만', '반복', '반복', '드라마', '가족', '없', '다', '연기', '못', '하', '사람', '만', '모엿', '네'], ['액션', '없', '는데', '재미', '있', '몇', '안', '되', '영화'], ['왜', '케', '평점', '낮', '건데', '꽤', '볼', '만', '한데', '헐리우드', '식', '화려', '함', '만', '너무', '길들여져', '있', '나']]
```

#### `from konlpy.tag import *`

-> KoNLPy 한국어 처리 패키지: 대한민국 헌법 말뭉치인 kolaw와 국회법안 말뭉치인 kobill을 제공한다.

**형태소 분석**

- Hannanum
- Kkma
- Komoran
- Mecab: 메카브
- Open Korean Text

**클래스 내 공통 메서드**

- nouns: 명사 추출
- morphs: 명사 + 형태소 추출
- pos: 품사 부착

X_test도 마찬가지로 수행!

```python
X_test = []
for sentence in test_data['document']:
  X_test.append([word for word in mecab.morphs(sentence) if not word in stopwords])
```

### 5️⃣ 빈도수 낮은 단어 제거

```python
threshold = 3
words_cnt = len(tokenizer.word_index)
rare_cnt = 0
words_freq = 0
rare_freq = 0

for key, value in tokenizer.word_counts.items():
  words_freq = words_freq + value

  if value < threshold:
    rare_cnt += 1
    rare_freq = rare_freq + value

print("전체 단어 수 : ", words_cnt)
print("빈도가 {} 이하인 회귀 단어 수 : {}".format(threshold - 1, rare_cnt))
print("회귀 단어 비율: {}".format((rare_cnt / words_cnt) * 100))
print("회귀 단어 등장 빈도 비율: {}".format((rare_freq / words_freq) * 100))

>>>
전체 단어 수 :  49946
빈도가 2 이하인 회귀 단어 수 : 28320
회귀 단어 비율: 56.70123733632323
회귀 단어 등장 빈도 비율: 1.7606762208782198
```

- word_index: 각 단어에 인덱스가 어떻게 부여되었는지 딕셔너리 형태로 리턴(인덱스 기준: 빈도수가 많을수록 작은 인덱스 부여)
- word_counts: 각 단어가 몇 개였는지 카운트된 결과를 리턴(key: 단어, value: 개수)

### 6️⃣ 패딩

- 리뷰의 전반적인 길이를 확인
- 모델의 입력을 위해 동일한 길이로 맞춰줌

```python
print('리뷰 최대 길이:', max(len(l) for l in X_train))
print('리뷰 평균 길이:', sum(map(len, X_train))/len(X_train))

>>>
리뷰 최대 길이: 83
리뷰 평균 길이: 13.801382583574082

plt.hist([len(s) for s in X_train], bins=50)
plt.xlabel('length of Samples')
plt.ylabel('Number of Samples')
plt.show()
```

![download2](https://user-images.githubusercontent.com/96654391/179431295-53b753b6-300b-4bfb-9d09-0b789a5b5c71.png)

최대 길이를 30 또는 60으로 잡음 -> 둘 중 상관 ㄴ

```python
max_len = 60
X_train = pad_sequences(X_train, maxlen = max_len)
X_test = pad_sequences(X_test, maxlen = max_len)
```

- pad_sequences: 케라스에서 패딩을 위한 메소드

### 7️⃣ 모델 구축 및 학습

```python
from tensorflow.keras.layers import Embedding, Dense, LSTM
from tensorflow.keras.models import Sequential

model = Sequential()
model.add(Embedding(vocab_size, 100)) # output = 100
model.add(LSTM(128, dropout=0.3))
model.add(Dense(1, activation='sigmoid'))

model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
             metrics=['acc'])
model.summary()
```

학습

```python
from tensorflow import keras

checkpoint_cb = keras.callbacks.ModelCheckpoint('best-lstm-model.h5', save_best_only=True)
early_stopping_cb = keras.callbacks.EarlyStopping(patience=3, restore_best_weights=True)
history = model.fit(X_train, y_train, epochs=10, batch_size=60, validation_split=0.2, callbacks=[checkpoint_cb, early_stopping_cb])

>>>
Epoch 1/10
1939/1939 [==============================] - 344s 175ms/step - loss: 0.3980 - acc: 0.8203 - val_loss: 0.3533 - val_acc: 0.8424
Epoch 2/10
1939/1939 [==============================] - 333s 172ms/step - loss: 0.3319 - acc: 0.8563 - val_loss: 0.3310 - val_acc: 0.8557
Epoch 3/10
1939/1939 [==============================] - 329s 170ms/step - loss: 0.3067 - acc: 0.8697 - val_loss: 0.3250 - val_acc: 0.8612
Epoch 4/10
1939/1939 [==============================] - 330s 170ms/step - loss: 0.2889 - acc: 0.8788 - val_loss: 0.3157 - val_acc: 0.8641
Epoch 5/10
1939/1939 [==============================] - 327s 169ms/step - loss: 0.2745 - acc: 0.8871 - val_loss: 0.3138 - val_acc: 0.8644
Epoch 6/10
1939/1939 [==============================] - 327s 168ms/step - loss: 0.2628 - acc: 0.8926 - val_loss: 0.3229 - val_acc: 0.8638
Epoch 7/10
1939/1939 [==============================] - 327s 169ms/step - loss: 0.2519 - acc: 0.8980 - val_loss: 0.3162 - val_acc: 0.8688
Epoch 8/10
1939/1939 [==============================] - 330s 170ms/step - loss: 0.2413 - acc: 0.9024 - val_loss: 0.3161 - val_acc: 0.8671
```

평가

```python
model.evaluate(X_test, y_test)

>>>
1537/1537 [==============================] - 38s 25ms/step - loss: 0.3218 - acc: 0.8609
[0.32183122634887695, 0.860874354839325]
```

### 8️⃣ 시각화

```python
hist_dict = history.history
loss = hist_dict['loss']
val_loss = hist_dict['val_loss']
acc = hist_dict['acc']
val_acc = hist_dict['val_acc']

plt.plot(loss, 'b--', label='training loss')
plt.plot(val_loss, 'r:', label='validation loss')
plt.legend()
plt.grid()

plt.figure()
plt.plot(acc, 'b--', label='training accuracy')
plt.plot(val_acc, 'r:', label='validation accuracy')
plt.legend()
plt.grid()
```

![download1](https://user-images.githubusercontent.com/96654391/179434342-1cbd4455-7779-4e74-937c-636f7ad3a80f.png)

![download2](https://user-images.githubusercontent.com/96654391/179434346-648dc13d-b11a-4f18-8386-d153a650b4cb.png)

### 🌗 감정 예측

```python
def sentiment_predict(new_sentence):
  new_token = [word for word in mecab.morphs(new_sentence) if not word in stopwords]
  new_sequences = tokenizer.texts_to_sequences([new_token])
  new_pad = pad_sequences(new_sequences, maxlen = max_len)
  score = float(model.predict(new_pad))

  if score > 0.5:
    print("{} -> 긍정 ({:.2f}%)".format(new_sentence, score * 100))
  else:
    print("{} -> 부정 ({:.2f}%)".format(new_sentence, (1-score) * 100))

sentiment_predict("정말 재미있고 흥미진진 했어요.")
sentiment_predict("어떻게 이렇게 지루하고 재미없죠?")
sentiment_predict("배우 연기력이 대박입니다. ")
sentiment_predict("분위기가 어두워요")
sentiment_predict("스토리가 복잡해요 ")

>>>
정말 재미있고 흥미진진 했어요. -> 긍정 (98.87%)
어떻게 이렇게 지루하고 재미없죠? -> 부정 (99.74%)
배우 연기력이 대박입니다.  -> 긍정 (96.64%)
분위기가 어두워요 -> 부정 (81.39%)
스토리가 복잡해요  -> 긍정 (85.32%)
```

- texts_to_sequences(): 각 단어에 해당하는 인덱스를 바탕으로 텍스트를 시퀀스로 변환
  ex.
  ```python
  {'my': 1, 'love': 2, 'dog': 3, 'i': 4, 'you': 5, 'cat': 6, 'do': 7, 'think': 8, 'is': 9, 'amazing': 10}
  [[4, 2, 1, 3], [4, 2, 1, 6], [5, 2, 1, 3], [7, 5, 8, 1, 3, 9, 10]]
  ```
