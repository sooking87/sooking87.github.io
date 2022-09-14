---
title: "2.2주차"
excerpt: "2.2주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 문제 1.

숫자 두 개를 입력받아서 사칙연산 출력하기

```cpp
#include <iostream>
using namespace std;

// 숫자 두개 입력받아서 사칙연산 출력하기

int main()
{
    int val1, val2;
    int largest, smallest;

    cout << "Please enter two integers: ";
    cin >> val1 >> val2;

    // 큰 값과 잡은값 정도는 변수로 저장해놓는 것이 편할 듯 하다.
    largest = (val1 > val2) ? val1 : val2;
    smallest = (val1 > val2) ? val2 : val1;
    cout << "largest: " << largest << endl;
    cout << "smallest: " << smallest << endl;

    cout << largest << " + " << smallest << " = " << (largest + smallest) << endl;
    cout << largest << " - " << smallest << " = " << (largest - smallest) << endl;
    cout << largest << " * " << smallest << " = " << (largest * smallest) << endl;
    cout << largest << " / " << smallest << " = " << (largest / smallest) << endl;

    return 0;
}
```

### 배운 점 1.

```cpp
int val1, val2;
```

이렇게 쓰면 declaration과 definition이 동시에 진행된 것이다. 왜냐하면 int를 통해서 declaration이 진행이 되었고 val1과 val2에 대한 메모리가 자동으로 생성이 되었기 때문이다. 여기서 definition은 변수를 위한 메모리 할당을 받는 것을 말한다.

#### 선언 vs 정의 vs 초기화

- 변수 기준 <br>
  변수의 경우는 선언과 정의가 무조건 동시에 발생한다. 왜냐하면 선언을 하게 되면 그 데이터형만큼의 메모리가 무조건 차지되기 때문에 정의까지 동시에 된다. 초기화의 경우는 `int a = 4;` 와 같이 한 번에 값까지 넣는 것을 말한다.

  - `int a;` : 선언 + 정의까지만
  - `int a = 4;` : 선언 + 정의 + 초기화까쥐

- 함수 기준 <br>

  - `void point(int x, int y);` : 선언 까쥐
  - 함수의 구현부 구현 : 정의 <br>

  함수는 초기화라는 표현은 쓰지 않는다. 그래도 굳이 따지자면 선언이랑 정의까지 한 번에 진행이 된 상태를 초기화라고 할 수는 있을 것 같다.

### 배운 점 2. endl vs \n

타자기 -> 키보드를 만들게 되었다. : 타자기는 잉크가 적셔져 있는 천이 있는데 그 앞에 하얀 종이가 있다. 타자기의 키판을 누르면 키 판에 해당하는 활자가 잉크가 묻어있는 천을 쿵 때린다. 때릴 때, 활자 모양대로 종이에 찍힌다. 쓰다보면 줄바꿈이 필요: 아래로 한줄 내리고 맨 앞으로 종이를 당겨야된다. 즉 x 축이동, y축 이동이 필요 -> 이거를 newline(y축)과 line feed(x축)이라고 한다. 이런 타자기의 특징을 키보드로 옮기는 데 있어서 사람마다 구현함이 다르다. newline(y축 이동) + line feed(x축 이동)을 따로 구현한 사람이 있고 newline이랑 line feed를 한꺼번에 구현한 사람이 있다. 이런 차이는 OS마다의 차이로 이어지게 되었다.

- \n이라는 것은 딱 newline에만 해당이 된다.
- endl이라는 것은 OS에 맞춰서 올바르게 정의가 된다. 필요에 따라서 유동적으로 다음 줄 첫 번째 칸으로 이동할 수 있도록 한다. <br>

따라서 endl을 사용하는 것을 권장한다.

## 문제 2.

숫자 세 개를 입력받아서 값 비교하기

```cpp
#include <iostream>
using namespace std;

// 숫자 세개를 입력받아서 값 비교하기
int main()
{
    int val1, val2, val3;
    int large, middle, small;

    cout << "enter three integers: ";
    cin >> val1 >> val2 >> val3;

    if (val1 > val2 && val1 > val3)
    {
        large = val1;
        if (val2 > val3)
        {
            middle = val2;
            small = val3;
        }
        else
        {
            middle = val3;
            small = val2;
        }
    }
    else if (val2 > val1 && val2 > val3)
    {
        large = val2;
        if (val1 > val3)
        {
            middle = val1;
            small = val3;
        }
        else
        {
            middle = val3;
            small = val1;
        }
    }
    else
    {
        large = val3;
        if (val1 > val2)
        {
            middle = val1;
            small = val2;
        }
        else
        {
            middle = val2;
            small = val1;
        }
    }

    cout << small << ", " << middle << ", " << large << endl;
}
```

## 문제 3.

짝수, 홀수 판단 <br>

출력 형식: The value 4 is an even number

```cpp
#include <iostream>
#include <string>
using namespace std;

// 짝수 홀수 판단
// 출력 형식 : The value 4 is an even number

int main()
{
    int num;
    string cat;
    cin >> num;

    if (num % 2 == 0)
    {
        cat = "even";
    }
    else
    {
        cat = "odd";
    }

    cout << "The value " << num << " is an " << cat << " number." << endl;

    return 0;
}
```

## 문제 4.

5개의 숫자를 문자로 타이핑하면 그 결과를 실제 숫자로 찍어라

```cpp
#include <iostream>
#include <string>
using namespace std;

// 5개의 숫자를 문자로 타이핑 -> 결과에 대해서 실제 숫자를 찍어줘라

int main()
{
    string strNum;
    int ans = -1;
    cin >> strNum;

    // 입력받은 문자를 소문자로 만들기
    for (int i = 0; i < strNum.size(); i++)
    {
        strNum[i] = tolower(strNum[i]);
    }

    // 문자열 비교
    // 다형성 사용됨 == 를 하면 value가 같은지를 비교를 하겠지 그래서 c++에서는 operator overloading에 의해서 값이 같은지를 비교를 해준다.
    if (strNum == "zero")
    {
        ans = 0;
    }
    else if (strNum == "one")
    {
        ans = 1;
    }
    else if (strNum == "two")
    {
        ans = 2;
    }
    else if (strNum == "three")
    {
        ans = 3;
    }
    else if (strNum == "four")
    {
        ans = 4;
    }
    else
    {
        ans = -1;
    }

    // 출력값
    if (ans == -1)
    {
        cout << "Not a valueI know." << endl;
    }
    else
    {
        cout << ans << endl;
    }

    return 0;
}
```

이 문제는 문자열도 switch를 사용할 수 있을까에 대한 질문을 가지고 해봤어야 하는 문제이다. 실제로 string을 기준으로 switch문을 사용하게 된다면 에러가 뜬다. <br>

왜냐하면 switch문은 원시형(int, char 등)과 같은 원시형만 사용이 가능하다. string과 같은 user defined 형은 사용할 수 없다.

## 문제 5.

덧셈 뺄셈 곱셈 나눗셈에 대해서 + 100 3.14 라고 입력을 받았을 때 결과값을 출력해라

```cpp
#include <iostream>
using namespace std;

// 덧셈 뺄셈 곱셈 나눗셈에 대해서 + 100 3.14 라고 입력을 받았을 때 결과값을 출력하자

int main()
{
    char oprt;
    double num1, num2;
    double result = 0;

    cin >> oprt >> num1 >> num2;

    double large, small;
    large = (num1 > num2) ? num1 : num2;
    small = (num1 > num2) ? num2 : num1;

    // char나 int 는 switch 문을 사용할 수 있다.
    switch (oprt)
    {
    case '+':
        result = large + small;
        break;
    case '-':
        result = large - small;
        break;
    case '*':
        result = large * small;
        break;
    case '/':
        result = large / small;
        break;
    default:
        result = 0;
        break;
    }

    cout << "The answer is " << result << endl;
}
```
