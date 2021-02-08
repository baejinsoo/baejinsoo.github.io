---
title: "도시 분할 계획"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-06

---

### 이코테 - 도시 분할 계획

> 문제유형 : 그래프

##### 해결방법 

이 문제는 최소 신장 트리를 2개로 만드는 문제이다.

방법은 최소 신장 트리를 만든 후, 구성하는 간선 중에서 비용이 가장 큰 간선의 값을 빼주면 된다.

나는 가장 큰 간선의 값을 빼주지않고, n개의 최소신장 트리를 구하는데 간선의 갯수는 n -1개가 필요하므로 n-1전까지 트리를 구성해서 해결하였다.

```
입력예시)
7 12
1 2 3
1 3 2
3 2 1
2 5 2
3 4 4
7 3 6
5 1 5
1 6 2
6 4 1
6 5 3
4 5 3
6 7 4
```

```python
import sys
input = sys.stdin.readline

def find_parent(parent, a):
    if parent[a] != a:
        parent[a] = find_parent(parent, parent[a])
    return parent[a]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

n, m = map(int, input().split())
parent = [i for i in range(n+1)]

citys = []
for i in range(m):
    a, b, cost = map(int, input().split())
    citys.append((cost, a, b))

citys.sort()
res = 0
cnt = 1
for city in citys:
    cost, a, b = city
    if cnt == n - 1:
        break
    if find_parent(parent,a) != find_parent(parent,b):
        union_parent(parent, a, b)
        res += cost
        cnt += 1

print(res)
# print(parent)
```