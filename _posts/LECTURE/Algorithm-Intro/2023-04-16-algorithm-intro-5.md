---
title: "중간 고사"
excerpt: "중간 고사"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## Chap 02 :: 하노이 탑 문제

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
n = int(input())

# 2번을 해보세요!


def hanoi_tower(n, fr, tmp, to):
    if(n == 1):
        print("원판 1: %s --> %s" % (fr, to))
    else:
        hanoi_tower(n - 1, fr, to, tmp)
        print("원판 %d: %s --> %s" % (n, fr, to))
        hanoi_tower(n - 1, tmp, fr, to)


# 출력합니다!
hanoi_tower(n, 'A', 'B', 'C')

```

## Chap 03 :: 깊이 우선 탐색

```py
# 2116313 손수경
# 1번을 해보세요!
def dfs(graph, start, visited):
    if start not in visited:
        visited.add(start)
        print(start, end=' ')
        nbr = graph[start] - visited
        for v in nbr:
            dfs(graph, v, visited)
    return None


# 2번을 해보세요!
n = int(input())
mygraph = dict()
for i in range(n):
    a, b = input().split()
    mygraph[a] = mygraph.setdefault(a, set()) | {b}
    mygraph[b] = mygraph.setdefault(b, set()) | {a}
print(mygraph)


# 출력합니다!
print('DFS : ', end='')
dfs(mygraph, "A", set())
print()
```

## Chap 03 :: 너비 우선 탐색

```py
# 2116313 손수경
# 필요한 모듈을 추가해 보세요!
import queue
# 1번을 해보세요!


def bfs(graph, start):
    visited = {start}
    que = queue.Queue()
    que.put(start)
    while not que.empty():
        v = que.get()
        print(v, end=' ')
        nbr = graph[v] - visited
        for u in nbr:
            visited.add(u)
            que.put(u)

    return None


# 2번을 해보세요!
n = int(input())
mygraph = dict()
for i in range(n):
    a, b = input().split()
    mygraph[a] = mygraph.setdefault(a, set()) | {b}
    mygraph[b] = mygraph.setdefault(b, set()) | {a}

# 출력합니다!
print('BFS : ', end='')
bfs(mygraph, "A")
print()
```
