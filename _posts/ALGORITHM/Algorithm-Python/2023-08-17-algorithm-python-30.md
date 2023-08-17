---
title: "[백준 2293][DynamicProgramming2] 동전 1"
excerpt: "[백준 2293][DynamicProgramming2] 동전 1"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2293 문제 링크](https://www.acmicpc.net/problem/2293) <br>

## 백준 2293 동전 1

n가지 종류의 동전 -> 가치의 합이 k원이 되도록하고 싶다. 그 경우의 수는?

## 풀이 코드

```python
# 2293 동전 1

# n가지 종류의 동전 -> 가치의 합이 k원이 되도록하고 싶다. 그 경우의 수는?

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
value = [int(input()) for i in range(n)]

dp = [0] * (k+1)
dp[0] = 1
# dp[k] 가 답이 될 수 있도록
for i in value:
    for j in range(i, k+1):
        if j-i >= 0:
            dp[j] += dp[j-i]
        # print(dp)
print(dp[k])
```

## 코드 설명

```python
dp[k] 가 답이 될 수 있도록
10 -> 5, 5 -> 1/2/2 5 -> 1/1/1/2 5 -> 1/1/1/1/1 5 -> 1/2/2 1/2/2 -> 1/2/2 1/1/1/2 -> 1/2/2 1/1/1/1/1 -> 1/1/1/2 1/2/2
0 1 1 0 0 1 0 0 0 0 0 #한 개로 만들 수 있는 가치
0 1 2(1(기존방법)+1(추가된 방법)) 1(0(기존방법)+1+1-1) 1 1 1 1 0 0 1 #두 개로 만들 수 있는 가치
0 1 2 2 2 2 2 2 1 1 1 #세 개로 만들 수 있는 가치
```
나는 동전 1개로 해당 가치를 만들 수 있는 방법 -> 2개로 해당 가치를 만들 수 있는 방법,,, <br>

이렇게 하려고 했는데 아무리 해도 규칙을 못찾아서 찾아보니까 1원을 무조건 썼을 때 해당 가치를 만들 방법, 2원을 무조건 썼을 때 해당 가치를 만들 방법 ,, 이런식으로 했다,, <br>

아쉽다 거의 했는데,,,,😢