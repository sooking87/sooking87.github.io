---
title: "[NLP] 텍스트 전처리 과정(Eng ver)"
excerpt: "[NLP] 텍스트 전처리 과정(Eng ver)"
categories: [Preparation]
tags: [Preparation, Python]
toc: true
toc_sticky: true
---

## 💎 텍스트 전처리

- 클렌징: HTML, XML 태그나 특정 기호를 제거
- 텍스트 토큰화(문장 토큰화, 단어 토큰화) -> NLTK는 토큰화를 위한 다양한 API 제공
- 스톱 워드(불용어) 제거
- Stemming, Lemmatization

### 문장 토큰화

마침표, \n 등 문장의 마지막을 뜻하는 기호에 따라 분리하는 것

```python
from nltk import sent_tokenize # 문장 토큰화 과정
import nltk
nltk.download('punkt') # 마침표, 개행 문자 등의 데이터 세트

text_sample = 'I was wondering if anyone out there could enlighten me on this car I saw the other day. It was a 2-door sports car, looked to be from the late 60s/\nearly 70s.'
sentences = sent_tokenize(text = text_sample)
print(type(sentences), len(sentences))
print(sentences)

>>>
<class 'list'> 2
['I was wondering if anyone out there could enlighten me on this car I saw the other day.', 'It was a 2-door sports car, looked to be from the late 60s/\nearly 70s.']
[nltk_data] Downloading package punkt to /root/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
```

### 단어 토큰화

기본적으로 공백, 콤마, 마침표, 개행문자 등으로 단어를 분리

```python
from nltk import word_tokenize

sentence = 'I was wondering if anyone out there could enlighten me on this car I saw the other day.'
words = word_tokenize(sentence)
print(type(words), len(words))
print(words)

>>>
<class 'list'> 19
['I', 'was', 'wondering', 'if', 'anyone', 'out', 'there', 'could', 'enlighten', 'me', 'on', 'this', 'car', 'I', 'saw', 'the', 'other', 'day', '.']
```

total

```python
from nltk import word_tokenize, sent_tokenize

# 여러 개의 문장으로 된 입력 데이터를 문장별로 단어 토큰화하게 만드는 함수
def tokenize_text(text):
  # 문장별로 분리 토큰 -> 1차원 리스트에 문장들이 들어있다.
  sentences = sent_tokenize(text)
  print('sentences', sentences)
  # 단어 별로 분리 토큰
  word_tokens = []
  for sentence in sentences: # 리스트에서 문장 하나를 가지고 와야되니까 반복문 사용.
    print('sentence', sentence)
    word_tokens.append(word_tokenize(sentence))
  return word_tokens
```

### 스톱 워드 제거

영어에서는 `is, the, a, will` 등 문맥적으로 의미가 없는 단어를 말하며 한국어에서는 `'의','가','이','은','들','는','좀','잘','걍','과','도','를','으로','자','에','와','한','하다'` 가 있다.
nltk에서 영어에 대한 stop word는 제공한다.

```python
import nltk
nltk.download('stopwords')

print('영어 stop words 개수:', len(nltk.corpus.stopwords.words('english')))
print(nltk.corpus.stopwords.words('english')[:20])

>>>
[29]
0초
import nltk
nltk.download('stopwords')

print('영어 stop words 개수:', len(nltk.corpus.stopwords.words('english')))
print(nltk.corpus.stopwords.words('english')[:20])
영어 stop words 개수: 179
['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves', 'you', "you're", "you've", "you'll", "you'd", 'your', 'yours', 'yourself', 'yourselves', 'he', 'him', 'his']
[nltk_data] Downloading package stopwords to /root/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
```

stop word 제거

```python
import nltk

stopwords = nltk.corpus.stopwords.words('english')
all_tokens = []
text_sample = 'I was wondering if anyone out there could enlighten me on this car I saw the other day. It was a 2-door sports car, looked to be from the late 60s/\nearly 70s.'
word_tokens = tokenize_text(text_sample)
print('word_tokens', word_tokens)
for sentence in word_tokens: # 단어 토큰화 된 한 문장 하나 당 반복문을 돌리면서 word 하나로 접근
  filtered_words = [] # stopword를 뺀 나머지
  # 개별 문장별로 토큰화된 문장 list 에 대해 스톱 워드를 제거하는 반복문
  for word in sentence:
    # 소문자로 모두 변환합니다.
    word = word.lower()
    # 토큰화된 개별 단어가 스톱 워드의 단어에 포함되지 않으면 word_tokens 에 추가
    if word not in stopwords:
      filtered_words.append(word)
  all_tokens.append(filtered_words)
print('all_tokens', all_tokens)

>>>
word_tokens [['I', 'was', 'wondering', 'if', 'anyone', 'out', 'there', 'could', 'enlighten', 'me', 'on', 'this', 'car', 'I', 'saw', 'the', 'other', 'day', '.'], ['It', 'was', 'a', '2-door', 'sports', 'car', ',', 'looked', 'to', 'be', 'from', 'the', 'late', '60s/', 'early', '70s', '.']]
all_tokens [['wondering', 'anyone', 'could', 'enlighten', 'car', 'saw', 'day', '.'], ['2-door', 'sports', 'car', ',', 'looked', 'late', '60s/', 'early', '70s', '.']]
```

### Stemming과 Lemmatization

과거/현재, 3인칭 단수 여부, 진행형 등 많은 조건에 따라 원래 단어가 변화한다.
work
works
worked
working ...

- stemming: 원형 단어로 변환 시 일반적인 방법을 적용하거나 더 단순화된 방법을 적용 -> 원래 단어에서 일부 철자가 훼손된 어근 단어를 추출하는 경향이 있다.
- Lemmatization: Stemming 보다 변환에 더 오랜 기간이 필요하다.

NLTK는 다양한 Stemmer을 제공
Porter, Lancaster, Snowball Stemmer
Lemmatization인 경우는 WordNetLemmatizer을 제공

- Stemming

  ```python
  from nltk.stem import LancasterStemmer
  stemmer = LancasterStemmer()

  print(stemmer.stem('working'), stemmer.stem('works'), stemmer.stem('worked'))
  print(stemmer.stem('amusing'), stemmer.stem('amuses'), stemmer.stem('amused'))
  print(stemmer.stem('happier'), stemmer.stem('happiest'))
  print(stemmer.stem('fancier'), stemmer.stem('fanciest'))

  >>>
  work work work
  amus amus amus
  happy happiest
  fant fanciest
  ```

- Lemmatization

  ```python
  from nltk.stem import WordNetLemmatizer
  import nltk
  nltk.download('omw-1.4')
  nltk.download('wordnet') # 일반적으로 원형 단어 추출을 위해 단어의 품사를 입력

  lemma = WordNetLemmatizer()
  print(lemma.lemmatize('amusing', 'v'), lemma.lemmatize('amuses', 'v'), lemma.lemmatize('amused', 'v'))
  print(lemma.lemmatize('happier', 'a'), lemma.lemmatize('happiest', 'a'))
  print(lemma.lemmatize('fancier', 'a'), lemma.lemmatize('fanciest', 'a'))

  >>>
  amuse amuse amuse
  happy happy
  fancy fancy
  ```
