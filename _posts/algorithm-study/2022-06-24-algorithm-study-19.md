---
title: "[JAVA] 크로스칼 알고리즘"
excerpt: "크로스칼 알고리즘"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

# 최소 신장 트리

최소 신장 트리는 Minimun Spanning Tree(MST)로서 그래프의 모든 꼭짓점을 노드로 포함하면서 노드 간의 비용을 최소로 하는 트리를 말하며, 이를 유도하기 위해서 크루스칼 알고리즘이나 프림 알고리즘을 사용한다.

# 크루스칼 알고리즘

이산 수학 교재 p.440에 나와있는 내용이다. 주어진 가중치 그래프에서 최소 신장 트리를 크루스칼 알고리즘으로 구하려면 다음과 같은 규칙에 따른다.
<br>

1. 가중치가 가장 작은 변을 차례로 선택한다.
2. 가중치가 같은 변은 모두 선택한다.
3. 선택된 변에 의해 순환이 형성되는 경우는 선택하지 않는다.
4. 그래프에 포함된 모든 꼭짓점의 수가 n개일 때, n-1개의 변이 연결되면 종료한다.
   <br>

## 📍 예시

![download1](https://user-images.githubusercontent.com/96654391/175553908-b36958ce-5974-424b-ba6c-e30be484ae5c.png) <br>

7개의 노드, 11개의 간선 <br>

1. 11개의 간선들 중 가장 작은 가중치를 가진 7 노드와 1 노드 사이의 **12 가중치 간선** 선택
2. 7노드와 연결된 **13짜리의 가중치 간선** 선택
3. **17 가중치 간선** 선택
4. **20 가중치 간선** 선택
5. **24 가중치 간선** 선택
6. 그 다음 **28 가중치 간선** 을 선택하게 된다면 그래프에 순환이 발생 => 선택 X
7. **37 가중치 가선** 선택

<br>

📌 **_총 비용: 12 + 13 + 17 + 20 + 24 + 37 = 123_**

## 📍 알고리즘

다른 예시 <br>

![download2](https://user-images.githubusercontent.com/96654391/175558535-23f7dc36-0276-4e9d-abfe-f95b9fe7ec1e.png)

<br>

```java
package Kruskal;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

/*
sample input(첫 줄의 첫 숫자는 정점의 개수, 두 번째 숫자는 간선의 개수).
6 9
1 6 5
2 4 6
1 2 7
3 5 15
5 6 9
3 4 10
1 3 11
2 3 3
4 5 7
 */

public class KruskalAlgo {
    static int V, E; // V: 노드/정점의 개수, E: 간선
    static int[][] graph;
    // 각 노드의 부모
    static int[] parent;
    static int finalCost;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
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
            System.out.println(i + "번째");
            if (find(graph[i][0] - 1) != find(graph[i][1] - 1)) {
                System.out.println(graph[i][0] + " " + graph[i][1]);
                System.out.println("<선택된 간선>");
                System.out.println(Arrays.toString(graph[i]));
                union(graph[i][0] - 1, graph[i][1] - 1);
                finalCost += graph[i][2];
                System.out.println("<각 노드가 가리키고 있는 부모>");
                System.out.println(Arrays.toString(parent) + "\n");
                continue;
            }
        }
        System.out.println("최종 비용: " + finalCost);

    }

    // 같은 부모인지 아닌지 판별하는 메소드
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
            System.out.println(x);
            return x;
        } else {
            System.out.println("else");
            return find(parent[x]);
        }
    }
}
```

<br>

부모를 찾는 이유 ❓ <br>
순환 구조인지 아닌지를 판별하기 위해서 <br>
그럼 부모가 무슨 노드인지는 어떻게 알아 ❓ <br>
parent 배열을 통해서 알 수 있다. 예를 들어서 [2 3 3] 구조가 크루스칼 알고리즘을 통해서 최소 가중치로 선택이 되었다면 parent의 배열은 [0 1 1 3 4 5]로 나오게 된다. 여기서 2번째 노드의 부모 노드는 1임을 알 수 있다.

## 📍 시간 복잡도

1. 모든 가중치를 정렬하는데(퀵 정렬로 정렬) => O(ElogE)
2. 크루스칼 알고리즘에서 O(ElogE)보다 영향력이 있는 연산이 없다 => O(ElogE)
3. V <= E <= V^2 즉, 간선의 수는 최소 노드의 개수부터 최대 노드의 제곱 개수까지 가능하다. => 최대 시간 복잡도 O(ElogE) = O(ElogV^2) = O(2ElogV) = O(ElogV) <br>

따라서 크루스칼 알고리즘의 시간 복잡도는 **_O(ElogV)_** 이다.
