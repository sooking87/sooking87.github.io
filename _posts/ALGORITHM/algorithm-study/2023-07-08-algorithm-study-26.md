---
title: "[Python] 퀵 정렬"
excerpt: "[Python] 퀵 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 퀵 정렬

![file](https://dudri63.github.io/image/algo6-2.png) <br>

피벗을 기준으로 피벗보다 작은 값은 왼쪽으로 큰 값은 오른쪽으로 이동 시킨다. <br>

피벗보다 작은 값을 찾으면 피벗보다 큰 값과 자리를 바꾼다. <br>

![image](https://dudri63.github.io/image/algo6-4.png)

## 코드

```python
def quick_sort(array, left, right):
    if left < right:
        mid = partition(array, left, right)
        quick_sort(array, left, mid - 1)
        quick_sort(array, mid + 1, right)

# 피벗 기준 작은 값은 왼쪽으로 큰 값은 오른쪽으로 분리해주는 함수
# 바뀐 피벗의 인덱스를 리턴


def partition(array, left, right):
    low = left + 1
    high = right
    pivot = array[left]

    while low <= high:
        while low <= right and array[low] <= pivot:
            low += 1
        while high >= left and array[high] > pivot:
            high -= 1
        # 피벗 기준 왼쪽에서 큰 값과 피벗 기준 오른쪽에서 작은 값의 위치 바꿈
        if low < high:
            array[low], array[high] = array[high], array[low]

    # low와 high 위치가 바뀐 경우 high와 pivot의 위치를 바꾼다.
    array[left], array[high] = array[high], array[left]

    return high
```

## 백준 2751 수 정렬하기 2

### 실패 코드

기존 퀵 정렬 공부했을 때의 코드를 사용

```python
# 2751 수 정렬하기 2

import sys


def quick_sort(array, left, right):
    if left < right:
        mid = partition(array, left, right)
        quick_sort(array, left, mid - 1)
        quick_sort(array, mid + 1, right)


def partition(array, left, right):
    pivot = array[left]
    low = left + 1
    high = right

    while low <= high:
        while low <= right and array[low] <= pivot:
            low += 1
        while high >= left and array[high] > pivot:
            high -= 1

        if low < high:
            array[low], array[high] = array[high], array[low]

    array[high], array[left] = array[left], array[high]

    return high


input = sys.stdin.readline
n = int(input())
arr = []

for _ in range(n):
    arr.append(int(input()))
quick_sort(arr, 0, len(arr) - 1)

for i in arr:
    print(i)
```

하지만 기존에 sort()라는 파이썬 기존 내장 함수 자체도 퀵 정렬을 기반으로 만들어진 것이고, 내가 구현한 것보다 훨씬 빠르므로 sort() 사용
