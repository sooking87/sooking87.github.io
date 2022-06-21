---
title: "[JAVA] BFS"
excerpt: "BFS"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 BFS

BFS란 Breadth First Search의 의미로 낮은 레발에서 시작해 왼쪽에서 오른쪽 방향으로 검색하고 한 레벨에서의 검색이 끝나면 다음 레벨로 넘어가서 다시 순회를 하는 방식이다. 

### 📍 특징

- 재귀를 사용하지 않는다. 
- DFS의 경우는 스택을 사용하였지만 BFS의 경우는 큐를 사용한다. 
- 노드의 수가 적고 깊이가 얕은 경우 빠르게 동작한다. 
- DFS와 달리 저장공간이 많이 필요하다. 
- 두 노드 사이의 최단 경로 또는 임의의 경로를 찾고 싶을 때 사용된다. 예를 들면 미로 문제 같은 경우,,

### 📍 알고리즘

1. 시작 노드 -> 큐 삽입 && 방문 처리
2. 큐에서 노드를 꺼냄 -> 방문하지 않은 인접 노드를 모든 큐에 삽입 && 방문 처리
3. 모든 노드가 큐에 EnQueue되고 DeQueue 될 때까지 2번 과정 반복

### 📍 큐로 구현

```java
package BFS;

import java.util.Iterator;
import java.util.LinkedList;
import java.util.Queue;

class BFSDemo {
    private int n; // 노드의 개수
    private LinkedList<Integer> adj[]; // 인접 리스트

    BFSDemo(int size) {
        n = size;
        adj = new LinkedList[size];
        for (int i = 0; i < size; ++i)
            adj[i] = new LinkedList();
    }

    // 노드 연결
    void addEdge(int v, int w) {
        adj[v].add(w);
        adj[w].add(v);
    }

    // root를 시작 노드로 BFS로 탐색하면서 탐색한 노드를 출력
    void BFS(int root) {
        boolean visited[] = new boolean[n];
        Queue<Integer> queue = new LinkedList<>(); // BFS를 위한 큐 생성

        // 1. 루트 노드를 방문하면서 BFS 시작
        visited[root] = true;
        queue.add(root);

        // 2. 모든 노드가 큐에 삽입 && 삭제 될 때까지 반복
        while (!queue.isEmpty()) {
            root = queue.poll(); // DeQueue
            System.out.print(root + 1 + " ");

            Iterator<Integer> i = adj[root].listIterator();
            while (i.hasNext()) {
                int n = i.next();

                // 다음 노드가 방문하지 않은 노드라면
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }

    public static void main(String args[]) {
        BFSDemo g = new BFSDemo(8);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 7);
        g.addEdge(2, 3);
        g.addEdge(2, 4);
        g.addEdge(5, 7);
        g.addEdge(6, 7);

        g.BFS(0);
    }
}
```

