---
title: "[백준 1260][DFS & BFS] DFS와 BFS"
excerpt: "[백준 1260][DFS & BFS] DFS와 BFS"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
---

📌 [백준 1260 문제 링크](https://www.acmicpc.net/problem/1260)

## 풀이

```python
from collections import deque


def DFS(start_node):
    visited[start_node] = True
    print(start_node, end=" ")

    for i in graph[start_node]:
        if not visited[i]:
            DFS(i)


def BFS(start_node):
    queue = deque([start_node])
    visited[start_node] = True
    while queue:
        v = queue.pop(0)
        print(v, end=" ")
        for i in graph[v]:
            if not visited[i]:
                visited[i] = True
                queue.append(i)


n, m, v = map(int, input().split())

# 전역변수 graph -> 인접 리스트
graph = [[] for _ in range(n + 1)]
for i in range(m):
    node1, node2 = map(int, input().split())
    graph[node1].append(node2)
    graph[node2].append(node1)

# graph 정렬
for i in graph:
    i.sort()

# 방문 여부
visited = [False] * (n + 1)
DFS(v)
print()

visited = [False] * (n + 1)
bfsList = BFS(v)
```
