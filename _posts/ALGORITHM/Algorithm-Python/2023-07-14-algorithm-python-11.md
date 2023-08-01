---
title: "[백준 20291][Implementation] 파일 정리"
excerpt: "[백준 20291][Implementation] 파일 정리"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 20291 문제 링크](https://www.acmicpc.net/problem/20291) <br>

## 백준 20291 파일 정리

확장자의 이름과 확장자 파일의 개수를 출력 -> 확장자 이름의 사전순으로 출력

## 풀이 코드

```python
# 20291 파일 정리

# 확장자의 이름과 확장자 파일의 개수를 출력 -> 확장자 이름의 사전순으로 출력

n = int(input())
files = []
# 입력값 중 확장자만 저장
for _ in range(n):
    files.append(input().split('.')[1])

organ = {}
# 확장자 기준 있으면 + 1, 없으면 1로 딕셔너리에 추가
for i in range(n):
    value = organ.get(files[i])

    if value == None:
        organ[files[i]] = 1
    else:
        organ[files[i]] += 1

[print(key, value) for (key, value) in sorted(organ.items())]
```

## 코드 설명

입력 파일 중 확장자만 리스트에 추가 -> 딕셔너리에 키값이 있으면 + 1, 키값이 없으면 1로 value 넣기
