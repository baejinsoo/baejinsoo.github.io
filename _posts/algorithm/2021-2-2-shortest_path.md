---
title: "최단 경로 (Shortest Path)"
excerpt: "최단 경로 알고리즘"
categories:
  - 알고리즘
last_modified_at: 2021-02-02
---

## 최단 경로 (Shortest Path)

최단 경로 알고리즘은 말 그대로 가장 짧은 경로를 찾는 알고리즘이다.

다양한 종류가 있는데, 상황에 맞는 효율적인 알고리즘이 이미 정립되어 있다.

최단 경로 알고리즘은 보통 그래프로 표현하는데 각 지점은 그래프에서 `노드` 로 표현되고, 지점 간의 연결된 도로는 그래프에서 `간선`으로 표시된다.

최단 경로 알고리즘은 크게 3종류가 있다.

> - 다익스트라 알고리즘
> - 플로이드 워셜 알고리즘
> - 벨만 포드 알고리즘



#### 다익스트라 알고리즘 (Dijkstra)

> 다익스트라 알고리즘은 그래프에서 여러 개의 노드가 있을 때, 특정한 노드에서 출발하여 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘이다.
>
> 다익스트라 알고리즘은 '음의 간선'이 없을 때 정상적으로 동작한다.
>
> 기본적으로 **그리디 알고리즘**으로 분류된다.

##### 원리

1. 출발 노드를 설정한다.
2. 최단 거리 테이블을 초기화한다.
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다.
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
5. 위 과정에서 *3번*과 *4번*을 반복한다.

> 최단 경로를 구하는 과정에서 각 노드에 대한 현재까지의 최단 거리 정보를 항상 1차원 리스트(*최단 거리 테이블*)에 저장하면서 리스트를 계속 갱신한다는 특징이 있다. 



##### 방법1. 간단한 다익스트라 알고리즘

이 방법은 O(n^2)의 시간 복잡도를 가진다.

처음에 각 노드에 대한 최단 거리를 담는 1차원 리스트를 선언하고, 이후에 단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 매 단계마다 1차원 리스트으 ㅣ모든 원소를 확인(*순차 탐색*)한다.

```python
import sys
input = sys.stdin.readline
INF = int(le9)

# 노드의 개수, 간선의 개수 입력받기
n, m= map(int, input().split())
# 시작 노드 번호 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 생성
graph = [[] for i in range(n+1)]
# 방문한 적 있는지 체크하는 목적의 리스트 생성
visited = [[False] * (n+1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a,b,c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append(b,c)

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = 1
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    for i in range(n-1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른노드를 학인
        for j in graph[now]:
            cost = distance[now] + j[i]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost

dijkstra(start)

for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한(INFINITY)라고 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])

```

##### 방법2. 개선된 다익스트라 알고리즘

이 방법으로 구현하게 되면 시간 복잡도는 O(Elogn)을 보장할 수 있다. (E: 간선의 개수, n: 노드의 개수)

개선된 방법은 힙 자료구조를 사용한다.

힙 자료구조를 사용하게 되면 특정 노드까지의 최단 거리에 대한 정보를 힙에 담아서 처리하므로 출발 노드로부터 가장 거리가 짧은 노드를 더욱 빠르게 찾을 수 있다.

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INF")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```



#### 플로이드 워셜 알고리즘 (Floyd-Warshall)

> 다익스트라 알고리즘은 **한 지점에서 다른 특정 지점까지의 최단 경로**를 구해야 하는 경우에 사용하는 알고리즘이다.
>
> 플로이드 워셜 알고리즘 (Floyd Warshall)은 **모든 지점에서 다른 모든 지점까지의 최단 경로**를 모두 구해야 하는 경우에 사용할 수 있는 알고리즘이다.



노드의 개수가 n 개 일 때, 알고리즘 상으로 n번의 단계를 수행하며, 단계마다 O(n^2)의 연산을 통해 현재 노드를 거쳐 가는 모든 경로를 고려한다. 따라서 이 알고리즘의 시간 복잡도는 O(n^3)이다.

다익스트라 알고리즘과 다르게 모든 노드에 대하여 다른 모든 노드로 가는 정보를 담아야 하기 때문에 최단 거리 정보 저장에 2차원 리스트에 저장한다.

##### 플로이드 워셜 알고리즘 파이썬 코드

```python
INF = int(1e9)

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
        if graph[a][b] == 1e9:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()
```

