---
title: "3.1주차"
excerpt: "3.1주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

📌 chapter 4. Computation

## You already know,,,

이미 이 수업은 대부분의 문법에 대해서 알고 있음을 가정하고 있음. if, for, while, functions.. 등 <br>

structual에서는 function을 잘 사용할 수 있는게 중요하다. function으로 divide & conquer을 한는게 중요하다. <br>

> What i will show you today is mostly just vocabulary and syntax for what you already know.

## Computation

Computation이 뭐야? -> 컴퓨터라는 얘기는 컴퓨트 하는 놈이라는 뜻. 일종의 state 머신.. state 머신이란 A라는 state를 B라는 state로 변경. 이론적인 기반을 현실화 한 것이 컴퓨터이다. 처응메는 수학적 이론에서 출발 -> 발전시키면서 중요한 사람이 튜링, 튜링 머신, state 머신 등 다양한 개념들이 있었음 -> 실제로 돌아가도록 하는 것이 컴퓨터이다. state 머신이 한 예 <br>

3, 1, 2 (현 state) -> state 머신 -> (1, 2, 3) <br>

프로그래밍이라는 것은 state가 RAm에 등장 ramㅇ 존재하는 초기 값을 input, 메모리에 저장되는 값을 output. input state -> 프로그래밍, Computation -> output state <br>

여기서 프로그래밍을 우리가 해야되는데 여기서 중요한 덕목이 있다. <br>

1. correctly(딱 원하는 output으로,,!) -> 이 과정에서 결과를 달성할때가지의 드는 비용(시간과 메모리)을 최소화하고 싶어 한다. / 상대적으로 시간이 좀더 중요하다. (거래 불가대상)
2. correctly까지 가는 과정이 simply & efficiently

> correctly 를 위해서 efficiently하게 접근해야되는데, 그 과정은 simply하게 하면 좋다. <br>

### One tool is called Divide and Conquer

sub task로 쪼개서 문제를 해결해라. 부러뜨리기 위한 전략은 쪼개라. 낱개로 divide하면 divide, conquer하기 쉽다. -> 코드로 어떻게 구현? **_Function_** 각각의 sub task로 나눠서 define -> main에서는 call만 하면 됨.

### Another tool is Abstraction

핸들, 기어, 패달만 신경쓰면되지, 엔진 돌아가는 거 보이고, 기름 지나가는 거 보이고 걍 다보여,,, -> 그럼 매우 당황스럽다. 즉, 필요한것만 보여주고 필요없는거는 보여주지 말자.

### Organization of data is often the key to good code.

## language features

- operator
- if 문 등장 중요 <br>

  1차원 적으로 수행하는 machine. 일열로 수행해야되는 명령어들의 집합 -> if문이 없다면 이 프로그램은 언제나 고정, 결과는 동일 = 표현력이 제한력, 정해져있는 하나의 flow, expression power 제한 <br>

  if의 선택에 따라서 결과가 다르게 나올 수 있다. = expression power가 증가

- while은 라인수를 줄이는 효과, expression power는 별로 상관 X.

- Function은 재활용용, 역시 라인수를 줄어주는 효과, deivide conquer로 문제의 해결을 쉽게 도와줌

## Expression

- binary operator
- unary operator

## statements

semicolon까지가 한 문장.

## Iteration(while loop, for loop)

c시절

```cpp
#include <iostream>

int main()
{
    int i;
    for (i = 0; i < 100; i++)
    {
        printf("%d", i);
    }
    printf("%d", i);
}
```

<br>

c++에서는 괄호안에서 선언 가능하도록 함.

```cpp
#include <iostream>

int main()
{
    // int i;
    for (int i = 0; i < 100; i++)
    {
        printf("%d", i);
    }
    // printf("%d", i); -> scope 종료
}
```

반복 횟수 실수 주의

## functions

기본적으로 선언과 정의가 있다. 선언은 리턴 타입, 매개변수 개수, 매개변수의 리턴 타입을 결정하는 것이다.

```cpp
#include <iostream>

int main()
{
    myfunc();
}

void myfunc()
{
    std::cout << "my" << std::endl;
}
```

컴파일러 에러 발생: 위에서 아래로 읽음로 없는 함수가 됨.
<br>

sol 1.

```cpp
#include <iostream>

void myfunc()
{
    std::cout << "my" << std::endl;
}

int main()
{
    myfunc();
}
```

<br>

sol 2.

```cpp
#include <iostream>

// 선언
void myfunc();

int main()
{
    myfunc();
}

// 선언 + 정의
void myfunc()
{
    std::cout << "my" << std::endl;
}
```

<br>

❗

```cpp
#include <iostream>

// 선언 -> 중복이 되어도 문제가 없어.
void myfunc();
void myfunc();

int main()
{
    myfunc();
}

// 선언 + 정의
void myfunc()
{
    std::cout << "my" << std::endl;
}
```

여기까지가 C의 문법 <br>

C++에서 확장된 문법 <br>

```cpp
#include <iostream>

// 선언 + 정의
void myfunc()
{
    std::cout << "my" << std::endl;
}

void myfunc(int a)
{
    std::cout << a << std::endl;
}

int main()
{
    myfunc();
    myfunc(5);
}
```

`void myfunc()` , `void myfunc(int a)` 는 다른 함수로 취급. 파라미터로 구별을 할 수 있으면 중복을 허용해주자! = 폴리모피즘. <br>

함수명 + 매개변수 개수/데이터형만 검사 -> 리턴형만 다르다고 다른 함수가 아니다. <br>

이 정도도 가능. 매개변수 개수가 같은데 데이터형만 다른 경우.

```cpp
#include <iostream>

// 선언 + 정의
void myfunc();
void myfunc(int a);
void myfunc(double a);

int main()
{
    myfunc();
    myfunc(5);
    myfunc(5.5);
}

void myfunc()
{
    std::cout << "my" << std::endl;
}

void myfunc(int a)
{
    std::cout << a << std::endl;
}

void myfunc(double a)
{
    std::cout << a << std::endl;
}

>>>
my
5
5.5
```

### 장점

1. 코드의 재사용 / 효율성
2. control flow clear => 언제가 함수쪽으로 갔다가 다시 돌아옴.
3. divide & conquer 가능 🌟🌟🌟

## vector

- array:

  - 장: 연속된 메모리
  - 단: 연속된 공간을 미리확보하는 거라서 메모리 할당량이 제한되어있다. = 확장성이 없다 / 삽입, 삭제가 어렵다.

- linked list:
  - 장: flexable, 삽입 / 삭제가 쉽다. = 딱 필요한 만큼만 메모리 사용.
  - 단: direct 접근 불가. <br>

<br>

둘의 장점을 섞을 수 없을까? <br>

그 희망사항때문에 태어난 게 Vector이다. random access 가능, space에 대한 효율성도 보장. 기본적으로 array인데, 더블링을 하는 array = 두배씩 늘린다. <br>

1개 배열 -> 하나 와 -> 2개 배열 / 첫 번째 배열 복사 + 추가된 값 -> 하나 추가 -> 4개짜리 배열 / 첫 번째, 두 번째 값 복사 + 추가된 값 -> ...

❓ 근데 추가 삭제는 어떻게 해결? 배열은 추가 삭제가 유동적이지 않고 비효율적이잖아.. <br>

A: => 근데 이 문제는 그냥 배열의 형식 그대로 진행된다. 추가/삭제에 대해서는 비효율이지만 direct 접근과 필요한 만큼만에 대한 메모리 유동 추가에 대한 장점은 가진다.
