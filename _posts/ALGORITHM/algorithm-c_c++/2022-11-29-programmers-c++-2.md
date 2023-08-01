---
title: "[프로그래머스] 푸드 파이트 대회"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
excerpt: "[프로그래머스] 푸드 파이트 대회"
toc: true
toc_sticky: true
---

## 문제

{1, 7, 1, 2} 라는 입력이 주어진다면 0번째 인덱스는 무조건 물 1개를 의미하고 그 외의 i 번째 인덱스는 음식의 개수를 의미한다. 이 음식을 대칭적으로 분포를 하고 가운데는 무조건 물을 배치하는 결과를 리턴하시오. 홀수면 1을 줄여서 짝수로 만들고 생각.

## 문제 풀이

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

class Test
{
protected:
    vector<int> food;
    string getReverse(string str);

public:
    Test(vector<int> food);
    string solve();
};
Test::Test(vector<int> food)
{
    this->food = food;
}
string Test::getReverse(string str)
{
    string reverse = "";
    for (int i = str.size() - 1; i >= 0; i--)
    {
        reverse += str[i];
    }
    return reverse;
}
string Test::solve()
{
    string answer = "";
    for (int i = 1; i < food.size(); i++)
    {
        if (food[i] % 2 != 0)
        {
            food[i]--;
        }
        for (int cnt = 0; cnt < (food[i] / 2); cnt++)
        {
            answer += i + '0';
        }
    }
    string reverse = getReverse(answer);
    answer += "0";
    answer += reverse;
    cout << answer << endl;
    return answer;
}
string solution(vector<int> food)
{
    string answer = "";
    Test t(food);
    answer = t.solve();
    return answer;
}
// {1, 7, 1, 2}
```

이제는 어느 정도 감이 잡히는 것 같은데, 일단 Test 클래스를 만들어주고, intput에 해당하는 초기값을 생성자를 통해서 초기화를 시켜준다. <br>
그 다음 solve 함수를 통해서 전반적인 틀을 만들고, 여기서 필요한 함수는 따로 빼서 protected로 넣어 둔다.
