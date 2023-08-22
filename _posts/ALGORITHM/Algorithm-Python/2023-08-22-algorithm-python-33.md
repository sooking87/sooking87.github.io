---
title: "[백준 17609][String] 회문"
excerpt: "[백준 17609][String] 회문"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 17609 문제 링크](https://www.acmicpc.net/problem/17609) <br>

## 백준 17609 회문

회문이면 0 출력, 유사회문이면 1 출력, 그 외 2 출력

## 실패 코드

```python
# 17609 회문

# 회문이면 0 출력, 유사회문이면 1 출력, 그 외 2 출력

import sys

input = sys.stdin.readline
n = int(input())
for _ in range(n):
    string = list(input().strip())
    length = len(string) // 2
    start = 0
    end = len(string) - 1
    is_possible = False # 회문인지 아닌지를 판별
    cnt = 0 # 유사회문인지 아닌지를 판별
    for i in range(length):
        if string[start] == string[end]:
            is_possible = True
            start += 1
            end -= 1
            continue
        else:
            is_possible = False
            if string[start+1] == string[end] or string[start] == string[end-1]:
                cnt += 1
                is_possible = True
            break
        
    if is_possible == True and cnt == 0:
        print(0)
    elif is_possible == True and cnt == 1:
        print(1)
    else:
        print(2)
```

`정답(1%)` ,, 뭐가 문제,,,? 시간이 너무 오래걸리나?

## 풀이 코드

```python

```

## 코드 설명
