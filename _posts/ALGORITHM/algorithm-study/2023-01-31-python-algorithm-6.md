---
title: "[Python] 완전탐색 (백트랙킹, 상태트리와 CUT EDGE)-DFS(깊이우선탐색)기초"
excerpt: "완전탐색 (백트랙킹, 상태트리와 CUT EDGE)-DFS(깊이우선탐색)기초"
categories: [Python Algorithm]
tags: [Python Algorithm, Python, Algorithm]
toc: true
toc_sticky: true
---

## 재귀함수란(이진수출력)

재귀함수 -> 스택을 사용을 한다. <br>
함수가 함수를 호출하기 때문에 반복문의 역할을 대신할 수 있다고 한다. (for문의 중첩이 여러 번 있다면 재귀함수의 코드가 더 유연하다.) <br>

재귀함수는 스택을 활용해서 운영이 된다. <br>
n = 3이라고 할 때,

```python
def DFS(x):
    if x > 0:
        DFS(x - 1)
        print(x, end = ' ')

n = int(input())
DFS(n)

>>>
1 2 3
```

VS

```python
def DFS(x):
    if x > 0:
        print(x, end = ' ')
        DFS(x - 1)

n = int(input())
DFS(n)

>>>
3 2 1
```

코드의 순서가 달라지면 출력되는 순서도 달라진다. 첫 번째 코드를 예를 들어 보자면 <br>

stack -> 3 기록(매개변수 x = 3, 지역변수, 복귀주소가 같이 기록이 된다.) <br>
stack -> 3, 2 기록(`DFS(x - 1)` 로 인해서) : 이때는 아직 `print(x, end = ' ')` 는 출력되지 않은 상태 <br>
stack -> 3, 2, 1 기록 <br>

이거를 활용해서 재귀함수를 이용해서 이진수를 만드는 방법은 다음과 같다.

```python
def tenToTwo(n):
    if n == 0:
        return
    else:
        tenToTwo(n // 2)
        print(n % 2, end='')


n = int(input())
tenToTwo(n)
```

## 이진트리순회

1번 노드부터 7번 노드까지 DFS를 이용해서 값을 출력하는 문제

```python
# * 전위 순회: PreOrder
# * 중위 순회: InOrder
# * 후위 순회: PostOrder


# ? 전위 순회
def DFS(start_node):
    if start_node > 7:
        return
    else:
        print(start_node, end=' ')
        DFS(start_node * 2)
        DFS(start_node * 2 + 1)


DFS(1)

# ? 중위 순회
def DFS(start_node):
    if start_node > 7:
        return
    else:
        DFS(start_node * 2)
        print(start_node, end=' ')
        DFS(start_node * 2 + 1)


DFS(1)

# ? 후위 순회
def DFS(start_node):
    if start_node > 7:
        return
    else:
        DFS(start_node * 2)
        DFS(start_node * 2 + 1)
        print(start_node, end=' ')


DFS(1)
```

내가 전에 풀었던 문제는 트리를 만들지 않고 인접 행렬과 인접 리스트를 이용해서 DFS를 적용하기 위해서 visited가 필요했던 것이었다. <br>

위의 예시는 사실상 노드번호가 탐색 순서이기 때문에 생각보다 간단하게 코드가 짜여진 것이다.

## 부분집합 구하기(DFS)

루트에서 사용하는지 아닌지를 비교를 하는 것을 상태트리라고 한다. <br>

DFS를 잘하기 위해서는 상태트리만 잘 구성하면 된다.
사용할 변수인지 아닌지를 확인하기 위해서 ch라는 리스트를 만든다.

```python
def DFS(v):
    if v == n + 1:
        # 사용하는 변수들 출력
        for i in range(1, n + 1):
            if ch[i] == 1:
                print(i, end=' ')
        print()
    else:
        ch[v] = 1  # 사용 O
        DFS(v + 1)
        ch[v] = 0  # 사용 X
        DFS(v + 1)


n = int(input())
ch = [0] * (n + 1)
DFS(1)
```

위 코드 상에서는 `ch[i] == 1` 일 때가 먼저 돌아간다. 그렇게 된다면 1 2 3이 출력되고 3부터 변수로 사용하지 않는다고 표시가 되면서 재귀함수가 돌아간다.

## 합이 같은 부분집합

```python
import sys


def DFS(index):
    if index == n:
        sum1 = 0
        sum2 = 0
        for i in range(n):
            if used[i] == 1:
                sum1 += nums[i]
            else:
                sum2 += nums[i]
        if sum1 == sum2:
            print("YES")
            sys.exit(0)
        if sum2 == sum(nums):
            print("NO")
    else:
        used[index] = 1
        DFS(index + 1)
        used[index] = 0
        DFS(index + 1)


n = int(input())
nums = list(map(int, input().split()))
used = [0]*(n + 1)
DFS(0)
```

부분 합이 같은 경우가 있다면 "YES"를 아니라면 "NO"를 출력하는 문제이다. <br>

나 같은 경우는 sum1은 used가 1인 경우의 합을 sum2는 used가 0인 경우의 합을 구한 후 그 합이 같다면 "YES"를 출력했다.
