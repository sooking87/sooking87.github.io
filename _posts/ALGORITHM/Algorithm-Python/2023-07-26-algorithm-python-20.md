---
title: "[백준 2437][Sort] 저울"
excerpt: "[백준 2437][Sort] 저울"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2437 문제 링크](https://www.acmicpc.net/problem/2437) <br>

## 백준 2437 저울

## 실패 코드

```python
# 2437 저울

# 입력받은 무게추들 중에서 측정할 수 없는 양의 정수 무게 중 최솟값을 구하기

import sys
import itertools as it

input = sys.stdin.readline
n = int(input())
weight = [int(i) for i in input().split()]
weight.sort()
# print(weight)
can_weight = [False for i in range(sum(weight) + 1)] # 인덱스랑 무게랑 맞춤

for repeat in range(len(weight)):
    pendulum = list(it.combinations(weight, repeat))
    # print(pendulum)
    for i in range(len(pendulum)):
        idx = sum(pendulum[i])
        if not can_weight[idx]:
            can_weight[idx] = True
print(can_weight.index(False))
```

일단 조합을 이용해서 가능한 무게에 대해서 하나하나 기록 -> `메모리 초과` <br>

일단 골드 문제이고 제한 시간이 1초 이기 때문에 어느정도,,, 예상은 함. 근데 이러 말고 할 수 있는 방법이 없을까? <br>
최소값을 구하는 것이기에 마지막 까지는 가능한 모든 무게를 구할 필요는 없다.

## 풀이 코드

```python
# 2437 저울

# 입력받은 무게추들 중에서 측정할 수 없는 양의 정수 무게 중 최솟값을 구하기

import sys
import itertools as it

input = sys.stdin.readline
n = int(input())
weight = [int(i) for i in input().split()]
weight.sort()

target = 1
# w를 더하다가 target보다 크게되면 그 다음 숫자부터는 만들 수 없는 추 무게가 된다...
for w in weight:
    if target < w:
        break
    target += w
print(target)
```

## 코드 설명

w를 더하다가 target보다 크게되면 그 다음 숫자부터는 만들 수 없는 추 무게가 된다... <br>

<small>아니 이런걸 어케 생각함.. 생각보다 코드는 넘 간단해 ㅎ,,,</small>
