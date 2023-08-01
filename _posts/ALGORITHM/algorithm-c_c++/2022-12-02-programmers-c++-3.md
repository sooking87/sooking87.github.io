---
title: "[프로그래머스] 숫자 짝꿍"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
excerpt: "[프로그래머스] 숫자 짝꿍"
toc: true
toc_sticky: true
---

## 문제

주어진 문자열 X와 Y에서 공통된 숫자를 뽑아서 최대 숫자의 조합으로 만드는 문제 <br>

예를 들어서 12321과 42531의 공통 숫자는 1, 2, 3이고 이 세 숫자를 통해서 만들 수 있는 최대 숫자는 321이므로 정답은 321

## 풀이

처음에는 X를 기준으로 Y에 있는 같은 숫자를 찾으면서 2중 포문을 돌렸고, 모아진 공통된 숫자를 이용해서 sort를 사용했다. 하지만 이렇게 되면 입력값이 길어지면 시간초과가 나기 때문에 패쓰,,, <br>

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

class Test
{
protected:
    string X;
    string Y;
    vector<int> getCount(string str);

public:
    Test(string X, string Y);
    string solve();
};

Test::Test(string X, string Y)
{
    this->X = X;
    this->Y = Y;
}
vector<int> Test::getCount(string str)
{
    vector<int> vec = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
    for (int i = 0; i < str.size(); i++)
    {
        vec[str[i] - '0']++;
    }
    return vec;
}
string Test::solve()
{
    string answer = "";
    vector<int> xArr = getCount(X);
    vector<int> yArr = getCount(Y);

    // 내림차순으로 정렬하기 위해서 9부터 시작
    for (int i = 9; i >= 0; i--)
    {
        int num = min(xArr[i], yArr[i]);
        for (int j = 0; j < num; j++)
        {
            answer += to_string(i);
        }
    }

    if (answer == "")
    {
        answer = "-1";
    }
    else if(answer[0]=='0')
    {
        answer = "0";
    }

    return answer;
}

string solution(string X, string Y)
{
    string answer = "";
    Test t(X, Y);
    answer = t.solve();
    return answer;
}
```

어차피 최대 10자리 수에다가 각 자리당 나올 수 있는 숫자는 0 ~ 9이므로 이 점을 이용해서 나타나는 숫자의 인덱스에 +1을 한다. <br>

그런 다음 min을 통해서 해당 인덱스가 겹치는 숫자를 뽑아낸다. 여기서 sort없이 내림차순으로 만들기 위해서 int j = 9부터 시작한 것이다.

## 겹치지 않는 숫자를 이용해서 최소값 만들기

Test 클래스를 상속받아서 겹치지 않는 숫자들 중 최솟값을 만드는 클래스를 만들어보려고 한다. 그러기 위해서는 기존에 Test 클래스에서의 solve 함수를 수정해야된다.

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

/* 겹치는 숫자를 이용해서 최대값 만들기 */
class Test
{
protected:
    string X;
    string Y;
    vector<int> getCount(string str);
    string getSorted(const vector<int> &xArr, const vector<int> &yArr);
    virtual int getNumForAnswer(int num1, int num2);
    virtual int getStartIndex();
    virtual int getDescent();

public:
    Test(string X, string Y);
    string solve();
};

/* 겹치지 않는 숫자를 이용해서 최소값 만들기 */
class Test2 : public Test
{
protected:
    virtual int getNumForAnswer(int num1, int num2);
    virtual int getStartIndex();
    virtual int getDescent();

public:
    Test2(string X, string Y);
};

/* Test 정의 */
Test::Test(string X, string Y)
{
    this->X = X;
    this->Y = Y;
}
vector<int> Test::getCount(string str)
{
    vector<int> vec = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
    for (int i = 0; i < str.size(); i++)
    {
        vec[str[i] - '0']++;
    }
    return vec;
}
string Test::getSorted(const vector<int> &xArr, const vector<int> &yArr)
{
    string answer = "";
    int startIdx = getStartIndex();
    int descent = getDescent();
    for (int i = 0; i < 10; i++, startIdx += descent)
    {
        int num = getNumForAnswer(xArr[startIdx], yArr[startIdx]);

        for (int j = 0; j < num; j++)
        {
            answer += to_string(startIdx);
        }
    }
    return answer;
}
int Test::getNumForAnswer(int num1, int num2)
{
    int returnNum = num1 > num2 ? num2 : num1;
    return returnNum;
}
int Test::getStartIndex()
{
    return 9;
}
int Test::getDescent()
{
    return -1;
}
string Test::solve()
{
    string answer = "";
    vector<int> xArr = getCount(X);
    vector<int> yArr = getCount(Y);

    answer = getSorted(xArr, yArr); // 내림 차순 정렬

    if (answer == "")
    {
        answer = "-1";
    }
    else if (answer[9 - getStartIndex()] == '0')
    {
        answer = "0";
    }
    cout << "answer: " << answer << endl;
    return answer;
}

/* Test2 정의 */
Test2::Test2(string X, string Y) : Test(X, Y)
{
}
int Test2::getNumForAnswer(int num1, int num2)
{
    int returnNum = num1 > num2 ? num1 : num2;
    return returnNum;
}
int Test2::getStartIndex()
{
    return 0;
}
int Test2::getDescent()
{
    return 1;
}
string solution(string X, string Y)
{
    string answer = "";
    Test t(X, Y);
    Test2 t2(X, Y);
    answer = t.solve();
    t2.solve();
    return answer;
}
// X = 1232145 -> answer: 522
// Y = 97252 -> answer: 112234579
```
