---
title: "[백준 20365][Greedy] 블로그 2"
excerpt: "[백준 20365][Greedy] 블로그 2"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 20365 문제 링크](https://www.acmicpc.net/problem/20365) <br>

## 백준 20365 블로그 2

풀어야되는 문제수 n, r은 빨간색, b는 파란색으로 칠한다. 이때 칠해야되는 최소 번수를 구해라.

## 실패 코드

처음에 단순 R의 개수 + 1 만큼 칠하는게 칠해야되는 최소 횟수인 줄 알았다..

```python
# 20365 블로그 2

# 풀어야되는 문제수 n, r은 빨간색, b는 파란색으로 칠한다.

import sys

input = sys.stdin.readline
n = int(input())
colors = list(input())[:-1]
cnt = 0

for i in colors:
    if i == 'R':
        cnt += 1

print(cnt + 1)
```

근데 왜 안되지? <br>
 
문제에는 `1~7번 문제를 파란색, 3번을 빨간색, 5번을 빨간색, 8번을 빨간색으로 순서대로 칠한다면 작업 횟수는 4번으로 가장 적다.` 이렇게 나와있다. -> 그럼 마지막이 R 인 경우와 아닌 경우로 나누어야되나? 무슨 차이지? 

## 실패 코드

전체 파란색으로 칠하고 부분부분 빨간색으로 칠하기 vs 색깔이 바뀔 때마다 색 칠하기 -> min 값 구하기

```python
# 20365 블로그 2

# 풀어야되는 문제수 n, r은 빨간색, b는 파란색으로 칠한다.

import sys

input = sys.stdin.readline
n = int(input())
colors = list(input())[:-1]
cnt_list = []
cnt1 = 0
cnt2 = 0

# 한 번에 파란색을 칠하고 빨간색만 추가적으로 칠하는 경우
for i in colors:
    if i == 'R':
        cnt1 += 1
cnt_list.append(cnt1+1)

# 교차로 칠하는 경우
for i in range(len(colors)-1):
    if colors[i] != colors[i+1]:
        cnt2 += 1
cnt_list.append(cnt2+1)

print(min(cnt_list))
```

```txt
10
RRBBRRBBRR
```

반례 발견

## 풀이 코드


```python
# 20365 블로그 2

# 풀어야되는 문제수 n, r은 빨간색, b는 파란색으로 칠한다.

import sys

input = sys.stdin.readline
n = int(input())
colors = list(input())[:-1]
cnt_list = []
cnt1 = 0
cnt2 = 0
cnt3 = 0

# 한 번에 파란색을 칠하고 빨간색만 추가적으로 칠하는 경우 + 바뀌기 전까지만 한 번에 칠하기 -> 반드시 파란색으로 덮는 것이 아니라 빨간색으로 덮고 파란색을 덫칠하는 경우도 생각

# 전체 파란칠 + R만 위에 덫칠
for i in range(len(colors)-1):
    if colors[i]=='B' and colors[i+1]=='R':
        cnt1 += 1
    if colors[0] == 'R':
        cnt1 += 1
cnt_list.append(cnt1+1)

# 전체 빨간칠 + B만 위에 덫칠
for i in range(len(colors)-1):
    if colors[i] == 'R' and colors[i+1] == 'B':
        cnt2 += 1
    if colors[0] == 'B':
        cnt2 += 1
cnt_list.append(cnt2+1)

# 해당 색깔별로 각각 칠하기
for i in range(len(colors)-1):
    if colors[i] != colors[i+1]:
        cnt3 += 1
cnt_list.append(cnt3+1)

# print(cnt_list)
print(min(cnt_list))
```

## 코드 설명

case를 나누어서 문제 풀이를 진행하면 되었다. <br>

- 전체 파란칠 + R만 위에 덫칠
- 전체 빨간칠 + B만 위에 덫칠
- 해당 색깔별로 각각 칠하기 <br>

이렇게 case를 나누어서 문제 풀이를 진행하였다.