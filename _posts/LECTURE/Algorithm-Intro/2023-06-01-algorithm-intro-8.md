---
title: "Chap 07. 동적 계획법"
excerpt: "Chap 07. 동적 계획법"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1. 피보나치수열(메모이제이션 이용)

```python
# 2116313 손수경
# 1번을 해보세요!
def fib_dp_mem(n):
    if (mem[n] == None):
        if n < 2:
            mem[n] = n
        else:
            mem[n] = fib_dp_mem(n-1) + fib_dp_mem(n-2)
    return mem[n]


# 2번을 해보세요!
n = int(input())

# 출력합니다!
mem = [None] * (n+1)
print('Fibonacci(%d) = ' % n, fib_dp_mem(n))

```

## 실습 2. 피보나치수열(테이블화 이용)

```python
# 2116313 손수경
# 1번을 해보세요!
def fib_dp_tab(n):
    f = [None] * (n+1)
    f[0] = 0
    f[1] = 1
    for i in range(2, n + 1):
        f[i] = f[i - 1] + f[i - 2]
    return f[n]


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print('Fibonacci(%d) = ' % n, fib_dp_tab(n))

```

## 실습 3. 이항계수 C(n, k) 계산 함수(분할 정복 기법)

```python
# 2116313 손수경
# 1번을 해보세요!
def bino_coef_dc(n, k):
    if k == 0 or k == n:
        return 1
    return bino_coef_dc(n - 1, k - 1) + bino_coef_dc(n - 1, k)


# 2번을 해보세요!
n = int(input())
k = int(input())


# 출력합니다!
print("C(%d,%d) =" % (n, k), bino_coef_dc(n, k))

```

## 실습 4. 이항계수 C(n, k) 계산 함수(동적 계획법)

```python
# 2116313 손수경
# 1번을 해보세요!
def bino_coef_dp(n, k):
    C = [[-1 for _ in range(k+1)] for _ in range(n+1)]

    for i in range(n+1):
        for j in range(min(i, k) + 1):
            if j == 0 or j == i:
                C[i][j] = 1
            else:
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j]
    return C[n][k]


# 2번을 해보세요!
n = int(input())
k = int(input())


# 출력합니다!
print("C(%d,%d) =" % (n, k), bino_coef_dp(n, k))

```

## 실습 5. 0-1 배낭 채우기 알고리즘(분할 정복 기법)

```python
# 2116313 손수경
# 1번을 해보세요!
def knapSack_bf(W, wt, val, n):
    if n == 0 or W == 0:
        return 0

    if (wt[n - 1] > W):
        return knapSack_bf(W, wt, val, n - 1)
    else:
        valWithout = knapSack_bf(W, wt, val, n - 1)
        valWith = val[n - 1] + knapSack_bf(W - wt[n - 1], wt, val, n - 1)
        return max(valWith, valWithout)


# 2번을 해보세요!
n = int(input())
val = [int(i) for i in input().split()]
wt = [int(i) for i in input().split()]
W = int(input())


# 출력합니다!
print("최대 가치:", knapSack_bf(W, wt, val, n))

```

## 실습 6. 0-1 배낭 채우기 알고리즘(동적 계획법)

```python
# 2116313 손수경
# 1번을 해보세요!
def knapSack_dp(W, wt, val, n):
    A = [[0 for x in range(W + 1)] for x in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(1, W + 1):
            if wt[i - 1] > w:
                A[i][w] = A[i - 1][w]
            else:
                valWith = val[i - 1] + A[i - 1][w - wt[i - 1]]
                valWithout = A[i - 1][w]
                A[i][w] = max(valWith, valWithout)
    return A[n][W]


# 2번을 해보세요!
n = int(input())
val = [int(i) for i in input().split()]
wt = [int(i) for i in input().split()]
W = int(input())


# 출력합니다!
print("최대 가치:", knapSack_dp(W, wt, val, n))

```

## 실습 7. 최장 공통 부분순서(순환 구조)

```python
# 2116313 손수경
# 1번을 해보세요!
def lcs_recur(X, Y, m, n):
    if m == 0 or n == 0:
        return 0
    elif X[m - 1] == Y[n - 1]:
        return 1 + lcs_recur(X, Y, m - 1, n - 1)
    else:
        return max(lcs_recur(X, Y, m, n - 1), lcs_recur(X, Y, m - 1, n))


# 2번을 해보세요!
X = input()
Y = input()


# 출력합니다!
print("X = ", X)
print("Y = ", Y)
print("LCS(분할 정복)", lcs_recur(X, Y, len(X), len(Y)))

```

## 실습 8. 최장 공통 부분순서(동적 계획법)

```python
# 2116313 손수경
# 1번을 해보세요!
def lcs_dp(X, Y):
    m = len(X)
    n = len(Y)
    L = [[None]*(n+1) for _ in range(m+1)]

    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0 or j == 0:
                L[i][j] = 0
            elif X[i - 1] == Y[j - 1]:
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j], L[i][j - 1])
    return L[m][n]


# 2번을 해보세요!
X = input()
Y = input()

# 출력합니다!
print("X = ", X)
print("Y = ", Y)
print("LCS(동적 계획)", lcs_dp(X, Y))

```

## 실습 9. LCS 테이블에서 LCS를 추적하는 알고리즘

```python
# 2116313 손수경
# 동적 계획법으로 최장 공통 부분순서를 구하는 함수
def lcs_dp(X, Y):
    m = len(X)
    n = len(Y)
    L = [[None]*(n+1) for _ in range(m+1)]

    for i in range(m+1):
        for j in range(n+1):
            if i == 0 or j == 0:
                L[i][j] = 0
            elif X[i-1] == Y[j-1]:
                L[i][j] = L[i-1][j-1]+1
            else:
                L[i][j] = max(L[i-1][j], L[i][j-1])

    # 함수 lcs_dp_traceback(X, Y, L)를 호출해요!
    print("LCS = ", lcs_dp_traceback(X, Y, L))

    return L[m][n]


# 1번을 해보세요!
def lcs_dp_traceback(X, Y, L):
    lcs = ""
    i = len(X)
    j = len(Y)
    while i > 0 and j > 0:
        v = L[i][j]
        if v > L[i][j - 1] and v > L[i - 1][j] and v > L[i - 1][j - 1]:
            i -= 1
            j -= 1
            lcs = X[i] + lcs
        elif v == L[i][j - 1] and v > L[i - 1][j]:
            j -= 1
        else:
            i -= 1

    return lcs


# 2번을 해보세요!
X = input()
Y = input()


# 출력합니다!
print("X = ", X)
print("Y = ", Y)
lcs_dp(X, Y)

```

## 실습 10. Floyd의 최단경로 탐색 알고리즘

```python
# 2116313 손수경
import copy


# 1번을 해보세요!
def shortest_path_floyd(vsize, W):
    D = copy.deepcopy(W)
    for k in range(vsize):
        for i in range(vsize):
            for j in range(vsize):
                if (D[i][k] + D[k][j] < D[i][j]):
                    D[i][j] = D[i][k] + D[k][j]
        printD(D)
    # 정점 k를 추가할 때마다 반드시 printD(D)를 호출하세요!


# 현재의 최단거리 행렬 D를 화면에 출력하는 함수
def printD(D):
    vsize = len(D)
    print("====================================")
    for i in range(vsize):
        for j in range(vsize):
            if (D[i][j] == INF):
                print(" INF ", end='')
            else:
                print("%4d " % D[i][j], end='')
        print("")


# 2번을 해보세요!
INF = 9999
vsize = int(input())
n = int(input())
weight = [[INF] * vsize for _ in range(vsize)]
for _ in range(n):
    i, j, w = [int(m) for m in input().split()[:3]]
    weight[i][j] = w
    weight[j][i] = w

for i in range(vsize):
    weight[i][i] = 0

# 출력합니다!
print("Shortest Path By Floyd's Algorithm")
shortest_path_floyd(vsize, weight)

```

## 실습 11. 편집 거리(순환 구조, 분할 정복)

```python
# 2116313 손수경
# 1번을 해보세요!
def edit_distance(S, T, m, n):
    if m == 0:
        return n
    if n == 0:
        return m

    if S[m - 1] == T[n - 1]:
        return edit_distance(S, T, m - 1, n - 1)

    return 1 + min(edit_distance(S, T, m, n - 1),
                   edit_distance(S, T, m - 1, n),
                   edit_distance(S, T, m - 1, n - 1))


# 2번을 해보세요!
S = input()
T = input()


# 출력합니다!
m = len(S)
n = len(T)
print("문자열:", S, T)
print("편집거리(분할정복)=", edit_distance(S, T, m, n))

```

## 실습 12. 편집 거리(동적 계획법, 메모이제이션 이용)

```python
# 2116313 손수경
# 1번을 해보세요!
def edit_distance_mem(S, T, m, n, mem):
    if m == 0:
        return n
    if n == 0:
        return m

    if mem[m - 1][n - 1] == None:
        if S[m - 1] == T[n - 1]:
            mem[m - 1][n - 1] = edit_distance_mem(S, T, m - 1, n - 1, mem)
        else:
            mem[m - 1][n - 1] = 1 + min(edit_distance_mem(S, T, m, n - 1, mem), edit_distance_mem(
                S, T, m - 1, n, mem), edit_distance_mem(S, T, m - 1, n - 1, mem))
    return mem[m-1][n-1]


# 2번을 해보세요!
S = input()
T = input()


# 출력합니다!
m = len(S)
n = len(T)
print("문자열:", S, T)
mem = [[None for _ in range(n)] for _ in range(m)]
dist = edit_distance_mem(S, T, m, n, mem)
print("편집거리(메모이제이션)=", edit_distance_mem(S, T, m, n, mem))

```
