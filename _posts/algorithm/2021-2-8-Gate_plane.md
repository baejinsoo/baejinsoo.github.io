---
title: "탑승구"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-08
---

### 이코테 - 탑승구

> 문제유형 : 그래프

##### 해결방법 

이 문제는 n = 100,000 이므로 O(n^2)로는 풀수 없다.

서로소 집합 알고리즘을 이용하면 효율적으로 해결할 수 있다.

- 비행기 번호를 받으면 해당 번호의  parent 노드를 찾는다
- parent 노드와 parent노드 -1을 union() 연산을 한다.
- parent 노드가 0 이라면 도킹이 불가능한 경우로 현재까지 도킹된 결과를 출력한다.

```
입력예시)
4
6
2
2
3
3
4
4
```

```python
G = int(input())
P = int(input())
datas = []
for _ in range(P):
    datas.append(int(input()))

def find(parent, x):
    if parent[x] != x:
        parent[x] = find(parent, parent[x])
    return parent[x]

def union(parent, a, b):
    a = find(parent, a)
    b = find(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

parent = [i for i in range(G+1)]
count = 0
for data in datas:
    root = find(parent, data)
    if root == 0:
        break
    else:
        union(parent, root-1, root)
        count += 1

print(count)
```