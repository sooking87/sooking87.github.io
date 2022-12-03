---
title: "[프로그래머스] 택배 상자"
categories: [Programmers Cpp]
tags: [Programmers, Cpp]
excerpt: "[프로그래머스] 택배 상자"
toc: true
toc_sticky: true
---

## 문제

입력받은 순서대로 택배상자를 트럭에 실으려고 한다. 근데 택배가 오는 순서는 1부터 N까지 차례대로 오고 보조 택배상자가 있어서 임시로 넣어놓을 수 있다. 보조 택배상자는 stack과 같이 LIFO 구조를 가지고 있다.

## 풀이

```cpp
// 시간 초과
#include <string>
#include <vector>
#include <iostream>
#include <stack>

using namespace std;

class Test
{
protected:
    vector<int> order;
    virtual vector<int> getBoxes();

public:
    Test(vector<int> order);
    int solve();
};

Test::Test(vector<int> order)
{
    this->order = order;
}
vector<int> Test::getBoxes()
{
    vector<int> boxes;
    for (int i = 1; i <= order.size(); i++)
    {
        boxes.push_back(i);
    }

    return boxes;
}
int Test::solve()
{
    vector<int> boxes = getBoxes();
    stack<int> assist;
    int cnt = 0;
    for (int i = 0; i < order.size(); i++)
    {
        if (boxes[order[i] - 1] != 0)
        {
            for (int j = 0; j < order[i]; j++)
            {
                if (boxes[j] != order[i])
                {
                    assist.push(boxes[j]);
                }
                else if (boxes[j] == order[i])
                {
                    cnt++;
                }
                boxes[j] = 0;
                std::cout << "if cnt: " << cnt << endl;
            }
        }
        else
        {
            if ((assist.top() == order[i]) && assist.size() != 0)
            {
                assist.pop();
                cnt++;
            }
            else
            {
                break;
            }
            // std::cout << "else cnt: " << cnt << endl;
            // std::cout << "assist.top() cnt: " << assist.top() << endl;
        }
    }
    std::cout << cnt << endl;
    return cnt;
}
int solution(vector<int> order)
{
    int answer = 0;
    Test t(order);
    answer = t.solve();
    return answer;
}
int main()
{
    solution({1, 2, 3, 4, 5});
}
```
