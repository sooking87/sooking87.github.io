---
title: "[백준 10814][Sort] 나이순 정렬"
excerpt: "[백준 10814][Sort] 나이순 정렬"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 10814 문제 링크](https://www.acmicpc.net/problem/10814) <br>

## 백준 10814 나이순 정렬

나이순 오름차순 정렬 -> 나이가 같다면 가입한 순으로 한 줄에 한 명씩 출력

## 풀이 코드

```python
# 10814 나이순 정렬

# 나이순 오름차순 정렬 -> 나이가 같다면 가입한 순으로 한 줄에 한 명씩 출력

import sys

input = sys.stdin.readline
n = int(input())
people = []
for _ in range(n):
    age, name = input().split()
    temp = []
    temp.append(int(age))
    temp.append(name)
    people.append(temp)

people.sort(key=lambda x: x[0])  # 나이로만 정렬

for i in range(n):
    age, name = people[i]
    print(age, name)
```

## 코드 설명

`people.sort(key=lambda x: x[0])` lambda를 통해서 나이로만 정렬이 되고, 나이가 같은 경우는 입력받은 대로 정렬이 될 수 있도록 코딩함.
