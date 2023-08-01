---
title: "[프로그래머스] 문자열 나누기"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
excerpt: "[프로그래머스] 문자열 나누기"
toc: true
toc_sticky: true
---

## 문제

- 먼저 첫 글자를 읽습니다. 이 글자를 x라고 합시다.
- 이제 이 문자열을 왼쪽에서 오른쪽으로 읽어나가면서, x와 x가 아닌 다른 글자들이 나온 횟수를 각각 셉니다. 처음으로 두 횟수가 같아지는 순간 멈추고, 지금까지 읽은 문자열을 분리합니다.
- s에서 분리한 문자열을 빼고 남은 부분에 대해서 이 과정을 반복합니다. 남은 부분이 없다면 종료합니다.
- 만약 두 횟수가 다른 상태에서 더 이상 읽을 글자가 없다면, 역시 지금까지 읽은 문자열을 분리하고, 종료합니다. <br>

위와 같이 문자열을 분리할 때, 몇 개로 분리되는지 리턴하시오

## 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

class Split
{
protected:
    string s;
public:
    Split(string s);
    int splitStr();

};

Split::Split(string s)
{
    this->s = s;
}
int Split::splitStr()
{
    char x = s[0];
    int x_cnt = 0;
    int not_x_cnt = 0;
    int cnt = 0;
    int flag = 1;
    string temp = "";
    for (int i = 0; i < s.size(); i++)
    {
        if (flag == 0)
        {
            flag = 1;
            x = s[i];
        }

        if (x == s[i])
        {
            x_cnt++;
        }
        else
        {
            not_x_cnt++;
        }
        if (x_cnt == not_x_cnt)
        {
            temp = s.substr(0, i + 1);
            cnt++;
            x_cnt = 0;
            not_x_cnt = 0;
            flag = 0;
        }
    }
    if (temp != s)
    {
        cnt++;
    }
    return cnt;
}
int solution(string s) {
    int answer = 0;
    Split str(s);
    answer = str.splitStr();
    return answer;
}
```
