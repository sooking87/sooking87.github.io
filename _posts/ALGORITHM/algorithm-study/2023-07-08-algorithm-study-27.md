---
title: "[Python] 삽입 정렬"
excerpt: "[Python] 삽입 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 삽입 정렬

![image](https://devjin-blog.com/static/ecd5862c2796e7a5289af51d65939b5b/39d76/insertion_sort.png) <br>

9는 이미 정렬된 상태이다. <br>
7을 기준으로 7보다 앞쪽 수열 중 7이 들어갈 자리를 탐색한다. <br>
7은 9보다 작으므로 9 앞으로 삽입 <br>

...

### 삽입 정렬 vs 선택 정렬

삽입 정렬의 경우는 진짜 **삽입** 하기 때문에 이를 위해서 그 삽입할 자리를 만들어주기 위해서 실제로 리스트 상의 수열들을 오른쪽(또는 왼쪽)으로 자리를 이동시켜준다. <br>

하지만 선택 정렬의 경우는 바꿀 두 수를 **선택** 해서 두 수의 위치만 바꾸어 준다.

## 코드

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1  # key 값 바로 앞부터 인덱스 0까지 중 key가 들어갈 자리 찾기

        while j >= 0 and arr[j] >= key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

    return arr
```

## 백준 24051 알고리즘 수업-삽입 정렬 1

### 코드

```python
# 24051 알고리즘 수업-삽입 정렬 1

import sys


def insertion_sort(arr):
    global cnt, k
    for i in range(1, len(arr)):
        key = arr[i]
        compare_idx = i - 1

        while compare_idx >= 0 and arr[compare_idx] > key:
            arr[compare_idx + 1] = arr[compare_idx]
            compare_idx -= 1
            cnt += 1
            if k == cnt:
                return arr[compare_idx + 1]

        if compare_idx + 1 != i:
            arr[compare_idx + 1] = key
            cnt += 1
            if k == cnt:
                return arr[compare_idx + 1]

    return -1


input = sys.stdin.readline
n, k = map(int, input().split())
nums = [int(i) for i in input().split()]
cnt = 0
print(insertion_sort(nums))
```

아 tlqkf,,,아니 loacl -> global 자체는 시간이 많이 든다,, 아니 이 문제 은근 빡침,,,,, <br>

질문 게시판을 찾아보니까 `# Python3 으로는 제한 시간 내에 수행이 되지 않으니 PyPy3로 제출하시기를 권장합니다 :)` 이런 문장 발견,,, -> 같은 코드 제출했는데 맞음,, 담부터는 PyPy3으로 제출해야겠다 ㅎㅎㅎ
