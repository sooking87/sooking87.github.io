---
title: "[Python] 탐색&시뮬레이션(string, 1차원, 2차원 리스트 탐색 )"
excerpt: "탐색&시뮬레이션(string, 1차원, 2차원 리스트 탐색 )"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
---

## 회문 문자열 검사

```python
n = int(input())

for i in range(n):
    word = input()
    word = word.lower()
    lenWord = len(word) - 1
    isSame = True
    for j in range(lenWord):
        if word[j] != word[len(word) - 1 - j]:
            isSame = False

    if isSame:
        print("#%d YES" % (i + 1))
    else:
        print("#%d NO" % (i + 1))
```

## 숫자만 추출

```python
def getDivisor(num):
    divisorList = []
    for i in range(1, num + 1):
        if num % i == 0:
            divisorList.append(i)
    return divisorList


t = input()
answer = ""
for i in range(len(t)):
    if t[i] >= '0' and t[i] <= '9':
        answer += t[i]

answer = int(answer)
print(answer)
print(len(getDivisor(answer)))
```

## 카드 역배치

```python
def getReverse(switchCards):
    temp = []
    for i in range(len(switchCards)-1, -1, -1):
        temp.append(switchCards[i])
    return temp


cards = [i for i in range(1, 21)]

for i in range(10):
    a, b = map(int, input().split())
    switchCards = cards[a - 1: b]
    switchCards = getReverse(switchCards)
    cards[a - 1: b] = switchCards

for i in cards:
    print(i, end=' ')
```

시간이 조금 걸렸던 이유 <br>

1. 리스트를 슬라이스를 통해서 일부만 sort를 할 수 없다.
2. sort(reverse=True)를 사용하는게 아니라 진짜 말 그래도 순서를 역으로 바꾸는 것이었다. <br>

파이썬에서의 교환 방법

```python
# 변수 교환하기
a, b = map(int, input().split())
a, b = b, a  # 파이썬에서의 교환
```

그래서 강의에서는 입력받은 인덱스 두개를 통해서 바꾸어야되는 반복문 횟수를 구한 다음에 두개의 수를 바꾸는 식으로 진행하였다.

```python
a=list(range(21))
for _ in range(10):
    s, e=map(int, input().split())
    for i in range((e-s+1)//2):
        a[s+i], a[e-i]=a[e-i], a[s+i]
a.pop(0)
for x in a:
    print(x, end=' ')
```

## 두 리스트 합치기

```python
n1 = int(input())
firstList = list(map(int, input().split()))
n2 = int(input())
secondList = list(map(int, input().split()))

answer = firstList + secondList
answer.sort()

for i in answer:
    print(i, end=' ')
```

이거는 무슨 문젤까,,,, ㅎㅎㅎㅎ 리스트 더하고 sort 하면 됨

## 수들의 합

연속적인 부분합의 합이 두 번째 입력값과 같으면 카운트를 한다.

```python
n, sumRes = map(int, input().split())
nums = list(map(int, input().split()))
cnt = 0
for i in range(n):
    sum = 0
    for j in range(i, n):
        sum += nums[j]
        if sum == sumRes:
            cnt += 1
            break
        if sum > sumRes:
            break

print(cnt)
```

근데 마지막 부분이 시간 초과가 떴다. <br>
나는 2중 반복문을 사용을 했지만, 정답 코드는 반복문 한 번으로 해결을 한 것을 알 수 있다. <br>

lt, rt는 포인터와 같은 역할이다. lt는 왼쪽 인덱스를 가리키고 rt는 오른쪽 인덱스인 1부터 가리키기 시작한다. 그리고 리스트에서 sumRes가 될 때까지 rt를 늘려가면서 `lt ~ (rt - 1)` 까지의 합을 구해서 sumRes와 비교를 한다. <br>

그리고 만약에 sum과 sumRes의 값이 같다면 lt를 오른쪽으로 한칸 이동시켜야되니까 전체 합에서 nums[lt] 만큼을 빼우고, 다음 rt의 값을 더할 준비를 한다.

```python
n, sumRes = map(int, input().split())
nums = list(map(int, input().split()))
lt = 0
rt = 1
sum = nums[0]
cnt = 0

while True:
    if sum < sumRes:
        if rt < n:
            sum += nums[rt]
            rt += 1
        else:
            break
    elif sum == sumRes:
        cnt += 1
        sum -= nums[lt]
        lt += 1
    else:
        sum -= nums[lt]
        lt += 1

print(cnt)
```

## 격자판 최대합

```python
n = int(input())
board = []

for i in range(n):
    row = list(map(int, input().split()))
    board.append(row)

sum = []
for row in range(n):
    temp1 = 0
    temp2 = 0
    for col in range(n):
        temp1 += board[row][col]
        temp2 += board[col][row]
    sum.append(temp1)
    sum.append(temp2)

temp = 0
for i in range(n):
    temp += board[i][i]
sum.append(temp)

print(max(sum))
```

그냥 격자판에서 가능한 합은 모두 구한 후 거기서 최대값을 구한다.

## 사과나무(다이아몬드)

```python
n = int(input())
farm = []
for i in range(n):
    temp = list(map(int, input().split()))
    farm.append(temp)

start = n // 2
end = start + 1
sum = 0
for row in range((n // 2) + 1):
    for col in range(start, end):
        sum += farm[row][col]
    start -= 1
    end += 1

start += 1
end -= 1
for row in range((n // 2) + 1, n):
    start += 1
    end -= 1
    for col in range(start, end):
        sum += farm[row][col]

print(sum)
```

약간 다이아몬드 점찍기처럼 인덱스를 필요로 하고 있다. <br>
이 문제는 좌표에서 다이아몬드 모양으로 그 안에 있는 숫자의 합을 구한다. <br>

정답 코드 ⏬

```python
n = int(input())
farm = [list(map(int, input().split())) for _ in range(n)]

res = 0
start = n // 2
end = n // 2

for i in range(n):
    for j in range(start, end):
        res += farm[i][j]
    if i < n // 2:
        start -= 1
        end += 1
    else:
        start += 1
        end -= 1
print(res)
```

## 곶감(모래시계)

0이면 왼쪽으로 1이면 오른쪽으로 첫 번째 입력값에 해당하는 행에 마지막 입력값만큼 이동으로 시키고 모래시계 모양으로 합을 구하는 문제이다.

```python
def getMoved(n, arrow, space, list):
    moved = []
    if arrow == 0:
        for i in range(len(list)):
            moved.append(list[(i + space) % n])
    if arrow == 1:
        haveToMove = n - space
        for i in range(len(list)):
            moved.append(list[(i + haveToMove) % n])
    return moved


def getSum(ground):
    n = len(ground)
    start = 0
    end = n
    sum = 0
    for row in range((n // 2) + 1):
        for col in range(start, end):
            sum += ground[row][col]
        start += 1
        end -= 1
    start -= 1
    end += 1
    for row in range((n // 2) + 1, n):
        start -= 1
        end += 1
        for col in range(start, end):
            sum += ground[row][col]
    return sum

# 0이면 왼쪽, 1이면 오른쪽
n = int(input())
ground = []
for i in range(n):
    temp = list(map(int, input().split()))
    ground.append(temp)

commandCnt = int(input())
for i in range(commandCnt):
    row, arrow, space = map(int, input().split())
    copy = ground[row - 1]
    movedList = getMoved(n, arrow, space, copy)
    ground[row - 1] = movedList

sum = getSum(ground)
print(sum)
```

## 봉우리

```python
n = int(input())
map = [list(map(int, input().split())) for _ in range(n)]
map.insert(0, [0]*n)
map.append([0]*n)

for x in map:
    x.insert(0, 0)
    x.append(0)

cnt = 0
# 상하좌우 비교를 할 때 이런식으로 한다.
x = [0, -1, 0, 1]
y = [-1, 0, 1, 0]
for row in range(1, n + 1):
    for col in range(1, n + 1):
        max = map[row][col]
        # all : 모두가 참일 때
        if all(max > map[row + y[k]][col + x[k]] for k in range(4)):
            cnt += 1

print(cnt)
```

**_배운 점_** <br>

1. 상하좌우를 비교하는 문제가 나오면 x, y같은 리스트를 통해서 4번 반복문을 돌린다.
2. all 이라는 키워드가 있는데, 이는 괄호 안에 모든 조건이 참일 때 참을 리턴한다.

## 스토쿠 검사

음... 말 그대로 스토쿠를 검사하는 문제이다. 근데 이ㄱ,, 이렇게 푸는게 맞아,,,,? 넘 구질구질;;; <br>

1. 먼저 행 검사를 한다. (1 ~ 9까지 있는지)
2. 그 다음 열 검사를 한다. (1 ~ 9까지 있는지)
3. 마지막으로 9칸에 1 ~ 9까지 있는지 검사를 한다.

```python
def isRightOneLine(line):
    line.sort()
    for i in range(1, 10):
        if i != line[i - 1]:
            return False
    return True


sudoku = []

for i in range(9):
    row = list(map(int, input().split()))
    sudoku.append(row)

# 행 검사
isRight = True
for i in range(9):
    temp = list(sudoku[i])
    if not isRightOneLine(temp):
        isRight = False

if isRight:
    # 열 검사
    for i in range(9):
        temp = []
        for j in range(9):
            temp.append(sudoku[j][i])
        if not isRightOneLine(temp):
            isRight = False

if isRight:
    # 9칸 검사
    for i in range(9):
        if i % 3 == 0:
            temp1 = []
            temp2 = []
            temp3 = []
        for j in range(9):
            if 0 <= j <= 2:
                temp1.append(sudoku[i][j])
            elif 3 <= j <= 5:
                temp2.append(sudoku[i][j])
            else:
                temp3.append(sudoku[i][j])

        if i % 3 == 2:
            if not isRightOneLine(temp1):
                if not isRightOneLine(temp2):
                    if not isRightOneLine(temp3):
                        isRight = False
if isRight:
    print("YES")
else:
    print("NO")
```

1. 그냥 temp = sudoku[i]를 하게 되면 같은 주소 공간을 가리키게 된다. 그래서 list라는 새로운 객체를 만들어주어야 한다.
2. 왜 `(not isRightOneLine(temp1)) or (not isRightOneLine(temp2)) or (not isRightOneLine(temp3))` 이라는 조건문은 먹지 않는 것일까?

## 격자판 회문수

```python
def getRotate(nums):
    if nums == nums[::-1]:
        return True
    else:
        return False


grid = [list(map(int, input().split())) for _ in range(7)]

cnt = 0
for start in range(3):
    for j in range(7):
        # 행 검사
        temp = grid[j][start: start + 5]
        if getRotate(temp):
            cnt += 1
        # 열 검사 -> 슬라이스로 검사를 할 수 없으므로 맨앞-맨뒤 이런식으로 반복문을 돌리면서 직접 비교를 한다. 5개를 가지고 비교를 하는 것이므로 2번만 비교를 하면 됨.
        for k in range(2):
            if grid[start + k][j] != grid[start + 5 - k - 1][j]:
                break
        else:
            cnt += 1
print(cnt)
```

리스트의 경우 회문자를 구하는 방법으로는 `nums == nums[::-1]` 가 있고, 리스트의 있는 값들 하나하나를 비교하기 위해서는 맨앞-맨뒤가 같은지, 짝꿍을 맞춰서 같은지 다른지를 비교하면 된다.
