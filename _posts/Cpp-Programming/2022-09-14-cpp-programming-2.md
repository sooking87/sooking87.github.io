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

1. C와 달리 입력받을 때 &를 사용하지 않았다. 왜?

2.
