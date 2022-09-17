---
title: "[C++] 리스트, 스택, 큐"
excerpt: "리스트, 스택, 큐"
categories: [Algorithm Study]
tags: [Algorithm Study, C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 연속된 자료 구조

- 정적 배열: 스택 메모리 영역에 할당되므로 자동으로 해제된다.
- 동적 배열: 힙 영역에 할당되므로 사용자가 직접 해제하기 전까지 유지된다. <br>

배열 같은 연속된 자료 구조에서 각 원소는 서로 인접해 있기 때문에 하나의 원소에 접근할 때 그 옆에 있는 원소 몇개도 함께 캐시로 가져온다. 이로써 배열의 경우는 더 빠른 작업이 가능하다. 이러한 속성을 캐시 지역성이라고 한다. <br>

따라서 배열의 경우는 연속된 원소에 매우 빠르게 접근할 수 있어서 빠르게 접근할 수 있다는 장점이 있다.

## 연결된 자료 구조

연결 리스트를 생각하면 편할 것 같다. 연결된 자료 구조는 노드라고 하는 여러 개의 메모리 청크에 데이터를 저장하며, 이 경우 서로 다른 메모리 위치에 데이터가 저장된다. <br>

연결 리스트의 경우 i번째 원소에 접근하려면 연결 리스트 내부를 i번 이동하는 작업이 필요하다. 시간 복잡도는 O(n)이 된다. 시간 복잡도는 크기만 그럼에도 연결 리스트는 삽입, 삭제에 굉장히 빠르게 가능하다. 다음 노드를 가리키는 포인트만 수정하면 되기 때문이다. <br>

연결 리스트에서는 원소가 메모리에 연속적으로 저장되지 않기 때문에 캐시 지역성을 기대할 수는 없다. 그러므로 다음 노드를 캐시로 불러올 수는 없다. 따라서 배열과 연결 리스트에서 모든 원소를 차례대로 방문하는 작업은 이론저긍로 같은 시간 복잡도를 가지지만 실제로는 배열이 좀더 빠른 수행이 가능하다.

|        --        |         연속된 자료 구조(배열)         |                   연결된 자료 구조(연결 리스트) 경우                    |
| :--------------: | :------------------------------------: | :---------------------------------------------------------------------: |
|        --        | 모든 데이터가 메모리에 연속적으로 저장 | 데이터는 노드에 저장, 노드들은 메모리 여기저기에 저장(연속X -> 지역성X) |
|        --        | 임의 원소에 즉각적으로 접근할 수 있다. |                 임의 원소에 접근하는 것은 배열보다 느림                 |
|    임의 접근     |                  O(1)                  |                                  O(n)                                   |
| 맨 뒤 원소 삽입  |                  O(1)                  |                                  O(1)                                   |
| 중간에 원소 삽입 |                  O(n)                  |                                  O(1)                                   |

## std::array

std::array는 메모리를 자동으로 할당하고 해제한다. 원소의 타입과 배열의 크기를 매개변수로 사용하는 클래스 템플릿이다.

```cpp
#include <iostream>
#include <array>

std::array<int, 4> arr;
```

식으로 std를 붙혀야 됨!

```cpp
#include <iostream>
#include <array>
using namespace std;

int main()
{
    array<int, 10> arr1;
    arr1[0] = 1;
    cout << "arr1 배열의 첫 번째 원소: " << arr1[0] << endl;

    array<int, 4> arr2 = {1, 2, 3, 4};
    cout << "arr2의 모든 원소: ";

    for (int i = 0; i < arr2.size(); i++)
    {
        cout << arr2[i] << " ";
    }
    cout << endl;
}

>>>
arr1 배열의 첫 번째 원소: 1
arr2의 모든 원소: 1 2 3 4
```

### at(index)

배열 원소에 접근할 수 있는 [] 연산자를 제공한다. [] 연산자에 접근하고자 하는 배열 우너소 인덱스를 지정할 경우, 빠른 동작을 위해 전달된 인덱스 값이 배열의 크기보다 작은지를 검사하지 않는다. -> 그 대신 std::array는 at(index) 형식의 함수도 함께 제공하며, 이 함수는 인자로 전달된 index 값이 유효하지 않으면 std::out_of_range 예외를 발생시킨다. 따라서 at() 함수가 [] 연산자보다는 느린편이지만 at() 함수를 이용해서 예외를 적절하게 처리할 수 있다.

```cpp
#include <iostream>
#include <array>

int main()
{
    std::array<int, 4> arr3 = {1, 2, 3, 4};

    try
    {
        std::cout << arr3.at(3) << std::endl;
        std::cout << arr3.at(4) << std::endl;
    }
    catch (const std::out_of_range &e)
    {
        std::cerr << e.what() << std::endl;
    }
}

>>>
4
array::at: __n (which is 4) >= _Nm (which is 4)
```

배운 점

- <>에서 후자에 있는 숫자는 인덱스 0부터 4개를 만든다는 의미. 즉, 인덱스는 0, 1, 2, 3까지 존재한다. 그러므로 인덱스 4는 out of range
- try catch 처리법

### 배열을 함수 매개변수로 전달

std::array 객체를 다른 함수로 전달하는 방식은 기본 데이터 타입 전달하는 것과 유사하다.

```cpp
#include <iostream>
#include <array>

void printValue(const std::array<int, 5> arr)
{
    std::cout << "printValue" << std::endl;
    for (auto ele : arr)
    {
        std::cout << ele << ", ";
    }
    std::cout << std::endl;
}

// 포인터 활용
void printRef(const std::array<int, 5> *arr)
{
    std::cout << "printRef" << std::endl;
    for (auto ele : *arr)
    {
        std::cout << ele << ", ";
    }
    std::cout << std::endl;
}

// 참조자 활용
void printRef2(const std::array<int, 5> arr)
{
    std::cout << "printRef2" << std::endl;
    for (auto ele : arr)
    {
        std::cout << ele << ", ";
    }
    std::cout << std::endl;
}
int main()
{
    std::array<int, 5> arr = {1, 2, 3, 4, 5};
    printValue(arr);
    printRef(&arr);
    printRef2(arr);
}

>>>
printValue
1, 2, 3, 4, 5,
printRef
1, 2, 3, 4, 5,
printRef2
1, 2, 3, 4, 5,
```

근데 이 예시의 문제점은 만드시 배열의 크기가 같아야 한다는 점이다. 배열의 크기가 다를 경우 매개변수로 전달이 되지 않기 때문이다. 다양한 크기에 맞게 알맞게 출력하는 함수를 만들기 위해서는 print()를 함수 템플릿으로 선언하고, 배열의 크기를 템플릿 매개변수로 전달하면 된다.

### 함수 템플릿

함수의 기능은 덧셈, 리턴값이 int형인 함수

```cpp
int Adder(int n1, int n2)
{
	return n1 + n2;
}
```

이러한 함수의 템플릿은 다음과 같다.

```cpp
template <typename T>
T Adder(T n1, T n2)
{
	return n1 + n2;
}
```

이 함수의 기능은 덧셈이고, 매개변수와 리턴값의 데이터형은 결정되어 있지 않다. <br>

결과적으로는 이런 느낌?

```cpp
#include <iostream>
#include <cstring>

using namespace std;

template <typename T>
T Adder(T n1, T n2)
{
    cout << "템플릿 함수 호출" << endl;
    return n1 + n2;
}

// 템플릿 함수와 비교를 위한 int형 함수
int Adder_int(int n1, int n2)
{
    cout << "int 형 함수 호출" << endl;
    return n1 + n2;
}

int main()
{
    cout << Adder<int>(1, 2) << endl;
    cout << Adder<double>(1.1, 2.2) << endl;
    cout << Adder_int(1.1, 2.2) << endl;

    return 0;
}

>>>
템플릿 함수 호출
3
템플릿 함수 호출
3.3
int 형 함수 호출
3
```

### 다양한 크기를 출력할 수 있는 함수 / begin(), end()

print()를 함수 템플릿으로 선언하고, 배열 크기를 템플릿 매개변수로 전달하면 된다.

```cpp
#include <iostream>
#include <array>

template <size_t N>
void print(const std::array<int, N> &arr)
{
    for (auto ele : arr)
    {
        std::cout << ele << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::array<int, 4> arr1 = {1, 2, 3, 4};
    std::array<int, 10> arr2 = {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'l'};

    print(arr1);
    print(arr2);
}

>>>
1 2 3 4
97 98 99 100 101 102 103 104 105 108
```

❓template 키워드의 기능이 뭘까?
<br>

여튼 위 코드를 보면 반복문을 통해서 값들을 출력을 하는데 이렇게 하다가 배열의 크기보다 인덱스의 크기가 같거나 크다면 에러를 발생시킨다. <br>

atd::array는 begin(), end() 라는 이름의 멤버 함수를 제공하여, 이들 함수는 가장 첫 번째 원소와 가장 마지막 원소의 위치(정확하게는 마지막 원소 다음 위치)를 반환한다. 즉, begin에서 시작해서 증가 연산자 ++ 을 사용해서 begin의 위치를 하나씩 뒤로 미루다가 end와 begin의 값이 같아지면 그 반복문을 종료시키는 형식으로 진행하면 된다. <br>

이 반복자는 std::array, std::vector, std::map, std::set, std::list처럼 반복 가능한 모든 STL 컨테이너에 대해 사용가능.

```cpp
#include <iostream>
#include <array>

template <size_t N>
void print(std::array<int, N> &arr)
{
    for (auto it = arr.begin(); it != arr.end(); it++)
    {
        auto element = (*it);
        std::cout << "it: " << it << " ";
        std::cout << "*it: " << element << std::endl;
    }
    std::cout << std::endl;
}

int main()
{
    std::array<int, 5> arr = {1, 2, 3, 4, 5};
    print(arr);
}

>>>
it: 0x61ff0c *it: 1
it: 0x61ff10 *it: 2
it: 0x61ff14 *it: 3
it: 0x61ff18 *it: 4
it: 0x61ff1c *it: 5
```

참조자로 줬는데 왜 그 값은 주소로 나오지? => begin, end는 해당 값에 대한 주소를 가지고 있다. 그래서 it = arr.begin() 이었으므로 it는 추소로 출력이 된것이고, 증가 연산자도 사용할 수 있었던 것이다. <br>

array에서 []연산자와 at() 함수 외에 std::array에서 원소 접근을 위해 사용할 수 있는 멤버 함수

- front() : 배열의 첫 번째 원소에 대한 참조를 반환
- back() : 배열의 마지막 원소에 대한 참조를 반환
- data() : 배열 객체 내부에서 데이터 메모리 버퍼를 가리키는 포인터를 반환.

```cpp
#include <iostream>
#include <array>

int main()
{
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    std::cout << arr.front() << std::endl;
    std::cout << arr.back() << std::endl;
    std::cout << (arr.data() + 1) << " = " << (*(arr.data() + 1)) << std::endl;
}

>>>
1
5
0x61ff00 = 2
```
