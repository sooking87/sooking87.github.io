---
title: "[백준 19598][Greedy] 최소 회의실 개수"
excerpt: "[백준 19598][Greedy] 최소 회의실 개수"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 19598 문제 링크](https://www.acmicpc.net/problem/19598) <br>

## 백준 19598 최소 회의실 개수

N개의 회의를 모두 진행할 수 있는 최소 회의실 개수 구하기

## 실패 코드

```python
# 19598 최소 회의실 개수

# N개의 회의를 모두 진행할 수 있는 최소 회의실 개수

import sys
import heapq

input = sys.stdin.readline
n = int(input())
meetings = []
for _ in range(n):
    temp = [int(i) for i in input().split()]
    meetings.append(temp)

meetings.sort()
heap = []
heapq.heappush(heap, meetings[0][1])

for i in range(1, n):
    if meetings[i][0] > heap[0]:
        heapq.heappush(heap, meetings[i][1])
    if meetings[i][0] <= heap[0]:
        heapq.heappop(heap)
        heapq.heappush(heap, meetings[i][1])
print(len(heap))

```

저번 강의실 배정 문제랑 똑같아서 똑같이 풀었는데 틀림,,, 왜지?

## 풀이 코드

```python
# 19598 최소 회의실 개수

# N개의 회의를 모두 진행할 수 있는 최소 회의실 개수

import sys
import heapq

input = sys.stdin.readline
n = int(input())
meetings = []
for _ in range(n):
    temp = [int(i) for i in input().split()]
    meetings.append(temp)

meetings.sort()
heap = []
heapq.heappush(heap, meetings[0][1])

for i in range(1, n):
    if meetings[i][0] < heap[0]:
        heapq.heappush(heap, meetings[i][1])
    if meetings[i][0] >= heap[0]:
        heapq.heappop(heap)
        heapq.heappush(heap, meetings[i][1])

print(len(heap))

```

아래 조건문 부등호를 잘못한 것이었다. 그리고 저 조건문 두 개의 순서가 바뀌면 안됨 <br>

왜냐면 heappop을 한 다음 다시 `meetings[i][0] < heap[0]` 을 판별을 하기 때문에,, 아니면 elif로 해도 괜찮다!

## 코드 설명

강의실 배정 문제랑 알고리즘은 동일하다.
