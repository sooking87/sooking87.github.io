---
title: "[C++] 트리, 힙, 그래프"
excerpt: "트리, 힙, 그래프"
categories: [Algorithm Study]
tags: [Algorithm Study, C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 비선형 문제

### 계층적 문제

예를 들면 회사 조직도, 대학의 교과 과정 계층도 처럼 계층 구조가 있는 문제입니다. 이러한 문제를 풀기 위해서는 트리라고 부르는 자료 구조를 사용해야 한다. 데이터가 저장된 부분을 보통 노드라고 부르고, 노드와 노드 사이를 잇는 선을 예지라고 한다.

### 순환 종속성

사람들의 친구 관계도 이런 구조를 그래프라고 한다. 또는 도시와 도시를 잇는 도로망 정도?

## 트리 : 상하 반전된 형태

트리는 노드와 노드 사이를 연결하는 예지를 이용하여 계층을 구성하낟. 트리의 계층 구조를 화면에 도식적으로 나타내려면 말 그대로 **나무 형태** 로 나타낼 수 있으며, 이때 예지는 나뭇가지처럼 표현된다. 트리의 중심이 되는 노드를 **루트 노드** 라고 부르고, 이 노드는 보통 가장 맨 위에 나타난다.

### 연습문제 : 조직도 구조 만들기

```cpp
#include <iostream>
#include <queue>

// if : 한 직원은 최대 두명의 부하 직원을 거느릴 수 있다. = 이진 트리 구조

struct node
{
    std::string position;
    node *first;
    node *second;
};

struct org_tree
{
    node *root;

    // 루트 노드 생성 함수
    static org_tree create_org_structure(const std::string &pos)
    {
        org_tree tree;
        tree.root = new node{pos, NULL, NULL};
        return tree;
    }

    // 조직도에서 부하 직원을 탐색하는 함수.
    // 상사의 직책 이름과 부하 직원의 직책 이름을 인자로 받으며, 이 중 상사의 직책은 이미 트리에 존재한다.
    static node *find(node *root, const std::string &value)
    {
        if (root == NULL)
        {
            return NULL;
        }

        if (root->position == value)
        {
            return root;
        }

        auto firstFound = org_tree::find(root->first, value);

        if (firstFound != NULL)
        {
            return firstFound;
        }

        return org_tree::find(root->second, value);
    }

    // 새로운 원소(부하 직원)을 추가하는 삽입 함수 => find() 함수 활용
    // 부하 직원을 정상적으로 삽입한다면 true를 아니라면 false를 리턴
    bool addSubordinate(const std::string &manager, const std::string &subordinate)
    {
        auto managerNode = org_tree::find(root, manager);

        // 해당 매니져의 노드가 없는 경우
        if (!managerNode)
        {
            std::cout << manager << "을(를) 찾을 수 없습니다: " << std::endl;
            return false;
        }

        // 해당 매니저 노드에 부하 직원 2명이 모두 차 있는 경우
        if (managerNode->first && managerNode->second)
        {
            std::cout << manager << " 아래에 " << subordinate << "을(를) 추가할 수 없습니다." << std::endl;
            return false;
        }

        // 부하 직원을 추가할 수 있는 경우
        if (!managerNode->first)
        {
            managerNode->first = new node{subordinate, NULL, NULL};
        }
        else
        {
            managerNode->second = new node{subordinate, NULL, NULL};
        }

        std::cout << manager << " 아래에 " << subordinate << "을(를) 추가했습니다." << std::endl;

        return true;
    }
};

int main()
{
    auto tree = org_tree::create_org_structure("CEO");

    tree.addSubordinate("CEO", "부사장");
    tree.addSubordinate("부사장", "IT부장");
    tree.addSubordinate("부사장", "마케팅부장");
    tree.addSubordinate("IT부장", "보안팀장");
    tree.addSubordinate("IT부장", "웹개발팀장");
    tree.addSubordinate("마케팅부장", "물류팀장");
    tree.addSubordinate("마케팅부장", "홍보팀장");
    tree.addSubordinate("부사장", "재무부장");
}

>>>
CEO 아래에 부사장을(를) 추가했습니다.
부사장 아래에 IT부장을(를) 추가했습니다.
부사장 아래에 마케팅부장을(를) 추가했습니다.
IT부장 아래에 보안팀장을(를) 추가했습니다.
IT부장 아래에 웹개발팀장을(를) 추가했습니다.
마케팅부장 아래에 물류팀장을(를) 추가했습니다.
마케팅부장 아래에 홍보팀장을(를) 추가했습니다.
부사장 아래에 재무부장을(를) 추가할 수 없습니다.
```

### 트리 순회

부모 노드를 기준으로 부모 노드를 "전"으로 검사하냐, "중"으로 검사하나, "후"로 검사하냐 이 차이다.

- 전위 순회(preorder)

  ```cpp
  // 전위 순회
  static void preOrder(node *start)
  {
      if (!start)
          return;

      // 부모 노드 먼저 검색
      std::cout << start->position << ", ";
      preOrder(start->first);
      preOrder(start->second);
  }

  >>>
  전위 순회: CEO, 부사장, IT부장, 보안팀장, 웹개발팀장, 마케팅부장, 물류팀장, 홍보팀장,
  ```

- 중위 순회(in-order)

  ```cpp
  // 중위 순회
  static void inOrder(node *start)
  {
      if (!start)
          return;

      // 부모 노드를 중간에 검색
      inOrder(start->first);
      std::cout << start->position << ", ";
      inOrder(start->second);
  }

  >>>
  중위 순회: 보안팀장, IT부장, 웹개발팀장, 부사장, 물류팀장, 마케팅부장, 홍보팀장, CEO,
  ```

- 후위 순회(post-order)

  ```cpp
  // 후위 순회
  static void postOrder(node *start)
  {
      if (!start)
          return;

      // 부모를 마지막에 검색
      postOrder(start->first);
      postOrder(start->second);
      std::cout << start->position << ", ";
  }

  >>>
  후위 순회: 보안팀장, 웹개발팀장, IT부장, 물류팀장, 홍보팀장, 마케팅부장, 부사장, CEO,
  ```

- 레벨 순서 순회

## 다양한 트리 구조

### 이진 검색 트리

이진 검색 트리(Binary Search Tree, BST)는 널리 사용되고 있는 형태의 이진 트리 <br>

해당 트리는 다음과 같은 속성이 있다. - 왼쪽 노드 <= 부모 노드 <= 오른쪽 노드 <br>

트리는 밑으로 갈수록 2배씩 노드의 개수가 많아지기 때문에 노드 하나를 검색, 삽입, 삭제의 경우 시간 복잡도는 O(log<sub>2</sub>N)이다. <br>

연습문제를 보면 find, insert, delete 함수는 public 멤버 함수를 통해서 main 함수를 접근을 가능하게 했고, @@\_impl 함수는 private 멤버 함수로서 진짜 검색, 삽입, 삭제에 대한 구현을 가지고 있는 함수는 private로 캡슐화하였습니다.

- 검색

  현재 노드와 value를 비교하면서 재귀함수로 진행이 된다. value가 current->data보다 작다면 트리 상에서 왼쪽에 있다는 것이고 크다면 트리 상에서 오른쪽에 있다는 것이다.

  ```cpp
      node *find(int value)
    {
        return find_impl(root, value);
    }

  private:
      node *find_impl(node *current, int value)
      {
          if (!current)
          {
              std::cout << std::endl;
              return NULL;
          }

          if (current->data == value)
          {
              std::cout << value << "을(를) 찾았습니다." << std::endl;
              return current;
          }

          // value 값이 현재 노드 왼쪽에 있는 경우
          if (value < current->data)
          {
              std::cout << current->data << "에서 왼쪽으로 이동: ";
              return find_impl(current->left, value);
          }

          // value 값이 현재 노드 오른쪽에 있는 경우
          std::cout << current->data << "에서 오른쪽으로 이동: ";
          return find_impl(current->right, value);
      }
  ```

- 삽입

  재귀적으로 하위 노드로 이동하면서 value가 current->data보다 작다면 트리상에 왼쪽 노드에 삽입을 해야된다. 이때 왼쪽 노드에 노드가 있다면 다시 함수를 통해서 삽입을 시킬 때까지 재귀 함수를 사용한다. value가 current->data보다 큰 경우도 마찬가지러 오른쪽 노드에 넣어야 되는데 그 노드가 차있다면 한 번더 함수에 넣어서 확인.. 이런식으로 진행된다.

  ```cpp
  public:
  // 재귀적으로 하위 노드로 이동하면서 삽입할 위치의 부모 노드를 찾는다.
      void insert(int value)
      {
          if (!root)
          {
              root = new node{value, NULL, NULL};
          }
          else
          {
              insert_impl(root, value);
          }
      }

  private:
      void insert_impl(node *current, int value)
      {
          // current 위치보다 왼쪽에 value가 들어가야되는 경우
          if (value < current->data)
          {
              // current의 왼쪽 노드가 비어있을 경우
              if (!current->left)
              {
                  current->left = new node{value, NULL, NULL};
              }
              else
              {
                  insert_impl(current->left, value);
              }
          }
          else
          {
              if (!current->right)
              {
                  current->right = new node{value, NULL, NULL};
              }
              else
              {
                  insert_impl(current->right, value);
              }
          }
      }
  ```

- 삭제 <br>

  삭제의 경우는 삭제할 노드가 다음과 같은 세 가지 경우를 따져봐야 된다. 여튼 삭제되고 밑에 있는 노드를 루트로 올리는 과정이다. 근데 여기서 자식이 없거나 하나인 경우는 바로 밑에 있는 노드를 부모 노드로 올리면 된다. 하지만 자식 노드가 두 개 다 있는 경우는 그 밑에 또 노드가 있을 수 있기 때문에 ,, 🌟잘 몰겠음...... 정확이 어떤 식으로 진행되는 지는 모르겠지만 서브 트리의 오른쪽 노드의 그 노드의 하위 왼쪽 노드를 지워진 자리로 올리는 것 같다.

  - 자식 노드가 없는 경우
  - 자식 노드가 하나만 있는 경우
  - 자식 노드가 두 개 다 있는 경우

  ```cpp
  public:
      // 노드 삭제 후 어떤 노드를 올릴지 탐색하는 함수.
      node *successor(node *start)
      {
          auto current = start->right;
          while (current && current->left)
          {
              current = current->left;
          }
          return current;
      }

      // 원소 삭제하기
      void delete_value(int value)
      {
          root = delete_impl(root, value);
      }

  private:
      node *delete_impl(node *start, int value)
      {
          if (!start)
              return NULL;
          if (value < start->data)
          {
              start->left = delete_impl(start->left, value);
          }
          else if (value > start->data)
          {
              start->right = delete_impl(start->right, value);
          }
          else
          {
              // 자식 노드가 전혀 없거나, 왼쪽 자식 노드만 없는 경우
              if (!start->left)
              {
                  auto tmp = start->right;
                  delete start;
                  return tmp;
              }

              // 오른쪽 자식 노드만 없는 경우
              if (!start->right)
              {
                  auto tmp = start->left;
                  delete start;
                  return tmp;
              }

              // 자식 노드가 둘 다 있는 경우
              auto succNode = successor(start);
              start->data = succNode->data;

              // 오른쪽 서브 트리에서 후속(successor)을 찾아 삭제
              start->right = delete_impl(start->right, succNode->data);
          }
          return start;
      }
  ```

### 균형 트리(balanced Tree)

편향된 트리의 경우 find() 함수의 시간 복잡도를 늘릴 수 있습니다. 실제로 트리의 시간 복잡도는 트리의 높이에 영향을 받기 때문에 높이가 높을수록 같은 개수의 노드더라도 더 많은 시간이 든다는 것이다. 그렇기 때문에 원소 검색의 시간 복잡도를 최적화하려면 트리의 높이를 최적화해야 된다. 즉, 트리의 **균형을 잡아야** 한다. <br>

이 트리의 균형을 잡는 방법은 여러 가지가 있으며 이를 통해서 AVL 트리, 레드 블랙 트리와 같은 다양한 트리를 만들 수 있다. AVL 트리의 기본 아이디어는 BST 속성을 유지하며서 트리 높이의 균형을 잡기 위해 약간의 회전을 수행하는 것이다.

### N-향 트리

지금까지는 주로 이진 트리에 대해 살펴봤다. N-향 트리는 각 노드가 N개의 자식을 가질 수 있다. N은 임의의 양수로 N개의 자식 노드는 벡터를 이용하여 저장할 수 있다.

```cpp
struct nTree
{
    int data;
    std::vector<nTree*> children;
}
```

## 힙

- 완전 이진 트리
- O(1): 최대 원소에 즉각적으로 접근
- O(log N): 원소 삽입에 대한 시간 복잡도
- O(log N): 최대 원소 삭제에 대한 시간 복잡도
- i, 2*i, 2*i+1

### 힙 연산

최대 힙을 가정

- 삽입: 먼저 루트 노드로 값을 삽입하고 순서를 바꾸면서 자신의 위치로 들어간다. -> O(logN)
- 삭제: 루트 노드와 마지막 노드 교환 -> 루트 노드의 값은 삽입과 마찬가지고 자신의 자리를 찾아서 가고, 마지막 노드(전 루트노드)는 삭제된다.
- 힙 초기화: 힙에 하나씩 원소를 직접 삽입하는 작업은 O(N log N) 시간 복잡도를 가지지만 힙 생성 알고리즘을 사용하면 O(N) 시간에 힙을 초기화할 수 있다. <br>
  맨 마지막 ㄹ벨은 자식 노드가 없으므로 이미 힙 솏ㅇ을 만족한다고 간주, 한 레벨씩 트리를 위로 올라가면서 힙 속성에 만족하도록 트리를 업데이트하는 과정이다. 이는 배열 또는 벡터 반복자를 인자로 받아 힙을 구성하는 std::make_heap() 함수를 제공한다.

## 그래프

트리는 계층적 데이터를 표현하는 좋은 방법이지만, 하나의 노드에서 다른 노드로 이동하는 경로가 하나만 존재하기 때문에 원형 또는 순환적인 종속성을 표현할 수 없다. 그러나 실생활에서는 순환 구조를 사용하여 표현해야하는 많은 시나리오도 존재한다.

- 비가중 그래프: 가중치가 없는 그래프
- 가중 그래프: 에지에 노드와 노드 사이 가중치를 지정한 그래프
- 무방향 그래프
- 방향 그래프

### 인접 행렬로 그래프 표현하기

노드가 N개일 경우, 이 그래프는 **_N \* N 크기의 2차원 배열_** 로 표현할 수 있다. 그리고 배열 안에는 각각의 노드들 사이의 에지의 가중치를 나타낸다. 이러한 방식으로 그래프를 표현하는 방법을 인접 행렬이라고 한다.

```cpp
#include <iostream>
#include <vector>

// enum 클래스로 도시 이름 지정
enum class city : int
{
    MOSCOW,
    LONDON,
    SEOUL,
    SEATTLE,
    DUBAI,
    SYDNEY
};
// city enum에 대한 << 연산자. 오 신기하네
// istream 클래스: operator>>가 istream 클래스에 정의된 연산자
// ostream 클래스: operator<<가 ostream 클래스에 정의된 연산자
std::ostream &operator<<(std::ostream &os, const city c)
{
    switch (c)
    {
    case city::LONDON:
        os << "런던";
        return os;
    case city::MOSCOW:
        os << "모스크바";
        return os;
    case city::SEOUL:
        os << "서울";
        return os;
    case city::SEATTLE:
        os << "시애틀";
        return os;
    case city::DUBAI:
        os << "두바이";
        return os;
    case city::SYDNEY:
        os << "시드니";
        return os;
    defualt:
        return os;
    }
}

struct graph
{
    std::vector<std::vector<int>> data;

    // 그래프 초기화 해당 코드에서는 6 * 6 벡터를 만든다.
    graph(int n)
    {
        data.reserve(n);
        std::vector<int> row(n);
        std::fill(row.begin(), row.end(), -1);

        for (int i = 0; i < n; i++)
        {
            data.push_back(row);
        }
    }

    void addEdge(const city c1, const city c2, int dis)
    {
        std::cout << "에지 추가: " << c1 << "-" << c2 << "=" << dis << std::endl;

        // static_cast<바꾸려고 하는 타입>(대상);
        auto n1 = static_cast<int>(c1);
        auto n2 = static_cast<int>(c2);
        data[n1][n2] = dis;
        data[n2][n1] = dis;
    }

    void removeEdge(const city c1, const city c2)
    {
        std::cout << "에지 삭제: " << c1 << "-" << c2 << std::endl;

        auto n1 = static_cast<int>(c1);
        auto n2 = static_cast<int>(c2);
        data[n1][n2] = -1;
        data[n2][n1] = -1;
    }
};
int main()
{
    graph g(6);
    g.addEdge(city::LONDON, city::MOSCOW, 2500);
    g.addEdge(city::LONDON, city::SEOUL, 9000);
    g.addEdge(city::LONDON, city::DUBAI, 5500);
    g.addEdge(city::SEOUL, city::MOSCOW, 6600);
    g.addEdge(city::SEOUL, city::SEATTLE, 8000);
    g.addEdge(city::SEOUL, city::DUBAI, 7000);
    g.addEdge(city::SEOUL, city::SYDNEY, 8000);
    g.addEdge(city::SEATTLE, city::MOSCOW, 8400);
    g.addEdge(city::SEATTLE, city::SYDNEY, 12000);
    g.addEdge(city::DUBAI, city::SYDNEY, 1200);

    g.addEdge(city::SEATTLE, city::LONDON, 8000);
    g.removeEdge(city::SEATTLE, city::LONDON);

    return 0;
}

>>>
에지 추가: 서울-모스크바=6600
에지 추가: 서울-시애틀=8000
에지 추가: 서울-두바이=7000
에지 추가: 서울-시드니=8000
에지 추가: 시애틀-모스크바=8400
에지 추가: 시애틀-시드니=12000
에지 추가: 두바이-시드니=1200
에지 추가: 시애틀-런던=8000
에지 삭제: 시애틀-런던
```

**_배운 점_** <br>

1. istream 클래스, ostream 클래스
2. static_cast: 자료형을 바꿀 때 사용
