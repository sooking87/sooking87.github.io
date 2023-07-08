---
title: "[Python] 선택 정렬"
excerpt: "[Python] 선택 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 선택 정렬

![download1](https://gmlwjd9405.github.io/images/algorithm-selection-sort/selection-sort.png)
<br>

인덱스 0을 기준으로 두 번째 인덱스부터 마지막까지 비교하여 가장 작은 값과 교환 <br>

인덱스 1을 기준으로 세 번째 인덱스부터 마지막까지 비교하여 가장 작은 값과 교환 <br>

## 코드

```python
n = int(input())
nums = [int(i) for i in input().split()]

for i in range(0, n - 1):
    min_idx = i
    for j in range(i + 1, n):
        if nums[min_idx] > nums[j]:
            min_idx = j

    nums[i], nums[min_idx] = nums[min_idx], nums[i]
print(nums)
```

## 백준 23881 알고리즘 수업-선택 정렬 1

선택정렬을 해서 k번 째 바뀌는 숫자 두 개를 출력하는 문제. <br>

다만 정렬을 0번째 인덱스부터 하는 것이 아니라 5번째 인덱스부터 하는 것이다.

### 실패 코드

```python
# 23881 알고리즘 수업-선택 정렬 1

# N, K를 입력받고, K번째 바뀐 숫자를 출력
import sys

input = sys.stdin.readline
n, k = map(int, input().split())
nums = [int(i) for i in input().split()]

count = 1
i = n - 1
for i in range(n - 1, 0, -1):
    max_idx = i
    for j in range(i - 1, -1, -1):
        if nums[max_idx] < nums[j]:
            max_idx = j

    if i != max_idx:
        if count == k:
            print(nums[i], nums[max_idx])
            break
        nums[max_idx], nums[i] = nums[i], nums[max_idx]
        count += 1

if i == 1:
    print(-1)
```

이 코드가 틀렸다고 나온 이유는 문제에서 나온 수도 코드에서는 selection이라는 함수로 정의가 되어있기 때문인 것 같다. <br>

selection이라는 함수 정의 이외의 다른 것은 건들인 것 없는데 `맞았습니다!` 로 바뀜(count, answer의 경우는 global로 정의를 해야 메인에서 사용 가능)

### 정답 코드

```python
# 23881 알고리즘 수업-선택 정렬 1

# N, K를 입력받고, K번째 바뀐 숫자를 출력
import sys

def selection(arr):
    global count, answer
    for i in range(n - 1, 0, -1):
        max_idx = i
        for j in range(i - 1, -1, -1):
            if arr[max_idx] < arr[j]:
                max_idx = j

        if i != max_idx:
            if count == k:
                answer = f'{arr[i]} {arr[max_idx]}'
                break
            arr[max_idx], arr[i] = arr[i], arr[max_idx]
            count += 1
    return answer

input = sys.stdin.readline
n, k = map(int, input().split())
arr = [int(i) for i in input().split()]
answer = -1
count = 1

print(selection(arr))
```
