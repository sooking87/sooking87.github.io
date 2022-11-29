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

## 확장

만약에 약수의 개수가 limit과 1차이가 난다면 power2로 대체, 1보다 차이가 크다면 power를 사용해서 답을 구하는 문제 <br>

Test를 상속받은 Test2를 사용할 건데, 여기서 solve에서 <br>

```cpp
if (divNums[i] > limit)
{
    weight += power;
}
```

부분을 수정해주어야 한다. 왜와이? limit보다 크다고 해서 무조건 power를 더하는 것이 아니라 Test2에서는 power와 power2를 분리해주어야 하기 때문이다. <br>

그래서 나는 이렇게 바꾸어 주었다.

```cpp
// 위 코드 중에서 바뀐 부분만 작성
class Test
{
protected:
    int number;
    int limit;
    int power;
    vector<int> getDivNums(int n);
    virtual int getPower(int n);

public:
    Test(int number, int limit, int power);
    int solve();
};
int Test::getPower(int n)
{
    return power;
}
int Test::solve()
{
    int weight = 0;
    vector<int> divNums = getDivNums(number);
    for (int i = 0; i < divNums.size(); i++)
    {
        if (divNums[i] > limit)
        {
            weight += getPower(divNums[i]);
        }
        else
        {
            weight += divNums[i];
        }
    }
    cout << weight << endl;
    return weight;
}
```

<br>

Test2 클래스 설계 ⏬

```cpp
/* limit과의 차이가 1인 경우 power2로 대체, 차이가 2이상인 경우 power로 대체 */
class Test2 : public Test
{
protected:
    int power2;
    virtual int getPower(int n);

public:
    Test2(int number, int limit, int power1, int power2);
};

/* Test2 정의 */
Test2::Test2(int number, int limit, int power1, int power2) : Test(number, limit, power1)
{
    this->power2 = power2;
}
int Test2::getPower(int n)
{
    if ((n - limit) == 1)
        return power2;
    else
        return power;
}
```

### 최종 코드

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <cmath>

using namespace std;

/* limit을 넘게 되면 power로 바로 대체 */
class Test
{
protected:
    int number;
    int limit;
    int power;
    vector<int> getDivNums(int n);
    virtual int getPower(int n);

public:
    Test(int number, int limit, int power);
    int solve();
};
/* limit과의 차이가 1인 경우 power2로 대체, 차이가 2이상인 경우 power로 대체 */
class Test2 : public Test
{
protected:
    int power2;
    virtual int getPower(int n);

public:
    Test2(int number, int limit, int power1, int power2);
};

/* Test 정의 */
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
    for (auto i : divNums)
    {
        cout << i << ", ";
    }
    return divNums;
}
int Test::getPower(int n)
{
    return power;
}
int Test::solve()
{
    int weight = 0;
    vector<int> divNums = getDivNums(number);
    for (int i = 0; i < divNums.size(); i++)
    {
        if (divNums[i] > limit)
        {
            weight += getPower(divNums[i]);
        }
        else
        {
            weight += divNums[i];
        }
    }
    cout << weight << endl;
    return weight;
}

/* Test2 정의 */
Test2::Test2(int number, int limit, int power1, int power2) : Test(number, limit, power1)
{
    this->power2 = power2;
}
int Test2::getPower(int n)
{
    if ((n - limit) == 1)
        return power2;
    else
        return power;
}
int solution(int number, int limit, int power)
{
    int answer = 0;
    Test t(number, limit, power);
    Test2 t2(number, limit, power, 10);

    answer = t.solve();
    int answer2 = t2.solve();
    return answer;
}
// input: 10, 3, 2
```
