---
title: "[백준 12904][String] A와 B"
excerpt: "[백준 12904][String] A와 B"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 12904 문제 링크](https://www.acmicpc.net/problem/12904) <br>

## 백준 12904 A와 B

문자열의 뒤에 A를 추가, 문자열을 뒤집고 뒤에 B를 추가 -> 위 규칙을 통해서 s를 t로 바꿀 수 있으면 1, 없으면 0을 출력

## 실패 코드

```python
# 12904 A와 B

# 문자열의 뒤에 A를 추가, 문자열을 뒤집고 뒤에 B를 추가
# 위 규칙을 통해서 s를 t로 바꿀 수 있으면 1, 없으면 0을 출력

import sys

input = sys.stdin.readline
s = input().rstrip()
t = input().rstrip()
# B -> BA -> ABB -> ABBA
# AB -> ABA -> ABAB
# A -> AB -> ABA -> ABAB
while len(s) != len(t):
    # B로 끝나면 뒤에 A만 추가
    if s[-1] == 'B':
        s += 'A'
    # A로 끝나면 뒤집고 B로 추가
    elif s[-1] == 'A':
        s = s[::-1] + 'B'
    print(s)

if s == t:
    print(1)
else:
    print(0)
```

마지막이 B로 끝나면 뒤에 A추가, A로 끝나면 뒤집고 B로 추가 -> 왜 틀림?

## 풀이 코드

```python
# 12904 A와 B

# 문자열의 뒤에 A를 추가, 문자열을 뒤집고 뒤에 B를 추가
# 위 규칙을 통해서 s를 t로 바꿀 수 있으면 1, 없으면 0을 출력

import sys

input = sys.stdin.readline
s = list(input().rstrip())
t = list(input().rstrip())
# B -> BA -> ABB -> ABBA
# AB -> ABA -> ABAB
# A -> AB -> ABA -> ABAB
while len(s) != len(t):
    # t에서 s로 가려면 A를 제거
    if t[-1] == 'A':
        t.pop()
    # t에서 s로 가려면 B가 제거되고 뒤집어야됨
    elif t[-1] == 'B':
        t.pop()
        t = t[::-1]
    # print(t)

if s == t:
    print(1)
else:
    print(0)

```

왜 틀렸냐면 사실 문제에는 어떤 경우에 A가 추가되고, 어떤 경우에 뒤집고 B가 추가되는지가 나와있ㅈㅣ 않는다. 결국, T에서 S로 유추를 하는 방법밖에 없다.

## 코드 설명

문제에서는 S -> T가 될 수 있다면 1을 출력, 아니라면 0을 출력하도록 나와있는데 <br>

결국 T -> S로 역추적하면서 S가 되는지를 봐야되는 문제 왜냐하면 어떠한 경우에 A가 추가되고, 어떤 경우에 뒤집고 B가 추가되는지를 모르기 때문에!
