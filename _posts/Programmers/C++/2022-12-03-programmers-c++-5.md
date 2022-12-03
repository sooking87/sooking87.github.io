---
title: "[프로그래머스] 연속 부분 수열 합의 개수"
categories: [Programmers Cpp]
tags: [Programmers, Cpp]
excerpt: "[프로그래머스] 연속 부분 수열 합의 개수"
toc: true
toc_sticky: true
---

## 문제

{7,9,1,1,4} 형태의 배열이라면 <br>
-> 1개 합: 7, 9, 1, 1, 4 <br>
-> 2개 합: 7+9, 9+1, 1+1, 1+4, 4+7 <br>
-> 3개 합: 7+9+1, 9+1+1, 1+1+4, 1+4+7, 4+7+9 <br>
-> 4개 합: 7+9+1+1, 9+1+1+4, 1+1+4+7, 1+4+7+9, 4+7+9+1 <br>
-> 5개 합: 7+9+1+1+4 <br>

=> 이 중에서 중복 지운 벡터 길이를 구하는 문제

## 풀이

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

class CArray
{
protected:
    vector<int> elements;
    vector<int> getSet(vector<int> &vec);

public:
    CArray(vector<int> elements);
    int solve();
};

CArray::CArray(vector<int> elements)
{
    this->elements = elements;
}
int CArray::solve()
{
    vector<int> vec;
    int len = elements.size();
    for (int i = 0; i < len * (len - 1) + 1; i++)
    {
        int n = (i / len) + 1; // n 개 더해야 됨
        int sum = 0;
        for (int j = (i % len); j < n + (i % len); j++)
        {
            sum += elements[j % elements.size()];
        }
        vec.push_back(sum);
    }
    sort(vec.begin(), vec.end());
    // 중복 제거하는 방법
    vec.erase(unique(vec.begin(), vec.end()), vec.end());

    int answer = vec.size();
    cout << answer << endl;
    return answer;
}
int solution(vector<int> elements)
{
    int answer = 0;
    CArray t(elements);
    answer = t.solve();
    return answer;
}
// {7, 9, 1, 1, 4}
```

### 배운 점

1. 중복 제거 : `vec.erase(unique(vec.begin(), vec.end()), vec.end());`
2. 전체 반복 횟수는 규칙이 있으므로 반복문 사용 횟수를 줄일 수 있다.
