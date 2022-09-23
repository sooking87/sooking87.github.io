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

## std::vector

std::array의 경우는 크기가 고정되어있어야 하고, 메모리 할당 방법을 변경할 수 없다. 하지만 대부분의 실제 응용 프로그램에서는 데이터는 동적이며 고정 크기가 아니다. 따라서 std::array를 사용하는 것이 항상 좋은 것은 아니며, 가변 크기의 데이터를 처리할 수 있는 컨테이너가 필요하기도 하다.

### std::vector - 가변 크기 배열

```cpp
#include <iostream>
#include <vector>

int main()
{
    // 크기가 0인 벡터 선언
    std::vector<int> vec1;

    // 지정한 초깃값으로 이루어진 크기가 5인 벡터 선언
    std::vector<int> vec2 = {1, 2, 3, 4, 5};

    // 크기가 10인 벡터 선언
    std::vector<int> vec3(10);

    // 크기가 10이고, 모든 원소가 5로 초기화된 벡터 선언
    std::vector<int> vec4(10, 5);
}
```

벡터의 크기를 명시적으로 지정하지 않거나 또는 초깃값을 지정하여 크기를 유추할 수 있게 코드를 작성하지 않을 경우, 컴파일러 구현 방법에 따른 용량을 갖는 벡터를 생성하게 된다.

### push_back() && insert()

백터의 새로운 원소를 추가하려면 push_back() 또는 insert() 함수를 사용한다.

- push_back() 함수는 벡터의 맨 마지막에 새로운 원소를 추가하는 함수
- insert() 함수는 삽입할 위치를 나타내는 반복자를 첫 번째 인자로 받음으로써 원하는 위치에 원소를 추가할 수 있다. <br>

용량이 부족하다면 벡터 용량의 두배로 늘린다. push_back() 함수의 평균 시간 복잡도는 O(1)에 가깝다. 즉, push_back()은 매우 빠르게 동작한다. <br>

insert() 함수의 경우는 지정한 반복자 위치 다음의 모든 원소를 이동시키는 연산이 필요하다. 원소들을 이동하는 연산 때문에 insert() 함수는 O(n)의 시간이 걸립니다.
<br>

push_back() 함수와 insert() 함수의 활용 예시

```cpp
#include <iostream>  // std::cout
#include <vector>    // std::vector
#include <algorithm> // std::find

void print(std::vector<int> v)
{
    for (auto ele : v)
    {
        std::cout << ele << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::vector<int> vec1 = {1, 2, 3, 4, 5};
    std::cout << "vec1 초기값: ";
    print(vec1);

    vec1.insert(vec1.begin(), 0);
    std::cout << "vec1 제일 앞에 0추가: ";
    print(vec1);

    vec1.insert(++vec1.begin(), 10);
    std::cout << "vec1 인덱스 1에 10추가: ";
    print(vec1);

    std::vector<int> vec2;
    vec2.push_back(1);
    std::cout << "vec2 빈 벡터에 1추가: ";
    print(vec2);

    vec2.push_back(2);
    std::cout << "vec2 맨 뒤에 2추가: ";
    print(vec2);

    vec2.insert(vec2.begin(), 3);
    std::cout << "vec2 맨 앞에 3추가: ";
    print(vec2);

    vec2.insert(find(vec2.begin(), vec2.end(), 1), 4); // 1앞에 4를 추가
    std::cout << "vec2 1앞에 4를 추가: ";
    print(vec2);
}

>>>
vec1 초기값: 1 2 3 4 5
vec1 제일 앞에 0추가: 0 1 2 3 4 5
vec1 인덱스 1에 10추가: 0 10 1 2 3 4 5
vec2 빈 벡터에 1추가: 1
vec2 맨 뒤에 2추가: 1 2
vec2 맨 앞에 3추가: 3 1 2
vec2 1앞에 4를 추가: 3 4 1 2
```

- begin() 함수를 통해서 첫 번째에 값을 넣을 수 있다. 즉, 첫 번째 인자의 형식은 주소이다. <br>

  ```cpp
  vec1.insert(vec1.begin(), 0);
  ```

- 주소이므로 증감 연산자를 통해서 두 번째 인덱스에 값을 넣을 수 있다. <br>

  ```cpp
  vec1.insert(++vec1.begin(), 10);
  ```

- find(start, end, value) 로, algorithm 라이브러리에 포함되어 있으며 start부터 end - 1까지 중에서 value를 검색한다. => 첫 번째에 위치하는 value의 값을 찾으면 벡터의 이터레이터를 리턴한다. <br>

  ```cpp
  vec2.insert(find(vec2.begin(), vec2.end(), 1), 4); // 1앞에 4를 추가
  ```

### emplace_back() && emplace()

근데 여기서 push\*back() 함수와 insert() 함수의 단점 중 하나는 이들 함수가 추가할 원소를 먼저 임시로 생성한 후, 벡터 버퍼 내부 위치로 복사 또는 이동을 수행한다는 점이다. 이러한 단점을 보안하기 위해서 \*\*\_emplace*back()**\* 또는 **\_emplace()*\*\* 함수가 구현되어 있다. 따라서 삽입의 경우는 emplace_back()이나 emplace()를 이용하여 구현하는 것이 좋다. <br>

emplace() 함수의 첫 번째 인수는 객체가 생성될 위치를 지정하는 반복자이다. 반복자로 지정한 원소 앞에 객체가 삽입될 것이다. emplace_back() 함수의 경우는 push_back()과 마찬가지고 맨 뒤에 값을 추가하는 함수이다.

```cpp
#include <iostream>
#include <vector>

void print(std::vector<int> v)
{
    for (auto ele : v)
    {
        std::cout << ele << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::vector<int> vec = {1, 2, 3, 4, 5};
    print(vec);

    vec.emplace_back(10);
    print(vec);

    vec.emplace(++vec.begin(), 20);
    print(vec);
}

>>>
1 2 3 4 5
1 2 3 4 5 10
1 20 2 3 4 5 10
```

### pop_back() && erase()

pop_back() 함수는 백터에서 맨 마지막 원소를 제거하며, 그 결과 벡터 크기는 1만큼 줄어든다. erase() 함수는 두가지 형태로 오버로딩되어 있다. 한가지 형태는 반복자 하나를 인자로 받아 해당 위치 원소를 제거하고 다른 형태는 범위의 시작과 끝을 나타내는 반복자를 받아 시작부터 끝 바로 앞 원소까지 제거한다. <br>

- pop_back() : 남아있는 위치를 조정할 필요가 없으므로 매우 빠르게 동작 -> O(1)
- erase() : 특정 위치 원소를 삭제한 후, 뒤쪽의 원소들을 모두 앞으로 이동 -> O(n)

```cpp
#include <iostream>
#include <vector>

void print(std::vector<int> v)
{
    for (auto ele : v)
    {
        std::cout << ele << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::vector<int> vec = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};

    // 맨 마지막 원소 하나를 제거합니다.
    vec.pop_back();
    std::cout << "pop_back(): ";
    print(vec);

    // 맨 처음 원소를 제거
    vec.erase(vec.begin());
    std::cout << "erase(): ";
    print(vec);

    vec.erase(vec.begin() + 2, vec.begin() + 4);
    std::cout << "2번째 인덱스부터 3번째 인덱스 까지 삭제: ";
    print(vec);
}

>>>
pop_back(): 0 1 2 3 4 5 6 7 8
erase(): 1 2 3 4 5 6 7 8
2번째 인덱스부터 3번째 인덱스 까지 삭제: 1 2 5 6 7 8
```

<br>

그 외의 함수 <br>

- clear(): 모든 원소를 제거하여 완전히 비어있는 벡터로 만듬
- reserve(capacity): 벡터에서 사용할 용량을 지정매개변수로 지정한 값이 현재 용량보다 크면 메모리를 매개변수 크기만큼 재할당
- shrink_to_fit(): 여부느이 메모리 공간을 해제하는 용도로 사용. 이 함수를 호출하면 벡터의 용량이 벡터 크기와 같게 설정된다.

### std::vector 할당자

사용자 정의 할당자를 사용하려면 정해진 인터페이스를 따라야 한다. 벡터는 메모리 접근과 관련된 대부분의 동작에서 할당자 함수를 사용하므로 할당자는 allocate(), deallocate(), construct(), destroy()등의 함수를 제공한다. 이런 기능을 통해서 std::array()의 단점을 해결할 수 있다. 할당자는 메모리 할당과 해제, 여타 동작에서 데이터를 손상시키지 않도록 주의해야 된다. <br>

일반적인 힙 메모리 대신 자체적인 메모리 풀 또는 이와 유사한 자원을 사용하거나 자동 메모리 관리가 필요한 응용 프로그램을 만들어야 하는 경웅에 사용자 정의 할당자를 사용한 유용하다.

### ❓할당자, 이터레이터, 사용자 정의 할당자?

1. 이터레이터 = 반복자 <br>

   c++에서는 반복자를 제공하는데, 이를 사용하면 컨테이너에 저장된 원소를 순회하고 접근하여 효과적으로 자료를 접근할 수 있다. vector 컨테이너에 접근하기 위해서는 iterator(반복자) 개념이 필요하다. iterator는 컨테이너 원소에 접근할 수 있는 포인터와 같은 객체라고 볼 수 있다. 벡터 컨테이너에 접근하기 위해서는 \* 연산자를 사용해서 접근한다.

   ```cpp
   #include <iostream>
   #include <vector>

   int main()
   {
       // vector 반복자 iter 선언
       std::vector<int>::iterator iter;

       // iter 초기화
       std::vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
       iter = v.begin();

       // 임의 접근
       std::cout << iter[1] << std::endl;

       // 연산 사용
       iter += 5; // 첫 번째 원소 이후로 5칸 뒤의 원소
       std::cout << *iter << std::endl;

       // vector 순방향
       for (std::vector<int>::iterator it = v.begin(); it != v.end(); it++)
       {
           std::cout << "&it: " << &it << std::endl;
           std::cout << "*it: " << *it << std::endl;
       }

       for (std::vector<int>::size_type i = 0; i < v.size(); i++)
       {
           std::cout << "vec의 " << i + 1 << " 번째 원소 :: " << v[i] << std::endl;
       }
       std::cout << std::endl;

       for (int i = 0; i < v.size(); i++)
       {
           std::cout << "vec의 " << i + 1 << " 번째 원소 :: " << v[i] << std::endl;
       }
   }

   >>>
    2
    6
    &it: 0x61fedc
    *it: 1
    &it: 0x61fedc
    *it: 2
    &it: 0x61fedc
    *it: 3
    &it: 0x61fedc
    *it: 4
    &it: 0x61fedc
    *it: 5
    &it: 0x61fedc
    *it: 6
    &it: 0x61fedc
    *it: 7
    &it: 0x61fedc
    *it: 8
    &it: 0x61fedc
    *it: 9
    &it: 0x61fedc
    *it: 10
    vec의 1 번째 원소 :: 1
    vec의 2 번째 원소 :: 2
    vec의 3 번째 원소 :: 3
    vec의 4 번째 원소 :: 4
    vec의 5 번째 원소 :: 5
    vec의 6 번째 원소 :: 6
    vec의 7 번째 원소 :: 7
    vec의 8 번째 원소 :: 8
    vec의 9 번째 원소 :: 9
    vec의 10 번째 원소 :: 10

    vec의 1 번째 원소 :: 1
    vec의 2 번째 원소 :: 2
    vec의 3 번째 원소 :: 3
    vec의 4 번째 원소 :: 4
    vec의 5 번째 원소 :: 5
    vec의 6 번째 원소 :: 6
    vec의 7 번째 원소 :: 7
    vec의 8 번째 원소 :: 8
    vec의 9 번째 원소 :: 9
    vec의 10 번째 원소 :: 10
   ```

   \* 연산자를 이용해서 it이 가리키는 원소를 볼 수 있다. 이터레이터는 실제 포인터가 아니고, \* 연산자를 오버로딩해서 마치 포인터처럼 동작하게 만든 것이다. 위의 예시 코드를 보면 결국 인덱스를 통해서 벡터에 접근을 할 수 있다. 하지만 그렇게 하는 것은 옳지 않다. 벡터의 경우는 원소 접근하는 방식이 iterator을 사용하여 접근하는 방식인데, 이를 사용하지 않고, 배열처럼 정수형 변수 i로 접근하는 것은 권장하지 않은 방식이다.

2. 할당자

## std::forward_list

지금까지 살펴본 배열과 백터 같은 연속된 자료 구조에서는 데이터 중간에 자료를 추가하거나 삭제하는 작업이 매우 비효율적이다. 그래서 연결 리스트와 같은 자료 구조가 등장한다. <br>

기본적인 연결 리스트를 구성하려면 포인터를 하나 가지고 있어야 하고, new와 delete 연산자를 이용하여 메모리를 할당하고 해제할 수 있어야 한다. C++에서는 기본적인 연결 리스트에 대한 **래퍼 클래스** 인 std::forward_list 클래스를 제공한다.

### ❓wrapper 클래스

wrapper란 필요한 데이터를 받거나 쓰기 위해 데ㅣ터 형태를 세팅해 제공하는 서비스이다.

```cpp
#include <iostream>

class int_wrapper
{
private:
    int *myPtr;

public:
    int_wrapper(int value = 0) : myPtr(new int(value))
    {
    }
    ~int_wrapper()
    {
        delete myPtr;
    }
};
```

위 클래스는 int에 대한 포인터를 래핑한다. <br>

자바에서는 int를 Integer로, char을 Character 표현한 경우에서 Integer와 Character을 래퍼 클래스, int를 원시 타입이라고 불렀다. <br>

wrapper 클래스를 사용하는 이유는 모든 데이터 타입 역시 객체로 만들기 위해서 기본 자료형에 대해 객체로서 인식되도록 포장을 하여 wrapper 클래스를 만드는 것이다. <br>

` C++에서는 기본적인 연결 리스트에 대한 **래퍼 클래스** 인 std::forward_list 클래스를 제공한다.` 그래서 이 말의 뜻을 다시 보면 원래 연결 리스트라는 개념이 있었는데 이를 객체로 만들기 위해서 forward_list 클래스를 만들었다는 말이다.

### std::forward_list에서 원소 삽입과 삭제

- 삽입: push_front(), insert_after()

  - push_front()의 경우는 연결 리스트 맨 앞에 새로운 원소를 삽입
  - insert_after()의 경우는 새로운 원소를 삽입한 후 해당 위치 앞에 있는 원소의 next포인터를 수정해야 하기 때문이다. <br>

  ```cpp
  #include <iostream>
  #include <forward_list>
  void print(std::forward_list<int> fwd_list)
  {
      for (auto ele : fwd_list)
      {
          std::cout << ele << " ";
      }
      std::cout << std::endl;
  }
  int main()
  {
      std::forward_list<int> fwd_list = {1, 2, 3};
      // 맨 앞에 0 추가
      fwd_list.push_front(0);
      std::cout << "맨 앞에 0 추가: ";
      print(fwd_list);
      auto it = fwd_list.begin();
      // 맨 처음 원소 뒤에 5 추가
      fwd_list.insert_after(it, 5);
      std::cout << "맨 처음 원소 뒤에 5 추가: ";
      print(fwd_list);
      // 맨 처음 원소 뒤에 6 추가
      fwd_list.insert_after(it, 6);
      std::cout << "맨 처음 원소 뒤에 6 추가: ";
      print(fwd_list);
  }

  >>>
  맨 앞에 0 추가: 0 1 2 3
  맨 처음 원소 뒤에 5 추가: 0 5 1 2 3
  맨 처음 원소 뒤에 6 추가: 0 6 5 1 2 3
  ```

  - ❓auto 키워드?

    auto 키워드는 초기화시에 초기화 값에 맞춰 자동으로 자료형을 판단하는 기능을 가진다. 주의할 점은 선언만하고 초기화를 하지 않으면 사용이 불가하다.

- 삽입: emplace_front(), emplace_after()
  이 두 함수의 경우는 insert_after()과 push_front()와 달리 추가적인 복사 또는 이동을 하지 않기 때문에 더 효율적입니다.

  ```cpp
  #include <iostream>
  #include <forward_list>

  void print(std::forward_list<int> fwd_list)
  {
      for (auto ele : fwd_list)
      {
          std::cout << ele << " ";
      }
      std::cout << std::endl;
  }

  int main()
  {
      std::forward_list<int> fwd_list = {1, 2, 3};
      // 맨 앞에 0 추가
      fwd_list.emplace_front(0);
      std::cout << "맨 앞에 0 추가: ";
      print(fwd_list);

      auto it = fwd_list.begin();

      // 맨 처음 원소 뒤에 5 추가
      fwd_list.emplace_after(it, 5);
      std::cout << "맨 처음 원소 뒤에 5 추가: ";
      print(fwd_list);
      // 맨 처음 원소 뒤에 6 추가
      fwd_list.emplace_after(it, 6);
      std::cout << "맨 처음 원소 뒤에 6 추가: ";
      print(fwd_list);
  }

  >>>
  맨 앞에 0 추가: 0 1 2 3
  맨 처음 원소 뒤에 5 추가: 0 5 1 2 3
  맨 처음 원소 뒤에 6 추가: 0 6 5 1 2 3
  ```

- 삭제: pop_front(), erase_after()

  - pop_front() 함수는 리스트의 맨 처음 원소를 제거
  - erase_after()은 두가지 형태로 제공되는데 하나는 특정 원소를 가리키는 반복자를 인자로 받아서 바로 다음 위치의 원소를 삭제하는 형태와 일련의 원소를 제거할 때에도 erase_after() 함수를 사용할 수 있으며, 이 경우에는 삭제할 범위의 시작 원소 앞을 가리키는 반복자와 삭제할 범위 끝 원소를 가리키는 반복자를 인자로 받는다.

  ```cpp
  #include <iostream>
  #include <forward_list>

  void print(std::forward_list<int> fwd_list)
  {
      for (auto ele : fwd_list)
      {
          std::cout << ele << " ";
      }
      std::cout << std::endl;
  }

  int main()
  {
      std::forward_list<int> fwd_list = {1, 2, 3, 4, 5};

      fwd_list.pop_front();
      std::cout << "첫 번째 원소 삭제: ";
      print(fwd_list);

      auto it = fwd_list.begin();

      fwd_list.erase_after(it);
      std::cout << "it 다음 위치 삭제(1번째 인덱스 삭제): ";
      print(fwd_list);

      fwd_list.erase_after(it, fwd_list.end());
      std::cout << "it 다음부터 끝까지 삭제: ";
      print(fwd_list);
  }

  >>>
  첫 번째 원소 삭제: 2 3 4 5
  it 다음 위치 삭제(1번째 인덱스 삭제): 2 4 5
  it 다음부터 끝까지 삭제: 2
  ```

### std::forward_list의 기타 멤버 함수

- remove(): 삭제할 원소 값 하나를 매개변수로 받는다. 이 함수는 저장된 데이터 타입에 정의된 등호 연산자를 사용하여 전달된 값과 일치하는 **모든 원소를 찾아 삭제**. 오직 등호에 근거하여 삭제하는 함수
- remove_if(): 원소 값을 검사하여 삭제하는데 remove()보다는 조금 더 유연하게 조건부 삭제까지 수행 가능.

```cpp
#include <iostream>
#include <forward_list>

bool del_less_five(const int value)
{
    return (value < 5);
}
void print(std::forward_list<int> myList)
{
    for (int ele : myList)
    {
        std::cout << ele << " ";
    }
    std::cout << std::endl;
}
int main()
{
    std::forward_list<int> fwd_list = {1, 2, 3, 4, 5, 6, 7, 8, 9, 7, 7, 1, 1, 2, 5};

    fwd_list.remove(7);
    std::cout << "7 제거: ";
    print(fwd_list);

    fwd_list.remove_if(del_less_five);
    std::cout << "remove_if(): ";
    print(fwd_list);
}

>>>
7 제거: 1 2 3 4 5 6 8 9 1 1 2 5
remove_if(): 5 6 8 9 5
```

## 반복자

반복자는 포인터와 비슷하지만 STL 컨테이너에 대해 공통의 인터페이스를 제공합니다. 반복자를 이용한 연산은 어떤 컨테이너에서 정의된 반복자인지에 따라 결정되는데 <br>

- 벡터와 배열에서 사용되는 반복자: 기능 면에서 가장 유연. 연속된 자료구조를 사용하기 때문에 특정 위치의 원소에 곧바로 접근 가능
- 연결 리스트: 역방향으로 이동하는 기능을 제공하지 않으며, 이전 노드로 이동하려면 맨 처음 노드부터 시작해서 찾아야 한다. 연산으로는 증가 연산만 가능하며 이러한 반복자를 순방향 반복자라고 한다.

### 반복자의 타입에 따라 사용할 수 있는 함수

- advance(): 반복자와 거리 값을 인자로 받고, 반복자를 거리 값만큼 증가시킨다.
- next(), prev(): 반복자와 거리 값을 인자로 받고, 해당 반복자에서 지정한 거리만큼 떨어진 위치의 반복자를 반환한다.

## std::list

std::forward_list는 아주 기본적인 형태로 구현된 연결 리스트이다. std::forward_list는 다른 유용한 기능 주에서도 리스트 끔에 원소 추가, 역방향 이동, 리스트 크기 반환 등의 기능은 제공하지 않습니ㅏ. 이는 메모리를 적게 쓰고 빠른 성능을 유지하기 위함입니다. 그리고 std::forward_list의 반복자는 매우 적은 기능만을 지원한다. <br>

이러한 단점을 보안하기 위해서 C++에서는 std::list의 기능을 제공한다. list는 양쪽 방향으로 연결된 리스트, 즉, **이중 연결 리스트** 구조로 되어있다.

### std::list 멤버 함수

- ::iterator

  - begin(): 맨 앞의 원소를 가리키는 iterator 리턴
  - end(): 맨 뒤의 다음 원소를 가리키는 iterator 리턴
  - rbegin(): 맨 뒤의 원소를 가리키는 iterator 리턴(뒤에서부터 순차적으로 접근할 때 사용)
  - rend(): 맨 앞 이전 원소를 가리키는 iterator 리턴

- 삽입
  - push_back(element): list 맨 뒤에 element 추가
  - push_front(element): list 맨 앞에 element 추가
  - insert(iterator, element): list의 iterator가 가리키는 위치 앞에 element 추가
  - emplace()
  - emplace_back(element): 맨 뒤에 element를 추가
- 삭제
  - pop_front(): list 맨 앞의 우너소 제거
  - pop_back(): list 맨 뒤에 원소 삭제
  - erase(iterator): iterator에 해당하는 원소 삭제
  - remove()
  - remove_if()

```cpp
#include <iostream>
#include <list>

// 원래 이중연결 리스트 노드 구조
struct doubly_linked_list_node
{
    int data;
    doubly_linked_list_node *next;
    doubly_linked_list_node *prev;
};

void print(std::list<int> list)
{
    for (auto it = list.begin(); it != list.end(); it++)
    {
        std::cout << *it << " ";
    }
    std::cout << std::endl;
}
int main()
{
    std::list<int> list1 = {1, 2, 3, 4, 5};
    list1.push_back(6);
    list1.insert(list1.begin(), 0);
    // list1.pust_front(0);
    list1.insert(list1.end(), 7);
    // list1.push_back(7);

    std::cout << "원소 추가: " << std::endl;
    print(list1);

    std::cout << "원소 삭제: " << std::endl;
    list1.pop_back();
    print(list1);
    list1.pop_front();
    print(list1);
}

>>>
원소 추가:
0 1 2 3 4 5 6 7
원소 삭제:
0 1 2 3 4 5 6
1 2 3 4 5 6
```

여튼 list는 이중 원형 리스트이므로 단일 연결 리스트보다 관리해야되는 포인터가 2배 많으믈 시간도 2배로 걸린다.

### 양방향 반복자

std::list의 반복자같은 경우, forward_list 기반의 순방향 반복자보다 유연성을 가지고 있다. 하지만 std::list 반복자는 **임의 접근 반복자** 보다는 유연하지 않다.
