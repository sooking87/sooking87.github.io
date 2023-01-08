---
title: "[+a] DFS & BFS"
excerpt: "DFS & BFS"
categories: [Python Algorithm]
tags: [Python Algorithm, Python, Algorithm]
toc: true
toc_sticky: true
---

## DFS의 기본 개념

DFS란 Depth First Search의 약자로 그래프 자료에서 데이터를 탐색하는 알고리즘이다. <br>
DFS는 한 루트로 계속 들어가 탐색한 뒤 탐색을 마치면 다시 돌아가 방문하지 않은 루트로 들어가 탐색하는 과정을 말하며 보통 모든 경우의 수를 찾기 위한 _백 트래킹_ 시 자주 사용되는 탐색 알고리즘이다. <br>

<small>담주에는 백 트래킹 공부해봐야지</small>

## DFS의 기본 원칙

DFS에서 데이터를 찾을 때는 항상 **앞으로 찾아 가야할 노드** 와 **이미 방문한 노드** 를 기준으로 데이터를 탐색한다.

## DFS 구현

근데 이 중에서도 데이터들을 표현할 수 있는 방법은 여러가지가 있다. 딕셔너리나 리스트를 통해서 **인접 리스트** 처럼 표현을 하던가, **인접 행렬** 처럼 활용하는 방법이 있다. <br>

깊이를 우선적으로 탐색을 하기 때문에 새로운 노드가 들어올 때마다 방문하지 않았으면 끝까지 방문을 한다.

### 인접 행렬 VS 인접 리스트

1. 인접 행렬 <br>
   - 장점: 두 노드의 간선의 존재 여부를 바로 알 수 있음
   - 단점: 모든 관계를 기록함으로 노드의 개수가 많을수록 불필요한 메모리 낭비가 일어남
2. 인접 리스트 <br>
   - 장점: 연결된 것들만 기록, 어떤 노드의 인접한 노드들을 바로 알 수 있음.
   - 단점: 두 노드가 연결되어 있는지 확인이 인접 행렬보다는 느림.

### 인접 리스트 + 재귀함수

루트 노드가 있으면 루트 노드부터 밑으로 내려가면서(리스트 상 다음 인덱스로 넘어가면서) 방문하지 않은 노드를 다시 DFS 함수 상의 시작 노드로 넣게 된다.

```python
def DFS(start_node):
    visited[start_node] = True
    print(start_node, end=" ")

    for i in graph[start_node]:
        if not visited[i]:
            DFS(i)

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
```

### 인접 행렬 + 재귀 함수

```python
def DFS(start_node):
    visited[start_node] = True
    print(start_node, end=" ")

    for i in range(len(graph[start_node])):
        # 그래프에 존재하고, 방문하지 않은 경우
        if graph[start_node][i] == 1 and not visited[i]:
            DFS(i)

n, m, v = map(int, input().split())

# 전역변수 graph -> 인접 리스트
graph = [[0] * (n + 1) for _ in range(n + 1)]
for i in range(m):
    node1, node2 = map(int, input().split())
    graph[node1][node2] = graph[node2][node1] = 1

# 방문 여부
visited = [False] * (n + 1)
DFS(v)
```

## BFS의 기본 개념

시작 노드로부터 가까운 노드를 순차적으로 탐색하는 알고리즘이다.

## BFS의 기본 원칙

DFS에서 데이터를 찾을 때는 항상 **앞으로 찾아 가야할 노드** 와 **이미 방문한 노드** 를 기준으로 데이터를 탐색한다.

## BFS 구현

연결되어 있는 노드를 큐에 넣고 순차적으로 추출해나가는 과정을 통해 구현한다. 큐는 방문 해야될 노드를 넣어놓는 구조이다. BFS는 너비를 우선적으로 탐색을 하기 때문에 일단 시작 노드와 연결된 노드가 모두 방문될 때까지 queue에 넣어두고 다시 가장 첫 번째 노드부터 방문을 시작한다.

### 인접 리스트 + 큐

```python
from collections import deque

def BFS(start_node):
    queue = deque([start_node])
    visited[start_node] = True
    while queue:
        v = queue.popleft()
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

visited = [False] * (n + 1)
bfsList = BFS(v)
```

### 인접 행렬 + 큐

인접 리스트에서 돌아야 될 반복문의 범위가 인덱스로 바뀌면서 그래프 내에 노드가 있는지 없는지는 2차원 리스트로 확인을 한다.

```python
from collections import deque

def BFS(start_node):
    queue = deque([start_node])
    visited[start_node] = True
    while queue:
        v = queue.popleft()
        if not visited[v]:
            print(v, end=" ")
            visited[v] = True
            for i in range(len(graph[v])):
                if graph[start_node][i] == 1 and not visited[i]:
                    queue.append(i)

n, m, v = map(int, input().split())

# 전역변수 graph -> 인접 리스트
graph = [[0] * (n + 1) for _ in range(n + 1)]
for i in range(m):
    node1, node2 = map(int, input().split())
    graph[node1][node2] = graph[node2][node1] = 1

visited = [False] * (n + 1)
bfsList = BFS(v)
```
