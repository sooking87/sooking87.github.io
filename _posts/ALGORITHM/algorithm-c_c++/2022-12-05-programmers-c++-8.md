---
title: "[프로그래머스] 명예의 전당"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
excerpt: "[프로그래머스] 명예의 전당"
toc: true
toc_sticky: true
---

## 문제

점수가 높은 사람 중에서 최대 k 명까지만 명예의 전당에 올릴 수 있고, 그 중에서 최하점인 점수 벡터를 구하시오.

## 풀이

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

vector<int> getList(vector<int> &score, int n)
{
    vector<int> temp(score.begin(), score.begin() + n + 1);
    sort(temp.begin(), temp.end());
    return temp;
}
vector<int> solution(int k, vector<int> score) {
    vector<int> answer;
    int min = score[0];
    for (int i = 0; i < score.size(); i++)
    {
        vector<int> nList = getList(score, i); // i 번째까지 중 명예의 전당 리스트 뽑기
        if (i < k)
        {
            answer.push_back(nList[0]);
        }
        else
        {
            answer.push_back(nList[nList.size() - k]);
        }
    }
    return answer;
}
```

일단 이렇게 풀고 클래스로 정의하였다. 이렇게 하는게 맞는건지는 모르겠지만 ㅎㅎㅎㅎ <br>

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

class Test
{
protected:
    int k;
    vector<int> score;
    vector<int> getList(vector<int> &score, int n);
    int size();

public:
    Test(int k, vector<int> score);
    vector<int> solution();
    friend ostream &operator<<(ostream &os, vector<int> s);
};
Test::Test(int k, vector<int> area)
{
    this->k = k;
    this->score = area;
}
vector<int> Test::getList(vector<int> &score, int n)
{
    vector<int> temp(score.begin(), score.begin() + n + 1);
    sort(temp.begin(), temp.end());
    return temp;
}
int Test::size()
{
    int len = score.size();

    return len;
}
vector<int> Test::solution()
{
    vector<int> answer;
    int min = score[0];
    for (int i = 0; i < score.size(); i++)
    {
        vector<int> nList = getList(score, i); // i 번째까지 중 명예의 전당 리스트 뽑기
        if (i < k)
        {
            answer.push_back(nList[0]);
        }
        else
        {
            answer.push_back(nList[nList.size() - k]);
        }
    }
    return answer;
}
ostream &operator<<(ostream &os, vector<int> s)
{
    os << "List of Score: ";
    for (int i = 0; i < s.size(); i++)
    {
        os << s[i] << ", ";
    }
    os << endl;
}
```

그런 다음 오퍼레이터 오버로딩을 해보았다.

### 배운 점

벡터 슬라이싱

```cpp
vector<int> temp(score.begin(), score.begin() + n + 1);
```

## 최하점 받은 사람들 중에서 앞에서 k등인 사람

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

/* 최고점 받은 사람들 중에서 k등인 사람 */
class Test
{
protected:
    int k;
    vector<int> score;
    vector<int> getList(vector<int> &score, int n);
    virtual int kBeforeIdx(vector<int> vec);
    virtual int kAfterIdx(vector<int> vec);
    int size();

public:
    Test(int k, vector<int> score);
    vector<int> solution();
    friend ostream &operator<<(ostream &os, vector<int> s);
};
/* 최하점 받은 사람들 중에서 k등인 사람 */
class Test2 : public Test
{
protected:
    virtual int kBeforeIdx(vector<int> vec);
    virtual int kAfterIdx(vector<int> vec);

public:
    Test2(int k, vector<int> score);
};
/* Test 정의 */
Test::Test(int k, vector<int> area)
{
    this->k = k;
    this->score = area;
}
vector<int> Test::getList(vector<int> &score, int n)
{
    vector<int> temp(score.begin(), score.begin() + n + 1);
    sort(temp.begin(), temp.end());
    return temp;
}
int Test::kBeforeIdx(vector<int> vec)
{
    return 0;
}
int Test::kAfterIdx(vector<int> vec)
{
    return vec.size() - k;
}
int Test::size()
{
    int len = score.size();

    return len;
}
vector<int> Test::solution()
{
    vector<int> answer;
    for (int i = 0; i < score.size(); i++)
    {
        vector<int> nList = getList(score, i); // i 번째까지 중 명예의 전당 리스트 뽑기
        if (i < k)
        {
            answer.push_back(nList[kBeforeIdx(nList)]);
        }
        else
        {
            answer.push_back(nList[kAfterIdx(nList)]);
        }
    }
    return answer;
}
ostream &operator<<(ostream &os, vector<int> s)
{
    os << "List of Score: ";
    for (int i = 0; i < s.size(); i++)
    {
        os << s[i] << ", ";
    }
    os << endl;
}
/* Test2 정의 */
Test2::Test2(int k, vector<int> score) : Test(k, score)
{
    ;
}
int Test2::kBeforeIdx(vector<int> vec)
{
    return vec.size() - 1;
}
int Test2::kAfterIdx(vector<int> vec)
{
    return k - 1;
}
```

결국 몇 번째 점수인지가 중요한 것이고, 나머지는 따로 정의할 필요가 없다. 그래서 kBeforeIdx, kAfterIdxvirtual 함수를 정의한 것이다.
