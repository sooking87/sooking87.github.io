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
