---
title: "[백준 1922번] 네트워크 연결"
excerpt: "[백준 1922번] 네트워크 연결"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

도현이는 컴퓨터와 컴퓨터를 모두 연결하는 네트워크를 구축하려 한다. 하지만 아쉽게도 허브가 있지 않아 컴퓨터와 컴퓨터를 직접 연결하여야 한다. 그런데 모두가 자료를 공유하기 위해서는 모든 컴퓨터가 연결이 되어 있어야 한다. (a와 b가 연결이 되어 있다는 말은 a에서 b로의 경로가 존재한다는 것을 의미한다. a에서 b를 연결하는 선이 있고, b와 c를 연결하는 선이 있으면 a와 c는 연결이 되어 있다.)
<br>
그런데 이왕이면 컴퓨터를 연결하는 비용을 최소로 하여야 컴퓨터를 연결하는 비용 외에 다른 곳에 돈을 더 쓸 수 있을 것이다. 이제 각 컴퓨터를 연결하는데 필요한 비용이 주어졌을 때 모든 컴퓨터를 연결하는데 필요한 최소비용을 출력하라. 모든 컴퓨터를 연결할 수 없는 경우는 없다. <br>

**_말은 거창하지만 결국은 크루스칼 알고리즘으로 풀어야하는 문제_**

## 입력

첫째 줄에 컴퓨터의 수 N (1 ≤ N ≤ 1000)가 주어진다.
<br>

둘째 줄에는 연결할 수 있는 선의 수 M (1 ≤ M ≤ 100,000)가 주어진다.

<br>
셋째 줄부터 M+2번째 줄까지 총 M개의 줄에 각 컴퓨터를 연결하는데 드는 비용이 주어진다. 이 비용의 정보는 세 개의 정수로 주어지는데, 만약에 a b c 가 주어져 있다고 하면 a컴퓨터와 b컴퓨터를 연결하는데 비용이 c (1 ≤ c ≤ 10,000) 만큼 든다는 것을 의미한다. a와 b는 같을 수도 있다.

## 출력

모든 컴퓨터를 연결하는데 필요한 최소비용을 첫째 줄에 출력한다.

## 예제 입력 1

6 <br>
9 <br>
1 2 5 <br>
1 3 4 <br>
2 3 2 <br>
2 4 7 <br>
3 4 6 <br>
3 5 11 <br>
4 5 3 <br>
4 6 8 <br>
5 6 8 <br>

## 예제 출력 1

23

## 📌 정답 풀이

```java
package Kruskal;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Backjoon1922 {
    static int V, E; // V: 노드/정점의 개수, E: 간선
    static int[][] graph;
    // 각 노드의 부모
    static int[] parent;
    static int finalCost;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        V = Integer.parseInt(br.readLine());
        E = Integer.parseInt(br.readLine());
        // 그래프 연결 상태(노드 1, 노드 2, 비용) -> 노드 1과 노드 2가 연결되어 있고, 해당 비용이 초기화되어있는 2차원 배열
        graph = new int[E][3];
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            graph[i][0] = Integer.parseInt(st.nextToken());
            graph[i][1] = Integer.parseInt(st.nextToken());
            graph[i][2] = Integer.parseInt(st.nextToken());
        }
        parent = new int[V];
        finalCost = 0;

        // 간선 비용(2번째 인덱스)을 오름차순으로 정렬
        Arrays.sort(graph, (o1, o2) -> Integer.compare(o1[2], o2[2]));

        // makeSet??
        for (int i = 0; i < V; i++) {
            parent[i] = i;
        }

        // 낮은 비용부터 크루스칼 알고리즘 진행
        for (int i = 0; i < E; i++) {
            // 같은 부모인지 아닌지를 판별하는 조건문
            if (find(graph[i][0] - 1) != find(graph[i][1] - 1)) {
                union(graph[i][0] - 1, graph[i][1] - 1);
                finalCost += graph[i][2];

                continue;
            }
        }
        System.out.println(finalCost);

    }

    // 유일한 부모인 경우 parent에 변경해주어야 한다.
    public static void union(int a, int b) {
        a = find(a);
        b = find(b);
        if (a > b) {
            parent[a] = b;
        } else {
            parent[b] = a;
        }
    }

    // 부모를 찾는 메소드
    public static int find(int x) {
        if (parent[x] == x) {
            return x;
        } else {
            return find(parent[x]);
        }
    }
}
```
