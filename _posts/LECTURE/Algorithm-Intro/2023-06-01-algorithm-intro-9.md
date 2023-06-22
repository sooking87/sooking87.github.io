---
title: "Chap 08. 탐욕적 기법"
excerpt: "Chap 08. 탐욕적 기법"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1. 거스름돈 최소화 알고리즘(탐욕적 기법)

```python
# 2116313 손수경
# 1번을 해보세요!
def min_coins_greedy( coins, V ):
    count = []
    for i in range(len(coins)):
        cnt = V // coins[i]
        count.append(cnt)
        V -= cnt * coins[i]
    return count


# 2번을 해보세요!
coins = [int(i )for i in input().split()]
V = int(input())


# 출력합니다!
print("잔돈 액수 = ", V)
print("동전 종류 = ", coins)
print("동전 개수 = ", min_coins_greedy(coins, V ))


```

## 실습 2. 분할 가능한 배낭 채우기(탐욕적 기법)

```python
# 2116313 손수경
# 1번을 해보세요!
def knapSack_fractional_greedy(obj, W):
    obj.sort(key=lambda o: o[2]/o[1], reverse=True)

    totalValue = 0
    for o in obj:
        if W <= 0: break
        if W - o[1] >= 0:
            W -= o[1]
            totalValue += o[2]
        else:
            fraction = W / o[1]
            totalValue += o[2] * fraction
            W = int(W - o[1] * fraction)
    return totalValue


# 2번을 해보세요!
n = int(input())
obj = []
for _ in range(n):
    name, weight, value = input().split()
    obj.append((name, int(weight), int(value)))

W = int(input())


# 출력합니다!
print("W =", W, obj)
print(knapSack_fractional_greedy(obj,W))
```

## 실습 3. Prim의 최소비용 신장트리 알고리즘

```python
# 2116313 손수경
INF = 9999


# 1번을 해보세요!
def getMinVertex(dist, selected) :
    minv = -1
    mindist = INF
    # 코드를 추가해보세요!
    for v in range(len(dist)):
        if not selected[v] and dist[v]<mindist:
            mindist= dist[v]
            minv=v
    return minv

# 2번을 해보세요!
def MSTPrim(vertex, adj) :
    vsize=len(vertex)
    dist=[INF]*vsize
    dist[0]=0

    selected = [False] * vsize
    for i in range(vsize):
        u=getMinVertex(dist, selected)
        selected[u]=True
        print(vertex[u], end=':')
        print(dist)

        for v in range(vsize):
            if(adj[u][v] != None):
                if selected[v]==False and adj[u][v]<dist[v]:
                    dist[v]=adj[u][v]

# 3번을 해보세요!
vertex = [i for i in input().split()]
n = int(input())
weight = [[INF] * len(vertex) for _ in range(len(vertex))]
for _ in range(n):
    v1, v2, w = [m for m in input().split()]
    i = vertex.index(v1)
    j = vertex.index(v2)
    weight[i][j] = int(w)
    weight[j][i] = int(w)

print(weight)
print(vertex)

# 출력합니다!
print("MST By Prim's Algorithm")
MSTPrim(vertex, weight)
```

## 실습 4. Kruskal의 최소비용 신장트리 알고리즘

```python
# 2116313 손수경
# 서로소 집합 클래스
INF =9999
class disjointSets:
    def __init__(self, n):
        self.parent = [-1]*n       # 각 노드는 모두 루트 노드
        self.set_size = n          # 전체 집합의 개수

    def find(self, id) :         # 정점 id가 속한 집합의 대표번호 탐색
        while (self.parent[id] >= 0) :   # 부모가 있으면(-1이 아닌 동안)
            id = self.parent[id]   # id를 부모 id로 갱신
        return id            # 최종 id 반환. 루트 노드의 id임

    def union(self, s1, s2) :      # 두 집합을 병합(s1을 s2에 병합시킴)
        self.parent[s1] = s2      # s1을 s2에 병합시킴
        self.set_size = self.set_size-1   # 집합의 개수가 줄어 듦


# 1번을 해보세요!
def MSTKruskal(V, adj):
    n=len(V)
    dsets=disjointSets(n)
    E=[]

    for i in range(n-1):
        for j in range(i+1,n):
            if adj[i][j] != None:
                E.append((i,j,adj[i][j]))

    E.sort(key=lambda e:e[2])

    ecount=0
    for i in range(len(E)):
        e=E[i]
        uset=dsets.find(e[0])
        vset=dsets.find(e[1])

        if uset != vset:
            dsets.union(uset, vset)
            print("간선 추가 : (%s, %s, %d)" % (V[e[0]], V[e[1]], e[2]))
            ecount +=1
            if ecount ==n-1:
                break

# 2번을 해보세요!
vertex = [i for i in input().split()]
# print(vertex)
n = int(input())
weight = [[INF] * n for _ in range(n)]
for _ in range(n):
    v1, v2, w = [m for m in input().split()]
    i = vertex.index(v1)
    j = vertex.index(v2)
    weight[i][j] = int(w)
    weight[j][i] = int(w)

print(weight)

# 출력합니다!
print("MST By Kruskal's Algorithm")
MSTKruskal(vertex, weight)
```

## 실습 5. Dijkstra의 최단경로 알고리즘

```python
# 2116313 손수경
# 1번을 해보세요!
def shortest_path_dijkstra(vtx, adj, start) :
    vsize = len(vtx)
    dist = list(adj[start])
    dist[start] = 0
    path = [start] * vsize
    found = [False] * vsize
    found[start] = True

    for i in range(vsize):
        print("Step%2d: "%(i + 1), dist)
        u = getMinVertex(dist, found)
        found[u] = True

        for w in range(vsize):
            if not found[w]:
                if dist[u] + adj[u][w] < dist[w]:
                    dist[w] = dist[u] + adj[u][w]
                    path[w] = u

    return path


# dist 배열에서 최소 가중치를 가진 정점을 찾는 함수
def getMinVertex(dist, selected) :
    minv = -1
    mindist = INF
    for v in range(len(dist)) :					# 모든 정점들에 대해
        if not selected[v] and dist[v]<mindist :	# 선택 안 되었고
            mindist = dist[v]						# 가중치가 작으면
            minv = v								# minv 갱신
    return minv					# 최소 가중치의 정점 반환


# 2번을 해보세요!
INF = 9999
vertex = [i for i in input().split()]
n = int(input())
weight = [[INF] * len(vertex) for _ in range(len(vertex))]
cnt = 0
for k in range(n):
    v1, v2, w = [m for m in input().split()]
    i = vertex.index(v1)
    j = vertex.index(v2)
    weight[i][j] = int(w)
    weight[j][i] = int(w)

for k in range(len(vertex)):
    if k == cnt:
        weight[k][k] = 0
    cnt += 1

# print(weight)
# 출력합니다!
print("Shortest Path By Dijkstra Algorithm")
start = 0
path = shortest_path_dijkstra(vertex, weight, start)

for end in range(len(vertex)) :
    if end != start :
        print("[최단경로: %s->%s] %s" %
				(vertex[start], vertex[end], vertex[end]), end='')
        while (path[end] != start) :
            print(" <- %s" % vertex[path[end]], end='')
            end = path[end]
        print(" <- %s" % vertex[path[end]])

```

## 실습 6. 허프만 트리 생성 알고리즘

```python
# 2116313 손수경
import heapq
from queue import PriorityQueue


# 1번을 해보세요!
def make_heap_tree(freq, label):
    q = PriorityQueue()
    n = len(freq)
    ㅗ = []
    for i in range(n):
        q.put((freq[i], label[i]))
    for i in range(1, n):
        e1 = q.get()
        e2 = q.get()
        q.put((e1[0] + e2[0], e1[1] + e2[1]))
        print(e1, '+', e2)
    print(q.get())


# 2번을 해보세요!
label = [i for i in input().split()]
freq  = [int(i) for i in input().split()]


# 출력합니다!
make_heap_tree(freq, label)
```
