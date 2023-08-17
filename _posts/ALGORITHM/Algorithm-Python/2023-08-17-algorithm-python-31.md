---
title: "[백준 2294][DynamicProgramming2] 동전 2"
excerpt: "[백준 2294][DynamicProgramming2] 동전 2"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2294 문제 링크](https://www.acmicpc.net/problem/2294) <br>

## 백준 2294 동전 2

가치 합이 k원이 되면서 동전의 개수가 최소가 되도록 하려면 동전은 몇 개가 되는지.

## 실패 코드

```python
# 2294 동전 2

# 가치 합이 k원이 되면서 동전의 개수가 최소가 되도록 하려면 동전은 몇 개가 되는지.

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
value = [int(input()) for i in range(n)]
value.sort(reverse=True)
dp = [0] * (k+1)
dp[0] = 1
min_cnt = float('inf')
for i in range(n):
    # i원을 사용했을 때의 개수
    cnt = 0
    temp_val = k
    # print('value:', value[i], 'cnt:', cnt)
    while temp_val > 0:
        # print('temp_val:', temp_val)
        temp_val -= value[i]
        cnt += 1
        for j in range(i, n):
            # print('temp_val:', temp_val)
            if temp_val % value[j] == 0:
                cnt += (temp_val // value[j])
                temp_val -= value[j] * (temp_val // value[j])
                break
    if temp_val == 0 and (cnt < min_cnt):
        min_cnt = cnt
    # print(min_cnt)
    # print('----------')
if min_cnt == float('inf'):
    print(-1)
else:
    print(min_cnt)
```

`정답 3%`

## 실패 코드

```python
# 2294 동전 2

# 가치 합이 k원이 되면서 동전의 개수가 최소가 되도록 하려면 동전은 몇 개가 되는지.

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
value = [int(input()) for i in range(n)]

dp = [100000] * (k+1)
for i in value:
    dp[i] = 1

for i in range(min(value)+1, k+1):
    temp = []
    temp.append(dp[i])
    for j in value:
        if (dp[i-j] < 100000) and i-j >= 0:
            temp.append(dp[i-j] + 1)
            # print(temp)
    dp[i] = min(temp)
    # print(dp)

print(dp[k] if dp[k] < 100000 else -1)
```

해당 가치를 만들기 위해서 필요한 동전 개수 = 만들어진 가치에서의 동전 개수 + 1(가치가 만들어질 수 있다면!) -> ex <br>

```txt
가치 (1~k)
0  1  2  3  4  5  6  7  8  9
   1  2  3  4  1  2  3  4  5
```

근데 `런타임 에러` ,,, 인덱스 에러 같은데,, 뭐가 문제지? <br>

반례 발견

```txt
1 2
3
```

이라면 -1이 나와야되는데 인덱스 에러 발생

## 실패 코드

```python
# 2294 동전 2

# 가치 합이 k원이 되면서 동전의 개수가 최소가 되도록 하려면 동전은 몇 개가 되는지.

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
value = [int(input()) for i in range(n)]

dp = [100001] * (10000+1)
# print(dp)
for i in value:
    dp[i] = 1

for i in range(min(value)+1, k+1):
    temp = []
    temp.append(dp[i])
    for j in value:
        if (i-j >= 0) and (dp[i-j] <= 100001):
            temp.append(dp[i-j] + 1)
            # print(temp)
            print(dp[i-j])
    dp[i] = min(temp)
    print(dp)

print(dp[k] if dp[k] < 100001 else -1)
```

구해야되는 가치가 입력된 가치보다 작다면 원소 개수가 작기 때문에 인덱스 에러가 발생했었음.. 그런데도 `런타임 에러` 왜????

## 풀이 코드

```python
# 2294 동전 2

# 가치 합이 k원이 되면서 동전의 개수가 최소가 되도록 하려면 동전은 몇 개가 되는지.

import sys

input = sys.stdin.readline
n, k = map(int, input().split())
value = [int(input()) for i in range(n)]

dp = [100001] * (100000+1)
# print(dp)
for i in value:
    dp[i] = 1

for i in range(min(value)+1, k+1):
    temp = []
    temp.append(dp[i])
    for j in value:
        if (i-j >= 0) and (dp[i-j] <= 100001):
            temp.append(dp[i-j] + 1)
            # print(temp)
    dp[i] = min(temp)
    # print(dp)

print(dp[k] if dp[k] < 100001 else -1)
```

허,, ㅁㅊㅁㅊㅁ!!!

## 코드 설명

해당 인덱스(==가치)로 만들 수 있는 동전 개수를 dp에 저장한다. dp[k]가 정답이 되도록!
