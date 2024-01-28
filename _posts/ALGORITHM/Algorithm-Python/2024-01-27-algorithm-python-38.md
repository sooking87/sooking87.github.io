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

:hand_with_index_finger_and_ :

## 풀이 코드

```python

```

## 코드 설명
