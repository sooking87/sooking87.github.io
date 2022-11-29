---
title: "3.2주차"
excerpt: "3.2주차"
categories: [Cpp Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

# Chap 03

## 프로그래머스

14860 강의를 찾을 것

## 실습 1

자리수를 각각 더하는 문제

```cpp
#include <iostream>
#include <string>
using namespace std;
int solution(int n)
{

    int answer = 0;
    for (int i = n; i > 0; i = i / 10)
    {
        answer += i % 10;
    }

    cout << answer << endl;
    return answer;
}

int main()
{
    solution(123);

    return 0;
}
```

## Vector

Vector is the most useful standard library data type. <br>

array와 연결 리스트의 장단점이 반대다 -> 두 개의 장점을 섞어 만든게 vector, 기본적으로 array 형식인데 space가 필요할 때마다 2배씩 길이를 더블링하는 것. 그냥 array를 사용한 비용과 vector을 통해서 사용되는 비용이 유사하다. <br>

![KakaoTalk_20220920_152435595](https://user-images.githubusercontent.com/96654391/191183325-ac980bf9-dcf3-4850-839a-49fb4426a8d8.jpg) <br>

vector는 자기가 몇 개의 데이터를 가지고 있는지 알고 그거에 대한 값을 리턴하는 함수가 size()라는 함수이다. array에 대한 포인터를 가지고 있다. 저 array를 바꿔타야되니까 일단 포인터로 array를 가지고 있다가 갈아탈일 일이 있을껄 더 큰 array로 allocation 해가지고 더 큰 array로 갈아탄다. <br>

별도로 데이터 타입에 따라 별도의 클래스가 필요해. 만약에 int에 대한 vector라면 int_vec, float에 대한 vector라면 float_vec 이것처럼 별도로 만들어야됨. 폴리모피즘 때문에 하고 싶은 거는 똑같은데, 데이터 타입만 다르다는 이유로 다른 클래스를 적용하기는 너무 비효율적이다. 그래서 여기서 나온 개념이 템플릿이다. 템플릿이란 다양한 형식의 데이터 타입을 수용할 수 있다. 모든 타입이 다 되는 것은 아닐 수 있으나 다양한 타입을 지원하는 것은 맞는 얘기.

<br>

![KakaoTalk_20220920_152434675](https://user-images.githubusercontent.com/96654391/191183318-e6ac6b92-e359-4798-84ac-fcdc062641f3.jpg)

길이 하나짜리 array -> 1복사, 뒤에 4 추가 -> array 갈아타 -> 실제 가져온 배열의 크기는 4이고, 1, 4를 복사, 마지막에 3 추가 -> 자신의 size()는 3으로 업데이트

### Vector에서 사용하는 함수

- push_back()
- insert()

### traversing a vector

```cpp
#include <iostream>
#include <vector>
using namespace std;

// 접근할 수 있는 방법
int main()
{
   vector<int> v = {1, 2, 3, 4, 5, 6};

   // 클래식 문법 => []연산자로 접근
   for (int i = 0; i < v.size(); i++)
   {
       cout << v[i] << endl;
   }

   // 최근 지원
   for (int i : v)
   {
       cout << i << endl;
   }

   for (auto it = v.begin(); it != v.end(); it++)
   {
       cout << *it << endl;
   }
}
```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<double> temps;
    double temp;

    // 길이 신경쓰지 않고 계속 push_back 가능
    while (cin >> temp)
        temps.push_back(temp);

    double sum = 0;
    for (int i = 0; i < temps.size(); ++i)
    {
        sum += temps[i];
        //일반적으로 array에 접근하는 방식과 같으며 vector 에서도 [] 연산자를 사용할 수 있다.
    }

    cout << "Mean temperature: " << sum / temps.size() << endl;
    sort(temps.begin(), temps.end());
}
```

### combining Language features

- Word list + Eliminate Duplicates

  ```cpp
  #include <iostream>
  #include <vector>
  #include <algorithm>
  using namespace std;

  // 중복한 워드는 한 번만 출력시키고 싶다.
  // point: 단어 벡터를 정렬시킨 후 앞뒤로 같은지 다른지를 판단한다.

  int main()
  {
      vector<string> words;
      for (string s; cin >> s && s != "quit";)
      {
          words.push_back(s);
      }

      sort(words.begin(), words.end());

      // 겹치지 않는 단어들을 넣어놓을 벡터
      vector<string> w2;
      if (words.size() > 0)
      {
          w2.push_back(words[0]);
          for (int i = 1; i < words.size(); i++)
          {
              if (words[i - 1] != words[i])
                  w2.push_back(words[i]);
          }
      }

      cout << "found " << words.size() - w2.size() << " duplicates" << endl;
      for (string s : w2)
      {
          cout << s << endl;
      }
  }

  ```

## 실습 2

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

bool solution(vector<int> arr)
{
    bool answer = true;
    // 정렬
    sort(arr.begin(), arr.end());

    for (int i = 1; i <= arr.size(); i++)
    {
        if (arr[i - 1] != i)
        {
            answer = false;
            break;
        }
    }
    cout << answer << endl;
    return answer;
}

int main()
{
    solution({4, 1, 3, 2});
}
```

sort를 사용하지 않고 비교하는 방법

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <numeric>
using namespace std;

// sort 안하고 문제 해결하기
bool solution2(vector<int> arr)
{
    bool ans = true;
    vector<int> count;
    // 0으로 초기화
    for (int i = 0; i < arr.size(); i++)
    {
        count.push_back(0);
    }

    for (int i = 0; i < arr.size(); i++)
    {
        if (arr[i] != 0 && arr[i] <= count.size())
        {
            count[arr[i] - 1]++;
        }
    }

    /*
    count 벡터의 전체 합이랑 count의 크기가 같은지 다른지를 비교하는 방식은
    [1, 1, 1, 1] = [0, 2, 1, 1] 이 모두 같은 값을 가지므로 의도하고자 하는 값을 찾을 수 없다.

    if (accumulate(count.begin(), count.end(), 0) == count.size())
    {
        ans = true;
    }
    else
    {
        ans = false;
    }
    */

    for (int i = 0; i < count.size(); i++)
    {
        if (count[i] != 1)
        {
            ans = false;
            break;
        }
    }

    return ans;
}

int main()
{
    solution2({4, 1, 3, 2});
}
```
