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

2.
