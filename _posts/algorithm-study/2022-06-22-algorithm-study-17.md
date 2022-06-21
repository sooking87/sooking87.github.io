---
title: "[JAVA] DFS"
excerpt: "DFS"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 DFS

DFS란 Depth First Search(깊이 우선 탐색)이라는 의미로 높이를 우선적으로 최대한 깊에 탐색하는 것을 의미한다. <br>

![Depth-First-Search](https://user-images.githubusercontent.com/96654391/174769534-fda71274-8c74-4bfc-a445-dcc93f0c0c5b.gif)

### 📍 특징

- 깊이 우선 탐색이 너비 우선 탐색보다 좀 더 간단하다. 
- 단순 검색 속도 자체는 너비 우선 탐색에 비해서 느리다. 

### 📍 스택을 사용한 DFS

```java
package DFS;

import java.util.Stack;

public class DFSStack {
    public static void dfs() {
        Stack<Integer> stack = new Stack<>();
        boolean[] visited;

        stack.push(V); // 시작 노드 push
        visited[V] = true;

        while (!stack.isEmpty()) {
            int n = stack.peek();
            boolean flag = false;

            if (!visited[node]) {
                stack.push(node);
                visited[node] = true; // 방문 처리
                flag = true;
                break;
            }
        }
        // 방문하지 않은 노드가 하나도 없다면.
        if (!flag) {
            stack.pop();
        }
    }
}
```
물론 변수가 선언 안된 것도 있지만 여튼 얘기하고자 하는 바는 방문하지 않았던 노드에 대해서 방문 후에는 해당 값을 push해주고 visited 배열을 true로 바꾸어준다. 

### 📍 재귀 함수로 구현

- 인접 행렬: O(n^2) <br>
    인접 행렬이란 인접해 있는 노드들인 경우 1, 아닌 경우 0을 가진 2차원 리스트이다. 
    ```java
    static int[][] gragh;	    // 그래프를 표현하기 위해 인접행렬
	static boolean[] visited; // 방문한 정점을 표현 (하지만 인덱스로 접근하므로 -1 고려)
	// static int[] visited;로 표현하기도 함
	
	// dfs 메소드
	static void dfs(int node) {
		visited[node] = true; // 
		for (int i=0; i<gragh[node].length; i++) { // gragh[node].length = 정점 	
			// 간선이 존재하고 방문하지 않은 정점이라면, 함수 호출 = 방문한다
			if (gragh[node][i] == 1 && visited[i] == false) { 
				dfs(i);	
		    }
	    }
    }
    ```
- 인접 리스트: O(n + e) <br>
    ![Untitled](https://user-images.githubusercontent.com/96654391/174775501-59a1af43-2fe5-4422-b281-cab0ef630d74.png)
    ```java
    public class DFS {
        static ArrayList<Integer> nodeList;	// 그래프를 표현하기 위해 인접리스트  
        static boolean[] visited; 
        
        static void dfs(int node)
        visited[node] = true;
        for (int i=0; i < nodeList[node].size(); i++) { // x에 있는 정점의 개수만큼 반복
            int nextNode = nodeList[node].get(i); // 간선에 연결된 다음 정점
            if (!check[nextNode]) { // 방문하지 않았으면 (간선이 존재하는지 체크하지 않아도 됨)
                dfs(nextNode);
            }
        }
    }
    ```