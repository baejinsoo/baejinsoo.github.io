---
title: "여행 계획"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-08
---

### 이코테 - 여행계획

> 문제유형 : 그래프

##### 해결방법 

이 문제는 서로소 집합 알고리즘을 이용하면 해결할 수 있다.

- 입력으로 받은 노드가 모두 같은 집합에 속하는지 parent를 찾아서 체크해주면 정답 판정을 받을 수 있다.

```
입력예시)
5 4
0 1 0 1 1
1 0 1 1 0
0 1 0 0 0
1 1 0 0 0
1 0 0 0 0
2 3 4 3
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

travel = []
for i in range(n):
    arr = list(map(int, input().split()))
    travel.append(arr)

result = list(map(int, input().split()))

parent = [i for i in range(n)]

for i in range(n):
    for j in range(n):
        if travel[i][j] == 1:
            union_parent(parent, i, j)

temp = parent[result[0] - 1]
answer = "YES"
for res in result:
    if parent[res-1] == temp:
        continue
    else:
        answer = "NO"
        break

print(answer)

```