---
title: "[프로그래머스] 기사단원 무기"
categories: [Programmers Cpp]
tags: [Programmers, Cpp]
excerpt: "[프로그래머스] 기사단원 무기"
toc: true
toc_sticky: true
---

## 문제

1부터 number까지의 숫자들의 약수의 개수를 구하고 그 중에서 limit을 넘는다면 power로 대체하여 모두 합하시오(필요한 철근의 무게를 구하시오.)

## 풀이

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <cmath>

using namespace std;

class Test
{
protected:
    int number;
    int limit;
    int power;
    vector<int> getDivNums(int n);

public:
    Test(int number, int limit, int power);
    int solve();
};
Test::Test(int number, int limit, int power)
{
    this->number = number;
    this->limit = limit;
    this->power = power;
}
vector<int> Test::getDivNums(int n)
{
    vector<int> divNums;
    for (int i = 1; i <= n; i++)
    {
        int cnt = 0;
        int standard = i;
        for (int j = 1; j <= sqrt(i); j++)
        {
            if (i % j == 0)
            {
                cnt++;
                if ((i / j) != j)
                    cnt++;
            }
        }
        divNums.push_back(cnt);
    }
    return divNums;
}
int Test::solve()
{
    int weight = 0;
    vector<int> divNums = getDivNums(number);
    for (int i = 0; i < divNums.size(); i++)
    {
        if (divNums[i] > limit)
        {
            weight += power;
        }
        else
        {
            weight += divNums[i];
        }
    }
    cout << weight << endl;
    return weight;
}
int solution(int number, int limit, int power)
{
    int answer = 0;
    Test t(number, limit, power);
    answer = t.solve();
    return answer;
}
```

포인트는 약수의 개수를 구할 때, 구하려는 수의 제곱근만큼을 구하고, 약수는 짝을 이루는 것을 바탕으로 cnt++ 을 한 번 더 해주는 것이다.
