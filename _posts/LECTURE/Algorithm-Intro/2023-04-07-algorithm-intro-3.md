---
title: "Chap 03"
excerpt: "Chap 03"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1 :: 순차 정렬 문제

정렬 - 오름차순 <br>

처음 코드

```py
# 2116313 손수경
# 1번을 해보세요!
def selection_sort(A):
    # 여기에 코드를 작성해보세요!
    for i in range(len(A) - 1):
        for j in range(i + 1, len(A)):
            if A[i] > A[j]:
                temp = A[i]
                A[i] = A[j]
                A[j] = temp
        printStep(A, i + 1)


def printStep(arr, val):
    print("  Step %2d = " % val, end='')
    print(arr)


# 2번을 해보세요!
A = [int(i) for i in input().split()]

# 출력합니다!
print("Original  :", A)
selection_sort(A)
print("Selection :", A)
```

-> 30점,,, :: 왜지,,,?

```py
# 2116313 손수경
# 1번을 해보세요!
def selection_sort(A):
    # 여기에 코드를 작성해보세요!
    for i in range(len(A) - 1):
        min_idx = i
        for j in range(i + 1, len(A)):
            if A[j] < A[min_idx]:
                min_idx = j
        A[i], A[min_idx] = A[min_idx], A[i]
        printStep(A, i + 1)


def printStep(arr, val):
    print("  Step %2d = " % val, end='')
    print(arr)


# 2번을 해보세요!
A = [int(i) for i in input().split()]

# 출력합니다!
print("Original  :", A)
selection_sort(A)
print("Selection :", A)
```

일단은 파이썬의 경우는 두 개의 변수를 바꿀 때는 위와 같은 방법으로 할 수 있음. <br>
그리고 위의 코드가 틀린 이유는 작은 것을 발견할 때마다 원소의 위치를 바꾸는 것이 아니라 A[i] 외의 가장 작은 원소인 인덱스를 min_idx에 저장을 해두고 두 변수를 반복문이 끝나면 바꾼다.

## 실습 2 :: 정렬되지 않은 리스트의 탐색 문제

리스트 내에서 key 찾아서 인덱스 반환하기

```py
# 2116313 손수경
# 1번을 해보세요!
def sequential_search(A, key):
    for i in range(len(A)):
        if A[i] == key:
            return i
    else:
        return -1


# 2번을 해보세요!
A = [int(i) for i in input().split()]
# 3번을 해보세요!
key = int(input())

# 출력합니다!
print(sequential_search(A, key))
```

## 실습 3 :: 문자열 매칭 문제

문자열에서 P와 동일한 문자열이 있는지 찾기 <br>

```py
# 2116313 손수경
# 1번을 해보세요!
def string_matching(T, P):
    for i in range(len(T)):
        if T[i] == P[0]:
            j = 0
            for j in range(len(P)):
                if T[i + j] != P[j]:
                    break
            if j == len(P):
                return i
    else:
        return -1


# 2번을 해보세요!
T = input()
P = input()

# 출력합니다!
print(string_matching(T, P))
```

처음에는 이렇게 생각을 했는데 이게 안되는 이유가 일단은 문자열이 다를 때 break를 해버리면 무조건 -1이 나온다. <br>

```py
# 2116313 손수경
# 1번을 해보세요!
def string_matching(T, P):
    for i in range(len(T)):
        if T[i] == P[0]:
            j = 0
            while j != len(P):
                if T[i + j] == P[j]:
                    j += 1
            if j == len(P):
                return i
    else:
        return -1


# 2번을 해보세요!
T = input()
P = input()

# 출력합니다!
print(string_matching(T, P))
```

그래서 while문을 돌면서 j가 len(P)가 아닐 때까지 반복문을 돈다. 그러면서 같은 문자가 있다면 j를 1씩 늘려준다. <br>

여기서 문제가 만약에 P가 T에 없다면 무한 루프를 돈다는 점이다. <br>

SO,

```py
# 2116313 손수경
# 1번을 해보세요!
def string_matching(T, P):
    for i in range(len(T)):
        if T[i] == P[0]:
            j = 0
            while j != len(P):
                if T[i + j] == P[j]:
                    j += 1
                else:
                    break
            if j == len(P):
                return i
    else:
        return -1


# 2번을 해보세요!
T = input()
P = input()

# 출력합니다!
print(string_matching(T, P))
```

## 실습 4 :: 최근접 쌍의 거리 문제

두 점 사이에 최솟값 거리 구하기 <br>

이 문제의 경우는 [(), () ,,, ()] 이런식으로 입력을 받는게 조금 어려웠다.

```py
# 2번을 해보세요!
n = int(input())
p = [tuple(int(i) for i in input().split()[:2]) for j in range(n)]
```

그리고 처음에 i에서 int로 바꾸지 않았기 때문에 str은 계산이 불가하다는 에러를 봤다. <br>

```py
# 2116313 손수경
# 필요한 모듈을 추가해 보세요!

# 1번을 해보세요!
def closest_pair(p):
    distance = float('inf')
    for i in range(len(p) - 1):
        for j in range(i + 1, len(p)):
            temp_dis = (((p[i][0] - p[j][0]) ** 2) +
                        ((p[i][1] - p[j][1]) ** 2)) ** 0.5
            if distance > temp_dis:
                distance = temp_dis

    return distance


# 2번을 해보세요!
n = int(input())
p = [tuple(int(i) for i in input().split()[:2]) for j in range(n)]

# 출력합니다!
print("최근점 거리:", closest_pair(p))
```

음,, 이렇게 했는데도,,, 0점 받음,,,,, 아 그리고 inf가 아니라 Inf임,, <br>
아 ㅋㅋㅋ 알고보니까 출력값이 "최근점" 이라고 나와있어서 그런 거,,

```py
# 2116313 손수경
# 필요한 모듈을 추가해 보세요!

# 1번을 해보세요!
def closest_pair(p):
    distance = float('Inf')
    for i in range(len(p) - 1):
        for j in range(i + 1, len(p)):
            temp_dis = (((p[i][0] - p[j][0]) ** 2) +
                        ((p[i][1] - p[j][1]) ** 2)) ** 0.5
            if distance > temp_dis:
                distance = temp_dis

    return distance


# 2번을 해보세요!
n = int(input())
p = [tuple(int(i) for i in input().split()[:2]) for j in range(n)]

# 출력합니다!
print("최근접 거리:", closest_pair(p))
```

## 실습 5 :: 깊이 우선 탐색

입력값,, 어케하누

```py
n = int(input())
mygraph = dict()
for i in range(n):
    a, b = input().split()
    mygraph[a] = mygraph.setdefault(a, set()) | {b}
    mygraph[b] = mygraph.setdefault(b, set()) | {a}
```

딕셔너리를 이용한 인접 리스트 입력받기 <br>

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

## 실습 6 :: 너비 우선 탐색

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
