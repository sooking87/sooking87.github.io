---
title: "[C++] 해시 테이블과 블룸 필터"
excerpt: "해시 테이블과 블룸 필터"
categories: [Algorithm Study]
tags: [Algorithm Study, C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 해시 테이블

사전 검색 -> 선형 검색의 경우는 O(N)의 시간이 필요하고, BST(이진 탐색 트리)의 경우에는 O(log N)의 시간이 필요하지만 검색 횟수가 크게 증가할 경우, 이 정도의 연산 속도도 만족스럽지 않을 수 있다. <br>

이런 상황에서 더 효율적인 방법은 해시 테이블이 있다. <br>

해시 테이블의 핵심은 해싱이다. 해싱은 각각의 데이터를 가그벅 고유한 숫자 값으로 표현하고, 나중에 같은 숫자 값을 사용하여 데이터의 유무를 확인하거나 또는 해당 숫자에 대응하는 원본 데이터를 추출하는 작업이다. 주어진 데이터로부터 고유한 숫자 값을 계산하는 함수를 **해시 함수** 라고 한다.

### 해싱

어떤 데이터가 있을 때, 그 데이터의 값이 들어있으면 true를 아니라면 false를 가지고 있는 배열을 가지고 있다고 하자. 근데 이 방법의 경우, 데이터가 실수인 경우, 데이터가 숫자가 아닌 경우, 데이터 범위가 너무 큰 경우라면 좋은 방법이 아니다. <br>

이를 해결하기 위해 어떤 데이터 타입의 값이든 <u>_원하는 범위의 정수로 매핑하는 함수_</u> 를 만들어 사용할 수 있다. 이 경우 원하는 정수의 범위를 적절히 설정하면 부울 타입 배열을 만드는 것이 전혀 부담이 되지 않을 수 있다. (-> ?) 이러한 역할을 하는 것이 해시 함수이다. 즉, 이 함수는 데이터 원자를 인자로 받고 정해진 범위의 정수를 반환한다. <br>
<br>

간단한 해시 함수는 큰 범위의 정수를 인자로 받아 정해진 정수로 나눈 나머지를 반환하는 모듈로 함수이며, 보통 % 기호로 표시한다. <br>

- 해시 값: 해시 함수에 의해 반환되는 숫자 값
- 충돌: 해시 함수가 서로 다른 키에 대해 같은 해시 값을 반환함으로써, 다수의 키가 같은 값을 갖게 되는 현상 <br>

일단은 같은 해시 값을 가지더라도 덮어 씌우는 함수

```cpp
#include <iostream>
#include <vector>

using uint = unsigned int;

class hash_map
{
    std::vector<int> data;

public:
    // 생성자
    hash_map(size_t n)
    {
        // data 벡터의 모든 원소를 -1로 초기화 = -1을 가지고 있다면 원소가 없음을 나타냄.
        data = std::vector<int>(n, -1);
    }

    void insert(uint value)
    {
        int n = data.size();
        data[value % n] = value;

        std::cout << value << "을(를) 삽입했습니다." << std::endl;
    }

    bool find(uint value)
    {
        int n = data.size();
        return (data[value % n] == value);
    }

    void erase(uint value)
    {
        int n = data.size();
        if (data[value % n] == value)
        {
            data[value % n] = -1;
            std::cout << value << "을(를) 삭제했습니다." << std::endl;
        }
    }
};

int main()
{
    hash_map map(7);

    auto print = [&](int value)
    {
        if (map.find(value))
            std::cout << "해시 맵에서 " << value << "을(를) 찾았습니다." << std::endl;
        else
            std::cout << "해시 맵에서 " << value << "을(를) 찾지 못했습니다." << std::endl;
    };

    map.insert(2);
    map.insert(25);
    map.insert(10);
    print(25);

    map.insert(100);
    print(100);
    print(2);

    map.erase(25);
    print(25);
}
>>>
2을(를) 삽입했습니다.
25을(를) 삽입했습니다.
10을(를) 삽입했습니다.
해시 맵에서 25을(를) 찾았습니다.
100을(를) 삽입했습니다.
해시 맵에서 100을(를) 찾았습니다.
해시 맵에서 2을(를) 찾지 못했습니다.
25을(를) 삭제했습니다.
해시 맵에서 25을(를) 찾지 못했습니다.
```

## 해시 테이블에서 충돌

### 체이닝

두 값을 모두 저장하는 여러 방법 중 하나이다. 해시 테이블의 특정 위치에서 하나의 키를 저장하는 것이 아니라 하나의 연결 리스트를 저장하는 방식이다. 여기서 벡터 대신 연결 리스트를 사용하는 이유는 특정 위치의 원소를 빠르게 삭제하기 위함이다.

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

using uint = unsigned int;

class hash_map
{
    std::vector<std::list<int>> data;

public:
    hash_map(size_t n)
    {
        data.resize(n);
    }

    void insert(uint value)
    {
        int n = data.size();
        data[value % n].push_back(value);
        std::cout << value << "을(를) 삽입했습니다." << std::endl;
    }

    bool find(uint value)
    {
        int n = data.size();
        // value % n번째 리스트를 찾아서 이를 entries라고 한다.
        auto &entries = data[value % n];
        // find의 값이 entries.end()와 같다면 value가 없다는 뜻.
        return std::find(entries.begin(), entries.end(), value) != entries.end();
    }

    void erase(uint value)
    {
        int n = data.size();
        auto &entries = data[value % n];
        auto iter = std::find(entries.begin(), entries.end(), value);

        if (iter != entries.end())
        {
            entries.erase(iter);
            std::cout << value << "을(룰) 삭제했습니다." << std::endl;
        }
    }
};

int main()
{
    hash_map map(7);

    auto print = [&](int value)
    {
        if (map.find(value))
            std::cout << "해시 맵에서 " << value << "을(를) 찾았습니다." << std::endl;
        else
            std::cout << "해시 맵에서 " << value << "을(를) 찾지 못했습니다." << std::endl;
    };

    map.insert(2);
    map.insert(25);
    map.insert(10);
    print(25);

    map.insert(100);
    print(100);
    print(2);

    map.erase(25);
    print(25);
}

>>>
2을(를) 삽입했습니다.
25을(를) 삽입했습니다.
10을(를) 삽입했습니다.
해시 맵에서 25을(를) 찾았습니다.
100을(를) 삽입했습니다.
해시 맵에서 100을(를) 찾았습니다.
해시 맵에서 2을(를) 찾았습니다.
25을(룰) 삭제했습니다.
해시 맵에서 25을(를) 찾지 못했습니다.
```

- 삽입 함수의 시간 복잡도: O(1)
- 룩업과 삭제의 시간 복잡도: O(N)

### 성능에 영향을 주는 것

1. 부하율 <br>

   부하율 = 전체 키 개수 / 해시 테이블 크기 <br>

   부햐율이 1이 가장 이상적인 경우이다. -> 하지만 전체 키 개수가 n개 이고, 해시 테이블 크기도 n개이지만 하나의 해시값에 n개가 모두 들어가 있는 경우는 검색 연산이 O(N)

2. 해시 함수 <br>

   버킷 하나에 여러개의 데이터가 모이면 안되므로 해시 함수의 역할도 중요하다.

### 열린 주소 지정

모든 원소를 해시 테이블 내부에 저장하는 방식이다. 여기서 비어있는 테이블을 찾는 방법으로는 2가지를 소개하고 있다.

#### 선형 탐색

해시 함수의 결과에 데이터가 들어있다면 다음 인덱스로 이동해서 빈 테이블을 찾을 때까지 검색을 합니다. <br>

문제점 <br>

1. 군집화 -> 검색 속도가 크게 느려질 수 있다.

#### 이차함수 탐색

선형 방정식이 아닌 이차 방정식을 사용하여 탐색을 수행하는 방식이다. 예를 들어서 해시 값이 x라면 x의 값에 데이터가 차있다면 x + 1<sup>2</sup> 의 위치에 데이터를 검색하고 그 다음은 x + 2<sup>2</sup> 을 검색하고 이런식으로 이동 폭을 이차 함수 형태로 증가시켜 군집화 문제를 줄인다.

### 뻐꾸기 해싱

완벽한 해싱 기법 중의 하나이다. 이 방법은 최악의 상황에서 시간 복잡도를 O(1)을 만족한다. <br>

두 개의 해시 테이블을 가지고 각각의 테이블은 서로 다른 해시 함수를 가진다. 모든 원소는 두 해시 테이블 중 하나에 있을 수 있으며, 그 위치는 해당 해시 테이블의 해시 함수에 의해 결정된다. <br>

- 특징
  1. 원소가 두 해시 테이블 중 어디든 저장될 수 있다.
  2. 원소가 나중에 다른 위치로 이동할 수 있다. (모든 원소가 두 개의 저장 가능한 위치를 가지며, 상황에 따라 이동할 수 있다.)

<img width="1000" alt="download1" src="https://user-images.githubusercontent.com/96654391/199192216-cec172cf-062b-464e-a4c3-f9fb15813966.png"> <br>

A를 넣을 때 B가 들어있다면 B 자리에 A를 넣고, B는 다른 해시 테이블로 넘긴다. 근데 만약에 B가 C자리로 들어가야된다면 C자리에 B를 넣고, C는 첫 번째 해시 테이블로 데이터를 이동 시킨다.

<img width="1000" alt="download2" src="https://user-images.githubusercontent.com/96654391/199192219-a24777ed-a9fe-4270-9cca-dba06e626058.png"> <br>

하지만 이렇게 된다면 무한 루프에 빠질 수 있다. 순환에 빠진다면 새로운 해시 함수를 이용하여 재해싱을 수행해야 된다. 그러나 적절한 해시 함수를 사용하면 높은 확률로 O(1)의 성능을 갖는다. <br>

열린 주소 지정 방법과 뻐꾸기 해싱 모두 전체 해시 테이블 크기 이상의 원소를 저장할 수 없다. 높은 성능을 보장하려면 부하율이 0.5보다 작게끔 설정해야된다.
