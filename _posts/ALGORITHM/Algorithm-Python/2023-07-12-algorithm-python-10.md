---
title: "[백준 20164][Implementation] 홀수 홀릭 호석"
excerpt: "[백준 20164][Implementation] 홀수 홀릭 호석"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 20164 문제 링크](https://www.acmicpc.net/problem/20164) <br>

## 백준 20164 홀수 홀릭 호석

- 숫자 개수가 1개 -> 그대로 출력
- 숫자 개수가 2개 -> 두 수를 더함
- 숫자 개수가 3개 이상 -> 임의의 지점에서 세 수를 나누어 더함
- 나올 수 있는 홀수의 최댓값과 최솟값을 구하는 문제

## 실패 코드

- 일단 나올 수 있는 경우의 수 만큼 쪼개는 것 까지는 가능
- 문제를 풀다 보니까 재귀로 해야되는 것 같은데 재귀로 어디서 리턴을 넣어야되는지 잘 모르겠음...

```python
# 세 개로 쪼개는 코드
for i in range(1, len(n) - 1):
    for j in range(i + 1, len(n)):
        first = int(copy_n[0:i])
        second = int(copy_n[i:j])
        last = int(copy_n[j:len(copy_n)])
```

```python
# 20164 홀수 홀릭 호석

# 숫자 개수가 1개 -> 그대로 출력
# 숫자 개수가 2개 -> 두 수를 더함
# 숫자 개수가 3개 이상 -> 임의의 지점에서 세 수를 나누어 더함
# 나올 수 있는 홀수의 최댓값과 최솟값을 구하는 문제

# 514(2) -> 5 + 1 + 4 = 10(1) -> 1(1)

# 쪼개진 상태로 그 값을 유지하면서 사용해야되므로 재귀를 사용해야될 것 같음.

import sys
import math


def main_func(cnt, copy_n):
    print("cnt:", cnt)
    if len(copy_n) == 1:
        if int(copy_n) % 2 != 0:
            cnt += 1
        print(copy_n, "리턴 전 cnt:", cnt)
        return cnt
    elif len(copy_n) == 2:
        print("2인 경우", copy_n)
        first = int(copy_n[0])
        second = int(copy_n[1])
        if first % 2 != 0:
            cnt += 1
        if second % 2 != 0:
            cnt += 1
        copy_n = str(first + second)
        print(cnt)
        main_func(cnt, copy_n)
    else:
        print('3이상인 경우')
        for i in range(1, len(copy_n) - 1):
            for j in range(i + 1, len(copy_n)):
                first = int(copy_n[0:i])
                second = int(copy_n[i:j])
                last = int(copy_n[j:len(copy_n)])
                if first % 2 != 0:
                    cnt += 1
                if second % 2 != 0:
                    cnt += 1
                if last % 2 != 0:
                    cnt += 1
                print(first, second, last)
                copy_n = str(first + second + last)

                main_func(cnt, copy_n)


input = sys.stdin.readline
n = input()
# 문자열 입력 시 \n 제거
n = n.replace('\n', '')
ans = n
cnt = 0
cnt_list = []
loop = math.comb(len(n) - 1, 2)  # 몇 개를 쪼갤 수 있는지
print(loop)
main_func(cnt, n)
print('cnt', cnt_list)
```

## 풀이 코드

```python
# 20164 홀수 홀릭 호석

# 숫자 개수가 1개 -> 그대로 출력
# 숫자 개수가 2개 -> 두 수를 더함
# 숫자 개수가 3개 이상 -> 임의의 지점에서 세 수를 나누어 더함
# 나올 수 있는 홀수의 최댓값과 최솟값을 구하는 문제

# 514(2) -> 5 + 1 + 4 = 10(1) -> 1(1)

# 쪼개진 상태로 그 값을 유지하면서 사용해야되므로 재귀를 사용해야될 것 같음.

import math


def odd_counting(n):
    odd_cnt = 0
    for i in n:
        if int(i) % 2 != 0:
            odd_cnt += 1
    return odd_cnt


def main_func(n, odd_cnt):
    global min_v, max_v

    if len(n) == 1:
        min_v = min(min_v, odd_cnt)
        max_v = max(max_v, odd_cnt)
    elif len(n) == 2:
        first = int(n[0])
        second = int(n[1])
        temp = str(first + second)
        main_func(temp, odd_cnt + odd_counting(temp))
    else:
        for i in range(1, len(n) - 1):
            for j in range(i + 1, len(n)):
                first = int(n[0:i])
                second = int(n[i:j])
                last = int(n[j:len(n)])
                temp = str(first + second + last)
                main_func(temp, odd_cnt + odd_counting(temp))


n = input()
min_v = math.inf
max_v = 0

main_func(n, odd_counting(n))
print(min_v, max_v)
```

## 코드 설명

거의 맞았는데(odd_counting 자체를 따로 빼기만 하면) 일단 재귀함수라고 해놓고는 `return` 을 해버리면 ㅋㅋㅋㅋ 거기서 그냥 함수가 끝나버림(돌아와서 다른 방식으로 3개로 분리가 안됨.) <br>

- 출력하라는 것을 잘 생각해서 함수의 매개변수를 잘 구성하기,, <br>

코드 자체는 문제에서 나온 규칙과 동일하므로 PASS!
