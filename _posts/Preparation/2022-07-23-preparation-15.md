---
title: "[NLP] 데이터셋 가져오기"
excerpt: "[NLP] 데이터셋 가져오기"
categories: [Preparation]
tags: [Preparation, Python]
toc: true
toc_sticky: true
---

- Sentiment Analysis of all Billboard Hot 100 Songs Over Time (1958–2019)
  <https://towardsdatascience.com/sentiment-analysis-of-all-billboard-hot-100-songs-over-time-1958-2019-3329439e7c1a>

- Programming for Cultural Heritage - Demo: Working with Genius.com API
  <https://www.youtube.com/watch?v=CokKFmDnDtw>
  -> 가사를 불러오는데 사용되는 API <br>
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

## 데이터셋

기존에 정했던 billboard100 데이터셋과 genius API를 사용해서 데이터를 불러올 예정이다.

[charts.csv](%5BNLP%5D%20Datasets%20a1d30c9bc3b84a5ba1f95e668742bc54/charts.csv)

노래 기준으로 중복을 없애면 32만 개에서 2만 5천개가 되는데 이게 맞아,,,,,,,,,,?

여튼,,근데 내 컴이 이상한 건지는 모르겠지만 한 번에 돌릴려고 시도해봤는데, 5000개 하는데 5시간 걸림,,,그냥 가사만 불러오는데,, 이게 맞아 ㅋ? 그래서 몇 개씩 분리해서 데이터를 가져오고 한 번에 합치는 방안으로 코드를 작성함!

### sample → 10개씩 분리 → join

[ 목표 ] : billboard_data.csv 얘랑 합치기 → 안 맞는 columns 가 있어서 최소한의 데이터만 가지고 합쳐야 될 듯,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

[ 데이터셋 길이 ] : (24436, 7)

[billboard_data.csv](%5BNLP%5D%20Datasets%20a1d30c9bc3b84a5ba1f95e668742bc54/billboard_data.csv)

```python
# 분리
import csv
import os
import pandas as pd

temp_df = pd.read_csv('./charts.csv', index_col=False)
temp_df.drop_duplicates(subset='song', inplace=True)
temp_df.reset_index()
testTemp1_df = temp_df.iloc[0:10, 0:]
testTemp2_df = temp_df.iloc[10:20, 0:]

testTemp1_df.to_csv("billboard_sample1.csv", index=False)
testTemp2_df.to_csv("billboard_sample2.csv", index=False)
```

[billboard_sample1.csv](%5BNLP%5D%20Datasets%20a1d30c9bc3b84a5ba1f95e668742bc54/billboard_sample1.csv)

genius 토큰 필요 ⇒ 공유해도 되려나,,?

```python
# sample 1 담당
# install modules
"""
pip install lyricsgenius
pip install vaderSentiment
pip install pandas
"""
import lyricsgenius
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer
import pandas as pd

# Function to return song lyrics

def get_lyrics(title, artist):
    try:
        return genius.search_song(title, artist).lyrics
    except:
        return 'not found'

# Function to return sentiment score of each song

def get_lyric_sentiment(lyrics):
    sentiment = sid_obj.polarity_scores(lyrics)
    return sentiment

genius = lyricsgenius.Genius(
    "DuO42xKa4Ts70InLe_Y_strEpeL_CxowzCtXyAMaiNlbAOVOTfFpt2q5FdP4lo_U")
sid_obj = SentimentIntensityAnalyzer()

"""sample: billboard_sample1.csv / actual: charts.csv"""
billboard100_1_df = pd.read_csv('billboard_sample1.csv')
billboard100_1_df = billboard100_1_df.drop(
    ['rank', 'last-week', 'peak-rank', 'weeks-on-board'], axis=1)
billboard100_1_df.drop_duplicates(subset='song', inplace=True)
billboard100_1_df.reset_index(drop=True)

# 노래 가사 불러오기
lyics1 = billboard100_1_df.apply(lambda row: get_lyrics(
    row['song'], row['artist']), axis=1)
billboard100_1_df['lyrics'] = lyics1
print(billboard100_1_df.shape)
# not found 제거
billboard100_1_df = billboard100_1_df.drop(
    billboard100_1_df[billboard100_1_df['lyrics'] == 'not found'].index)

# Use get_lyric_sentiment to get sentiment score for all the song lyrics
sentiment1 = billboard100_1_df.apply(
    lambda row: get_lyric_sentiment(row['lyrics']), axis=1)

for i in billboard100_1_df.index.tolist():
    billboard100_1_df.loc[i, 'neg_sentiment'] = sentiment1[i]['neg']
    billboard100_1_df.loc[i, 'neu_sentiment'] = sentiment1[i]['neu']
    billboard100_1_df.loc[i, 'pos_sentiment'] = sentiment1[i]['pos']
    billboard100_1_df.loc[i, 'com_sentiment'] = sentiment1[i]['compound']

billboard100_1_df.to_csv("billboard_dataset.csv", index=False)
```

[billboard_sample2.csv](%5BNLP%5D%20Datasets%20a1d30c9bc3b84a5ba1f95e668742bc54/billboard_sample2.csv)

```python
# sample 2 담당
# install modules
"""
pip install lyricsgenius
pip install vaderSentiment
pip install pandas
"""
import lyricsgenius
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer
import pandas as pd

# Function to return song lyrics

def get_lyrics(title, artist):
    try:
        return genius.search_song(title, artist).lyrics
    except:
        return 'not found'

# Function to return sentiment score of each song

def get_lyric_sentiment(lyrics):
    sentiment = sid_obj.polarity_scores(lyrics)
    return sentiment

genius = lyricsgenius.Genius(
    "DuO42xKa4Ts70InLe_Y_strEpeL_CxowzCtXyAMaiNlbAOVOTfFpt2q5FdP4lo_U")
sid_obj = SentimentIntensityAnalyzer()
"""sample: billboard_sample2.csv / actual: charts.csv"""
billboard100_2_df = pd.read_csv('billboard_sample2.csv')
billboard100_2_df = billboard100_2_df.drop(
    ['rank', 'last-week', 'peak-rank', 'weeks-on-board'], axis=1)
billboard100_2_df.drop_duplicates(subset='song', inplace=True)
billboard100_2_df.reset_index(drop=True)

# 노래 가사 불러오기
lyrics2 = billboard100_2_df.apply(lambda row: get_lyrics(
    row['song'], row['artist']), axis=1)
billboard100_2_df['lyrics'] = lyrics2
print(billboard100_2_df.shape)
# not found 제거
billboard100_2_df = billboard100_2_df.drop(
    billboard100_2_df[billboard100_2_df['lyrics'] == 'not found'].index)

# Use get_lyric_sentiment to get sentiment score for all the song lyrics
sentiment2 = billboard100_2_df.apply(
    lambda row: get_lyric_sentiment(row['lyrics']), axis=1)

for i in billboard100_2_df.index.tolist():
    billboard100_2_df.loc[i, 'neg_sentiment'] = sentiment2[i]['neg']
    billboard100_2_df.loc[i, 'neu_sentiment'] = sentiment2[i]['neu']
    billboard100_2_df.loc[i, 'pos_sentiment'] = sentiment2[i]['pos']
    billboard100_2_df.loc[i, 'com_sentiment'] = sentiment2[i]['compound']

billboard100_2_df.to_csv("billboard_sample2.csv", index=False)
```

```python
# join
import pandas as pd

temp1_df = pd.read_csv('billboard_sample1.csv', index_col=False)
temp2_df = pd.read_csv('billboard_sample2.csv', index_col=False)
final_df = pd.concat([temp1_df, temp2_df], ignore_index=True)
final_df.reset_index()

print(final_df)
```

[billboard_sample_total.csv](%5BNLP%5D%20Datasets%20a1d30c9bc3b84a5ba1f95e668742bc54/billboard_sample_total.csv)
