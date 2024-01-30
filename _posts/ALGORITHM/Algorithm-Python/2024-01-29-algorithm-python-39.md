---
title: "[백준 16935][Greedy] A -> B"
excerpt: "[백준 16935][Greedy] A -> B"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 16935 문제 링크](https://www.acmicpc.net/problem/16935) <br>

## 백준 16935 A -> B

정수 A를 B로 바꾸려고 한다. 

2를 곱하거나 1을 수의 가장 오른쪽에 추가한다. 두 가지 연산 중 연산의 최소값을 구해보자

## 실패 코드

```python
# 16935 A->B

# 정수 A를 B로 바꾸려고 한다. 
# 2를 곱하거나 1을 수의 가장 오른쪽에 추가한다. 두 가지 연산 중 연산의 최소값을 구해보자

import sys

input = sys.stdin.readline
a, b = map(int, input().split())
cnt = 0

while b > a:
    if b % 2 == 0:
        b //= 2

    elif (b % 10 != 0) and (int(str(b)[-1]) == 1):
        b //= 10
    cnt += 1
    
if a == b:
    print(cnt + 1)
else:
    print(-1)
```

`시간 초과` 발생

## 실패 코드

```python
# 16935 A->B

# 정수 A를 B로 바꾸려고 한다. 
# 2를 곱하거나 1을 수의 가장 오른쪽에 추가한다. 두 가지 연산 중 연산의 최소값을 구해보자

import sys

input = sys.stdin.readline
a, b = map(int, input().split())
cnt = 0

while b > a:
    if b % 2 == 0:
        b //= 2

    elif (b % 10 != 0) and (int(str(b)[-1]) == 1):
        b //= 10

    if (int(str(b)[-1]) != 1) and (b % 2 != 0):
        break
    cnt += 1
    # print(b)

    
if a == b:
    print(cnt + 1)
else:
    print(-1)
```

`15% 틀렸습니다.`

## 풀이 코드

```python
# 16935 A->B

# 정수 A를 B로 바꾸려고 한다. 
# 2를 곱하거나 1을 수의 가장 오른쪽에 추가한다. 두 가지 연산 중 연산의 최소값을 구해보자

import sys

input = sys.stdin.readline
a, b = map(int, input().split())
cnt = 0

while b > a:
    if b % 2 == 0:
        b //= 2

    elif (b % 10 != 0) and (int(str(b)[-1]) == 1):
        b //= 10
    cnt += 1

    if (int(str(b)[-1]) != 1) and (b % 2 != 0):
        break
    
if a == b:
    print(cnt + 1)
else:
    print(-1)
```

## 코드 설명

마지막이 1로 끝나지 않는 홀수는 만들어질 수 없으므로 해당 조건도 넣었어야 됐다.