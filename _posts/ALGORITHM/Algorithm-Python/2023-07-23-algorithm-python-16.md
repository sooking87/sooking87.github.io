---
title: "[백준 2668][DFS-BFS] 숫자 고르기"
excerpt: "[백준 2668][DFS-BFS] 숫자 고르기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2668 문제 링크](https://www.acmicpc.net/problem/2668) <br>

## 백준 2668 숫자 고르기

첫 째줄과 둘 째줄에서 집합으로 겹치는 최대 개수랑, 숫자를 출력

## 풀이 코드

📌 [참고 코드](https://velog.io/@deannn/BOJ-%EB%B0%B1%EC%A4%80-2668%EB%B2%88-%EC%88%AB%EC%9E%90%EA%B3%A0%EB%A5%B4%EA%B8%B0-Python) <br>

```python
# 2669 숫자고르기

# 첫 째줄과 둘 째줄에서 집합으로 겹치는 최대 개수랑, 숫자를 출력

# BFS, DFS를 어떤 식으로 사용하려나?
# https://velog.io/@deannn/BOJ-%EB%B0%B1%EC%A4%80-2668%EB%B2%88-%EC%88%AB%EC%9E%90%EA%B3%A0%EB%A5%B4%EA%B8%B0-Python
# 근데 왜 이코드가 dfs이지? -> 재귀 사용

import sys
from collections import deque

def make_set(first_line, second_line, num):
    first_line.add(num)
    second_line.add(arr[num])
    
    if arr[num] in first_line:
        if first_line == second_line: # 첫 째줄 집합과 둘 째줄 집합이 같다면
            ans.update(first_line)
            return True
        return False
    return make_set(first_line, second_line, arr[num])

input = sys.stdin.readline
n = int(input())
arr = [0]
for _ in range(n):
    arr.append(int(input()))

ans = set()
for i in range(1, n + 1):
    if i not in ans:
        make_set(set(), set(), i)

print(len(ans))
print(*sorted(list(ans)), sep = '\n')
```

## 코드 설명

첫 째줄에 있는 숫자와 매칭이 되고 있는 둘 째줄의 숫자를 따라간다고 생각하면 된다. <br>
1 -> 3이면 3에 매칭되는 숫자를 본다. <br>

`visited` 를 사용을 안한 이유는 이미 방문을 했더라도 다음 비교 숫자를 위해서 다시 방문이 필요할 수 있기 때문이다. <br>
그리고 first_line은 첫 번째 줄에 있던 숫자만 비교를 해가면서 추가를 하고, second_line은 두 번째 줄에 있던 숫자만 추가를 해서 비교를 한다.
