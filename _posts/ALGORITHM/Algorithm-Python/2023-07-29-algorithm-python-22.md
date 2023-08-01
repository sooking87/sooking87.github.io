---
title: "[백준 20444][BinarySearch] 색종이와 가위"
excerpt: "[백준 20444][BinarySearch] 색종이와 가위"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 20444 문제 링크](https://www.acmicpc.net/problem/20444) <br>

## 백준 20444 색종이와 가위

n번의 가위질로 k개의 색종이 조각을 만들 수 있다면 YES, 아니라면 NO를 출력

## 실패 코드

```python
# 20444 색종이와 가위

# n번의 가위질로 k개의 색종이 조각을 만들 수 있다면 YES, 아니라면 NO를 출력

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
# 1번 자름 -> 2개
# 2번 자름 -> 4개
# 3번 자름 -> 6개
# 4번 자름 -> 9개 / 8개
start = 1
end = k
count = 0
while start != end:
    mid = (start + end) // 2
    end = mid
    count += 1
    # print(start, end)
if count == n:
    print('YES')
else:
    print('NO')
```

mid 가 의미하고 있는게 무엇인지 중요한 것 같다... 뭐를 의미하고 있는거지,,,?

## 풀이 코드

```python

```

## 코드 설명
