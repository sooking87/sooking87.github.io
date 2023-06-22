---
title: "Chap 09. 백트래킹과 분기 한정 기법"
excerpt: "Chap 09. 백트래킹과 분기 한정 기법"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1. 순열 생성 알고리즘(백트래킹)

```python
# 2116313 손수경
# 1번을 해보세요!
def all_permutations(data):
    bUsed = [False] * len(data)
    DFS_permutation (data, [], 0, bUsed)

# 2번을 해보세요!
def DFS_permutation (data, sol, level, bUsed):
    if level == len(data):
        print(sol)
        return

    for i in range(len(data)):
        if not bUsed[i]:
            sol.append(data[i])
            bUsed[i]=True
            DFS_permutation(data, sol, level+1, bUsed)
            sol.pop()
            bUsed[i]=False

# 3번을 해보세요!
data = input().split()

# 출력합니다!
all_permutations(data)
```

## 실습 2. 합이 M인 모든 부분집합 찾기(백트래킹)

```python
# 2116313 손수경
# 리스트로 주어지는 입력 S에서 합이 M인 모든 부분집합 찾기 함수
def all_sum_of_subsets(S, M):
    DFS_sum_of_subsets(S, M, 0, [], sum(S))

# 1번을 해보세요!
def DFS_sum_of_subsets(S, M, level, sol, remaining):
    if sum(sol)==M:
        print(sol)
        return

    if sum(sol)>M:
        return

    for i in range(level, len(S)):
        sol.append(S[i])
        DFS_sum_of_subsets(S, M, i+1, sol, remaining-S[i])
        sol.pop()

# 2번을 해보세요!
nums = list(map(int, input().split()))
M = int(input())

# 출력합니다!
solution = all_sum_of_subsets(nums, M)
print("입력 집합 :", nums, "M=", M )
```

## 실습 3. 백트래킹을 이용한 미로탐색

```python
# 2116313 손수경
# 1번을 해보세요!
def isSafe( maze, x, y, mark ):
    W, H = len(maze[0]), len(maze)
    if x>=0 and x<W and y>=0 and y<H:
        if maze[y][x]!=0 and mark[y][x]==0:
            return True
    return False
def solve_maze( maze, x, y ):
    W, H = len(maze[0]), len(maze)                  # 미로 맵의 크기
    sol = [[0 for j in range(W)] for i in range(H)] # 해 경로 맵
    mark= [[0 for j in range(W)] for i in range(H)] # 방문 맵
    if DFS_maze(maze, x, y, sol, mark) == False:   # 탐색 실패
        print("출구를 찾을 수 없음")
    else :                               # 탐색 성공
        for i in sol: print(i)               # 해 경로 맵 출력
def DFS_maze(maze, x, y, sol, mark):
    W, H = len(maze[0]), len(maze)
    if not isSafe(maze, x, y, mark):
        return False
    mark[y][x]=1
    sol[y][x]=1
    if maze[y][x]==2: return True
    if DFS_maze(maze, x+1, y, sol, mark)==True: return True
    if DFS_maze(maze, x, y+1, sol, mark)==True: return True
    if DFS_maze(maze, x-1, y, sol, mark)==True: return True
    if DFS_maze(maze, x, y-1, sol, mark)==True: return True
    sol[y][x]=0
    return False
x,y = list(map(int, input().split()))
# 출력합니다!
maze = [ [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0],
         [0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0],
         [0, 1, 1, 1, 1, 1, 0, 1, 0, 1, 0],
         [0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0],
         [0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 2],
         [0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0],
         [0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0],
         [0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]
solve_maze(maze, x, y)
```

## 실습 4. N-Queen

```python
# 2116313 손수경
# 1번을 해보세요!
def isSafe(board, x, y):
    N=len(board)
    for i in range(y):
        if board[i][x]==1: return False
    for i, j in zip(range(y-1, -1, -1), range(x-1, -1, -1)):
        if board[i][j]==1: return False
    for i, j, in zip(range(y-1, -1, -1), range(x+1, N)):
        if board[i][j]==1: return False
    return True
# 2번을 해보세요!
def solve_N_Queen(board, y):
    N=len(board)
    if y==N:
        printBoard(board)
        return
    for x in range(N):
        if isSafe(board, x, y):
            board[y][x] = 1
            solve_N_Queen(board, y+1)
            board[y][x]=0
# 출력 함수
def printBoard(board):
    for i in range(len(board)):
        for j in range(len(board)):
            if board[i][j] == 1:
                print("Q", end=" ")
            else:
                print(".", end=" ")
        print()
    print()

# 3번을 해보세요!
N = int(input())

# 출력합니다!
board = [[0 for i in range(N)] for j in range(N)]
solve_N_Queen(board, 0)
```

## 실습 5. 그래프 색칠

```python
# 2116313 손수경
# 1번을 해보세요!
def isSafe(g, v, c, color):
    for i in range(len(g)):
        if g[v][i] == 1 and color[i] == c:
            return False
    return True


# 2번을 해보세요!
def DFS_graph_coloring(graph, k, v, color):
    if v == len(graph):
        return True
    for c in range(1, k + 1):
        if isSafe(graph, v, c, color):
            color[v] = c
            if DFS_graph_coloring(graph, k, v+1, color):
                return True
            color[v] = 0
    return False


# 그래프 색칠 주 함수
def graphColouring(graph, k, states):
    color = [0] * len(graph)       # 정점의 색 배정 리스트: 초기 0
    ret = DFS_graph_coloring(graph, k, 0, color)  # 0번 정점부터 처리
    if ret :
        for i in range(len(graph)) :
            print("%3s = "%states[i], color_name[color[i]])
    else :
        print("그래프를 색칠할 수 없음!")


# 3번을 해보세요!
k = int(input())


# 출력합니다!
states = ['NT', 'WA', 'Q', 'SA', 'NSW', 'V']
color_name = ["none", "빨강", "초록", "파랑", "노랑", "보라"]
g = [ [0, 1, 1, 1, 0, 0],
      [1, 0, 0, 1, 0, 0],
      [1, 0, 0, 1, 1, 0],
      [1, 1, 1, 0, 1, 1],
      [0, 0, 1, 1, 0, 1],
      [0, 0, 0, 1, 1, 0],]
print("색상 %d개:" %(k))
graphColouring(g, k, states)

```

## 실습 6. 분기 한정 기법을 이용한 0-1 배낭 채우기

```python
# 2116313 손수경
# 2116313 손수경
# 노드를 탐색하는 순서와 각 노드에서 계산된 값들을 출력하는 함수
def printNode(knapsack, level, weight, profit, bound, maxProfit):
    print("%d %-16s :  %3.1fKg 가치/한계합 = %5.1f / %5.1f > %5.1f(최고합)"%
          (level, knapsack, weight, profit, bound, maxProfit))
def knapSack_bnb(obj, knapsack, W, level, weight, profit, maxProfit, bound) :
    printNode(knapsack, level, weight, profit, bound, maxProfit)
    if(level == len(obj)):
        return maxProfit
    if weight + obj[level][0] <= W:
        newWeight = weight + obj[level][0]
        newProfit = profit + obj[level][1]
        if newProfit > maxProfit:
            maxProfit = newProfit
        newBound = bound1(obj, W, level, newWeight, newProfit)
        if newBound >= maxProfit:
            knapsack.append(obj[level][2])
            maxProfit = knapSack_bnb(obj, knapsack, W, level+1, newWeight, newProfit, maxProfit, newBound)
            knapsack.pop()
    newWeight = weight
    newProfit = profit
    newBound = bound1(obj, W, level, newWeight, newProfit)
    if newBound >= maxProfit:
        maxProfit = knapSack_bnb(obj, knapsack, W, level+1, newWeight, newProfit, maxProfit, newBound)
    return maxProfit

def bound1(obj, W, level, weight, profit) :
    if weight>W:
        return 0
    pBound = profit
    for j in range(level+1, len(obj)):
        pBound += obj[j][1]
    return pBound
# 3번을 해보세요!
n = int(input())
obj = []
for _ in range(n):
    weight, value, name = input().split()
    obj.append((float(weight), float(value), name))
W = int(input())
# 출력합니다!
print(obj)
print("0-1배낭문제(분기 한정): ")
knapSack_bnb(obj, [], W, 0,0,0,0, 0)
```

## 실습 7. 분기 한정 기법을 이용한 0-1 배낭 채우기(개선된 한계가치 계산 방법)

```python
# 2116313 손수경
# 노드를 탐색하는 순서와 각 노드에서 계산된 값들을 출력하는 함수
def printNode(knapsack, level, weight, profit, bound, maxProfit):
    print("%d %-16s :  %3.1fKg 가치/한계합 = %5.1f / %5.1f > %5.1f(최고합)" %
          (level, knapsack, weight, profit, bound, maxProfit))

# 분기 한정을 이용한 0-1 배낭 채우기 함수


def knapSack_bnb(obj, knapsack, W, level, weight, profit, maxProfit, bound):
    printNode(knapsack, level, weight, profit, bound, maxProfit)

    if (level == len(obj)):
        return maxProfit

    if weight + obj[level][0] <= W:
        newWeight = weight + obj[level][0]
        newProfit = profit + obj[level][1]
        if newProfit > maxProfit:
            maxProfit = newProfit

        newBound = bound2(obj, W, level, newWeight, newProfit)
        if newBound >= maxProfit:
            knapsack.append(obj[level][2])
            maxProfit = knapSack_bnb(obj, knapsack, W, level+1, newWeight,
                                     newProfit, maxProfit, newBound)
            knapsack.pop()

    newWeight = weight
    newProfit = profit
    newBound = bound2(obj, W, level, newWeight, newProfit)
    if newBound >= maxProfit:
        maxProfit = knapSack_bnb(obj, knapsack, W, level+1, newWeight,
                                 newProfit, maxProfit, newBound)

    return maxProfit


# 1번을 해보세요!
def bound2(arr, W, level, weight, profit):
    if weight > W:
        return 0
    pBound = profit
    tWeight = weight

    j = level + 1
    n = len(arr)

    while j < n and (tWeight + obj[j][0] <= W):
        tWeight += arr[j][0]
        pBound += arr[j][1]
        j += 1

    if (j < n):
        pBound += (W - tWeight) * (arr[j][1] / arr[j][0])
    return pBound


# 2번을 해보세요!
n = int(input())
obj = []
for _ in range(n):
    weight, value, name = input().split()
    obj.append((float(weight), float(value), name))

W = int(input())
# 출력합니다!
obj.sort(key=lambda e: e[1]/e[0], reverse=True)
print(obj)
print("0-1배낭문제(분기 한정): ", knapSack_bnb(obj, [], W, 0, 0, 0, 0, 0))

```

## 실습 7. 최적우선탐색을 이용한 일 배정 문제(분기한정)

```python
# 2116313 손수경
import heapq


# 1번을 해보세요!
def job_assign_BFBnB(mat):
    N = len(mat)
    Q = []
    bound = calcBound(mat, [])
    heapq.heappush(Q, (bound+0, (0, bound, [])))

    while len(Q) > 0:
        total, (cost, bound, jobs) = heapq.heappop(Q)
        print("현재 노드: ", total, jobs)

        level = len(jobs)
        if level == N:
            return (total, jobs)

        for j in range(N):
            if j not in jobs:
                jbs = jobs + [j]
                cst = cost + mat[level][j]
                bnd = calcBound(mat, jbs)
                heapq.heappush(Q, (cst+bnd, (cst, bnd, jbs)))

# 2번을 해보세요!
def calcBound(mat, jobs):
    N = len(mat)
    J = len(jobs)
    bound = 0
    for i in range(J, N):
        min= 9999
        for j in range(N):
            if j not in jobs:
                if min > mat[i][j]:
                    min = mat[i][j]
        bound += min
    return bound


# 3번을 해보세요!
n = int(input())
Man2Job = [[int(i) for i in input().split()] for _ in range(n)]
print(Man2Job)


# 출력합니다!
total, jobs = job_assign_BFBnB(Man2Job)
print("배정 결과: ", jobs)
print("전체 비용: ", total)
```
