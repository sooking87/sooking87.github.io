---
title: "[백준 1541][Greedy] 잃어버린 괄호"
excerpt: "[백준 1541][Greedy] 잃어버린 괄호"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
---


📌 [백준 1541 문제 링크](https://www.acmicpc.net/problem/1541) <br>

## 백준 1541 잃어버린 괄호

입력받은 수식에서 괄호를 쳐서 최소의 값을 구하는 문제

## 실패 코드

```python
# 1541 잃어버린 괄호

# 입력받은 수식에서 괄호를 쳐서 최소의 값을 구하는 문제
import sys
from collections import deque

input = sys.stdin.readline
expression = input()

# operator: 연산자, operand: 피연산자
# 연산자 구하기
operator = []
for op in expression:
    if (op == '+') or (op == '-'):
        operator.append(op)

# 피연산자 구하기
temp = expression.replace('-', '+')
temp_operand = temp.split('+')
operand = []
for i in temp_operand:
    operand.append(int(i))

# deque는 파이썬에서 스택으로 사용됨
# append -> 오른쪽에 원소 삽입, pop -> 오른쪽 원소 반환
# 일단은 리스트로 가능하므로 생략
ans_ex = []
# 구현하고자 하는 것
# - 다음 숫자부터 다음 -가 나오거나 연산자 리스트가 0이 될 때까지의 합을 구하고, 그 다음도 똑같이 비교해서 최대의 값만 더해진 값으로 넣어서 eval로 계산,,,,
while True:
    if len(operator) == 0:
        break
    if operator[0] == '-':
        ans_ex.append(operand.pop(0))
        ans_ex.append(operator.pop(0))
        wtf = 0
        while True:
            wtf += operand.pop(0)
            print(wtf)
            operator.pop(0)
            print(wtf, operand, operator, '\n')
            if len(operator) == 0 or operator[0] == '-':
                break
        print(wtf)
```

너무 꼬여서 그냥 구글링 해봄,,,,,,,, 아니 근데!

## 풀이 코드

이렇게 심플할 일이냐구,, 개짜증나네 ㅡㅡ

```python
# 1541 잃어버린 괄호

# 입력받은 수식에서 괄호를 쳐서 최소의 값을 구하는 문제
import sys
from collections import deque

input = sys.stdin.readline
expression = input()

sp_minus = expression.split('-')
sum = 0
# - 앞쪽 부분은 무조건 + 일 것 이므로 모두 더해준다.
for i in sp_minus[0].split('+'):
    sum += int(i)

for i in sp_minus[1:]:
    # - 이후에 + 가 있다면 걔는 - 로 바꾸어주면 괄호를 친 격이 된다(-( + + ) == - - ) 괄호 풀면 -로 바뀜
    for j in i.split('+'):
        sum -= int(j)
print(sum)

```


## 코드 설명

`-` 앞쪽은 무조건 `+` 일 것이므로 더하고, 그 뒤에는 `-` 기준으로 쪼개는 `+` 와 피연산자의 조합이므로 거기에는 **다** 괄호를 치면 된다. <br>

아씨 또 문제 이해 잘못함,,,, 괄호를 *한 번* 만 칠 수 있는 줄 알았다,,, 그래서 연산자와 피연산자를 분리하고 -로 분리해서 최대가 되는 곳만 - 처리를 해주고 그 외는 입력받은 수식대로 계산을 해주려고 해서 코드가 꼬였다. <br>

결국,, ***문제 좀 똑바로 읽자? ^^***