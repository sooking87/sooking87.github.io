---
title: "5.2주차"
excerpt: "5.2주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 실습 11

### 문제 설명

i팩토리얼 (i!)은 1부터 i까지 정수의 곱을 의미합니다. 예를들어 5! = 5 _ 4 _ 3 _ 2 _ 1 = 120 입니다. 정수 n이 주어질 때 다음 조건을 만족하는 가장 큰 정수 i를 return 하도록 solution 함수를 완성해주세요. <br>

i! ≤ n

### 제한사항

0 < n ≤ 3,628,800

### 입출력 예

|    n    | result |
| :-----: | :----: |
| 3628800 |   10   |
|    7    |   3    |

### 내가 제출한 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int getFactorial(int num, int i)
{
    return num * i;
}
int solution(int n)
{
    int answer = 0;
    int i = 1;
    int fact = 1;

    while (true)
    {
        if (fact > n)
        {
            break;
        }
        i++;
        fact = getFactorial(fact, i);
    }

    answer = i - 1;
    return answer;
}
```

### 교수님 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(int n)
{
    int answer = 0;
    int temp = 1;
    for (int i = 1; i < n; i++)
    {
        temp *= i;
        if (temp <= n)
        {
            answer = i;
        }
        else
            break;
    }
    return answer;
}
```

처음에 팩토리얼을 구하는 블랙박스를 만들었지만 지웠다. 왜그러냐면 3팩을 통해서 4팩을 구하기 위해서는 3팩 \* 4를 해주면 되기 때문에 굳이 1부터 n까지 값을 구해주는 일을 하지 않아도 같은 값을 낼 수 있다. 1부터 n까지의 곱을 구하는 함수를 지운 것이다.

## 실습 12

### 문제 설명

정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소 중 두 개를 곱해 만들 수 있는 최댓값을 return하도록 solution 함수를 완성해주세요.

### 제한사항

0 ≤ numbers의 원소 ≤ 10,000 <br>
2 ≤ numbers의 길이 ≤ 100

### 입출력 예

|        numbers        | result |
| :-------------------: | :----: |
|    [1, 2, 3, 4, 5]    |   20   |
| [0, 31, 24, 10, 1, 9] |  744   |

### 내가 제출한 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> numbers)
{
    int answer = numbers[0] * numbers[1];
    int temp = 0;

    for (int i = 0; i < numbers.size() - 1; i++)
    {
        for (int j = 0; j < numbers.size(); j++)
        {
            if (i != j)
            {
                temp = numbers[i] * numbers[j];
                if (temp > answer)
                {
                    answer = temp;
                }
            }
        }
    }
    return answer;
}
```

### 교수님 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> numbers)
{
    int answer = numbers[0] * numbers[1];
    int temp = 0;

    for (int i = 0; i < numbers.size() - 1; i++)
    {
        for (int j = i + 1; j < numbers.size(); j++)
        {
            temp = numbers[i] * numbers[j];
            if (temp > answer)
            {
                answer = temp;
            }
        }
    }
    return answer;
}
```

## 예외 처리

예외 처리 과정에서 C와 C++의 처리 방식이 다르다. <br>

예시. 나누기가 0인 경우 에러 처리하는 방법

```c
// C스러운 코딩
int div(int i, int j)
{
    if (j == 0)
    {
        return -1;
    }
    else
        return i / j;
}
```

뭔가 약속된 코드값을 리턴해서 특정값은 에러라고 인식할 수 있도록 하는 것이 C스러운 방식이다. 이 문제 상황을 인지하지 못하면 저게 정상적인 정답인 줄 안다. <br>

코드를 보면 j가 0일때 코드만 보게 되면 에러 처리임을 알 수가 없다. 의미를 숙지하고 있으면 -1로 출력되는 것이 예외 처리임을 알 수 있다. 아무튼 문법적으로 정상적인 플로우랑 비정상적인 플로우의 의미 분석이 필요하다. (C의 경우는) <br>

```cpp
// C++스러운 방식
class myerror
{
};

int div(int i, int j)
{
    if (j == 0)
    {
        throw myerror();
    }
    else
        return i / j;
}
```

> 프로그램이 죽으면 에러가 벌어졌어요!!!! <br>

throw를 하게 된다면 무조건 에러가 발생했음을 나타낸다. 프로그램이 죽으면 에러가 벌어졌어요!!!! 하고 죽게 된다. myerror가 throwing되고 죽었어요!! 라고 죽어버림. 문제 발생에 대한 책임이 없이 죽게 되버린다. 책임을 져야되는데 어떻게 책임을 지냐면 try & catch를 이용한다.

```cpp
// C++에서의 main 함수
int main()
{
    int i, j;
    cin>> i >> j;
    try
    {
        int ans = div(i, j);
        cout << ans;
    }
    catch(myerror e)
    {
        cout << "myerror";
    }
}
```

이렇게 main 코드를 바꾸게 된다면 myerror라고 나오게 되고 정상종료가 되었다. 정상 종료 -> 여기서 정상 종료가 된 이유는 예외 상황에 대해서 문제가 발생했음을 인지하고 그 상황을 정해진 무언가의 적절한 처리를 하고 정상 상황으로 돌아갔기 때문이다. <br>

catch는 비정상적인 상황일 때만 발생하는 코드이다. myerror는 누군가 throw를 한 것을 catch해서 발생한 문법이다. throw는 문제상황 발생을 의미하고, catch는 throw로 발생한 문제 상황 처리를 위한 플로우이다.
