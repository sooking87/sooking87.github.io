---
title: "2.1주차"
excerpt: "2.1주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

📌 Chapter 3. Objects, types, and values

## Input and Output

```cpp
#include <iostream>
#include <string>
using namespace std;
// 원래의 full name: std::cout , std::cin 그래야 애매함이 없어짐.

// c시절 코딩
int main()
{
    char first_name[100];
    printf("Please enter your first name (followed ");
    printf("by 'enter'):\n");
    scanf("%s", first_name);

    printf("Hello %s\n", first_name);
}

// cpp 코딩
// 이 방법이 직관적이고 편리하다.
int main()
{
    cout << "Please enter your first name (followed "
         << "by 'enter'):\n";
    string first_name;
    cin >> first_name;
    cout << "Hello, " << first_name << "\n";
}
// include 없이 컴파일하게 되려면
```

- standard input: 키보드를 이용한 input
- standard output: cmd 창으로 실행이 되는 output
- namespace 개념: 다음 소단원에서 설명 예정

### namespace 개념

namespcae는 _폴리모피즘_ 을 구현하기 위한 수단이다. c의 경우는 함수 이름이 같으면 안된다. 이름이 고유해야 구별이 가능하기 때문이다. 하지만 이 경우는 컴파일러는 편하지만 user(사용자)는 함수 이름이 점점 길어지고 같은 기능을 하는 함수더라도 조금씩 다른 이름을 가져서 너무 복잡해질 것이다. <br>

C++에서는 OOP의 개념을 도입한 만큼 누군가 만들어둔 소스코드를 재사용할 수 있어야 된다. 그래서 비슷한 역할을 하는 함수의 경우는 같은 이름을 사용하여 조금씩 다른 기능을 할 수 있도록 하였다. <br>

예를 들어서 "탄다" -> (자전거를), (기차를), (속이), (장작이) -> 목적어에 따라 조금씩 다른 뜻이지만 결국 탄다라는 의미에서 파생된 의미들이다. 그래서 **_다형성_** 을 도입하여서 비슷한 역할의 함수 이름을 모두 통일 시켰다. 하지만 그럼에도 애매함이 완전히 사라지지 않았으므로 namespace 라는 개념을 가지고 온 것이다. 즉, 그냥 cout 했으면 앞에 default로 std를 붙혀서 찾아라 라는 의미! <br>

❓다형성?

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person
{
private:
    int age;
    string name;

public:
    Person(int a, string n) : age(a), name(n)
    {
    }
    void showName() const
    {
        cout << "Hi My name is " << name << ".  ";
    }
    void showAge() const
    {
        cout << "I am " << age << " years old. " << endl;
    }
    void showInfo() const
    {
        showName();
        showAge();
    }
};

class Student : public Person
{
private:
    int score;

public:
    Student(int a, string n, int s) : Person(a, n), score(s)
    {
    }
    // Overwriting
    void showInfo() const
    {
        showName();
        showAge();
        cout << "My score is " << score << ". " << endl
             << endl;
    }
};

class Professor : public Person
{
private:
    int classNum;

public:
    Professor(int a, string s, int cn) : Person(a, s), classNum(cn)
    {
    }
    // overwrite
    void showInfo() const
    {
        showName();
        showAge();
        cout << "My ClassNum is " << classNum << "." << endl
             << endl;
    }
};

int main()
{
    Person p1 = Person(22, "Sohn");
    p1.showInfo();
    >>> Hi My name is Sohn.  I am 22 years old.

    p1 = Student(21, "Choi", 90);
    p1.showInfo();
    >>> Hi My name is Choi.  I am 21 years old.

    p1 = Professor(40, "Chul", 01);
    p1.showInfo();
    >>> Hi My name is Chul.  I am 40 years old.

    Student s1 = Student(30, "Kim", 70);
    s1.showInfo();
    >>> Hi My name is Kim.  I am 30 years old.
        My score is 70.

    Professor pro1 = Professor(50, "Yeon", 02);
    pro1.showInfo();
    >>> Hi My name is Yeon.  I am 50 years old.
        My ClassNum is 2.
}
```

### ❓ Person 형을 가지고 Person, Student, Professor 인스턴스를 모두 가질 수 있는게 다형성 아니였나?

C++에서의 다형성이란 **가상 함수** , **함수 템플릿** , **함수 오버로드** , **연산자 오버로드** 가 있다. 다형 -> 형태가 다양하다라는 의미를 가지고 있는데, 오버 로드의 경우 같은 이름을 가지고 있지만 다른 기능을 함으로써 서로 다른 형태를 가지고 있다고 할 수 있다. 가상 함수의 경우는 클래스마다 같은 이름의 다른 역할을 할 수 있는 함수들이 있다. 자바에서는 오버라이딩이라고 배웠다. 여기서는 오버라이딩의 기능을 하기 위해서는 virtual이라는 키워드가 필요한 것 같다. 여튼 virtual을 사용한 함수를 가상 함수라고 하는데, 이를 사용하게 되면 클래스 별로 같은 이름의 다른 기능을 하는 함수를 만들 수 있다. <br>

같은 OOP라도 이름이 서로 다를 수 있다. 하지만 내가 이해했던 저 방식으로는 정의하지 않는다. 머리에 박아! 자바의 경우는 다형성을 오버라이딩과 오버 로딩을 통해서 구현하였고, C++의 경우는 다형성을 가상 함수, 템플릿, 오버 로딩을 통해서 구현하였다. 함수들끼리 같은 이름의 _다른 형태를_ 가지고 있는 것을 **_다형성_** 이라고 한다.

### 컴파일러

1. user가 직접 선언
2. 헤더 파일을 가져오기 <br>

둘 중 하나를 하는 경우 컴파일러는 선언이 되었다고 판단을 한다. 여기서 헤더파일이란 라이브러리가 default로 제공해주는 선언을 헤더파일이라고 한다. `#include = declaration`

### # 의 의미

전처리기가 컴파일러엑 코드를 주기 전에 처리한다. #include, #define 모두 pre processing에 해당! #이 붙으면 컴파일러에게 input을 주기 전에 istream의 전체 내용을 replace가 되서 컴파일이 시작된다. 그래서 #include, #define 코드는 컴파일러는 볼리가 없다.

## String input

```cpp
#include <iostream>
using namespace std;

int main()
{
    string first, second;

    cout << "Please enter your first and second names" << endl;
    cin >> first >> second;
    string name = first + ' ' + second;

    cout << "Hello, " << name << endl;
}

>>>
Please enter your first and second names
Sohn SooKyoung
Hello, Sohn SooKyoung
```

1. C와 달리 입력받을 때 &를 사용하지 않았다. 왜? <br>

```cpp
cin >> first >> second;
```

C와의 가장 큰 차이점 **call by reference** !! <br>

- call by value <br>

  교도소 면회 -> 서로 간의 물질 교환을 못하게 유리로 막아놓음 서로 물건을 못 주고 받아 = call by value -> 서로 물건을 주고받지 못하기 때문에 값을 복사해야 전달 가능! -> 두목이 어디가서 뭘 찾아오라고 전달을 할때 주소를 빼껴 적어야돼. 그 적힌 종이를 주고받을 수 없으니까 -> 그래서 value를 복사할 수 밖에 없어. 종이는 다르지만 값은 같아 이거시 **_CALL BY VALUE_** <br>

  C언어는 문법적으로 Call by ref를 지원하지 않아. 안정성을 위해서 value만 지원해 <br>

  call by value 만 지원하면 <br>

  - 장점: 데이터의 안정성 확보. 내 데이터는 값을 수정할 수 없어
  - 단점: 효율성이 떨어짐. 하나하나 다 복사해야되니까 <br>

  그래서 이를 타개하기 위해서 C는 포인터라는 개념을 동비한다. 값을 복사하긴 복사하는데 주소를 복사하는 방식! 결론적으로는 주소라는 value를 지원하지만 주소를 복사하였으므로 ref와 같은 역할을 한다.

- call by reference <br>

  적힌 종이를 전달하는 방식 -> 물리적으로는 저장 공간 자체를 share

  - 장점: 효율성
  - 단점: 데이터의 안정성이 보장되지 않음 <br>

  CPP는 call by value랑 call by ref 둘다 지원한다. 그렇기 때문에 굳이 주소를 전달해줄 필요가 없이 ref로 바로 전달이 가능하므로 c와 달리 값을 입력받을 때 굳이 &를 사용할 필요가 없다.

2. +, == 등 폴리모피즘을 확인할 수 있다. <br>

```cpp
string name = first + ' ' + second;
```

C에서는 +가 sum으로만 사용된다. 어떤 형태든 숫자형 데이터에만 사용이 가능하다. char 같은 경우는 사용할 수 없다(의도한대로). 하지만 C++ dptjsms +가 str에 사용된다면 문자(열) 끼리 붙히는 기능을 제공한다. 이를 폴리모피즘이라고 할 수 있는데 왜냐면 함수로 생각을 해봤을 때 +라면 sum이라는 기능을 한다. 하지만 그 매개변수가 int, double 형이라면 두개를 덧셈을 하면 되는거고, char, string 형이라면 그 두개를 붙히면되는 것이다. 즉, function에 대해서 다형성을 지원하였고, +와 ==과 같은 기능 역시 **오버레이터 오버로딩** 이라고 할 수 있다. 이는 C++의 고유 기능이다. (물론 파이썬도,, 가능!)

> 폴리모피즘 철학: 저마다의 이름을 외우게 하지 말자. 귀찮다 <br>

## const 사용

함수나 변수에 const를 굳이 사용하지 않아도 된다. 그럼에도 프로그래머가 실수를 최소화하기 위해서는 값이 변경되지 않는 변수나 함수에서는 const를 붙혀서 실수를 최소화하는 것이 좋다.

## Type safety

정적인 type safety를 추구하여 어느 정도 관용은 배품

- static type safety: 한번 부여된 type은 계속 그 타입이어야 된다. 데이터형을 동해서 declaration된다면 그 데이터형에 대한 맡는 용량의 집을 제공해준다. 그 집은 죽을 때까지 사용해야되는 집이다. <br>

  c++의 경우는 완벽하게 체크를 하지 않는다. 예를 들어서 i == 1.0인지 아닌지를 체크할 때, i가 int 형이더라도 T를 내는 정도

- dynamic type safety: 파이썬은 인터프리터 언어이므로 해당 줄에 쓰임을 보고 타입을 결정해준다. 즉, 라인에 따라서 자유자재로 변경가능하다. 여기서는 내 집이라는 개념이 없고 약간 에어비엔비같은 개념이다. 4byte야? 그럼 4byte에 맞는 집 예약해, 8byte야? 그럼 8byte에 맞는 집을 예약해 이런 방식. 항상 새로운 집(메모리 공간)을 사용한다. 타입이 자유롭게 변동이 가능하다.
