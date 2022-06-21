---
title: "[백준 2667번] DFS"
excerpt: "[백준 2667번] DFS"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

<그림 1>과 같이 정사각형 모양의 지도가 있다. 1은 집이 있는 곳을, 0은 집이 없는 곳을 나타낸다. 철수는 이 지도를 가지고 연결된 집의 모임인 단지를 정의하고, 단지에 번호를 붙이려 한다. 여기서 연결되었다는 것은 어떤 집이 좌우, 혹은 아래위로 다른 집이 있는 경우를 말한다. 대각선상에 집이 있는 경우는 연결된 것이 아니다. <그림 2>는 <그림 1>을 단지별로 번호를 붙인 것이다. 지도를 입력하여 단지수를 출력하고, 각 단지에 속하는 집의 수를 오름차순으로 정렬하여 출력하는 프로그램을 작성하시오.
![Untitled](https://user-images.githubusercontent.com/96654391/174782777-8ec9fd00-1976-4fa1-852c-9741f1888a8b.png)



## 입력

첫 번째 줄에는 지도의 크기 N(정사각형이므로 가로와 세로의 크기는 같으며 5≤N≤25)이 입력되고, 그 다음 N줄에는 각각 N개의 자료(0혹은 1)가 입력된다.

## 출력

첫 번째 줄에는 총 단지수를 출력하시오. 그리고 각 단지내 집의 수를 오름차순으로 정렬하여 한 줄에 하나씩 출력하시오.

## 예제 입력 1 

7 <br>
0110100 <br>
0110101 <br>
1110101 <br>
0000111 <br>
0100000 <br>
0111110 <br>
0111000

## 예제 출력 1 

3 <br>
7 <br>
8 <br>
9 <br>

## 📌 문제 풀이

```java
package DFS;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

public class Backjoon_2667 {
    static int n; // 입력 받을 n
    static int cnt; // 집을 셀 cnt

    static int house[][]; // 지도 입력 배열
    static boolean check[][]; // 방문 여부

    static ArrayList<Integer> arr = new ArrayList<>();

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        house = new int[n][n];
        check = new boolean[n][n];

        // 1. 지도 입력 받기
        for (int i = 0; i < n; i++) {
            String temp = sc.next();
            for (int j = 0; j < n; j++) {
                house[i][j] = temp.charAt(j) - '0';
            }
        }

        // 2. 단지 방문
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (house[i][j] == 1 && check[i][j] == false) {
                    cnt = 1;
                    dfs(i, j);
                    arr.add(cnt);
                }
            }
        }

        // 3. 출력
        System.out.println(arr.size());
        Collections.sort(arr);
        for (int i = 0; i < arr.size(); i++) {
            System.out.println(arr.get(i));
        }
    }

    static void dfs(int checkRow, int checkCol) {
        // dfs 1. 방문한 노드를 true로 바꾸고
        check[checkRow][checkCol] = true;
        // dfs 2. 주변에 방문 안한 노드를 찾기
        // 현재 탐색한 노드 기준 상
        if (checkRow > 0 && house[checkRow - 1][checkCol] == 1 && check[checkRow - 1][checkCol] == false) {
            cnt++;
            dfs(checkRow - 1, checkCol);
        }
        // 현재 탐색한 노드 기준 하
        if (checkRow < n - 1 && house[checkRow + 1][checkCol] == 1 && check[checkRow + 1][checkCol] == false) {
            cnt++;
            dfs(checkRow + 1, checkCol);
        }
        // 현재 탐색한 노드 기준 좌
        if (checkCol > 0 && house[checkRow][checkCol - 1] == 1 && check[checkRow][checkCol - 1] == false) {
            cnt++;
            dfs(checkRow, checkCol - 1);
        }
        // 현재 탐색한 노드 기준 우
        if (checkCol < n - 1 && house[checkRow][checkCol + 1] == 1 && check[checkRow][checkCol + 1] == false) {
            cnt++;
            dfs(checkRow, checkCol + 1);
        }

    }
}
```
전체 n*n 만큼 반복문을 돌면서 dfs()를 통해서 붙어있는 단지인지(dfs() 메소드에서), 떨어져있는 단지인지(메인에서 반복문을 통해)를 판단한다. 