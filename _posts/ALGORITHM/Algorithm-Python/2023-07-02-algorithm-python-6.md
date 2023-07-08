---
title: "[백준 11000][Greedy] 강의실 배정"
excerpt: "[백준 11000][Greedy] 강의실 배정"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 11000 문제 링크](https://www.acmicpc.net/problem/11000) <br>

## 그리디 알고리즘을 사용한 이유

- 이거 역시 계획표에 넣을 수 있는 강의 **개수** 의 최대수를 구하라고 하였으므로 그리디를 생각할만 하다,, 아마도?

## 백준 11000 강의실 배정

S부터 T까지 진행되는 N개의 수업 중 수강 신청할 수 있는 최대 수업수

## 실패 코드

```python
# 11000 강의실 배정

# S부터 T까지 진행되는 N개의 수업 중 수강 신청할 수 있는 최대 수업수

# 입력받기
n = int(input())
classes = []
for _ in range(n):
    temp = list(map(int, input().split()))
    classes.append(temp)

# 정렬순: S -> T 즉, S순으로 정렬 후 수업 진행 시간이 작은 순대로 정렬됨
classes.sort()
standard = 0
cnt = 1
while True:
    if standard == n:
        break

    S = classes[standard][0]
    T = classes[standard][1]

    for j in range(n):
        if standard != j:
            if T <= classes[j][0]:
                standard += j - 1
                cnt += 1
                break
    standard += 1

print(cnt)
```

-> 런타임 에러 <br>

아마도 RecursionError인 듯 한데,, <br>

우선 이 코드에서 내가 구현하고자 하였던 것은 T보다 크거가 같은 다음 수업(그 수업은 T보다 크거나 같고, 수업 진행시간이 작은 수업임 -> 가능한 최대 수업을 카운트하기 위함)을 다시 standard로 잡아서 다음 가능한 수업의 개수를 세는 식으로 진행하고자 하였다. <br>

이렇게 하게되면 standard가 0인거를 무조건 start로 확정을 짓게 된다. = 그리디 알고리즘에 가장 잘 부합하지 않나? standard를 기준으로 당장 가장 좋은 선택을 하기 때문에? <br>
왜 틀렸지?

## 실패 코드

일단 위 코드의 문제점

```txt
8
1 8
9 16
3 7
8 10
10 14
5 6
6 11
11 12
```

라고 한다면 standard가 9가 나오기 때문에 break가 안되어서 에러가 났다. -> sol break문을 >= 로 부등호 수정 <br>

```python
# 11000 강의실 배정

# S부터 T까지 진행되는 N개의 수업 중 수강 신청할 수 있는 최대 수업수

# 입력받기
n = int(input())
classes = []
for _ in range(n):
    temp = list(map(int, input().split()))
    classes.append(temp)

# 정렬순: S -> T 즉, S순으로 정렬 후 수업 진행 시간이 작은 순대로 정렬됨
classes.sort()
standard = 0
cnt = 1
while True:
    if standard >= n:
        break

    S = classes[standard][0]
    T = classes[standard][1]

    for j in range(n):
        if standard != j:
            if T <= classes[j][0]:
                standard += j - 1
                cnt += 1
                break
    standard += 1

print(cnt)
```

`틀렸습니다` 로 에러 변경 -> 시간이 너무 오래걸려서 그런가?

## 실패 코드

```python
# 11000 강의실 배정

# S부터 T까지 진행되는 N개의 수업 중 수강 신청할 수 있는 최대 수업수

# 입력받기
n = int(input())
classes = []
for _ in range(n):
    temp = list(map(int, input().split()))
    classes.append(temp)

classes.sort()
standard = 0
cnt = 1
while True:
    if standard >= n:
        break

    S = classes[standard][0]
    T = classes[standard][1]

    # 정렬했으니까 standard부터 시작하도록
    for j in range(standard, n):
        # if standard != j: -> 그렇게 되면 필요없음
        if T <= classes[j][0]:
            standard += j - 1
            cnt += 1
            break
    standard += 1

print(cnt)
```

`채점 중(1%)` <br>

질문 게시판을 대충 확인해보니까 자료구조의 문제인 것 같기도,,? -> 입력받은 것 중 FIFO 방식으로 pop, push가 되었으면 좋겠으므로 큐를 사용할 예정

## 실패 코드(큐 변경)

```python
# 11000 강의실 배정

# S부터 T까지 진행되는 N개의 수업 중 수강 신청할 수 있는 최대 수업수

from queue import PriorityQueue  # 정렬을 해주어야 되므로 우선순위 큐를 임포트

# 입력받기
n = int(input())
classes = PriorityQueue()
for _ in range(n):
    temp = list(map(int, input().split()))
    classes.put(temp)

cnt = 1

temp = classes.get()
S = temp[0]
T = temp[1]

while not classes.empty():
    compare = classes.get()
    if T <= compare[0]:
        cnt += 1
        S = compare[0]
        T = compare[1]
print(cnt)
```

코드가 많이 짧아지고 단순해지기 했는데, `채점 중(2%)`,,,,,tlqkf

## 풀이 코드

📌 [참고 코드 사이트](https://velog.io/@slbin-park/%EB%B0%B1%EC%A4%80-11000%EB%B2%88-%EA%B0%95%EC%9D%98%EC%8B%A4-%EB%B0%B0%EC%A0%95-%ED%8C%8C%EC%9D%B4%EC%8D%AC) <br>

```python
import heapq
import sys

# 입력받기
input = sys.stdin.readline  # 얘의 용도?
n = int(input())
classes = []
for _ in range(n):
    temp = list(map(int, input().split()))
    classes.append(temp)

# 정렬순: S -> T 즉, S순으로 정렬 후 수업 진행 시간이 작은 순대로 정렬됨
classes.sort()
heap = []
heapq.heappush(heap, classes[0][1])  # 첫 번째 강의가 끝나는 시간을 넣음

for i in range(1, n):
    if heap[0] > classes[i][0]:
        heapq.heappush(heap, classes[i][1])
    if heap[0] <= classes[i][0]:
        heapq.heappop(heap)
        heapq.heappush(heap, classes[i][1])
print(len(heap))
```

heap을 사용한 것 이외에는 정렬을 해야되는 것과, 다음 수업 시작시간과의 비교를 통해서 수업 개수를 세는 것은 비슷하다. 하지만 다음 두 개가 차이점이 있다.

### ❓sys.stdin.readline의 용도

input()은 문자열 변환, 줄 바꿈 제거 등 추가적인 과정이 있고, 데이터가 하나씩 버퍼에 들어가는 반면, sys.stdin.readline()은 문자열로 변환, 줄 바꿈 과정이 없으며 데이터가 한 번에 버퍼에 들어가므로 <br>

**_sys.stdin.readline()이 input()보다 빠르다._**

### ❓정렬을 해야되는데 왜 heap을 사용하였나

[heapq 모듈은 왜 빠를까?](https://velog.io/@min49590/%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%98-heapq-%EB%AA%A8%EB%93%88%EC%9D%80-%EC%99%9C-%EB%B9%A0%EB%A5%BC%EA%B9%8C) <br>
[PriorityQueue & heapq / 우선순위큐와 힙큐](https://slowsure.tistory.com/130) <br>

heap 모듈의 경우는 속도도 빨라서 직접 구현한 힙 클래스로는 시간초과 문제를 해결할 수 있다. 우선순위 큐는 heapq를 활용한 모듈이다. 근데 queue 속 PriorityQueue는 Tread-Safe하고, heapq는 Non-safe하다. 즉, safe한지 아닌지 확인 절차가 필요하므로 속도가 더 느리다. <br>

또한 heapq는 리스트를 힙처럼 사용할 수 있다.

## 코드 설명

와 미친,,, 실패코드 위쪽 주석을 확인해보면 문제 해석하기 전까지도 문제 이해 잘못함,,,, -> ㅄ,,,,? <br>

수강 신청 할 수 있는 최대의 강의수를 찾는게 아니라 강의실을 최소로 개설하는 것이 문제였다,,, <br>
결국, 끝나는 시간과 시작하는 시간을 비교하는 것은 맞았지만, 경우의 수가 조금 달랐다. <br>

시작하는 순으로 정렬을 했을 때

- 끝나는 시간(heap[0]) <= 시작 시간(classes[i][0]): 기존 강의실에 개설 가능
- 끝나는 시간(heap[0]) > 시작 시간(classes[i][0]): 새로운 강의실 개설 필요 <br>

결국 heap[0]은 가장 빨리 끝나는 강의 시간, heap[1], heap[2],,,는 가장 빨리 시작하는 강의 시간의 끝나는 시간이 min-heap 구조로 정렬이 된다.

## 배운 점

1. sys.stdin.readline()
2. 문제 똑바로 읽자
3. heapq는 빠르다. <br>

골드는 골드다,,,
