---
title: "[백준 1463][DynamicProgramming1] 1로 만들기"
excerpt: "[백준 1463][DynamicProgramming1] 1로 만들기"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 1463 문제 링크](https://www.acmicpc.net/problem/1463) <br>

## 백준 1463 거스름돈

X가 3으로 나누어 떨어지면 3으로 나눈다. X가 2로 나누어 떨어지면 2로 나눈다. 1을 뺀다.

## 풀이 코드

```python
# 1463 1로 만들기

# X가 3으로 나누어 떨어지면 3으로 나눈다. X가 2로 나누어 떨어지면 2로 나눈다. 1을 뺀다.

import sys

input = sys.stdin.readline
n = int(input())
cnt = [0] * (n + 1)

# 그리디의 경우는 처음에 생각한 최적의 방법이 끝까지 반례없이 적용이 되는 경우다. 이런 경우는 무조건 n != 1일 떄까지 3으로 나누거나 2로 나누거나 1을 빼가면서 구해가면 된다. 
# 하지만 이 문제의 경우 10 -> 5 -> 4 -> 2 -> 1 보다는 10 -> 9 -> 3 -> 1이 최솟값을 가진다.
# 메모이제이션 방법은 중복해 계산되는 값을 저장해 효율을 높여준다.
for i in range(2, n + 1):
    cnt[i] = cnt[i - 1] + 1 # i - 1에서 1을 더하는 연산 횟수
    # cnt[1]은 1이 1이 되는데 필요한 연산 횟수
    # cnt[2]는 2가 1이 되는데 필요한 연산 횟수
    # cnt[i]는 i가 1이 되는데 필요한 연산 횟수
    if i % 3 == 0:
        cnt[i] = min(cnt[i], cnt[i // 3] + 1) # i // 3까지의 연산 횟수 + i를 3으로 나누는 연산 횟수(1회)
    if i % 2 == 0:
        cnt[i] = min(cnt[i], cnt[i // 2] + 1) # i // 2까지의 연산 횟수 + i를 2으로 나누는 연산 횟수(1회)
    # print(cnt)
print(cnt[n])    
```

## 코드 설명

위 코드 내 주석 처리 참고,,, <br>

<small>뒈지게 어렵네 ㅡㅡ</small>
