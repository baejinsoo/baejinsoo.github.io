---
title: "팀 결성"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-06
---

### 이코테 - 팀 결성

> 문제유형 : 그래프

##### 해결방법 

이 문제는 서로소 집합 알고리즘을 이용하면 해결할 수 있다.

0 일때는 `union()` 연산을 하고

1 일때는 `find_parent()`연산을 통해 parent가 같은 값인지 확인하고 결과 값을 출력하면 된다.

```
입력예시)
7 8
0 1 3
1 1 7
0 7 6
1 7 1
0 3 7
0 4 2
0 1 1
1 1 1
```

```python
import sys
input = sys.stdin.readline

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

def find_parent(parent, a):
    if parent[a] != a:
        parent[a] = find_parent(parent, parent[a])
    return parent[a]


n, m = map(int, input().split())
parent = [0] * (n + 1)

for i in range(1, n+1):
    parent[i] = i

for i in range(m):
    check, a, b = map(int, input().split())
    if check == 0:
        union_parent(parent, a, b)
    elif check == 1:
        if find_parent(parent, a) != find_parent(parent, b):
            print("NO")
        else:
            print("YES")

```