---
title: "[Python] Dynamic Programming"
excerpt: "[Python] Dynamic Programming"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 동적 계획법

📌 [참고 링크](https://velog.io/@bonjaski0989/%EB%8F%99%EC%A0%81%EA%B3%84%ED%9A%8D%EB%B2%95Dynamic-Programming-%EC%A0%95%EB%A6%AC%EA%B8%80Python) <br>

이미 진행이 되었던 연산이 반복되는 결점을 보안하기 위해 동적 계획법이 고안되었다. <br>

- 메모이제이션(Top-Down, 하향식)
- 테이블화(Bottom-Up, 상향식)

### 보통 어떤 문제에 적용?

소문제의 결과를 다른 소문제를 푸는데 사용되는 풀이법 <br>

- 동적 계획법: 소문제 종속적(소문제가 상위 문제에 영향을 끼치며 원소들이 종속적) / Always 최적의 결과 도출
- 분할 정복: 소문제 독립적(퀵정렬, 병합 정렬)
- 그리디: '현 상태'에 대해서 최적의 경우를 판단하므로 최적해가 구해지지 않을 수 있음