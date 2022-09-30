---
title: "5.1주차"
excerpt: "5.1주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 과제 3

문자열 2진수 덧셈 계산하기

### 내 코드

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <cmath>

using namespace std;

long long tenConvertTwo(int num)
{
    long long result = 0;
    for (long long i = 1; num > 0; i *= 10)
    {
        int binary = num % 2;
        result += binary * i;
        num /= 2;
    }
    return result;
}
int twoConvertTen(int num)
{
    int result = 0, mul = 1;
    while (num > 0)
    {
        if (num % 2)
        {
            result += mul;
        }
        mul *= 2;
        num /= 10;
    }

    return result;
}
string addBin(int num1, int num2)
{
    int ten_num1 = twoConvertTen(num1);
    int ten_num2 = twoConvertTen(num2);
    // ok

    int result = ten_num1 + ten_num2;
    long long answer = tenConvertTwo(result);
    string return_ans = to_string(answer);

    return return_ans;
}
string solution(string bin1, string bin2)
{
    string answer = "";

    if (bin1 == "")
    {
        bin1 = "0";
    }
    if (bin2 == "")
    {
        bin2 = "0";
    }
    int num_bin1 = stoi(bin1);
    int num_bin2 = stoi(bin2);

    answer = addBin(num_bin1, num_bin2);
    return answer;
}

int main()
{
    solution("1011111111", "1100000011");
}
```

기본 구조는 2진수 문자열 -> 2진수 정수형 -> 10진수 정수형 -> 덧셈 -> 2진수 정수형 -> 2진수 문자열 루트로 돌아간다.

### 교수님 코드

```cpp
#include <iostream>
#include <string>
using namespace std;

int getDigit(string bin, int i)
{
    // i번째란 뒤에서부터 i 번째라는 의미
    // ?? 근데 만약에 bin1이랑 bin2길이가 다르면 없는 인덱스도 있을 텐데 그거에 대한 i는 어떻게 뽑는다는 거지? 짧은 거를 기준으로 len을 잡고 그외의 나머지는 makeAnswer를 통해서 그냥 붙혀나갸야되는거 아닌가?
    // 해결책 : if 문
    if (bin.length() > i)
    {
        return bin[bin.length() - i - 1] - '0';
        // '0'을 빼야 진짜로 integer 가 리턴된다. 그렇지 아니면 0또는 1의 문자의 아스키코드가 리턴된다.
    }
    else
    {
        return 0;
    }
}
string makeAnswer(string ans, int i)
{
    if (i == 1)
    {
        return "1" + ans;
    }
    else
    {
        return "0" + ans;
    }
}
string solution(string bin1, string bin2)
{
    string answer = "";
    int a, b, c, s; // a = getDigit(bin1, i);, b = getDigit(bin2, i);
    // i번째 값을 리턴해주는 디짓
    // c는 자리올림
    c = 0;
    int len = bin1.length();
    if (len < bin2.length())
    {
        len = bin2.length();
    }

    for (int i = 0; i < len; i++)
    {

        a = getDigit(bin1, i);
        b = getDigit(bin2, i);
        s = (a + b + c) % 2; // 뒷자리
        c = (a + b + c) / 2; // carry-out
        answer = makeAnswer(answer, s);
        // s를 asnwer에 계속 추가해서 아무튼 새로운 답을 늘려나갈것이다.
    }

    if (c == 1)
    {
        answer = makeAnswer(answer, c);
    }
    cout << answer << endl;
    return answer;
}

int main()
{
    solution("11", "1000");
}

// 이 코드가 확실이 디바이드 먼쿼가 왜 중요한지 나오는 과정이다.
// 아 진짜 써야되는데,,,,, 다 타이핑 하게 되면 내가 무슨일을 하는지 햇갈려진다.
/*
한꺼번에 한 함수에서 구현하게 된다면 실수할 확률이 높아진다.
0. 나 스스로를 따라해라. 내가 하는 행동을 컴퓨터가 하도록 구현하는 것이다.
ex. 2진수 덧셈 하려면 무조건 뒤부터, 긴 숫자를 위에 적고 덧셈을 할것이다. 그럼 그렇게 프로그래밍을 해라.
1. 패턴 반복
2. 블랙박스 만드록 채우기..... ******************* 죨라 중요,,,,
*/
```

**_배운 점_** <br>

0. 나 스스로를 따라해라. 내가 하는 행동을 컴퓨터가 하도록 구현하는 것이다.
   ex. 2진수 덧셈 하려면 무조건 뒤부터, 긴 숫자를 위에 적고 덧셈을 할것이다. 그럼 그렇게 프로그래밍을 해라.
1. 패턴 반복
2. 블랙박스 만드록 채우기..... **\*\*\*\***\*\*\***\*\*\*\*** 죨라 중요,,,,

## 실습 9

### 문제 설명

정수 배열 array와 정수 n이 매개변수로 주어질 때, array에 들어있는 정수 중 n과 가장 가까운 수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

1 ≤ array의 길이 ≤ 100 <br>
1 ≤ array의 원소 ≤ 100 <br>
1 ≤ n ≤ 100 <br>

**_가장 가까운 수가 여러 개일 경우 더 작은 수를 return 합니다._**

### 입출력 예

|    array     |  n  | result |
| :----------: | :-: | :----: |
| [3, 10, 28]  | 20  |   28   |
| [10, 11, 12] | 13  |   12   |

### 내가 제출한 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> array, int n)
{
    int answer = 0;
    vector<int> abs_diff;

    for (int i = 0; i < array.size(); i++)
    {
        int diff = abs(array[i] - n);
        abs_diff.push_back(diff);
    }

    int min_diff = abs_diff[0];
    int min_index = 0;
    for (int i = 1; i < array.size(); i++)
    {
        if ((min_diff >= abs_diff[i]))
        {
            if (min_diff == abs_diff[i])
            {
                min_index = (array[min_index] < array[i]) ? min_index : i;
            }
            else
            {
                min_index = i;
            }
            min_diff = abs_diff[i];
        }
    }

    answer = array[min_index];
    cout << min_index << endl;
    return answer;
}
int main()
{
    solution({3, 10, 17}, 13);
}
```

### 교수님 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int getDiff(int n, int m)
{
    if (n > m)
        return n - m;
    else
        return m - n;
}

int solution(vector<int> array, int n)
{
    int answer = -200;
    for (int i = 0; i < array.size(); i++)
    {
        if ((getDiff(array[i], n) < getDiff(answer, n)) || (getDiff(array[i], n) == getDiff(answer, n) && answer > array[i]))
        {
            answer = array[i];
        }
    }

    return answer;
}
int main()
{
    solution({3, 10, 17}, 13);
}
```

## 실습 10

### 문제 설명

머쓱이는 프로그래머스에 로그인하려고 합니다. 머쓱이가 입력한 아이디와 패스워드가 담긴 배열 id_pw와 회원들의 정보가 담긴 2차원 배열 db가 주어질 때, 다음과 같이 로그인 성공, 실패에 따른 메시지를 return하도록 solution 함수를 완성해주세요. <br>

아이디와 비밀번호가 모두 일치하는 회원정보가 있으면 "login"을 return합니다.
로그인이 실패했을 때 아이디가 일치하는 회원이 없다면 “fail”를, 아이디는 일치하지만 비밀번호가 일치하는 회원이 없다면 “wrong pw”를 return 합니다.

### 제한사항

회원들의 아이디는 문자열입니다. <br>
회원들의 아이디는 알파벳 소문자와 숫자로만 이루어져 있습니다. <br >
회원들의 패스워드는 숫자로 구성된 문자열입니다. <br>
회원들의 비밀번호는 같을 수 있지만 아이디는 같을 수 없습니다. <br>
id_pw의 길이는 2입니다. <br>
id_pw와 db의 원소는 [아이디, 패스워드] 형태입니다. <br>
1 ≤ 아이디의 길이 ≤ 15 <br>
1 ≤ 비밀번호의 길이 ≤ 6 <br>
1 ≤ db의 길이 ≤ 10 <br>
db의 원소의 길이는 2입니다. <br>

### 입출력 예

|           id_pw           |                                       db                                        |   result   |
| :-----------------------: | :-----------------------------------------------------------------------------: | :--------: |
|   ["meosseugi", "1234"]   |          [["rardss", "123"], ["yyoom", "1234"], ["meosseugi", "1234"]]          |  "login"   |
| ["programmer01", "15789"] | [["programmer02", "111111"], ["programmer00", "134"], ["programmer01", "1145"]] | "wrong pw" |
|   ["rabbit04", "98761"]   |      [["jaja11", "98761"], ["krong0313", "29440"], ["rabbit00", "111333"]]      |   "fail"   |

### 내가 제출한 코드

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string solution(vector<string> id_pw, vector<vector<string>> db)
{
    string answer = "";
    cout << id_pw[0] << endl;
    for (int i = 0; i < db.size(); i++)
    {
        cout << i << endl;
        for (int j = 0; j < db[i].size(); j++)
        {
            if (id_pw[0] == db[i][0])
            {
                if (id_pw[1] == db[i][1])
                {
                    answer = "login";
                }
                else
                {
                    answer = "wrong pw";
                }
            }
            else
            {
                answer = "fail";
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

int match(vector<string> id_pw, vector<string> each_db)
{
    if (id_pw[0] == each_db[0])
    {
        if (id_pw[1] == each_db[1])
        {
            return 2;
        }
        else
        {
            return 1;
        }
    }
    else
    {
        return 0;
    }
}
string solution(vector<string> id_pw, vector<vector<string>> db)
{
    string answer = "fail";
    int case_each;

    for (int i = 0; i < db.size(); i++)
    {
        case_each = match(id_pw, db[i]);

        if (case_each == 2)
            return "login";
        else if (case_each == 1)
            return "wrong pw";
        else
            return "fail";
    }
    return answer;
}
```
