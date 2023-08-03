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
# 20444 색종이와 가위

# n번의 가위질로 k개의 색종이 조각을 만들 수 있다면 YES, 아니라면 NO를 출력

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
# 1번 자름 -> 2개
# 2번 자름 -> 4개
# 3번 자름 -> 6개
# 4번 자름 -> 9개 / 8개
start = 0
end = n // 2
isPossible = False

# 가위질을 가로로 자른 횟수와 세로로 자른 횟수로 나뉨
# = 조각 개수는 (row_cut + 1) * (col_cut + 1)

# 거기에다가 row_cut과 col_cut은 대칭적이기 때문에 row_cut 기준으로 n // 2만큼 확인하면 됨
while start <= end:
    row_cut = (start + end) // 2 # mid라는게 가로로 자르는 횟수로 봄
    col_cut = n - row_cut

    pieces = (row_cut + 1) * (col_cut + 1)
    if k == pieces:
        print('YES')
        isPossible = True
        break
    if k > pieces:
        start = row_cut + 1
    else:
        end = row_cut - 1

if not isPossible:
    print('NO')

```
mid라는게 가로로 자르는 횟수로 봄. 

## 코드 설명


가위질을 가로로 자른 횟수와 세로로 자른 횟수로 나뉨 = 조각 개수는 (row_cut + 1) * (col_cut + 1) <br>

거기에다가 row_cut과 col_cut은 대칭적이기 때문에 row_cut 기준으로 n // 2만큼 확인하면 됨 <br>

잘려진 횟수가 k보다 적다는 것은 행으로 자른 횟수가 너무 적다는 것이므로 행 자르는 횟수를 늘린다. <br>
반대로 k보다 많다는 것은 행으로 자른 횟수는 줄이고 열로 자른 횟수를 늘려야된다는 것이다. <br>

이분 탐색이라는 주제 자체가 코드 상으로 이해는 쉬운데 그걸 이해하는 게 어렵다. 특히 mid를 어떻게 이해하고 어떤 식으로 활용해서 break 문을 만들 것인지가 중요한듯?