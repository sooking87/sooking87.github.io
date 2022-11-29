---
title: "[C++] 분할 정복"
excerpt: "분할 정복"
categories: [Algorithm Study]
tags: [Algorithm Study, C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

📌알고리즘이란: 주어진 문제가 있을 때, 데이터에 대한 정확한 정의와 데이터 변환 순서는 일련의 명령에 의해 결정하는 것

## 이진 검색

선형 검색 <br>
장점: 입력 시퀀스의 정렬 여부와 상관없이 항상 잘 동작한다. <br>
단점: 비효율(시간 복잡도 O(N))<br>

주어진 시퀀스가 정렬되어 있을 때 검색 방법 = **이진 탐색**

1. 전체 시퀀스 범위를 range로 설정
2. 현재 range의 가운데 원소를 M이라고 하고, M과 N을 비교
3. M == N이라면 검색 중단
4. 그렇지 않다면 <br>
   N < M 이라면 M의 왼쪽에 N이 있으므로 M의 오른쪽은 제거 <br>
   N > M 이라면 M의 오른쪽에 N이 있으므로 M의 왼쪽은 제거
5. range에 여러 개 값이 남아있다면 2단계로 넘어감
6. N 탐색 완료 후 검색 종료

### 선형 검색 코드

```cpp
bool linear_search(int N, std::vector<int> &S)
{
    for (auto i : S)
    {
        if (i == N)
            return true; // 원소를 찾음!
    }

    return false;
}
```

### 이진 검색 코드

```cpp
bool binary_search(int N, std::vector<int> &S)
{
    auto first = S.begin();
    auto last = S.end();

    while (true)
    {
        // 현재 검색 범위의 중간 원소를 mid_element에 저장
        auto range_length = std::distance(first, last);
        auto mid_element_index = std::floor(range_length / 2);
        auto mid_element = *(first + mid_element_index);

        // mid_element와 N 값을 비교
        if (mid_element == N)
            return true;
        else if (mid_element > N)
            std::advance(last, -mid_element_index);
        else
            std::advance(first, mid_element_index);

        // 현재 검색 범위에 하나의 원소만 남아 있다면 false를 반환
        if (range_length == 1)
            return false;
    }
}
```

std::advance(\_InIt& \_Where, \_Diff \_Off) 함수를 이용하면 list나 map같은 컨테이너도 [] 연산이 가능해진다. 첫 번째 인자는 어디에서 시작했는지에 대한 it 값이고, 두 번째 인자는 그로부터 얼마나 떨어졌는지에 대한 인자이다.

## 분할 정복 이해하기

분할 정복을 해결하려면 필요한 세 단계 <br>

1. 분할: 여러 부분의 문제로 나눈다.
2. 정복: 각 부분 문제에 대한 해답을 구한다.
3. 결합: 각 부분 문제의 해답을 결합하여 전체 문제에 대한 해답을 구한다.

### 병합 정렬

전체 배열을 여러 개의 부분 배열로 나누는 작업을 반복하며, 이 작업은 각 부분 배열이 하나의 원소만 가질 때 멈춘다. 그 이후 다시 배열을 정렬을 하면서 합쳐진 배열 원소를 갖는다. 주로 대용량의 데이터를 정렬하는데 사용된다.

<img width="1000" alt="download2" src="https://user-images.githubusercontent.com/96654391/201798768-fbea2054-9758-440b-b270-b483ba36f83a.png">

### 퀵 정렬

평균 실행 시간을 줄이는 것이 목표이다.

<img width="700" alt="download2" src="https://user-images.githubusercontent.com/96654391/201802848-d35649d8-8c48-4b6f-8860-e497cdd1f36f.png">

1. 분할(Divide): 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열(피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)로 분할한다.
2. 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출 을 이용하여 다시 분할 정복 방법을 적용한다.
3. 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다. <br>

순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

### 선형 시간 선택

1. 입력 백터 V 가 있을 때 여기서 i 번째로 작은 원소를 찾으려고 한다.
2. 입력 벡터 V를 5개로 분할 -> 각 벡터를 정렬
3. 각 벡터에서의 중앙값을 모아서 집합 M을 생성
4. 집합 M에서 중앙값을 찾는다. 중앙값 = q라고 할 때.
5. q를 피벗으로 삼아 전체 벡터 V를 L과 R 벡터로 분할
6. 이때 L에 k - 1개의 원소가 있다고 하면 i == k이므로 V의 i 번째 원소는 q가 된다. <br>
   i < k 라면 V = L로 설정하고 1단계로 이동 <br>
   i > k라면 V = R로 설정하고 1단계로 이동
