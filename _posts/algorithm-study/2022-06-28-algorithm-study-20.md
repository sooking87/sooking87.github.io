---
title: "[JAVA] 프림 알고리즘"
excerpt: "프림 알고리즘"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

# 최소 신장 트리

최소 신장 트리는 Minimun Spanning Tree(MST)로서 그래프의 모든 꼭짓점을 노드로 포함하면서 노드 간의 비용을 최소로 하는 트리를 말하며, 이를 유도하기 위해서 크루스칼 알고리즘이나 프림 알고리즘을 사용한다.

# 프림 알고리즘

1. 각 인접한 정점들 중 최소 비용으로 이동 가능한 정점을 선택하여 추가한다.
2. 우선 순위 큐를 이용하여 임의의 정점부터 인접한 정점 거리를 기준으로 정렬한다.
3. 최소 거리의 정점을 꺼내서 다시 인접한 정점을 넣고 정렬한다.

## 📍 알고리즘

```java
package Prim;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class primAlgo {

    static int V;
    static int E;
    public static ArrayList<Node>[] nodeList; // 연결리스트
    public static int finalCost = 0;
    public static boolean[] visited;

    public static void main(String args[]) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        V = Integer.parseInt(st.nextToken()); // 정점 개수 입력
        E = Integer.parseInt(st.nextToken()); // 간선 개수 입력

        visited = new boolean[6 + 1]; // 1로 인덱스 맞추기 위함
        Arrays.fill(visited, false); // 방문여부 초기화

        nodeList = new ArrayList[6 + 1];
        for (int i = 1; i < 7; i++) { // 연결리스트 초기화
            nodeList[i] = new ArrayList<Node>();
        }

        // 연결리스트에 간선과 비용 설정
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());

            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            // 인접 리스트
            nodeList[start].add(new Node(start, end, cost));
            nodeList[end].add(new Node(start, end, cost));
        }

        prim(1); // 시작 정점 1
    }

    public static void prim(int p) {
        PriorityQueue<Node> pq = new PriorityQueue<Node>(); // 비용을 오름차순으로 정렬하는 Queue
        Queue<Integer> q = new LinkedList<>();

        // 시작노드
        q.offer(p);

        while (!q.isEmpty()) {
            int node = q.poll();
            visited[node] = true;

            // node에 연결된 정점들에 대한 정보 중에서
            // 방문하지 않은 Node를 pq에 담는다.
            for (Node n : nodeList[node]) {
                // 종료노드
                if (!visited[n.end]) {
                    pq.add(n);
                }
            }

            // pq에 담긴 정보들을 순차적으로 mst에 담는다.
            while (!pq.isEmpty()) {
                Node e = pq.poll();

                if (!visited[e.end]) {
                    q.add(e.end);
                    visited[e.end] = true;
                    finalCost += e.cost;
                    break;
                }
            }
        }
        System.out.println(finalCost);
    }
}

class Node implements Comparable<Node> {
    int start; // 시작 정점
    int end; // 종료 정점
    int cost; // 비용

    Node(int start, int end, int cost) {
        this.start = start;
        this.end = end;
        this.cost = cost;
    }

    // 비용으로 오름차순 정렬하기 위한 Comparable method
    @Override
    public int compareTo(Node node) {
        return node.cost >= this.cost ? -1 : 1;
    }
}
```
