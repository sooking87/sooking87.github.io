---
title: "[JAVA] 힙 정렬"
excerpt: "힙 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 힙 정렬이란

힙 정렬은 힙을 사용하여 정렬하는 알고리즘이다. 여기서 힙은 **_부모의 값이 자식의 값보다 항상 크다_** 는 조건을 만족하는 완전이진트리이다. 이를 Max-HIP 이라고 한다. **_부모의 값이 자식보다 항상 작아도 힙_** 이라고 하고, 이를 Min-HIP 이라고 한다.

### 📍 힙 정렬 과정

1. 루트 힙을 없애고 마지막 노드를 루트로 이동
2. 다시 힙 상태를 유지하도록 만들어줌
3. 이때, 자식의 값이 작거나 잎에 다다르면 작업 종료

### 📍 배열로 힙 만들기
