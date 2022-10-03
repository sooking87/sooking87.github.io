---
title: "[백준 11279] 최대 힙"
excerpt: "[백준 11279] 최대 힙"
categories: [Algorithm C_C++, Backjoon C++]
tags: [Algorithm Study, C/C++, Algorithm, Backjoon C++]
toc: true
toc_sticky: true
---

## 문제

널리 잘 알려진 자료구조 중 최대 힙이 있다. 최대 힙을 이용하여 다음과 같은 연산을 지원하는 프로그램을 작성하시오. <br>

0이 입력되면 자료 구조에 있는 숫자를 출력하고, 숫자가 들어있지 않다면 0을 출력한다.

## 실패 코드

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <functional> // greater, less

int main()
{

    int n;
    std::cin >> n;

    std::priority_queue<int> nums;
    std::vector<int> ans;
    for (int i = 0; i < n; i++)
    {
        int temp;
        std::cin >> temp;

        if (temp == 0)
        {
            if (nums.empty())
            {
                std::cout << 0 << std::endl;
            }
            else
            {
                std::cout << nums.top() << std::endl;
                nums.pop();
            }
        }
        else
        {
            nums.push(temp);
        }
    }
}
```

계속 시간 초과가 떠서 검색을 해보니 <br>

1. std::endl -> "\n"
2. std::cin.sync_with_stdio(0);, std::cin.tie(0); 추가 <br>

가 달랐다. 확실히 endl보다는 \n의 속도가 빠른 것 같다.

## 정답 코드

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <functional> // greater, less

int main()
{
    std::cin.sync_with_stdio(0);
    std::cin.tie(0);

    int n;
    std::cin >> n;

    std::priority_queue<int> nums;
    std::vector<int> ans;
    for (int i = 0; i < n; i++)
    {
        int temp;
        std::cin >> temp;

        if (temp == 0)
        {
            if (nums.empty())
            {
                std::cout << 0 << "\n";
            }
            else
            {
                std::cout << nums.top() << "\n";
                nums.pop();
            }
        }
        else
        {
            nums.push(temp);
        }
    }
}
```

- `std::cin.sync_with_stdio(0);` : c의 stdio와 cpp의 iostream을 동기화시켜주는 역할을 하는데, 이때 iostream과 stdio의 버퍼를 모두 사용하기 때문에 딜레이가 발생된다. 이런 문제를 해결해주기 위해서 위 코드를 작성을 해줌으로써 동기화를 비활성화 시켜준다. <br>

  이로 인해, cpp만의 독립적인 버퍼가 생성되어 c의 버퍼와 병행하여 사용할 수는 없지만 사용하는 버퍼의 수가 줄었기 때문에 실행 속도가 빨라지게 된다.

- `std::cin.tie(0);` : cin과 cout의 묶음을 풀어준다. <br>

  기본적으로 cin과 cout은 묶여있고, 묶여있는 스트림들은 한 스트림이 다른 스트림에서 각 IO작업을 진행하기 전에 자동으로 퍼버를 비워줌을 보장한다. 한마디로, 입력과 출력을 여러 번 번갈아가며 반복해야되는 경우 필수적으로 필요한 코드이다.
