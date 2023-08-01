---
title: "[Python] 완전 탐색"
excerpt: "[Python] 완전 탐색"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 완전 탐색

컴퓨터의 빠른 계산 성능을 활용하여 가능한 모든 경우의 수를 탐색하는 방법 == *무식하게 푼다* 의 의미인 **Brute Force**  라고도 부름 <br>
문제에서 주어질 수 있는 모든 경우의 수를 탐색하는 알고리즘

### 완전 탐색 방법

📌 [완전 탐색 풀이법 참고 링크](https://velog.io/@sxbxn/%EC%99%84%EC%A0%84%ED%83%90%EC%83%89) <br>

1. 해결하고자 하는 문제의 가능한 경우의 수를 대략적으로 계산
2. 가능한 모든 방법을 다 고려 -> 여기에는 단순 Brute Force, 순열, 재귀 호출, 비트마스크, BFS, DFS
3. 실제 답을 구할 수 있는지 적용 <br>

- 단순 Brute Force: 반복문, 조건문을 활용하여 단순하게 모든 방법을 찾는 방법(ex. 자물쇠 암호를 찾는 경우 0000 ~ 9999 모든 경우를 확인)
- BFS, DFS 활용: 그래프 자료구조에서 모든 정점을 탐색하기 위한 방법
- 순열: 임의의 수열이 있을 때, 그것을 다른 순서로 연산하는 방법인 순열을 활용하는 방법
- 재귀 호출: 재귀 함수를 통해 해결하는 방법
- 비트마스크: 비트 연산을 통해 부분 집합을 표현하는 방법

### 완전 탐색은 언제 사용하면 좋을까?

보통 완전 탐색 문제는 for문과 if문을 활용하거나, BFS/DFS를 활용하는 경우가 대부분. <br>
+a. 순열을 활용해 완전 탐색 문제를 푸는 방법도 자주 나옴 <br>

1. 입력으로 주어지는 데이터의 크기가 매주 작을 떼(데이터의 크기가 커지게 되면 O(2^N)이나, O(N!)이므로!)
2. 답의 범위가 작고, 임의의 답을 하나 선택했을 때 문제 조건을 만족하는지 역추적할 수 있을 떼. -> ❓

### 알고리즘에서 주로 쓰는 함수

1. product(곱집합) `itertools.product('1234', repeat = 2)` <br>
    이중 for문 형식으로 생각 <br>
    ```txt
    [('1', '1'), ('1', '2'), ('1', '3'), ('1', '4'),
    ('2', '1'), ('2', '2'), ('2', '3'), ('2', '4'),
    ('3', '1'), ('3', '2'), ('3', '3'), ('3', '4'),
    ('4', '1'), ('4', '2'), ('4', '3'), ('4', '4')]
    ```
2. permutations(순열) `itertools.permutations('1234', 2)` <br>
    가능한 모든 순서를 반환, 반복되는 요소가 없다. <br>
    위의 예시로는 1234 중 2개를 순서 상관 있이 뽑는 경우의 수. 즉, <small>4</small>P<small>2</small> <br>
    ```txt
    [('1', '2'), ('1', '3'), ('1', '4'),
    ('2', '1'), ('2', '3'), ('2', '4'),
    ('3', '1'), ('3', '2'), ('3', '4'),
    ('4', '1'), ('4', '2'), ('4', '3')]
    ```
3. combinations(조합) `combinations('1234', 2)` <br>
    <small>4</small>C<small>2</small> <br>
    ```txt
    [('1', '2'), ('1', '3'), ('1', '4'),
    ('2', '3'), ('2', '4'),
    ('3', '4')]
    ```
4. combinations_with_replacement(중복이 가능한 조합) `combinations_with_replacement('1234', 2)` <br>
    조합에서 개별 요소마다 두 번이상 반복할 수 있다. <br>
    ```txt
    [('1', '1'), ('1', '2'), ('1', '3'), ('1', '4'),
    ('2', '2'), ('2', '3'), ('2', '4'),
    ('3', '3'), ('3', '4'),
    ('4', '4')]
    ```

### itertools 사용

```python
import itertools as it

str = '1234'
li = ['a', 'b', 'c']

pro_str = it.product(str, repeat=3)
pro_li = it.product(li, repeat=2)
print('product:', list(pro_str))
print('product:', list(pro_li))

per_str = it.permutations(str, 2)
per_li = it.permutations(li, 2)
print('permytation:', list(per_str))
print('permutation:', list(per_li))

com_str = it.combinations(str, 2)
com_li = it.combinations(li, 2)
print('combinations:', list(com_str))
print('combinations:', list(com_li))
```