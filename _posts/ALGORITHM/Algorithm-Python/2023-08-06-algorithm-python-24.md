---
title: "[백준 1920][BinarySearch] 수 찾기"
excerpt: "[백준 1920][BinarySearch] 수 찾기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 1920 문제 링크](https://www.acmicpc.net/problem/1920) <br>

## 백준 1920 수 찾기

정수 n개 중 x라는 정수가 존재하는지 알아내는 프로그램

## 풀이 코드

```python
# 1920 수 찾기

# 정수 n개 중 x라는 정수가 존재하는지 알아내는 프로그램

import sys

input = sys.stdin.readline
n = int(input())
a = [int(i) for i in input().split()]
a.sort()
m = int(input())
is_in_a = [int(i) for i in input().split()]

for i in range(m):
    is_possible = False
    compare = is_in_a[i]
    start_idx = 0
    end_idx = n - 1
    while start_idx <= end_idx:
        mid_idx = (start_idx + end_idx) // 2
        if compare == a[mid_idx]:
            print(1)
            is_possible = True
            break
        if compare > a[mid_idx]:
            start_idx = mid_idx + 1
        else:
            end_idx = mid_idx - 1
    if not is_possible:
        print(0)
```


## 코드 설명

하나의 숫자에 대해서 해당 숫자가 있는지 없는지 탐색한다. = 전형적인 이분탐색의 문제