---
title: "[백준 10844][DynamicProgramming1] 쉬운 계단 수"
excerpt: "[백준 10844][DynamicProgramming1] 쉬운 계단 수"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 10844 문제 링크](https://www.acmicpc.net/problem/10844) <br>

## 백준 10844 쉬운 계단 수

옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

## 실패 코드

```python
# 10844 쉬운 계단 수

# 옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

import sys

input = sys.stdin.readline
n = int(input())  # n 자리수
# 10, 12, 21, 23, 32, 34, 43, 45, 54, 56, 65, 67, 76, 78, 87, 89, 98
cnt = 0
num = [0 for i in range(10**n + 1)]  # 계단은 1부터 시작
# n == 1: 10**1 전까지
# n == 2: 10**2 전까지
# print(num)
is_possible = True
for i in range(10**(n - 1), 10**n):  # 딱 n자리 수까지만
    str_num = str(i)
    for j in range(1, n):
        if abs(int(str_num[j - 1]) - int(str_num[j])) != 1:
            is_possible = False
            break
        is_possible = True
    if is_possible:
        cnt += 1

print(cnt)
```

`메모리 초과`

## 실패 코드

```python
# 10844 쉬운 계단 수

# 옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

import sys

input = sys.stdin.readline
n = int(input())  # n 자리수
# 10, 12, 21, 23, 32, 34, 43, 45, 54, 56, 65, 67, 76, 78, 87, 89, 98

num = [0 for i in range(10**n + 1)]  # 계단은 1부터 시작
# n == 1: 10**1 전까지
# n == 2: 10**2 전까지
for i in range(1, 10):
    num[i] = 1
# 1차이가 나는 숫자들을 봤더니 2자리 수라면 쉬운 계단인 애들에서 3자리 수인 쉬운 계단이 되려면 10 자리수에서 차이가 1만 나는 애를 보면 된다.
is_possible = True
if n != 1:
    for i in range(10, 10**n):  # 딱 n자리 수까지만
        str_num = str(i)
        # print('str_num', str_num)
        start = len(str_num) - 2 # 2자리수면 1 3자리수면 2
        end = len(str_num) - 1 # 2자리수면 2 3자리수면 3

        if abs(int(str_num[start]) - int(str_num[end])) == 1:
            end_idx = len(str(i)) - 1 # n자리부터 n - 1자리까지
            if num[int(str(i)[0:end_idx])] == 1:
                num[i] = 1
                # print(i)
        
        # print('------------')
        # print(num)
cnt = len([i for i in num[10**(n - 1):10**n] if i == 1])
print(cnt % 1000000000)
```

2자리 부터 쉬운 계단인 경우를 체크한다. 왜냐하면 12는 쉬운 계단인데, 3자리인 경우의 쉬운 계단은 121, 123 이 쉬운 계단이므로 앞에 2자리수는 n == 2일때의 쉬운 계단과 동일, 맨 마지막 자리와 맨 마지막에서 두 번째 자리에 있는 숫자만 1차이가 나는지 확인하면 됨. 그래서 모든 쉬운 계단을 체크하고 해당 자리수에 해당하는 1을 카운트한다. <br>

근데 `메모리초과`  <br>

무조건 `num` 때문에 발생하는 건데 쟤를 어케 더이상 줄여?

## 풀이 코드


```python
# 10844 쉬운 계단 수

# 옆 계단이 1차이가 나는 계단이 쉬운 계단이다. 길이가 n인 계단 수가 총 몇개 있는지, 1로 시작하는 계단수

import sys

input = sys.stdin.readline
n = int(input())  # n 자리수

# dp 테이블 초기화,,
dp = [[0] * 10 for _ in range(n + 1)]

# 1의 자릿수의 경우의 수 초기화
for i in range(1, 10):
    dp[1][i] = 1

# 나머지 자릿수의 경우의 수 탐색
for i in range(2, n + 1):
    for j in range(10):
        if j == 0:
            dp[i][j] = dp[i-1][1]
        elif 1 <= j <= 8:
            dp[i][j] = dp[i-1][j-1] + dp[i-1][j+1]
        else:
            dp[i][j] = dp[i-1][8]
print(sum(dp[n]) % 1000000000)
```

## 코드 설명


📌 [참고 링크](https://wooono.tistory.com/642) <br>

최소한의 규칙(점화식)을 발견하자,,,,,,,,,,,,,,,,,,, 규칙을 보게 되면 뒷 자리가 0인 경우는 앞에 1만 올 수 있음. <br>
뒤에 1~8이 오면 두 개가 올 수 있음. <br>
뒤에 9가 오면 앞에 8만 올 수 있음. <br>

```txt
각 자릿수에서 가장 뒤에 오는 숫자(0~9)
           0  1  2  3  4  5  6  7  8  9
자릿수(0)   0  0  0  0  0  0  0  0  0  0
자릿수(1)   0  1  1  1  1  1  1  1  1  1
자릿수(2)   1  1  2  2  2  2  2  2  2  1
자릿수(3)   1  3  3  4  4  4  4  4  3  2
``` 
가능한 횟수에 뒷자리만 비교를 하면 되는데(여기까지 비슷했는데) 0 / 1~8 / 9 의 규칙은 발견하지 못했다....고 한다.. 뭬친!

### 배운 점

DP는 최소한의 규칙/점화식을 발견하자! 심플하게 하면 할수록 정답에 가까워짐!