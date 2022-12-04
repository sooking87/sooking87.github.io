---
title: "[프로그래머스] n^2 배열 자르기"
categories: [Programmers Cpp]
tags: [Programmers, Cpp]
excerpt: "[프로그래머스] n^2 배열 자르기"
toc: true
toc_sticky: true
---

## 문제

![Depth-First-Search](https://user-images.githubusercontent.com/96654391/205458989-049dfd3c-6a61-4a9c-aa2b-4eb711d0d0b6.gif) <br>

와 같이 2차원 배열을 만들어서 1차원 배열로 이어 붙힌다음 left부터 right까지의 배열을 출력한다.

## 내가 짠 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

class TDArray
{
protected:
    vector<vector<int>> arr;
    int n;
    long long left;
    long long right;
    vector<int> getFC();

public:
    TDArray(int n, long long left, long long right);
    vector<int> solve();
};

TDArray::TDArray(int n, long long left, long long right)
{
    vector<vector<int>> temp(n, vector<int>(n, 0));
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < i + 1; j++)
        {
            temp[i][j] = (i + 1);
        }
        for (int j = i + 1; j < n; j++)
        {
            temp[i][j] = (j + 1);
        }
    }

    this->arr = temp;
    this->n = n;
    this->left = left;
    this->right = right;
}
vector<int> TDArray::getFC()
{
    vector<int> fc(n * n, 0);
    int idx = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            fc[idx] = arr[i][j];
            idx++;
        }
    }
    return fc;
}
vector<int> TDArray::solve()
{
    vector<int> flatten = getFC();
    vector<int> answer;
    for (int i = left; i <= right; i++)
    {
        answer.push_back(flatten[i]);
    }

    for (int i = 0; i < answer.size(); i++)
    {
        cout << answer[i] << " ";
    }
    return answer;
}
vector<int> solution(int n, long long left, long long right)
{
    vector<int> answer;
    TDArray t(n, left, right);
    answer = t.solve();
    return answer;
}
```

TDArray 객체를 만들어서 2차원 배열을 만든다면 getFC를 이용해서 1차원 배열로 만들고 left부터 right까지의 값을 answer 벡터에 push_back 해주는 방식을 사용했다.

## 정답 코드

ㄹㅇ,,,,,,,대박 진심,,,와,,,,,,,,,,,,,,,,

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(int n, long long left, long long right) {
    vector<int> answer;

    for (long long i = left; i <= right; i++)
    {
        int divisor = i / n;
        int mod = i % n;

        answer.push_back(divisor < mod ? mod + 1 : divisor + 1);
    }

    return answer;
}
```

결국 규칙 찾기,,,

### 배운 점

1. class를 활용하느라 어쩔 수 없지만 그래도 규칙이 있다는 것은 최대한 효율적으로 만들 수 있다.
2. 규칙 + 정답 형식 = 굳이 2차원 배열을 만들 필요 없이 내가 필요한 결과값만 도출을 하면 된다.

## 활용 문제?
