---
title: "[백준 10866] 덱"
excerpt: "[백준 10866] 덱"
categories: [Algorithm C_C++, Backjoon C++]
tags: [Algorithm Study, C/C++, Algorithm, Backjoon C++]
toc: true
toc_sticky: true
---

## 문제

해당 명령어에 맞게 덱에 원소를 추가, 삭제 등을 구하는 것이다.

## 코드

```cpp
#include <iostream>
#include <deque>
#include <string>

int main()
{
    std::cin.sync_with_stdio(0);
    std::cin.tie(0);

    std::deque<int> myDeque;
    int n;

    std::string command;
    int num;
    std::cin >> n;

    for (int i = 0; i < n; i++)
    {
        std::cin >> command;

        if (command == "push_front")
        {
            std::cin >> num;
            myDeque.push_front(num);
        }
        else if (command == "push_back")
        {
            std::cin >> num;
            myDeque.push_back(num);
        }
        else if (command == "pop_front")
        {
            if (myDeque.empty())
            {
                std::cout << -1 << "\n";
            }
            else
            {
                std::cout << myDeque.front() << "\n";
                myDeque.pop_front();
            }
        }
        else if (command == "pop_back")
        {
            if (myDeque.empty())
            {
                std::cout << -1 << "\n";
            }
            else
            {
                std::cout << myDeque.back() << "\n";
                myDeque.pop_back();
            }
        }
        else if (command == "size")
        {
            std::cout << myDeque.size() << "\n";
        }
        else if (command == "empty")
        {
            std::cout << myDeque.empty() << "\n";
        }
        else if (command == "front")
        {
            if (myDeque.empty())
            {
                std::cout << -1 << "\n";
            }
            else
            {
                std::cout << myDeque.front() << "\n";
            }
        }
        else if (command == "back")
        {
            if (myDeque.empty())
            {
                std::cout << -1 << "\n";
            }
            else
            {
                std::cout << myDeque.back() << "\n";
            }
        }
    }
}
```

## 배운 점

pop_front(), pop_back()의 경우는 딱 앞 또는 뒤의 원소를 빼주는 것이지 리턴한 값은 없다(파이썬과 다르다!)
