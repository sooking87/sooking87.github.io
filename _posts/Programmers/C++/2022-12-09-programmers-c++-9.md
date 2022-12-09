---
title: "[프로그래머스] 할인 행사"
categories: [Programmers Cpp]
tags: [Programmers, Cpp]
excerpt: "[프로그래머스] 할인 행사"
toc: true
toc_sticky: true
---

## 문제

want 벡터를 number 만큼 사려고 하는데, 모든 품목이 할인이 가능할 때 사려고 한다. discount는 최대 10일을 하므로 10일이 넘어가면 행사 품목에서 제외된다. 모든 품목이 행사를 받을 때 회원등록을 하려고 할 때, 회원 등록이 가능한 날짜의 총 일수를 return하시오.

## 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

class MarketList
{
protected:
    vector<string> want;
    vector<int> number;

public:
    MarketList(vector<string> want, vector<int> number);
    bool operator==(vector<string> discountList);
};
MarketList::MarketList(vector<string> want, vector<int> number)
{
    this->want = want;
    this->number = number;
}
bool MarketList::operator==(vector<string> discountList)
{
    vector<int> copy(number);
    int i;
    for (i = 0; i < discountList.size(); i++)
    {
        for (int j = 0; j < want.size(); j++)
        {
            if (want[j] == discountList[i])
            {
                copy[j]--;
            }
        }
    }
    for (int i = 0; i < copy.size(); i++)
    {
        if (copy[i] != 0)
        {
            return false;
        }
    }
    return true;
}
int solution(vector<string> want, vector<int> number, vector<string> discount)
{
    int answer = 0;
    // want의 number와 discount len10에 맞는지 확인.
    MarketList list(want, number);
    int i;
    for (i = 0; i < discount.size() - 9; i++)
    {
        vector<string> temp(discount.begin() + i, discount.begin() + 10 + i);
        if (list == temp)
        {
            answer++;
        }
    }
    cout << answer << endl;
    return answer;
}
int main()
{
    solution( { "banana", "apple", "rice", "pork", "pot" }, { 3, 2, 2, 2, 1 }, { "chicken", "apple", "apple", "banana", "rice", "apple", "pork", "banana", "pork", "rice", "pot", "banana", "apple", "banana" } );
}
```

### 배운 점

타이핑 하기 귀찮아서 복붙하다가 MarketList 클래스 생성자의 매개 변수를 잘못 넣어버림........ 이거 시험 때도 주의 하자.
