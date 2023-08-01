---
title: "[백준 14916][Greedy] 거스름돈"
excerpt: "[백준 14916][Greedy] 거스름돈"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 14916 문제 링크](https://www.acmicpc.net/problem/14916) <br>

## 그리디 알고리즘

- 그리디 알고리즘은 탐욕법이라고도 하며, 현재 상황에서 지금 당장 좋은 것만 고르는 방법
- 일반적인 그리디 알고리즘은 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력을 요구

## 백준 14916 거스름돈

거스름돈 동전의 개수가 최소가 되도록 거슬러주기

## 풀이 코드

```python
# 14916 거스름돈

# 거스름돈 동전의 개수가 최소가 되도록 거슬러주기

coins = [5, 2]
money = int(input())
count = 0

while True:
    # 5원부터 거스름돈 구하기 -> 최소가 되기 위함
    if money % 5 == 0:
        count += money // 5
        money = 0
    # 거스를 수 없으면(음수) -> -1 출력
    # 거스를 수 있으면(0) -> count 출력
    if money < 0:
        print(-1)
        break
    elif money == 0:
        print(count)
        break
    # 5원을 못거스르면 2원씩 빼기
    money -= 2
    count += 1
```

## 코드 설명

5원으로 나뉘어진다면 `money // 5` 만큼 나누어 주는게 BEST <br>
그게 아니라면 2월을 빼보고 다시 5원으로 나누어지는지 확인(5로 나누어지는게 BEST기 때문)
