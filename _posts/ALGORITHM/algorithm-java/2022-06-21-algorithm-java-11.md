---
title: "[백준 2178번] BFS"
excerpt: "[백준 2178번] BFS"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

N×M크기의 배열로 표현되는 미로가 있다. <br>

1	0	1	1	1	1 <br>
1	0	1	0	1	0 <br>
1	0	1	0	1	1 <br>
1	1	1	0	1	1 <br>
미로에서 1은 이동할 수 있는 칸을 나타내고, 0은 이동할 수 없는 칸을 나타낸다. 이러한 미로가 주어졌을 때, (1, 1)에서 출발하여 (N, M)의 위치로 이동할 때 지나야 하는 최소의 칸 수를 구하는 프로그램을 작성하시오. 한 칸에서 다른 칸으로 이동할 때, 서로 인접한 칸으로만 이동할 수 있다. <br>

위의 예에서는 15칸을 지나야 (N, M)의 위치로 이동할 수 있다. 칸을 셀 때에는 시작 위치와 도착 위치도 포함한다.

## 입력

첫째 줄에 두 정수 N, M(2 ≤ N, M ≤ 100)이 주어진다. 다음 N개의 줄에는 M개의 정수로 미로가 주어진다. 각각의 수들은 붙어서 입력으로 주어진다.

## 출력

첫째 줄에 지나야 하는 최소의 칸 수를 출력한다. 항상 도착위치로 이동할 수 있는 경우만 입력으로 주어진다.

## 예제 입력 1 
4 6 <br>
101111 <br>
101010 <br>
101011 <br>
111011

## 예제 출력 1 
15 

## 📌문제 풀이

```java
package BFS;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Backjoon_2178 {
    static int n, m;
    static int[][] dist;
    static String[] A; // 미로 입력받기 위한 변수

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        A = new String[n];
        for (int i = 0; i < n; i++) {
            A[i] = br.readLine();
        }

        dist = new int[n][m];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], -1); // 배열을 -1 로 초기화
        }

        BFS(0, 0);
        System.out.println(dist[n - 1][m - 1]);
    }

    static void BFS(int x, int y) {
        Queue<Integer> Q = new LinkedList<>();
        Q.add(x); // x좌표
        Q.add(y); // y좌표
        dist[x][y] = 1; // 시작 칸 1로 초기화 -> 방문 O
        int[][] dir = { { 0, -1 }, { 1, 0 }, { 0, 1 }, { -1, 0 } }; // 갈 수 있는 방향 (남, 동, 북, 서)

        while (!Q.isEmpty()) {
            x = Q.poll();
            y = Q.poll();
            for (int i = 0; i < 4; i++) {
                int nx = x + dir[i][0]; // 다음 x좌표 후보
                int ny = y + dir[i][1]; // 다음 y좌표 후보
                if (nx < 0 || ny < 0 || nx >= n || ny >= m)
                    continue; // 미로 범위 안에 있는지 확인
                if (A[nx].charAt(ny) == '0') // 0이면 길이 존재하지 않으므로 갈 수 없다.
                    continue;
                if (dist[nx][ny] != -1) // -1이 아니라는 것은 이미 방문을 했다는 뜻(처음에 -1로 초기화 시켰으므로)
                    continue;

                dist[nx][ny] = dist[x][y] + 1; // 방문 처리
                Q.add(nx);
                Q.add(ny);

            }
        }

    }
}
```

- dist: 방문을 했는지 아닌지 확인하기 위한 배열
- String A: 미로를 입력받기 위한 문자 배열
<br>

코드 설명 -> dist를 먼저 -1로 초기화를 시켜놓고, 루트 노드(0, 0)부터 BFS 탐색을 시작
1. 방문을 했다면 dist를 1로 바꾼다. 
2. 방문한 노드를 기준으로 상하좌우를 봐서 dist가 -1이 아니거나 A[nx].charAt(ny)가 0이거나, n과 m의 범위를 벗어났다면 탐색할 필요가 없다. = continue;
3. 2번이 아니라면 방문해도 되는 길이므로 방문을 하고 전에 방문했던 곳보다 숫자 1을 늘려서 최종 몇 번의 길을 통해서 이동했는지 확인한다. 