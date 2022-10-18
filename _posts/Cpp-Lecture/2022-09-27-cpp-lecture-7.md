---
title: "4.2주차"
excerpt: "4.2주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 실습 5

### 문제 설명

정수 n과 정수 배열 numlist가 매개변수로 주어질 때, numlist에서 n의 배수가 아닌 수들을 제거한 배열을 return하도록 solution 함수를 완성해주세요.

### 제한사항

1 ≤ n ≤ 10,000 <br>
1 ≤ numlist의 크기 ≤ 100 <br>
1 ≤ numlist의 원소 ≤ 100,000 <br>

### 입출력 예

|  n  |            numlist             |       result       |
| :-: | :----------------------------: | :----------------: |
|  3  | [4, 5, 6, 7, 8, 9, 10, 11, 12] |     [6, 9, 12]     |
|  5  |      [1, 9, 3, 10, 13, 5]      |      [10, 5]       |
| 12  |   [2, 100, 120, 600, 12, 12]   | [120, 600, 12, 12] |

### 내가 제출한 코드 == 교수님 코드

```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int n, vector<int> numlist)
{
vector<int> answer;

    for (int i = 0; i < numlist.size(); i++)
    {
        if (numlist[i] % n == 0)
        {
            answer.push_back(numlist[i]);
        }
    }
    return answer;

}
```

## 실습 6

### 문제 설명

정수 배열 array가 매개변수로 주어질 때, 가장 큰 수와 그 수의 인덱스를 담은 배열을 return 하도록 solution 함수를 완성해보세요.

### 제한사항

1 ≤ array의 길이 ≤ 100 <br>
0 ≤ array 원소 ≤ 1,000 <br>
array에 중복된 숫자는 없습니다. <br>

### 입출력 예

|     array      | result  |
| :------------: | :-----: |
|   [1, 8, 3]    | [8, 1]  |
| [9, 10, 11, 8] | [11, 2] |

### 내 코드 == 교수님 코드

```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> array)
{
    vector<int> answer;
    int max = array[0];
    int max_index = 0;

    for (int i = 1; i < array.size(); i++)
    {
        if (max < array[i])
        {
            max = array[i];
            max_index = i;
        }
    }

    answer.push_back(max);
    answer.push_back(max_index);

    return answer;
}
```

## 실습 7

### 문제 설명

문자열 my_string이 매개변수로 주어질 때, 대문자는 소문자로 소문자는 대문자로 변환한 문자열을 return하도록 solution 함수를 완성해주세요.

### 제한사항

1 ≤ my_string의 길이 ≤ 1,000 <br>
my_string은 영어 대문자와 소문자로만 구성되어 있습니다.

### 입출력 예

my_string result
"cccCCC" "CCCccc"
"abCdEfghIJ" "ABcDeFGHij"

### 입출력 예

|  my_string   |    result    |
| :----------: | :----------: |
|   "cccCCC"   |   "CCCccc"   |
| "abCdEfghIJ" | "ABcDeFGHij" |

### 내가 제출한 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(string my_string)
{
    string answer = "";
    for (int i = 0; i < my_string.size(); i++)
    {
        // 대문자
        if (my_string[i] >= 65 && my_string[i] <= 90)
        {
            answer.push_back(my_string[i] + 32);
        }
        // 소문자
        else if (my_string[i] >= 97 && my_string[i] <= 122)
        {
            answer.push_back(my_string[i] - 32);
        }
    }
    return answer;
}
```

### 교수님 코드

divide & conquer을 이용한다.

```cpp
#include <string>
#include <vector>

using namespace std;

char change(char c)
{
    if (c > 'Z') // lower case
    {
        c -= 'a' - 'A';
    }
    else // upper case
    {
        c += 'a' - 'A';
    }

    return c;
}
string solution(string my_string)
{
    string answer = "";
    for (int i = 0; i < my_string.length(); i++)
    {
        answer += change(my_string[i]);
        // i번째 캐릭터를 인풋해준다. 그 캐릭터라는 값을 cahnge가 대문자, 소문자로 바꾸어준다. 리턴을 바뀌어진 캐릭터로 리턴
    }
    return answer;
}
```

**_배운 점_** <br>

- 소문자의 아스키 코드 값이 더 크다. 따라서 소문자를 대문자로 바꾸고 싶다면 'a'-'A'의 값을 빼고, 대문자를 소문자로 바꾸기 위해서는 'a'-'A' 값을 더하면 된다.
- change() 함수는 대문자를 소문자로 바꾸어주거나, 소문자를 대문자로 바꾸어주는 함수이다.

## 실습 8

### 문제 설명

머쓱이는 친구들과 369게임을 하고 있습니다. 369게임은 1부터 숫자를 하나씩 대며 3, 6, 9가 들어가는 숫자는 숫자 대신 3, 6, 9의 개수만큼 박수를 치는 게임입니다. 머쓱이의 순서 order가 매개변수로 주어질 때, 머쓱이가 쳐야할 박수 횟수를 return 하도록 solution 함수를 완성해보세요.

제한사항

입출력 예
order result
3 1
29423 2

### 제한사항

1 ≤ order ≤ 1,000,000

### 입출력 예

| order | result |
| :---: | :----: |
|   3   |   1    |
| 29423 |   2    |

### 내가 제출한 코드

자리수를 한 숫자씩 판단하는 것을 활용하는 문제

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(int order)
{
    int answer = 0;

    for (int i = order; i > 0; i /= 10)
    {
        int num = i % 10;
        if (num % 3 == 0 && num != 0)
        {
            answer++;
        }
    }
    cout << answer << endl;
    return answer;
}
```

### 교수님 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int countDigit(int order, int num)
{
    int cnt = 0;
    for (int i = order; i > 0; i /= 10)
    {
        if (i % 10 == num)
        {
            cnt++;
        }
    }

    return cnt;
}
int solution(int order)
{
    int answer = 0;

    // countDigit은 order 안에 3, 6, 9가 각각 몇번 들어있는지를 확인하는 함수이다.
    answer += countDigit(order, 3);
    answer += countDigit(order, 6);
    answer += countDigit(order, 9);
    cout << answer << endl;
    return answer;
}
```

- countDigit => 인자는 몇 개, 리턴형은 뭔지를 생각하고 그 함수이름을 solution 함수에서 사용해주는 것이다.
- countDigit() 함수는 order에서 두 번째 인자가 몇 개인지를 count 해주는 함수이다.

## Chap 05: Errors
