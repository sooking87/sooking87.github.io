---
title: "[C/C++] O(N^2) 정렬"
excerpt: "[C/C++] O(N^2) 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 버블 정렬

![버블정렬](https://velog.velcdn.com/images%2Fchaem%2Fpost%2Ff6075244-4450-4377-baec-23f51f5c3e2b%2Fbubble-sort-visualization.gif) 

버블이라는 이름을 보면 가장 큰 수가 점점 거품처럼 올라오는? 그런 느낌! 큰 수부터 정렬이 되는 느낌이다.

### 코드

```c++
#include <bits/stdc++.h>
using namespace std;

void printVec(const vector<int>& vec) {
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << ' ';
    }
    cout << '\n';
}

vector<int> bubbleSort(vector<int> target) {
    int n = target.size();
    int temp;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (target[j] > target[j+1]) {
                temp = target[j];
                target[j] = target[j+1];
                target[j+1] = temp;
            }
            printVec(target);
        }
    }
    return target;
}

int main() {
    int arr[] = {5, 3, 1, 4, 2};
    vector<int> target(arr, arr+sizeof(arr) / sizeof(arr[0]));
    vector<int> result = bubbleSort(target);
    printVec(result);
    return 0;
}
```

## 삽입 정렬

![삽입정렬](https://blog.kakaocdn.net/dn/pY2WC/btrGWzOvGga/mKX2rmAL8WkxDE3QRObkkK/img.gif)

삽입이라는 말 처럼 인덱스 1기준으로 앞쪽과 비교를 하면서 key보다 크면 vec[j]를 뒤로 한 칸씩 민다. 그 후 자기 자리에 삽입한다.

### 코드

```c++
#include <bits/stdc++.h>
using namespace std;

void printVec(vector<int> vec) {
    int n = vec.size();
    for (int i = 0; i < n; i++) {
        cout << vec[i] << ' ';
    }
    cout << '\n';
}
vector<int> insertSort(vector<int> vec) {
    int j;
    for (int i = 1; i < vec.size(); i++) {
        int key = vec[i]; // key를 기준으로 key가 작으면 그 앞에 위치 시킴
        for (j = i - 1; j >= 0; j--) {
            if (vec[j] > key) {
                vec[j+1] = vec[j]; // key보다 크다면 오른쪽으로 민다
            }
            else {
                break;
            }
        }
        vec[j+1] = key;
        printVec(vec);
    }
    return vec;
}
int main() {
    int arr[] = {4, 5, 2, 3, 1};
    vector<int> vec(arr, arr+sizeof(arr)/sizeof(arr[0]));
    printVec(vec);
    vector<int> result = insertSort(vec);
}
```