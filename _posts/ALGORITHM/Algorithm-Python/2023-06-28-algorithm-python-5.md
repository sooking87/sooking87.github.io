---
title: "[백준 11047][Greedy] 동전 0"
excerpt: "[백준 11047][Greedy] 동전 0"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 11047 문제 링크](https://www.acmicpc.net/problem/11047) <br>

## 그리디 알고리즘

- 뭔가 개수를 세야되는데 최소를 구하라,, 이런 느낌이면 그리디를 사용하는 듯?

## 백준 11047 동전 0

N개의 동전의 가치를 입력받고, K의 가치를 만들기

## 실패 코드

```python
# 11047 동전 0

# N개의 동전의 가치를 입력받고, K의 가치를 만들기

n, k = map(int, input().split(' '))
values = []
for _ in range(n):
    values.append(int(input()))

# 가치가 큰 동전부터 K의 가치를 채울 수 있는지 확인
i = n - 1
cnt = 0
while True:
    # k보다 큰 가치라면 -> 그보다 작은 가치랑 비교 필요(--)
    if values[i] > k:
        i -= 1
    # k보다 작은 가치라면 -> 가치를 추가(cnt += 1)
    else:
        k -= values[i]
        cnt += 1
    if k == 0:
        break
print(cnt)

```

-> 70프로 정답 + 시간 초과 <br>

어제 풀었던 문제처럼 나뉘어지는거면 한 번에 나누면서 cnt에 더하는 것이 빠를 것 같다.

## 풀이 코드

```python
# 11047 동전 0

# N개의 동전의 가치를 입력받고, K의 가치를 만들기

n, k = map(int, input().split(' '))
values = []
for _ in range(n):
    values.append(int(input()))

# 가치가 큰 동전부터 K의 가치를 채울 수 있는지 확인
i = n - 1
cnt = 0
while True:
    # k보다 큰 가치라면 -> 그보다 작은 가치랑 비교 필요(--)
    if values[i] > k:
        i -= 1
    # k보다 작은 가치라면 -> values[i]로 나눈 나머지부터 다시 개수 세야됨
    else:
        cnt += k // values[i]
        k = k % values[i]
    if k == 0:
        break
print(cnt)
```

## 코드 설명

k보다 values[i]가 작다면 일단은 나누어지므로 그것만큼 개수를 count하고, 그 다음 나머지를 다시 values[i]랑 비교하면서 개수를 세어나아간다.
