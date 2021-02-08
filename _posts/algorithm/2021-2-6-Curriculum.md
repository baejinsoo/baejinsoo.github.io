---
title: "커리큘럼"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 그래프"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-06

---

### 이코테 - 커리큘럼

> 문제유형 : 그래프

##### 해결방법 

이 문제는 위상 정렬 알고리즘을 사용해서 해결할 수 있다.

입력받는 강의에 대해 수강하기까지 걸리는 시간을 출력해야 한다.

이 때 시간을 비교해서 입력받기 위해 time 리스트를 초기에 `deepcopy()`함수를 사용해야한다.

선수과목이 없는 과목부터 차례대로 진행하면 된다.

```
입력예시)
5
10 -1
10 1 -1
4 1 -1
4 3 1 -1
3 3 -1
```

```python
import sys
from collections import deque
import copy
input = sys.stdin.readline

n = int(input())

indegree = [0] * (n+1)
time = [0] * (n+1)
graph = [[] for _ in range(n+1)]

for i in range(1, n+1):
    data = list(map(int, input().split()))
    time[i] = data[0]
    for x in data[1:-1]:
        indegree[i] += 1
        graph[x].append(i)

def topology_sort():
    global time
    result = copy.deepcopy(time)
    q = deque()

    for i in range(1, n + 1):
        if indegree[i] == 0:
            q.append(i)
    
    while q:
        now = q.popleft()
        for i in graph[now]:
            result[i] = max(result[i], result[now] + time[i])
            indegree[i] -= 1
            if indegree[i] == 0:
                q.append(i)
    
    for i in range(1, n + 1):
        print(result[i])

topology_sort()
```