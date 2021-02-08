---
title: "어두운 길"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-08
---

### 이코테 - 어두운길

> 문제유형 : 그래프

##### 해결방법 

이 문제는 크루스칼 알고리즘을 사용해서 최소 신장 트리를 만들어 풀면 간단하게 해결할 수 있다.

그래프 문제는 크게 크루스칼 알고리즘과 위상정렬 알고리즘으로 이루어져 있으므로 쉽게 구현할 수 있게 코드를 확실히 이해하고 외워두는 것이 좋다.

```
입력 예시)
7 11
0 1 7
0 3 5
1 2 8
1 3 9
1 4 7
2 4 5
3 4 15
3 5 6
4 5 8
4 6 9
5 6 11
```

```python
import sys
input = sys.stdin.readline


def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

n, m = map(int, input().split())
parent = [i for i in range(n)]

roads = []
for i in range(m):
    a, b, cost = map(int, input().split())
    roads.append((cost, a, b))

roads.sort()
result = 0
total = 0
for road in roads:
    cost, a, b = road
    total += cost
    if find_parent(parent, a) != find_parent(parent, b):
        result += cost
        union_parent(parent, a, b)

print(total - result)

```