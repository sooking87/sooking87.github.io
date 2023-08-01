---
title: "[백준 7576][DFS-BFS] 토마토"
excerpt: "[백준 7576][DFS-BFS] 토마토"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 7576 문제 링크](https://www.acmicpc.net/problem/7576) <br>

## 백준 7576 토마토

익은 토마토와 인접해 있으면 위, 아래, 오른쪽, 왼쪽이 익는다. <br>
1: 익은 토마토, 0: 익지 않은 토마토, -1: 토마토가 없음 <br>

토마토가 다 익는 최소 일수를 출력하는 프로그램

## 풀이 코드

```python
# 7675 토마토

# 익은 토마토와 인접해 있으면 위, 아래, 오른쪽, 왼쪽이 익는다
# 1: 익은 토마토, 0: 익지 않은 토마토, -1: 토마토가 없음

# 1이 있는 위치 찾기 -> 1이 없으면 모든 토마토가 익을 수 없음
# -1이 있더라도 모두 익을 수는 있음
# BFS, DFS를 어케 사용? -> 미로 탐색 참고

import sys
# 먼저 들어간 좌표에 대해서 주변 토마토가 익어야되므로 큐 사용
from collections import deque

def count_days(start):
    queue = deque()
    for pos in start:
        queue.append((pos[0], pos[1]))

    dx = [0, 0, -1, 1] # 행을 x축으로
    dy = [-1, 1, 0, 0] # 열을 y축으로

    ansX = 0
    ansY = 0
    while queue:
        x, y = queue.popleft()
        # print(x, y)

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            # print(nx, ny)
            if nx < 0 or nx >= m or ny < 0 or ny >= n:
                continue
            if tomatoes[nx][ny] == 0:
                tomatoes[nx][ny] = tomatoes[x][y] + 1
                queue.append((nx, ny))
                ansX = nx
                ansY = ny
        # print(tomatoes)
    return ansX, ansY

def is_ripens(tomatoes):
    for i in range(m):
        for j in range(n):
            if tomatoes[i][j] == 0:
                return False
    return True

input = sys.stdin.readline
n, m = map(int, input().split())
tomatoes = []
start = []

for j in range(m):
    row = [int(i) for i in input().split()]
    for i in range(n):
        if row[i] == 1:
            start.append([j, i])
    tomatoes.append(row)

x, y = count_days(start)
is_all_ripens = is_ripens(tomatoes)
if is_all_ripens:
    print(tomatoes[x][y] - 1)
else:
    print(-1)
```

트리 형태의 경우는 `visited` 를 통해서 방문 여부를 파악했지만, 이중 리스트의 경우는 인덱스를 통해서, 또는 해당 인덱스의 값을 통해서 방문 여부를 파악한다. <br>
누가봐도 트리를 사용한 문제의 경우는 해당 값(노드의 value)를 출력해야되는 경우가 많으므로 visited를 통해서 파악했지만, 이중 리스트의 경우는 해당 값을 수정해가면서 방문 여부를 알 수 있기 때문에 visited가 굳이 필요없었다. <br>
경우에 따라서 이중 리스트임에도 visited가 필요할 수도 있겠지? <br>

그리고 토마토가 익은 순대로 주변 토마토가 익음을 수정해주어야 하므로 큐를 사용 -> BFS 사용

## 코드 설명

익은 토마토 기준으로 위, 아래, 왼쪽, 오른쪽이 0이면 익어야되므로 tomatoes[x][y] 기준으로 1을 더해준다. 1로 넣어도되지만 최종적으로 구해야하는 값이 익은 일수이므로 count 대신 리스트 안의 값으로 활용했다.
