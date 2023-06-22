---
title: "Chap 05. 분할 정복 기법"
excerpt: "Chap 05. 분할 정복 기법"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1. 병합 정렬

```python
# 2116313 손수경
# 1번을 해보세요!
def merge_sort(A, left, right):
    if left < right:
        mid = (left + right) // 2
        merge_sort(A, left, mid)
        merge_sort(A, mid + 1, right)
        merge(A, left, mid, right)


# 2번을 해보세요!
def merge(A, left, mid, right):
    k = left
    i = left
    j = mid + 1
    while i <= mid and j <= right:
        if A[i] <= A[j]:
            sorted[k] = A[i]
            i, k = i + 1, k + 1
        else:
            sorted[k] = A[j]
            j, k = j + 1, k + 1
    if i > mid:
        sorted[k:k+right-j+1] = A[j:right+1]
    else:
        sorted[k:k+mid-i+1] = A[i:mid+1]
    A[left:right+1] = sorted[left:right+1]


# 3번을 해보세요!
data = [int(i) for i in input().split()]

# 출력합니다!
sorted = [0] * len(data)			# 길이가 len(data)인 임시 리스트를
print("Original  : ", data)			# 만들고 모든 항목을 0으로 초기화
merge_sort(data, 0, len(data)-1)  # 병합 정렬
print("MergeSort : ", data)

```

## 실습 2. 퀵 정렬

```python
# 2116313 손수경
# 1번을 해보세요!
def quick_sort(A, left, right):
    if left < right:
        mid = partition(A, left, right)
        quick_sort(A, left, mid - 1)
        quick_sort(A, mid + 1, right)


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
data = [int(i) for i in input().split()]


# 출력합니다!
print("Original  : ", data)
quick_sort(data, 0, len(data)-1)
print("QuickSort : ", data)

```

## 실습 3. 이진트리의 높이

```python
# 2116313 손수경
# 이진트리를 위한 노드 클래스
class TNode:
    def __init__(self, data, left, right):  # 생성자
        self.data = data 			# 노드의 데이터
        self.left = left			# 왼쪽 자식을 위한 링크
        self.right = right			# 오른쪽 자식을 위한 링크


# 1번을 해보세요!
def calc_height(root):
    if root is None:
        return 0
    hLeft = calc_height(root.left)
    hRight = calc_height(root.right)
    return max(hLeft, hRight) + 1


# 2번을 해보세요!
n = int(input())
binary_tree = [TNode(0, 0, 0) for _ in range(n)]

for i in range(n):
    data, left, right = [int(m) for m in input().split()][:3]
    binary_tree[i].data = data
    binary_tree[i].left = binary_tree[left - 1] if left > 0 else None
    binary_tree[i].right = binary_tree[right - 1] if right > 0 else None


# 출력합니다!
root = binary_tree[0]
print("트리의 높이 =", calc_height(root))

```

## 실습 4. 이진트리의 전위 순회

```python
# 2116313 손수경
# 이진트리를 위한 노드 클래스
class TNode:
    def __init__(self, data, left, right):  # 생성자
        self.data = data 			# 노드의 데이터
        self.left = left			# 왼쪽 자식을 위한 링크
        self.right = right			# 오른쪽 자식을 위한 링크


# 1번을 해보세요!
def preorder(n):
    if n is not None:
        print(n.data, end=' ')
        preorder(n.left)
        preorder(n.right)


# 2번을 해보세요!
n = int(input())
binary_tree = [TNode(0, 0, 0) for _ in range(n)]
for i in range(n):
    data, left, right = [int(m) for m in input().split()][:3]
    binary_tree[i].data = data
    binary_tree[i].left = binary_tree[left-1] if left > 0 else None
    binary_tree[i].right = binary_tree[right-1] if right > 0 else None


# 출력합니다!
root = binary_tree[0]
print('Pre-Order : ', end='')
preorder(root)
print()

```

## 실습 5. 이진트리의 중위 순회

```python
# 2116313 손수경
# 이진트리를 위한 노드 클래스
class TNode:
    def __init__(self, data, left, right):  # 생성자
        self.data = data 			# 노드의 데이터
        self.left = left			# 왼쪽 자식을 위한 링크
        self.right = right			# 오른쪽 자식을 위한 링크


# 1번을 해보세요!
def inorder(n):
    if n is not None:
        inorder(n.left)
        print(n.data, end=' ')
        inorder(n.right)


# 2번을 해보세요!
n = int(input())
binary_tree = [TNode(0, 0, 0) for _ in range(n)]
for i in range(n):
    data, left, right = [int(m) for m in input().split()][:3]
    binary_tree[i].data = data
    binary_tree[i].left = binary_tree[left-1] if left > 0 else None
    binary_tree[i].right = binary_tree[right-1] if right > 0 else None


# 출력합니다!
root = binary_tree[0]
print('In-Order : ', end='')
inorder(root)
print()

```

## 실습 6. 이진트리의 후위 순회

```python
# 2116313 손수경
# 이진트리를 위한 노드 클래스
class TNode:
    def __init__(self, data, left, right):  # 생성자
        self.data = data 			# 노드의 데이터
        self.left = left			# 왼쪽 자식을 위한 링크
        self.right = right			# 오른쪽 자식을 위한 링크


# 1번을 해보세요!
def postorder(n):
    if n is not None:
        postorder(n.left)
        postorder(n.right)
        print(n.data, end=' ')


# 2번을 해보세요!
n = int(input())
binary_tree = [TNode(0, 0, 0) for _ in range(n)]
for i in range(n):
    data, left, right = [int(m) for m in input().split()][:3]
    binary_tree[i].data = data
    binary_tree[i].left = binary_tree[left-1] if left > 0 else None
    binary_tree[i].right = binary_tree[right-1] if right > 0 else None


# 출력합니다!
root = binary_tree[0]
print('Post-Order : ', end='')
postorder(root)
print()

```

## 실습 10. 피보나치수열(분할 정복)

```python
# 2116313 손수경
# 1번을 해보세요!
def fib(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fib(n - 1) + fib(n - 2)


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print(fib(n))

```

## 실습 11. 피보나치수열(반복 구조)

```python
# 2116313 손수경
# 1번을 해보세요!
def fib_iter(n):
    # for문을 이용해보세요!
    if n < 2:
        return n
    last = 0
    current = 1
    for i in range(2, n + 1):
        tmp = current
        current += last
        last = tmp
    return current


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print(fib_iter(n))

```

## 실습 12. 피보나치수열(축소 정복 기법의 행렬 거듭제곱 이용)

```python
# 2116313 손수경
# 1번을 해보세요!
def fib_mat(n):
    if n < 2:
        return n
    mat = [[1, 1], [1, 0]]
    result = powerMat(mat, n)
    return result[0][1]


# powerMat(x, n) 함수
def powerMat(x, n):
    if n == 1:
        return x
    elif (n % 2) == 0:
        return powerMat(multMat(x, x), n // 2)
    else:
        return multMat(x, powerMat(multMat(x, x), (n - 1) // 2))


# multMat(M1, M2) 함수
def multMat(M1, M2):
    result = [[0 for _ in range(len(M2[0]))] for __ in range(len(M1))]
    for i in range(len(M1)):
        for j in range(len(M2[0])):
            for k in range(len(M1[0])):
                result[i][j] += M1[i][k] * M2[k][j]
    return result


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print(fib_mat(n))

```
