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
