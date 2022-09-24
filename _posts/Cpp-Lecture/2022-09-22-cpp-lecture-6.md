---
title: "4.1주차"
excerpt: "4.1주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 과제 리뷰

🌟 개중요 : divide & conquer

### 과제 3

문자열 2개가 주어지는데 첫 번째 인자에서 몇 번 돌아가야 두 번째 인자와 같은 문자열을 가지게 되는지 구하는 문제이다. 다만 아무리 돌려도 같은 문자열이 나오지 않는 경우는 -1을 리턴한다.

```cpp
#include <vector>
#include <string>

using namespace std;

bool isSame(string A, string B, int shift)
{
    for (int i = 0; i < A.length(); i++)
    {
        // 인덱스가 넘치는 것을 해결해주기 위해서 (i + shift) % A.length()로 해주면 된다.
        if (A[i] != B[(i + shift) % B.length()])
        {
            return false;
        }
    }
    return true;
}

int solution(string A, string B)
{
    for (int answer = 0; A.length() == B.length() && answer < A.length(); answer++) // A와 B의 길이가 같음을 전제로 함.
    {
        // isSame을 answer 번 밀었을 떼, A와 B를 비교한다.
        // 5분뒤의 나를 믿고 일다 ㄴisSame의 동작 결과까지 생각을 하고 solution 함수를 구현하다. -> 이렇게 구현을 했다면 isSame을 구현해주면 된다.
        if (isSame(A, B, answer))
            return answer;
    }
    return -1;
}
// 이번 강의에서 제일 보여주고 싶은것은 devide & conquer -> 그 함수/isSame가 정상적으로 돌아갈 것이라는 가정하에, 함수/isSame를 만들어서 문제를 해결한다.
// devide & conquer를 해놓았기 때문에 디버깅도 빨리진다.
int main()
{
    int ans = solution("hello", "ohell");
}
```

**_반드시 알아야 되는 점_** <br>

1. 코딩을 하려면 무조건 devide & conquer 방식으로 진행해야 된다.
   위의 코드를 예로 들자면 먼저 solution 함수를 코딩할 때, 몇 번 밀었을 때 같아지는지를 출력할 함수 isSame의 리턴값을 예상해서 코딩을 한다. 아직 isSame이 구체적으로 어떤 역할을 할지는 코딩하지 않았지만 몇 번 돌려서 B와 문자열이 같아졌는지를 리턴하는 함수라는 것을 예상해서 코딩을 한다. <br>

   그런 다음 isSame 함수를 코딩을 한다. isSame 함수는 B의 인덱스를 shift해서 A와 같은지 다른지를 비교를 통해서 리턴하는 형태의 함수를 만들어주면 된다.

2. 인덱스가 넘치는 것을 해결해주기 위해서 (i + shift) % A.length()로 해주면 된다. (뭔가 맨 뒤에서 앞으로 돌아가야되는 구조인 경우)

## 문제 4

입력받은 문자가 제곱인지 아닌지

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int getAnswer(double sqrt_n)
{
    double temp = sqrt_n - int(sqrt_n);
    if (temp > 0)
    {
        return 2;
    }
    else
    {
        return 1;
    }
}
int solution(int n)
{
    int answer = 0;
    double sqrt_n = sqrt(n);

    answer = getAnswer(sqrt_n);
    cout << answer << endl;
    return answer;
}

int main()
{
    solution(976);
}
```

결국 나는 sqrt를 사용했지만 교수님의 의도는 직접 반복문을 통해서 제곱을 시키면서 이게 제곱수인지 아닌지를 판단해보라는 의도

## 문제 5

개수와 이 개수만큼 합했을 때 나와야 되는 값이 입력된다. 예: 3, 12 -> (3, 4, 5) <br>

그래서 출력값은 3, 4, 5가 되어야 한다.

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int getStartNum(int num, int total)
{
    // startNum이 음수도 가능하다 따라서 -1000부터 1000까지의 범위 중에서 num 개 만큼 더해가면서 getTotal이 total과 같은 경우 시작 숫자를 리턴한다.
    for (int startNum = -1000; startNum <= 1000; startNum++)
    {
        int getTotal = 0;
        for (int i = startNum; i < startNum + num; i++)
        {
            cout << "i: " << i << endl;
            getTotal += i;
            cout << "getTotal: " << getTotal << endl;
        }
        if (getTotal == total)
        {
            return startNum;
        }
    }
}
vector<int> solution(int num, int total)
{
    vector<int> answer;
    int startNum = getStartNum(num, total);
    cout << "StartNum: " << startNum << endl;

    for (int i = startNum; i < startNum + num; i++)
    {
        answer.push_back(i);
    }

    for (auto i : answer)
    {
        cout << i << " ";
    }
    return answer;
}

int main()
{
    solution(5, 15);
}
```

나는 getStartNum이라는 함수를 통해서 시작 숫자를 구했다. 근데 여기서 문제가 출력 가능 범위가 따로 정해지지 않았으므로 음수도 가능하다는 말이다. 그렇기 때문에 -1000부터 1000까지의 범위 중에서 num 개 만큼 더해가면서 getTotal이 total과 같은 경우 시작 숫자를 리턴한다. (두 번째 입력값 범위가 0부터 1000까지 였으므로)

```cpp
// 교수님 풀이
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int sum(int i, int num)
{
    int total = 0;
    for (int j = 0; j < num; j++)
    {
        total += i + j;
    }
    return total;
}
vector<int> solution(int num, int total)
{
    vector<int> answer;
    for (int i = -1000; i <= 1000; i++)
    {
        if (sum(i, num) == total)
        {
            for (int j = 0; j < num; j++)
            {
                answer.push_back(j + i);
            }
            return answer;
        }
    }
}
```
