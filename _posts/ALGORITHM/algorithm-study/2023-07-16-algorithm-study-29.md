---
title: "[Python] BFS & DFS"
excerpt: "[Python] BFS & DFS"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

📌 [[Daily PS] 파이썬으로 구현하는 BFS와 DFS](https://cyc1am3n.github.io/2019/04/26/bfs_dfs_with_python.html)

## DFS(Depth First Search, 깊이 우선 탐색)

![gif](https://upload.wikimedia.org/wikipedia/commons/7/7f/Depth-First-Search.gif) <br>

스택을 사용해서 구현 가능 <br>
파이썬에서 스택은 리스트를 사용해서 `append` 와 `pop` 을 사용

```python
def DFS(graph, root):
    visited = []
    stack = [root]

    while stack:
        n = stack.pop()
        if n not in visited:
            visited.append(n)
            # 방문 했던 노드는 제외하고 스택에 추가
            stack += graph[n] - set(visited)
    return ''.join(str(i) for i in visited)
```

## BFS(Breadth First Search, 너비 우선 탐색)

![gif](https://upload.wikimedia.org/wikipedia/commons/5/5d/Breadth-First-Search-Algorithm.gif) <br>

이 알고리즘의 핵심은 **큐** 자료구조를 사용하는 것이다. <br>
노드를 방문하면서 인접한 노드 중 방문하지 않았던 노드의 정보만 큐에 넣어서 먼저 큐에 들어있던 노드부터 방문 <br>

파이썬으로 큐를 구현하는 방법으로는 <br>
`list.append` , `list.pop(0)` -> 비효율적인 코드 <br>
`from collections import deque` :: `queue.append` , `queue.popleft()` -> 사용

```python
def BFS(graph, root):
    visited = []
    queue = deque([root])

    while queue:
        n = queue.popleft()
        if n not in visited:
            visited.append(n)
            queue += graph[n] - set(visited)

    return visited
```
