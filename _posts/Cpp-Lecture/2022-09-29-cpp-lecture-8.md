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

## 과제 3-1

### 문제 설명

2차원 좌표 평면에 변이 축과 평행한 직사각형이 있습니다. 직사각형 네 꼭짓점의 좌표 [[x1, y1], [x2, y2], [x3, y3], [x4, y4]]가 담겨있는 배열 dots가 매개변수로 주어질 때, 직사각형의 넓이를 return 하도록 solution 함수를 완성해보세요.

### 제한사항

dots의 길이 = 4 <br>
dots의 원소의 길이 = 2 <br>
-256 < dots[i]의 원소 < 256 <br>
잘못된 입력은 주어지지 않습니다. <br>

### 입출력 예

|                 dots                 | result |
| :----------------------------------: | :----: |
|   [[1, 1], [2, 1], [2, 2], [1, 2]]   |   1    |
| [[-1, -1], [1, 1], [1, -1], [-1, 1]] |   4    |

### 내가 제출한 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int solution(vector<vector<int>> dots)
{
    int answer = 0;
    int start_x = dots[0][0]; // min x
    int start_y = dots[0][1]; // min y
    int end_x = dots[0][0];   // max x
    int end_y = dots[0][1];   // max y
    for (int i = 1; i < dots.size(); i++)
    {
        if (start_x > dots[i][0])
        {
            start_x = dots[i][0];
        }
        if (start_y > dots[i][1])
        {
            start_y = dots[i][1];
        }
        if (end_x < dots[i][0])
        {
            end_x = dots[i][0];
        }
        if (end_y < dots[i][1])
        {
            end_y = dots[i][1];
        }
    }

    int width = end_x - start_x;
    int height = end_y - start_y;
    answer = width * height;

    return answer;
}

int main()
{
    solution({{1, 1}, {2, 1}, {2, 2}, {1, 2}});
}
```

### 교수님 코드

## 과제 3-2

### 문제 설명

문자열 my_string이 매개변수로 주어집니다. my_string은 소문자, 대문자, 자연수로만 구성되어있습니다. my_string안의 자연수들의 합을 return하도록 solution 함수를 완성해주세요.

### 제한사항

1 ≤ my_string의 길이 ≤ 1,000 <br>
1 ≤ my_string 안의 자연수 ≤ 1000 <br>
연속된 수는 하나의 숫자로 간주합니다. <br>
000123과 같이 0이 선행하는 경우는 없습니다. <br>

### 입출력 예

|    my_string    | result |
| :-------------: | :----: |
| "aAb1B2cC34oOp" |   37   |
| "1a2b3c4d123Z"  |  133   |

### 내가 제출한 코드

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int makeInteger(string strNum)
{
    int num = 0;
    for (int i = 0; i < strNum.size(); i++)
    {
        int temp = strNum[i] - '0';
        int multiplier = 1;
        // 자리수 맞추기
        for (int j = 0; j < strNum.size() - i - 1; j++)
        {
            multiplier *= 10;
            cout << "mul: " << multiplier << endl;
        }

        num += temp * multiplier;
        cout << "num: " << num << endl;
    }
    // num = stoi(strNum);

    return num;
}
int solution(string my_string)
{
    int answer = 0;
    string connect = "";

    for (int i = 0; i < my_string.size(); i++)
    {
        if (my_string[i] >= '0' && my_string[i] <= '9') // 현재는 숫자, 다음은 문자인 경우 또는 문자열 마지막인 경우
        {
            connect += my_string[i];
            cout << "connect: " << connect << endl;
        }
        if ((my_string[i] < '0' || my_string[i] > '9') && connect != "")
        {
            answer += makeInteger(connect);
            connect = "";
            cout << answer << endl;
        }
    }

    if (connect != "")
    {
        answer += makeInteger(connect);
    }

    cout << "answer: " << answer << endl;
    return answer;
}

int main()
{
    solution("1a2b3c4d1234");
}
```

### 교수님 코드

## 과제 3-3

문제 설명

제한사항

입출력 예

### 문제 설명

머쓱이는 RPG게임을 하고 있습니다. 게임에는 up, down, left, right 방향키가 있으며 각 키를 누르면 위, 아래, 왼쪽, 오른쪽으로 한 칸씩 이동합니다. 예를 들어 [0,0]에서 up을 누른다면 캐릭터의 좌표는 [0, 1], down을 누른다면 [0, -1], left를 누른다면 [-1, 0], right를 누른다면 [1, 0]입니다. 머쓱이가 입력한 방향키의 배열 keyinput와 맵의 크기 board이 매개변수로 주어집니다. 캐릭터는 항상 [0,0]에서 시작할 때 키 입력이 모두 끝난 뒤에 캐릭터의 좌표 [x, y]를 return하도록 solution 함수를 완성해주세요. <br>

[0, 0]은 board의 정 중앙에 위치합니다. 예를 들어 board의 가로 크기가 9라면 캐릭터는 왼쪽으로 최대 [-4, 0]까지 오른쪽으로 최대 [4, 0]까지 이동할 수 있습니다.

### 제한사항

board은 [가로 크기, 세로 크기] 형태로 주어집니다. <br>
board의 가로 크기와 세로 크기는 홀수입니다. <br>
board의 크기를 벗어난 방향키 입력은 무시합니다. <br>
0 ≤ keyinput의 길이 ≤ 50 <br>
1 ≤ board[0] ≤ 99 <br>
1 ≤ board[1] ≤ 99 <br>
keyinput은 항상 up, down, left, right만 주어집니다. <br>

### 입출력 예

|                 keyinput                  |  board   | result  |
| :---------------------------------------: | :------: | :-----: |
| ["left", "right", "up", "right", "right"] | [10, 10] | [2, 1]  |
| ["down", "down", "down", "down", "down"]  |  [6, 8]  | [0, -4] |

### 내가 제출한 코드

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<string> keyinput, vector<int> board)
{
    vector<int> answer;
    int x = 0;
    int y = 0;
    int max_x = board[0] / 2;
    int min_x = -max_x;
    int max_y = board[1] / 2;
    int min_y = -max_y;
    for (int i = 0; i < keyinput.size(); i++)
    {
        if (x == max_x || x == min_x)
        {
            continue;
        }
        if (y == max_y || y == min_y)
        {
            continue;
        }
        if (keyinput[i] == "left")
        {
            x--;
        }
        if (keyinput[i] == "right")
        {
            x++;
        }
        if (keyinput[i] == "up")
        {
            y++;
        }
        if (keyinput[i] == "down")
        {
            y--;
        }
    }
    answer.push_back(x);
    answer.push_back(y);

    for (auto i : answer)
    {
        cout << i << endl;
    }
    return answer;
}
int main()
{
    solution({"right", "right", "right", "right", "right", "right", "right"}, {10, 10});
}
```

처음에는 이렇게 했었는데, 이렇게 된다면 (5, 0), board (10, 10)인 경우 x는 더이상 오른쪽으로 이동할 수는 없지만 y는 이동이 가능해야된다. 하지만 이럴 경우, x에 의해서 continue가 되기 때문에 몇 가지가 실패가 나왔던 것이다.

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<string> keyinput, vector<int> board)
{
    vector<int> answer;
    int x = 0;
    int y = 0;
    int max_x = board[0] / 2;
    int min_x = -max_x;
    int max_y = board[1] / 2;
    int min_y = -max_y;
    for (int i = 0; i < keyinput.size(); i++)
    {
        if (keyinput[i] == "left" && x > min_x)
        {
            x--;
        }
        if (keyinput[i] == "right" && x < max_x)
        {
            x++;
        }
        if (keyinput[i] == "up" && y < max_y)
        {
            y++;
        }
        if (keyinput[i] == "down" && y > min_y)
        {
            y--;
        }
    }
    answer.push_back(x);
    answer.push_back(y);

    for (auto i : answer)
    {
        cout << i << endl;
    }
    return answer;
}
int main()
{
    solution({"right", "right", "right", "right", "right", "right", "right"}, {10, 10});
}
```

### 교수님 코드
