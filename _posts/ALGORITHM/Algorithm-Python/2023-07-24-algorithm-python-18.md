---
title: "[백준 2470][Sort] 두 용액"
excerpt: "[백준 2470][Sort] 두 용액"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2470 문제 링크](https://www.acmicpc.net/problem/2470) <br>

## 백준 2470 두 용액

## 실패 코드

```python
# 2470 두 용액

# 합쳐서 0에 가까운 두 용액을 출력

import sys
import math

input = sys.stdin.readline
n = int(input())
solution = [int(i) for i in input().split()]

solution.sort()
minus = 0
plus = len(solution) - 1
close_zero = math.inf
ans_minus = 0
ans_plus = 0
while True:
    while solution[plus] >= 0:
        temp = solution[minus] + solution[plus]
        if abs(close_zero) > abs(temp):
            close_zero = temp
            ans_minus = minus
            ans_plus = plus
        # print(solution[minus], solution[plus], temp)
        plus -= 1
    if minus >= plus:
        break
    minus += 1
    plus = len(solution) - 1
print(solution[ans_minus], solution[ans_plus])
```

`시간 초과` 에러

## 풀이 코드

```python

```

## 코드 설명
