---
title: "[백준 21314][Implementation] 민겸수"
excerpt: "[백준 21314][Implementation] 민겸수"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 21314 문제 링크](https://www.acmicpc.net/problem/21314) <br>

## 백준 21314 민겸수

10**n꼴의 십진수는 M이 N+1개 

5*10**n꼴이면 n개의 m 뒤에 1개의 k를 이어붙히기


## 실패 코드

```python
# 21314 민겸수

# 10**n꼴의 십진수는 M이 N+1개
# 5*10**n꼴이면 n개의 m 뒤에 1개의 k를 이어붙히기

import sys

input = sys.stdin.readline
word = input().rstrip()
# MKKMMK -> 505500 / 155105
# K = 5 / M = 10
max = ''
min = ''
# 최소가 되려면 M 연속이면 M-1 개수만큼 0을 붙힌다
# 최소가 되려면 K가 나올때마다 끊어야됨
# 최대가 되려면 M 연속이면 K까지에서 끊어야됨
temp_min_cnt = 0
temp_max_cnt = 0
for i in range(len(word)):
    if i != len(word)-1:
        if word[i]=='M':
            if word[i+1]=='M':
                temp_min_cnt += 1
                temp_max_cnt += 1
            elif word[i+1]=='K':
                min += '1' + '0'*temp_min_cnt
                temp_min_cnt = 0
                temp_max_cnt += 1
                max += '5' + '0'*temp_max_cnt
                temp_max_cnt = 0
        elif word[i]=='K':
            min += '5'
            if word[i+1]=='K':
                temp_max_cnt = 0
                max += '5'
    else:
        if word[i]=='M':
            min += '1'
            max += '1'
        elif word[i]=='K':
            min += '5'
        

print(max)
print(min)
```
`1% 틀렸습니다.` -> 나름 규칙을 찾아서 했는데 반례가 뭐지? 

`MMM` 의 경우 연속된 상태로 끝이 나는 경우 숫자가 추가되지 않음.

## 풀이 코드

📌 [참고 코드](https://yuna0125.tistory.com/44) 

```python
# 21314 민겸수

# 10**n꼴의 십진수는 M이 N+1개
# 5*10**n꼴이면 n개의 m 뒤에 1개의 k를 이어붙히기

import sys

input = sys.stdin.readline
word = input().rstrip()
# MKKMMK -> 505500 / 155105
# K = 5 / M = 10
max = ''
min = ''
# 최소가 되려면 M 연속이면 M-1 개수만큼 0을 붙힌다
# 최소가 되려면 K가 나올때마다 끊어야됨
# 최대가 되려면 M 연속이면 K까지에서 끊어야됨
temp = 0
for i in word:
    if i == 'M':
        temp += 1
    else:
        if temp > 0:
            max += str(5 * (10**temp))
            min += str(10**temp + 5)
        else:
            max += '5'
            min += '5'
        temp = 0
        
# 'M'으로 끝날 경우
if temp>0:
    max += '1'*temp
    min += str(10**(temp-1))
print(max)
print(min)
```

## 코드 설명

temp를 기준으로 0 개수를 조절하여 min, max를 구하는데, 문제는 쉬워보이나 규칙을 찾기가 생각보다 복잡한,, 문제 -> 노트에 쓰면서 했으면 좀더 쉬웠으려나.. 

하,,, 또 포스팅은 왜 안올라가,,,,