---
title: "[백준 2805][BinarySearch] 나무 자르기"
excerpt: "[백준 2805][BinarySearch] 나무 자르기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2805 문제 링크](https://www.acmicpc.net/problem/2805) <br>

## 백준 2805 나무 자르기

높이 h 지정 -> 모두 잘라 -> 필요한 만큼만 집으로 가져가려고 하는데, 이때 적어도 M미터의 나무를 집에 가져가기 위해서 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램

## 실패 코드

```python
# 2805 나무 자르기

# 높이 h 지정 -> 모두 잘라 -> 필요한 만큼만 집으로 가져가려고 하는데, 이때 적어도 M미터의 나무를 집에 가져가기 위해서 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램
import sys

input = sys.stdin.readline
n, m = map(int, input().split())
height = [int(i) for i in input().split()]

start = 1
end = max(height)
isPossible = False
while start <= end:
    mid = (start + end) // 2
    get = 0
    # 얻은 나무의 길이 구하기
    for i in range(n):
        # 나무가 자를 길이보다 짧다면 얻을 수 있는 길이가 없음.
        if height[i] - mid >= 0:
            get += height[i] - mid
    if get == m:
        print(mid)
        break
    if get < m:
        end = mid - 1
    else:
        start = mid + 1
```

`정답(2%)` <br>

반례 <br>
```
3 4
3 3 5
``` 

필요한 길이랑 가장 비슷하게 잘라야되는 길이는 2이다.... 하지만 출력은 안되고 while 문 조건때문에 출력은 안되고 반복문이 끝남. <br>

## 실패 코드

```python
# 2805 나무 자르기

# 높이 h 지정 -> 모두 잘라 -> 필요한 만큼만 집으로 가져가려고 하는데, 이때 적어도 M미터의 나무를 집에 가져가기 위해서 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램
import sys

input = sys.stdin.readline
n, m = map(int, input().split())
height = [int(i) for i in input().split()]

start = 1
end = max(height)
mid = 0
while start <= end:
    mid = (start + end) // 2
    get = 0
    # 얻은 나무의 길이 구하기
    for i in range(n):
        # 나무가 자를 길이보다 짧다면 얻을 수 있는 길이가 없음.
        if height[i] - mid >= 0:
            get += height[i] - mid
    # print(get, m)
    if get == m:
        
        break
    if get < m:
        end = mid - 1
    else:
        start = mid + 1

print(mid)
``` 

무조건 나무를 가져가야되므로 반드시 잘린 나무가 M일 필요는 없음.
## 풀이 코드

```python

```

## 코드 설명
