---
title: "[백준 16926][Implementation] 배열 돌리기 1"
excerpt: "[백준 16926][Implementation] 배열 돌리기 1"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 16926 문제 링크](https://www.acmicpc.net/problem/16926) <br>

## 백준 16926 배열 돌리기 1

첫 째줄 배욜의 크기 n, m, 회전의 수 r이 입력될 때, r만큼 회전을 시킨다.

## 풀이 코드

```python
# 16926 배열 돌리기 1

# 첫 째줄 배욜의 크기 N, M, 회전의 수 R
# 둘 째줄 N개의 줄에 원소가 주어짐

# 2차원 -> 1차원으로 바꿔서 R 만큼 인덱스 수정

import sys
from collections import deque

input = sys.stdin.readline
n, m, r = map(int, input().split())
arr = []
deq = deque() # popleft를 통해서 O(1)을 사용하기 위해서
answer = [[0]*m for _ in range(n)]
loops = min(n, m) // 2

for i in range(n):
    temp = list(map(int, input().split()))
    arr.append(temp)

for i in range(loops):
    # 1차원 배열로 변환
    deq.clear()
    deq.extend(arr[i][i:m-i]) # 위쪽
    deq.extend([row[m-i-1] for row in arr[i+1:n-i-1]]) # 오른쪽
    deq.extend(arr[n-i-1][i:m-i][::-1]) # 아래쪽
    deq.extend([row[i] for row in arr[i+1:n-i-1]][::-1]) # 왼쪽

    deq.rotate(-r) # -r만큼 오른쪽으로(-이므로 왼쪽으로) 회전한다.
    for j in range(i, m-i):
        answer[i][j] = deq.popleft()
    for j in range(i+1, n-i-1):
        answer[j][m-i-1] = deq.popleft()
    for j in range(m-i-1, i-1, -1):
        answer[n-i-1][j] = deq.popleft()
    for j in range(n-i-2, i, -1):
        answer[j][i] = deq.popleft()

for row in answer:
    for col in row:
        print(col, end=' ')
    print()
```

## 코드 설명

- [참고 코드](https://velog.io/@leetaekyu2077/%EB%B0%B1%EC%A4%80-16926%EB%B2%88-%EB%B0%B0%EC%97%B4-%EB%8F%8C%EB%A6%AC%EA%B8%B0-1) <br>

2차원을 1차원으로 바꾸어서 `rotate` 함수를 사용하였다. 제일 바깥 껍질부터 한 줄(1차원)으로 만든 후 rotate를 사용하였다. <br>

근데 여기서 바깥 껍질을 1줄로 만드는 과정, 1줄로 만든 껍질을 2줄로 만드는 것이 너무 어려웠다.. (사실 지금도,,,,,,,,) 인덱스를 통해서 2차원 <-> 1차원을 바꾸는 것이 정말 어려웠다..

