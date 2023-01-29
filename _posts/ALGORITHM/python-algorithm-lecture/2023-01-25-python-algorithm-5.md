---
title: "[Python] 섹션 5. 자료구조 활용(스택, 큐, 해쉬, 힙)"
excerpt: "섹션 5. 자료구조 활용(스택, 큐, 해쉬, 힙)"
categories: [Python Algorithm]
tags: [Python Algorithm, Python, Algorithm]
toc: true
toc_sticky: true
---

## 가장 큰 수(스택)

파이썬의 경우 스택에 대한 라이브러리는 없고, 그냥 list를 활용한다. pop을 하면 LIFO에 따라 제일 나중에 들어갔던 데이터가 나오고, append를 하면 제일 뒤에 추가된다.

```python
num, m = map(int, input().split())
num = list(map(int, str(num)))
stack = []

for x in num:
    # x기준 앞에 있는 애들이 x보다 작을 경우
    while stack and m > 0 and stack[-1] < x:
        stack.pop()
        m -= 1

    stack.append(x)

if m > 0:
    stack = stack[:-m]

res = ''.join(map(str, stack))
print(res)
```

## 쇠막대기(스택)

왜 생각을 못했지? 비슷하게는 생각을 했는데, 뭔가 짝지어야되는 느낌? 이면 스택을 사용해서 문제를 푸는 것 같음

```python
n = list(map(str, input()))
temp = []
cnt = 0
raser = 0

for i in range(len(n)):
    if n[i] == '(':
        temp.append(n[i])
    else:
        temp.pop()
        if n[i - 1] == '(':
            cnt += len(temp)
        else:
            cnt += 1
print(cnt)
```

비슷하게 생각은 했는데 아쉽당,,,

## 후위표기식 만들기

- 후위표기와 스택: 중위표기식을 스택을 사용하여 후위표기식으로 구현할 수 있는데, 연산자의 우선순위에 따라 스택에 연산자를 push/pop한다.

```python
n = list(map(str, input()))
operator = []
res = ""

for i in n:
    if '0' <= i <= '9':
        res += i
    else:
        if i == '(':
            operator.append(i)
        elif i == '*' or i == '/':
            while operator and (operator[-1] == '*' or operator[-1] == '/'):
                res += operator.pop()
            operator.append(i)
        elif i == '+' or i == '-':
            while operator and (operator[-1] != '('):
                res += operator.pop()
            operator.append(i)
        elif i == ')':
            while operator and operator[-1] != '(':
                res += operator.pop()
            operator.pop()
while operator:
    res += operator.pop()
print(res)
```

- '(': 나오면 바로 스택에 push한다.
- ')': 우선순위가 가장 높은 괄호연산자가 끝난다는 뜻이므로, 괄호 안에 남아있는 연산자를 전부 pop하고 '('도 pop해줌. ')'는 처음부터 스택에 넣지 않는다.
- '_', '/': 스택에 '_', '/'가 있다면 그것들을 먼저 없어질 때까지 pop해주고 끝나면 push한다. ('+','-'은 우선순위가 낮으므로 pop안함)
- '+', '-': 스택에 다른 사칙연산자가 있다면 그것들을 먼저 없어질 때까지 (괄호연산자 직전가지)pop해주고 끝나면 push한다.

## 후위식 연산

```python
n = list(map(str, input()))
nums = []
for i in n:
    if not i.isdecimal():
        n2 = nums.pop()
        n1 = nums.pop()
        if i == '+':
            nums.append(n1 + n2)
        elif i == '-':
            nums.append(n1 - n2)
        elif i == '*':
            nums.append(n1 * n2)
        elif i == '/':
            nums.append(n1 / n2)
    else:
        nums.append(int(i))
print(nums.pop())
```

규칙자체는 <br>

1. 후위표기식을 기준으로 연산자를 찾는다.
2. 피연산자는 리스트에 따로 넣어둔다.
3. 연산자를 찾았으면 연산자 앞에 두개의 숫자를 해당 연산자로 계산을 한다.(nums.pop() 두 번) <br>

그리고 물론 일반적인 C/C++/Java의 경우는 아스키 코드를 통해서 숫자인지 아닌지를 판별했지만 파이썬의 경우는 isalpha(), isdecimal()이라는 함수를 통해서 할 수 있다. <br>
사실 코드 한 줄이기 때문에 무슨 차이가 있을까 하지만 파이썬에서 만들어준 함수를 굳이 안쓸 이유가 있을까?
