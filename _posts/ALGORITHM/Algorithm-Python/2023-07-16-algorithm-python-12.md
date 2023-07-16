---
title: "[백준 22860][Implementation] 폴더정리(small)"
excerpt: "[백준 22860][Implementation] 폴더정리(small)"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 22860 문제 링크](https://www.acmicpc.net/problem/22860) <br>

## 백준 22860 폴더정리(small)

폴더 -> 1, 파일 -> 0으로 입력되고, 다음 입력된 경로의 파일의 종류의 개수와 파일의 총 개수(같은 파일이 여러 개 있을 경우 하나로 계산)

## 풀이 코드

```python
# 22860 폴더 정리(small)

# 폴더 -> 1, 파일 -> 0으로 입력되고, 다음 입력된 경로의 파일의 종류의 개수와 파일의 총 개수(같은 파일이 여러 개 있을 경우 하나로 계산)
import sys


class Node(object):
    def __init__(self, name, type):
        self.name = name
        self.type = typ
        self.file_list = []
        self.folder_list = []


def append_files(folder):
    files = []
    for next in folders[folder].folder_list:
        files += append_files(next.name)
    files += folders[folder].file_list
    return files


input = sys.stdin.readline
# 폴더의 총 개수 N, 파일의 총 개수 M
n, m = map(int, input().split())

# 와,, 어떻게 입력을 받아야되지?
# 트리 구조로 받고싶음
folders = {}
for _ in range(n+m):
    parent, name, typ = input().strip().split()
    # 루트 노드가 없다면(처음 추가될 경우)
    if parent not in folders:
        node = Node(parent, '1')
        folders[parent] = node

    # 파일이라면 해당 부모 폴더 파일리스트에 추가
    if typ == '0':
        folders[parent].file_list.append(name)
    # 폴더라면 처음 생긴 폴더만 추가해주면 됨.
    else:
        if name not in folders:
            node = Node(name, '1')
            folders[name] = node
        folders[parent].folder_list.append(folders[name])

request_num = int(input())
# 출력 형식 -> 파일 종류의 총 개수 / 파일 총 개수
for i in range(request_num):
    path = input().strip().split('/')  # strip -> 인자로 전달된 문자를 string의 오른족에서 제거

    # 이 과정을 재귀로 해야될 것 같음 -> 폴더가 있다면 들어가서 개수 카운트
    file_list = append_files(path[-1])
    print(len(set(file_list)), len(file_list))

```

## 코드 설명

연결 리스트 + 트리처럼 해당 폴더/파일 아래 어떤게 있는지를 추가하는 식으로 입력을 받았다. <br>

또한 폴더/파일 분리를 해서 넣어야 나중에 출력값을 출력하기 위해서 편리하기 때문에 노드에 file_list와 folder_list를 따로 넣어준다. <br>

마지막에 파일 개수를 카운트 하기 위해서는 같은 경우는 재귀를 사용해야될 것 같아서(main의 경로의 경우는 folderA와 folderB 둘 다에 대한 파일 개수를 세야되므로) append_files라는 함수를 통해서 재귀 방식으로 file을 리스트에 추가했다.
