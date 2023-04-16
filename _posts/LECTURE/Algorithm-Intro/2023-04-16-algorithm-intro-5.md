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

## Chap 04 :: 삽입 정렬

반복문 횟수나, 어디서 어디 값을 옮기는지 잘보기

```py
# 삽입 정렬
def insertion_sort(data):
    n = len(data)
    for i in range(1, n):
        key = data[i]
        j = i - 1
        while j >= 0 and data[j] > key:
            data[j + 1] = data[j]
            j -= 1
        data[j + 1] = key
        printStep(data, i)


def printStep(arr, val):
    print("  Step %2d = " % val, end='')
    print(arr)


data = [int(i) for i in input().split()]


# 출력합니다!
print("Original  :", data)
insertion_sort(data)
print("Insertion :", data)

```

## Chap 04 :: 위상 정렬

```py
def topological_sort(mygraph):
    inDeg = dict()
    # 차수 행렬 setup
    for i in mygraph:
        inDeg[i] = 0
    for i in mygraph:
        for j in mygraph[i]:
            inDeg[j] += 1
    # 방문해야되는 노드 리스트 setup
    vList = []
    for i in inDeg:
        if inDeg[i] == 0:
            vList.append(i)
    while len(vList) != 0:
        v = vList.pop()
        print(v, end=' ')
        for j in mygraph[v]:
            inDeg[j] -= 1
            if inDeg[j] == 0:
                vList.append(j)


n = int(input())
n2 = int(input())
mygraph = dict()
for i in range(65, n + 65):
    mygraph[chr(i)] = mygraph.setdefault(chr(i), set())

for i in range(n2):
    a, b = input().split()
    mygraph[a] |= {b}

# 출력합니다!
print('topological_sort: ')
topological_sort(mygraph)
print()
```

## Chap 04 :: 거듭제곱(축소 정복 기법)

```py
def power(x, n):
    if n == 0:
        return 1
    elif n % 2 == 0:
        return power(x*x, n // 2)
    else:
        return x * power(x*x, n // 2)


x = int(input())
n = int(input())

print("축소정복기법(%d**%d) =" % (x, n), power(x, n))
```

## Chap 04 :: 행렬의 거듭제곱(축소 정복 기법)

```py
def powerMat(x, n):
    if n == 1:
        return x
    elif n % 2 == 0:
        return powerMat(multMat(x, x), n // 2)
    else:
        return multMat(x, powerMat(multMat(x, x), (n - 1) // 2))


# 행렬을 곱하는 multMat(M1, M2) 함수에요!
def multMat(M1, M2):
    result = [[0 for _ in range(len(M2[0]))] for __ in range(len(M1))]
    for i in range(len(M1)):
        for j in range(len(M2[0])):
            for k in range(len(M1[0])):
                result[i][j] += M1[i][k] * M2[k][j]
    return result


n = int(input())
n2 = int(input())
x = [[int(i) for i in input().split()] for _ in range(n2)]

# 출력합니다!
result = powerMat(x, n)
print()
for row in result:
    for num in row:
        print(num, end=' ')
    print()
```

## Chap 04 :: 축소 정복 기법을 이용한 k번째 작은 수 찾기

🌟 원리 이해하기,, 다시보자,,
