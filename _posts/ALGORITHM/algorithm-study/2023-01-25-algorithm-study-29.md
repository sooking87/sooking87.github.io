---
title: "[Python] 자료구조 활용(스택, 큐, 해쉬, 힙)"
excerpt: "자료구조 활용(스택, 큐, 해쉬, 힙)"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
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

## 공주구하기(큐)

파이썬에서는 큐는 리스트를 통해서 구현을 할 수 있다. 물론 `from collections import deque` 가 있긴 하지만(popleft를 사용할 수 O) 리스트에서 pop(0)을 사용해도 되므로 별 상관은 없는 것 같다. <br>

아래 코드는 큐를 통해서 구현한 것이지만 최종적으로는 리스트를 사용했다. 그래도 정답이 나오는 것 보면 뭐,,, 상관은 없는 듯?-?

```python
n, k = map(int, input().split())
prince = [i for i in range(1, n + 1)]
count = 1
while len(prince) != 1:
    if count == k:
        prince.pop(0)
        count = 1
    else:
        temp = prince.pop(0)
        prince.append(temp)
        count += 1
print(prince.pop())
```

## 응급실(큐)

처음에 내가 푼 코드 ⏬

```python
n, m = map(int, input().split())
people = list(map(int, input().split()))
num = people[m]
cnt = 0

while people:
    standard = people.pop(0)
    max = standard
    for i in range(len(people)):
        if max < people[i]:
            max = people[i]

    if standard != max:
        people.append(standard)
        people.remove(max)
    cnt += 1

    if max == num:
        print(cnt)
        break
```

근데 이렇게 풀면은 위험도가 같은 경우에는 문제의 답과 틀리게 된다. 그래서 나는 _위험도가 같은 경우 인덱스까지 어떻게 구분을 할 수 있을까_ 고민을 했다. <br>

일단 내가 문제를 잘못 이해했었음,,,,,,, <br>
왜 와이? 나는 위험도가 높은 사람이 있으면 그 사람 면저 진료를 받아야되서 pop이 필요하다고 생각 <br>
하지만 그게 아니라 위험도가 높은 사람이 있으면 그냥 뒤로 순서를 넘기기만 하는 것이었다. <br>

정답 코드 ⏬

```python
from collections import deque
n, m = map(int, input().split())
people = [(pos, val)
          for pos, val in enumerate(list(map(int, input().split())))]

people = deque(people)
cnt = 0

while True:
    cur = people.popleft()
    if any(cur[1] < x[1] for x in people):
        people.append(cur)
    else:
        cnt += 1
        if cur[0] == m:
            break
print(cnt)
```

### 배운 점

1. enumerate: 인덱스와 원소를 동시에 접근할 수 있다.
2. any 함수를 통해서 현재 값보다 큰 값이 있는지 없는지를 알 수 있다.

## 교육과정 설계(큐)

```python
from collections import deque

temp = input()
essential = list(map(str, temp))
essential.append('F') # * 지대 어거지긴 하다,,,
n = int(input())

for i in range(1, n + 1):
    cnt = 0
    ess = essential[cnt]
    timeTable = input()
    for j in timeTable:
        if ess == j:
            cnt += 1
            ess = essential[cnt]
    if cnt == len(essential) - 1:
        print("#%d YES" % i)
    else:
        print("#%d NO" % i)
```

처음에는 이렇게 생각했다. <br>

- ? 필수 수업중에 마지막 수업을 못찾더라도 이미 pop된 상태이므로 essential 자체에는 남아있는 수업이 없다. 그래서 if not essential 조건문에 걸리게 되는데 이거는 어떻게 해결할까? -> 찾으면 pop을 시키는? 식으로?
- ? 아니면 같은 수업을 발견하면 cnt += 1 하는 식으로? 그리고 그 cnt == len(essential)이게 되면 break <br>

결과적으로 exit_code1 이 떠서 정답 코드가 되지는 못했당,,,,, ㅎ 😢

```python
from collections import deque
essential = input()
n = int(input())
for i in range(1, n + 1):
    plan = input()
    dq = deque(essential)
    for x in plan:
        if x in dq:
            if x != dq.popleft():
                print("#%d NO" % (i))
                break
    else:
        if len(dq) == 0:
            print("#%d YES" % (i))
        else:
            print("#%d NO" % (i))
```

정답 코드인데 <br>

- `x in plan` : 문자열 안에 x가 있는지 없는지(필수 과목이 일단은 포함이 되는지 아닌지) <br>
  그 다음 필수 과목이 순서대로 있어야되므로 popleft를 통해서 확인을 한다.

## 단어 찾기

write에 있는 것 중 poem에 쓰이지 않은 단어 찾기

```python
n = int(input())
write = []
poem = []

for _ in range(n):
    write.append(input())

for _ in range(n - 1):
    poem.append(input())

for i in range(n):
    if write[i] in poem:
        continue
    else:
        print(write[i])
        break
```

## 아나그램(구글)

단어 조합상 str1이 str2가 될 수 있으면 YES를 출력, 아니면 NO를 출력한다.

```python
str1 = list(map(str, input()))
str2 = list(map(str, input()))

if len(str1) != len(str2):
    print("NO")
else:
    while str1:
        if str1[0] in str2:
            str2.remove(str1[0])
            str1.pop(0)
        else:
            print("NO")
            break
    if len(str1) == 0:
        print("YES")
```

## 최소힙

파이썬에서는 최소힙에 대한 모듈이 만들어져있다. <br>

`import heapq` 인데 <br>

- heapq.heappush(정렬 리스트 이름, 넣을 데이터)
- heapq.heappop(정렬 리스트 이름)
- heapq.heapify(정렬 리스트 이름) : 리스트를 한 번에 최소힙으로 정렬 <br>

```python
import heapq

heap = []
while True:
    n = int(input())
    if n == -1:
        break
    if n == 0:
        if len(heap) == 0:
            print(-1)
        else:
            res = heapq.heappop(heap)
            print(res)
    else:
        heapq.heappush(heap, n)
```

## 최대힙

하지만 최대힙에 대한 구현은 없으므로 힙 정렬을 하려면 튜플을 사용해주어야 한다. <br>

'-'를 붙히게 되면 순서가 역전되기 때문이다. 그리고 거기서 출력을 할 때, 다시 '-'를 붙히거나 아예 튜플 형태로 원래의 값과 '-'가 붙혀진 값을 모두 넣는다. <br>

아래 코드는 후자를 기준으로 최대힙을 구현하였다.

```python
import heapq

maxHeap = []
while True:
    n = int(input())
    if n == -1:
        break

    if n == 0:
        if len(maxHeap) == 0:
            print(-1)
        else:
            res = heapq.heappop(maxHeap)[1]
            print(res)
    else:
        heapq.heappush(maxHeap, (-n, n))
```

## 정리

최종적으로 스택, 큐, 힙에 대해서 했는데, 스택은 따로 구현된 모듈은 없이 append, pop을 사용해서 했고, 큐의 경우는 deque 모듈이 있다. 하지만 큐의 규칙에만 맞게 pop(0)을 해도 상관은 없다. <br>
힙의 경우는 최소힙을 heapq라는 모듈에 구현을 해두었고 최대힙을 하기 위해서는 '-'를 붙혀서 역전된 결과를 활용하면 된다.
