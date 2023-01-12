---
title: "[백준 2178] 미로 탐색"
excerpt: "[백준 2178] 미로 탐색"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
---

📌 [백준 2178 문제 링크](https://www.acmicpc.net/problem/2178) <br>

BFS, DFS 관련 문제를 찾아보다가 **미로 탐색** 이라는 문제를 발견했다. BFS, DFS는 이름에서처럼 탐색을 할 때 사용하는 것을 알 수 있다. <br>

- BFS: queue를 사용해서 조건에 맞으면 queue에 넣는 식으로 진행을 한다. (앞에서부터 검사)
- DFS: list를 사용해서 조건에 맞으면 list에 넣는 식으로 진행을 한다. (뒤에서부터 검사)

## 풀이 코드

```python
from collections import deque


def bfs(x, y):
    # 이동할 네 가지 방향 정의
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]

    # deque 생성
    queue = deque()
    queue.append((x, y))

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            # 그래프 내에서 벗어나면 안됨
            if nx < 0 or nx >= row or ny < 0 or ny >= col:
                continue
            # 0 이면 이동 불가
            if graph[nx][ny] == 0:
                continue
            # 1 이면 이동 가능
            if graph[nx][ny] == 1:
                # 이동 횟수를 위해서 전에 (x, y)가 몇 번째 이동한 것인지를 체크
                graph[nx][ny] = graph[x][y] + 1
                queue.append((nx, ny))
    return graph[row-1][col-1]


row, col = map(int, input().split())
graph = []

for _ in range(row):
    graph.append(list(map(int, input())))

# (0, 0)부터 탐색
print(bfs(0, 0))
```

## 코드 설명

(0, 0)부터 탐색을 시작한다. 처음에 시작을 하면 queue에 넣어주었다. <br>
그리고 queue에 값이 없을 때까지 반복문을 돌리면서 맨 앞에 있는 x와 y를 빼서 다음에 이동할 수 있는 위치를 찾는다. <br>

여기서 visited에 대한 표시는 방문한 곳은 `graph[nx][ny] = graph[x][y] + 1` 를 통해서 방문했음을 표시했다. 여기서 1이 아니면 방문을 이미 했다는 뜻이기 때문이다. 동시에 저 코드를 통해서 몇 번 이동을 했는지를 알 수 있다.
