---
title: "[백준 2615][Implementation] 오목"
excerpt: "[백준 2615][Implementation] 오목"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 2615 문제 링크](https://www.acmicpc.net/problem/2615) <br>

## 백준 2615 오목

검은 바둑알 1, 흰 바둑알 2, 알이 놓여있지 않는 경우 0 <br>
출력형식은 검은색 승 1, 흰색 승 2, 승부 결정 X 0 <br>
검은색 또는 흰색이 이겼을 경우 연속된 다섯 개의 바둑알 중 가장 왼쪽에 있는 바둑알의 가로줄 번호와 세로줄 번호를 차레로 출력 <br>

## 실패 코드

그냥 단순 직관적 구현,, 가로줄, 세로줄, 대각선에서 반복분 돌리면서 찾기

```python
# 2615 오목

# 검은 바둑알 1, 흰 바둑알 2, 알이 놓여있지 않는 경우 0
# 출력형식은 검은색 승 1, 흰색 승 2, 승부 결정 X 0
# 검은색 또는 흰색이 이겼을 경우 연속된 다섯 개의 바둑알 중 가장 왼쪽에 있는 바둑알의 가로줄 번호와 세로줄 번호를 차레로 출력

import sys

input = sys.stdin.readline
board = [list(map(int, input().split())) for _ in range(19)]
is_win = 0
ans_row = 0
ans_col = 0
temp_list = []
# 가로줄 확인
for row in range(19):
    for col in range(14):
        for k in range(5):
            if board[row][col+k] == board[row][col+k+1] and board[row][col+k] != 0:
                temp_list.append(board[row][col+k])
                is_win = 1
                ans_row = row+1
            ans_col = col+1
        # print(temp_list)
        if len(temp_list) == 4:
            is_win = 1
            ans_row = row+1
            ans_col = col+1
            temp_list = []
        temp_list = []

# 세로줄 확인
for col in range(19):
    for row in range(14):
        for k in range(5):
            if board[row+k][col] == board[row+k+1][col] and board[col][row+k] != 0:
                temp_list.append(board[col][row+k])
        # print(temp_list)
        if len(temp_list) == 4:
            is_win = 1
            ans_row = row+1
            ans_col = col+1
            temp_list = []
        temp_list = []

# 대각선 확인
for row in range(14):
    for col in range(14):
        for k in range(5):
            if board[row+k][col+k] == board[row+k+1][col+k+1] and board[row+k][col+k] != 0:
                temp_list.append(board[row+k][col+k])
        # print(temp_list)
        if len(temp_list) == 4:
            is_win = 1
            ans_row = row+1
            ans_col = col+1
            temp_list = []
            break
        temp_list = []

print(is_win)
print(ans_row, ans_col)
```

반례 발견 ❗ -> 중복 답이 생길 경우에도 답을 출력한다. <br>

가로 승리 시 답안 <br>

```txt
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 1 2 0 0 2 2 2 1 0 0 0 0 0 0 0 0 0 0
0 0 1 2 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0
0 0 0 1 2 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 1 2 2 0 0 0 0 0 0 0 0 0 0 0 0
0 0 1 1 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 2 1 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 2 2 2
```

## 실패 코드

```python
# 대각선 확인
for row in range(14):
    for col in range(14):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row+k][col+k] != 0):
                if (board[row+k][col+k] == board[row+k+1][col+k+1]):
                    temp_list.append(board[row+k][col+k])
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row+k+1][col+k+1])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1
        temp_list = []
```

뭔가 이런 식으로 현재 위치와 그 다음 위치를 비교하면서 하고 싶었는데, 그렇게 된다면 (14, 14), (19, 14), (14, 19) 와 같은 인덱스를 비교하게 된다면 `out of range` 에러가 뜸,, -> 어케 해결? 

음,,, 

```txt
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 1 2 0 0 2 2 2 1 0 0 0 0 0 2 0 0 0 0
0 0 1 2 0 0 0 0 1 0 0 0 0 0 0 2 0 0 0
0 0 0 1 2 0 0 0 0 0 0 0 0 0 0 0 2 0 0
0 0 0 0 1 2 2 0 0 0 0 0 0 0 0 0 0 2 0
0 0 1 1 0 1 2 0 0 0 0 0 0 0 0 0 0 0 2
0 0 0 0 0 0 2 1 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 2 2 2
```

## 실패 코드

```python
# 대각선 확인
for row in range(15):
    for col in range(15):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row+k][col+k] != 0):
                if (0 <= row+k <= 17) and (0 <= col+k <= 17) and (board[row+k][col+k] == board[row+k+1][col+k+1]):
                    temp_list.append(board[row+k][col+k])
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row+k+1][col+k+1])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1
        temp_list = []
``` 

인덱스 에러가 나면 단순히 인덱스 범위를 조건문의 조건으로 지정을 해주면 된다. 다만 대각선 뿐만 아니라 역대각선도 인지할 수 있어야 된다. 

## 실패 코드

```python
# 2615 오목

# 검은 바둑알 1, 흰 바둑알 2, 알이 놓여있지 않는 경우 0
# 출력형식은 검은색 승 1, 흰색 승 2, 승부 결정 X 0
# 검은색 또는 흰색이 이겼을 경우 연속된 다섯 개의 바둑알 중 가장 왼쪽에 있는 바둑알의 가로줄 번호와 세로줄 번호를 차레로 출력

import sys

input = sys.stdin.readline
board = [list(map(int, input().split())) for _ in range(19)]
is_win = 0
ans_row = 0
ans_col = 0
temp_list = []

# 대각선 확인
for row in range(15):
    for col in range(15):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row+k][col+k] != 0):
                if (0 <= row+k <= 17) and (0 <= col+k <= 17) and (board[row+k][col+k] == board[row+k+1][col+k+1]):
                    temp_list.append(board[row+k][col+k])
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row+k+1][col+k+1])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1
        temp_list = []

# 역대각선 확인
for row in range(18, 3, -1):
    for col in range(14, -1, -1):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row-k][col+k] != 0):
                if (0 <= row-k <= 17) and (0 <= col+k <= 17) and (board[row-k][col+k] == board[row-k-1][col+k+1]):
                    temp_list.append(board[row-k][col+k])
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row-k-1][col+k+1])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1
        if len(temp_list) > 5:
            is_win += len(temp_list)-4
        temp_list = []

# 가로선 확인
for row in range(19):
    for col in range(15):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row][col+k] != 0):
                if (0 <= col+k <= 17) and (board[row][col+k] == board[row][col+k+1]):
                    temp_list.append(board[row][col+k])
                    # print(temp_list)
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row][col+k+1])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1
        temp_list = []

# 세로선 확인
for col in range(19):
    for row in range(15):
        for k in range(5):
            # 1, 2만 temp_list에 넣어주기
            if (board[row+k][col] != 0):
                if (0 <= row+k <= 17) and (board[row+k][col] == board[row+k+1][col]):
                    temp_list.append(board[row+k][col])
                    # 5번째 돌 넣어주기
                    if k == 3:
                        temp_list.append(board[row+k+1][col])  
            # 0이 하나라도 있는다면 break
            else:
                break
        if len(temp_list) == 5:
            is_win += 1
            ans_row = row+1
            ans_col = col+1

if is_win == 1:
    print(is_win)
    print(ans_row, ans_col)
else:
    print(0)
```

`13%` 오답,,, 왜지 -> 육목인 경우는 승리했다볼 수 없고, 육목+오목이 있다면 오목의 색깔이 승리했다고 본다. 나는 육목이 있으면 무조건 0을 출력했기 때문에 틀렸다고 나온 것 같다. -> 육목이 있는 부분 자체는 부분적으로 보면 오목이긴 하지만 육목 부분 자체는 없다고 생각해야되나?

```txt
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 2 2 2 2
0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 2 0 2 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 2 0 0 2 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 2 0 0 0 2 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 2 2 2 2
```
## 풀이 코드

📌 [참고 코드](https://ywtechit.tistory.com/150)

```python
# 2615 오목

# 검은 바둑알 1, 흰 바둑알 2, 알이 놓여있지 않는 경우 0
# 출력형식은 검은색 승 1, 흰색 승 2, 승부 결정 X 0
# 검은색 또는 흰색이 이겼을 경우 연속된 다섯 개의 바둑알 중 가장 왼쪽에 있는 바둑알의 가로줄 번호와 세로줄 번호를 차레로 출력

import sys

input = sys.stdin.readline
board = [list(map(int, input().split())) for _ in range(19)]

dx = [1, 1, 0, -1]
dy = [0, 1, 1, 1] # 하, 우하, 우. 우상 확인

def solution():
    for x in range(19):
        for y in range(19):
            if board[x][y]: # 1, 2이면(True)
                for i in range(4):
                    nx = x + dx[i]
                    ny = y + dy[i]
                    cnt = 1

                    if nx < 0 or ny < 0 or nx >= 19 or ny >= 19:
                        continue
                    while 0 <= nx < 19 and 0 <= ny < 19 and board[x][y] == board[nx][ny]:
                        cnt += 1

                        if cnt == 5:
                            # 육목 확인 1
                            if 0 <= nx+dx[i] < 19 and 0 <= ny+dy[i] < 19 and board[nx][ny] == board[nx+dx[i]][ny+dy[i]]:
                                break
                            # 육목 확인 2
                            if 0 <= x-dx[i] < 19 and 0 <= y-dy[i] < 19 and board[x][y] == board[x-dx[i]][y-dy[i]]:
                                break
                            return board[x][y], x+1, y+1
                        nx += dx[i]
                        ny += dy[i]
    return 0, -1, -1 # 승부가 나기 않을 때

color, x, y = solution()
if not color:
    print(color)
else:
    print(color)
    print(x, y)
```

## 코드 설명

대각선/역대각선/가로선/세로선을 확인해야되므로 dx, dy를 하, 우하, 우, 우상 방향으로 잡았다. -> 4방향을 확인하는데, 만약 같다면 같은 방향으로 계속 이동하면서 같은 숫자가 연속하여 있는지를 확인한다. 그 후 육목인지 판단하기 위해서 가장 큰 인덱스 기준 한 칸 더 이동해서 해당 숫자 역시 같은지/가장 작은 인덱스 기준 한 칸 더 빼서 해당 숫자 역시 같은지를 확인한다. 
오목이 된다면 return을 통해서 승리 확정(승리는 중복하지 않으므로)

- 2차원 리스트 판별 시: 인덱스 에러를 줄이기 위해서 해당 크기 안에서만 돌아갈 수 있도록 while이나 if 문을 사용하여 조건에 넣어준다. 
- dx, dy와 같은 방향 리스트를 적극 활용해보자. -> 방향 리스트를 사용함으로써 반복문을 완전히 줄일 수 있었음.