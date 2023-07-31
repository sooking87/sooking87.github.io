---
title: "[백준 1654][BinarySearch] 랜선 자르기"
excerpt: "[백준 1654][BinarySearch] 랜선 자르기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 1654 문제 링크](https://www.acmicpc.net/problem/1654) <br>

## 백준 1654 랜선 자르기

k개의 랜선을 가지고 있는데, N개의 같은 길이의 랜선을 만들고 싶다.

## 풀이 코드

```python
# 1654 랜선 자르기

# k개의 랜선을 가지고 있는데, N개의 같은 길이의 랜선을 만들고 싶다.

import sys

input = sys.stdin.readline
k, n = map(int, input().split())
lines = []
for _ in range(k):
    lines.append(int(input()))

start = 1
end = max(lines)

while start <= end:
    mid = (start + end) // 2  # 최대 길이가 mid일 때
    line_cnt = 0
    # 개수가 count
    for i in lines:
        line_cnt += i // mid

    if line_cnt >= n:
        start = mid + 1
    else:
        end = mid - 1
print(end)

```

## 코드 설명

기존 이분 탐색의 코드에서 구하고자 하는데 필요한 랜선 개수를 구하기 위해 for 문을 사용 <br>

이 문제에서 mid 자체가 잘라야되는 랜선으로 활용이 되었다. 이분 탐색을 풀기 위해서는 mid 라는게 어떤거를 의미하고 어떻게 사용해야될지를 잘 생각해봐야될 것 같다.
