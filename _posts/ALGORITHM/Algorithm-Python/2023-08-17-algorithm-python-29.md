---
title: "[백준 2156][DynamicProgramming2] 포도주 시식"
excerpt: "[백준 2156][DynamicProgramming2] 포도주 시식"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2156 문제 링크](https://www.acmicpc.net/problem/2156) <br>

## 백준 2156 포도주 시식

연속으로 놓여져 있는 포도주 잔에서 최대의 양을 마실 수 있다. 최대의 양을 출력하는 프로그램

## 풀이 코드

```python
# 2156 포도주 시식

# 연속으로 놓여져 있는 포도주 잔에서 최대의 양을 마실 수 있다. 최대의 양을 출력하는 프로그램

import sys

input = sys.stdin.readline
n = int(input())
wine = [0] * 10000
for i in range(n):
    wine[i] = int(input())
# 이것도 부분합처럼 규칙이 있지 않을까?
# 6 10 13 9 8 1
dp = [0] * 10000
dp[0] = wine[0]
dp[1] = wine[0] + wine[1]
# 6 16 23 9
dp[2] = max(wine[2]+wine[0], wine[2]+wine[1], dp[1])
for i in range(3, n):
    dp[i] = max(wine[i]+dp[i-2], wine[i]+wine[i-1]+dp[i-3], dp[i-1])

print(max(dp))
```

## 코드 설명

규칙에 따라서 wine(입력값)과 dp(합)을 사용을 하는건데 동적 계획법은 이런식으로 진행을 하는 것 같다. <br>

+a. `dp = [0] * 10000` 이런 느낌으로 입력을 받는다면 인덱스 에러를 줄일 수 있다.