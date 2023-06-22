---
title: "Chap 04. 축소 정복 기법"
excerpt: "Chap 04. 축소 정복 기법"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1

```py
# 2116313 손수경
# 1번을 해보세요!
def insertion_sort(A):
    for i in range(1, len(A)):
        key = A[i]
        j = i - 1
        while j >= 0 and A[j] > key:
            A[j + 1] = A[j]
            j = j - 1
        A[j + 1] = key
        printStep(A, i)

# 중간 과정을 출력하는 함수에요!


def printStep(arr, val):
    print("  Step %2d = " % val, end='')
    print(arr)


# 2번을 해보세요!
data = [int(i) for i in input().split()]

# 출력합니다!
print("Original  :", data)
insertion_sort(data)
print("Insertion :", data)
```

## 실습 2

```py
# 2116313 손수경
# 1번을 해보세요!
def topological_sort(graph):
    inDeg = {}
    # 차수 setting
    for v in graph:
        inDeg[v] = 0
    for v in graph:
        for u in graph[v]:
            inDeg[u] += 1

    # 차수가 0인 리스트 setting
    vList = []
    for v in graph:
        if inDeg[v] == 0:
            vList.append(v)

    while len(vList) != 0:
        v = vList.pop()
        print(v, end=' ')
        for u in graph[v]:
            inDeg[u] -= 1
            if inDeg[u] == 0:
                vList.append(u)


# 2번을 해보세요!
mygraph = dict()
n1 = int(input())
for i in range(n1):
    mygraph.setdefault(chr(ord('A') + i), set())

n2 = int(input())
for i in range(n2):
    a, b = input().split()
    mygraph[a] |= {b}


# 출력합니다!
print('topological_sort: ')
topological_sort(mygraph)
print()
```

## 실습 3 :: 이진 탐색(순환구조)

```py
# 2116313 손수경
# 1번을 해보세요1
def binary_search(A, key, low, high):
    mid = (low + high) // 2
    if key == A[mid]:
        return mid
    elif key < A[mid]:
        high = mid - 1
    else:
        low = mid + 1
    return -1


# 2번을 해보세요!
listA = [int(i) for i in input().split()]
key = int(input())

# 출력합니다!
print("입력 리스트 =", listA)
print("%d 탐색(순환) -->" % (key), binary_search(listA, key, 0, len(listA)-1))
```

60점? <br>
내가 한 방법은 순환 구조와 반복 구조를 섞은 방식이다. 만약 반복문을 사용하고 싶지 않다면 조건문 밑에 `return binary_search(A, key, low, high)` 를 넣어주면 된다. <br>

```py
# 2116313 손수경
# 1번을 해보세요1
def binary_search(A, key, low, high):
    while low <= high:
        mid = (low + high) // 2
        if key == A[mid]:
            return mid
        elif key < A[mid]:
            high = mid - 1
        elif key > A[mid]:
            low = mid + 1
    return -1


# 2번을 해보세요!
listA = [int(i) for i in input().split()]
key = int(input())

# 출력합니다!
print("입력 리스트 =", listA)
print("%d 탐색(순환) -->" % (key), binary_search(listA, key, 0, len(listA)-1))
```

아 근데 이 방법은 반복 구조이므로 실습 4번에 복붙,,, <br>

```py
# 2116313 손수경
# 1번을 해보세요1
def binary_search(A, key, low, high):
    if low <= high:
        mid = (low + high) // 2
        if key == A[mid]:
            return mid
        elif key < A[mid]:
            return binary_search(A, key, low, mid - 1)
        elif key > A[mid]:
            return binary_search(A, key, mid + 1, high)

    return -1


# 2번을 해보세요!
listA = [int(i) for i in input().split()]
key = int(input())

# 출력합니다!
print("입력 리스트 =", listA)
print("%d 탐색(순환) -->" % (key), binary_search(listA, key, 0, len(listA)-1))
```

## 실습 4 :: 이진 탐색(반복구조)

```py
# 2116313 손수경
# 1번을 해보세요1
def binary_search(A, key, low, high):
    while low <= high:
        mid = (low + high) // 2
        if key == A[mid]:
            return mid
        elif key < A[mid]:
            high = mid - 1
        elif key > A[mid]:
            low = mid + 1
    return -1


# 2번을 해보세요!
listA = [int(i) for i in input().split()]
key = int(input())

# 출력합니다!
print("입력 리스트 =", listA)
print("%d 탐색(반복) -->" % (key), binary_search(listA, key, 0, len(listA)-1))
```

## 실습 5 :: 거듭제곱(억지 기법)

```py
# 2116313 손수경
# 1번을 해보세요!
def slow_power(x, n):
    for i in range(n - 1):
        x *= x
    return x


# 2번을 해보세요!
x = float(input())
n = int(input())

# 출력합니다!
print("억지기법(%d**%d) =" % (x, n), slow_power(x, n))
```

처음에 이렇게 했는데 왜 틀린거지? <br>

```py
# 2116313 손수경
# 1번을 해보세요!
def slow_power(x, n):
    result = 1.0
    for i in range(n):
        result *= x
    return result


# 2번을 해보세요!
x = int(input())
n = int(input())

# 출력합니다!
print("억지기법(%d**%d) =" % (x, n), slow_power(x, n))
```

## 실습 6 :: 거듭제곱(축소 정복 기법)

-> 순환 구조로 하란다. <br>

```py
# 2116313 손수경
# 1번을 해보세요!
def power(x, n):
    # 순환 구조로
    if n == 0:
        return 1
    elif n % 2 == 0:
        return power(x * x, n // 2)
    else:
        return power(x * x, (n - 1) // 2)


# 2번을 해보세요!
x = int(input())
n = int(input())

# 출력합니다!
print("축소정복기법(%d**%d) =" % (x, n), power(x, n))
```

60점. <br>
아! 왜냐면 n이 홀수인 경우 마지막에 x 한번 더 곱해주어야 된다.

## 실습 7 :: 행렬의 거듭제곱(축소 정복 기법) | p.163

```py
# 2116313 손수경
# 1번을 해보세요!
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


# 2번을 해보세요!
n = int(input())
row_col = int(input())
x = [[int(i) for i in input().split()] for i in range(row_col)]

# 출력합니다!
result = powerMat(x, n)
print()
for row in result:
    for num in row:
        print(num, end=' ')
    print()
```

## 실습 8 :: 정렬을 이용한 k번째 작은 수 찾기 | p.165

```py
# 2116313 손수경
# 1번을 해보세요!
def kth_smallest_sort(A, k):
    A.sort()

    return A[k - 1]


# 2번을 해보세요!
array = [int(i) for i in input().split()]
k = int(input())


# 출력합니다!
print("입력 리스트 =", array)
print("[정렬기법] %d번째 작은 수: " % (k), kth_smallest_sort(array, k))
```

## 실습 9 :: 축소 정복 기법을 이용한 k번째 작은 수 찾기 | p.168

```py
# 2116313 손수경
# 1번을 해보세요!
def quick_select(A, left, right, k):
    pos = partition(A, left, right)

    if pos + 1 == left + k:
        return A[pos]
    elif pos + 1 > left + k:
        return quick_select(A, left, pos - 1, k)
    elif pos + 1 < left + k:
        return quick_select(A, pos + 1, right, k - (pos + 1 - left))

# 2번을 해보세요!


def partition(A, left, right):
    low = left + 1
    high = right
    pivot = A[left]
    while low <= high:
        while low <= right and pivot >= A[low]:
            low += 1
        while high >= left and pivot < A[high]:
            high -= 1
        if low < high:
            A[low], A[high] = A[high], A[low]
    A[left], A[high] = A[high], A[left]
    return high


# 3번을 해보세요!
array = [int(i) for i in input().split()]
k = int(input())

# 출력합니다!
n = len(array)
print("입력 리스트 =", array)
print("[축소정복] %d번째 작은 수: " % (k), quick_select(array, 0, n-1, k))
```
