---
title: "[백준 1744][Sort] 수 묶기"
excerpt: "[백준 1744][Sort] 수 묶기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 1744 문제 링크](https://www.acmicpc.net/problem/1744) <br>

## 백준 1744 수 묶기

입력 받은 수를 단 한 번 또는 0번 묶어서 최대 수 출력하기

## 실패 코드

```python
# 1744 수 묶기

# 입력 받은 수를 단 한 번 또는 0번 묶어서 최대 수 출력하기

import sys

input = sys.stdin.readline
n = int(input())
nums = []
for _ in range(n):
    nums.append(int(input()))

nums.sort(reverse = True)

ans = 0
i = 0
is_last = False
while i < n - 1:
    temp1 = nums[i] * nums[i + 1]
    temp2 = nums[i] + nums[i + 1]
    if temp1 < temp2:
        ans += nums[i]
        is_last = False
    else:
        ans += temp1
        i += 1
        is_last = True
    i += 1
if not is_last:
    ans += nums[-1]
print(ans)
```

예제 코드는 다 맞았는데 `채점 중(5%)` ,,, <br>

뭐지 뭐가 문제지? <br>
질문 게시판의 반례를 찾아보니까
```txt
3
1
2
3
```
의 값은 7이 나와야되는데 6이 나옴...

## 실패 코드

위의 반례가 맞을 수 있도록 (원인: is_last를 통해서 마지막에 더해야되는지 말아야되는지 판단 한 것) 코드를 수정했다. 

```py
# 1744 수 묶기

# 입력 받은 수를 단 한 번 또는 0번 묶어서 최대 수 출력하기

import sys
from collections import deque

input = sys.stdin.readline
n = int(input())
nums = []
for _ in range(n):
    nums.append(int(input()))

nums.sort(reverse = True)
queue = deque(nums)

ans = 0
i = 0
is_last = False
num1 = queue.popleft()
while queue:
    num2 = queue.popleft()
    # print(num1, num2)
    temp1 = num1 * num2
    temp2 = num1 + num2
    if temp1 < temp2:
        ans += num1
        num1 = num2
    else:
        ans += temp1
        num1 = queue.popleft()
    # print(ans)
if not is_last:
    ans += nums[-1]
print(ans)
```

큐를 사용해서 큐가 빌 때까지 위 과정을 반복하는 것이다. -> `런타임 에러(IndexError),,` <br>

else문에 있는 popleft() 때문에 생긴다. 사실 queue가 비어있으면 그 상태로 종료를 해야되므로 해당 부분 코드 수정 완료

## 실패 코드

```python
# 1744 수 묶기

# 입력 받은 수를 단 한 번 또는 0번 묶어서 최대 수 출력하기

import sys
from collections import deque

input = sys.stdin.readline
n = int(input())
nums = []
for _ in range(n):
    nums.append(int(input()))

nums.sort(reverse = True)
queue = deque(nums)
# print(queue)

ans = 0
num1 = queue.popleft()
while queue:
    num2 = queue.popleft()
    # print(num1, num2)
    # print(queue)
    temp1 = num1 * num2
    temp2 = num1 + num2
    if temp1 < temp2:
        ans += num1
        num1 = num2
    else:
        ans += temp1
        if queue:
            num1 = queue.popleft()
    # print(ans)

print(ans)
```

음,,, 바로 `틀렸습니다` 로 뜸,,,, 왜? <br>

```txt
5
-1
-2
-3
-4
-5

ans = 25
```
반례 발견 -> 양수는 내림차순 정렬, 음수는 오름차순 정렬로 해보면 어떨까? / 음수만 짝수개 있으면 상관이 없는데 홀수개로 있는 경우가 문제.

## 풀이 코드

```python

```

## 코드 설명
