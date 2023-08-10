---
title: "[백준 10844][DynamicProgramming1] 쉬운 계단 수"
excerpt: "[백준 10844][DynamicProgramming1] 쉬운 계단 수"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 10844 문제 링크](https://www.acmicpc.net/problem/10844) <br>

## 백준 10844 쉬운 계단 수

옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

## 실패 코드

```python
# 10844 쉬운 계단 수

# 옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

import sys

input = sys.stdin.readline
n = int(input())  # n 자리수
# 10, 12, 21, 23, 32, 34, 43, 45, 54, 56, 65, 67, 76, 78, 87, 89, 98
cnt = 0
num = [0 for i in range(10**n + 1)]  # 계단은 1부터 시작
# n == 1: 10**1 전까지
# n == 2: 10**2 전까지
# print(num)
is_possible = True
for i in range(10**(n - 1), 10**n):  # 딱 n자리 수까지만
    str_num = str(i)
    for j in range(1, n):
        if abs(int(str_num[j - 1]) - int(str_num[j])) != 1:
            is_possible = False
            break
        is_possible = True
    if is_possible:
        cnt += 1

print(cnt)
```

`메모리 초과`

## 풀이 코드

```python

```

## 코드 설명
