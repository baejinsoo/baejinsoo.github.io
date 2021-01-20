---
title: "백준 - 미로탐색"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - DFS/BFS"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-21
---

### 백준(BOJ) - 미로탐색

[BOJ](https://www.acmicpc.net/problem/2178)

##### 해결방법 

이 문제는 BFS를 이용했을 때 효과적으로 해결할 수 있다.  BFS는 시작 점에서 가까운 노드부터 차례대로 그래프의 모든 노드를 탐색하기 때문이다.

```python
from collections import deque

n, m = map(int, input().split())
maze = []
maze = [list(map(int, input())) for _ in range(n)]
# 이동방향 설정 (상,하,좌,우)
dx = [-1,1,0,0]
dy = [0,0,-1,1]


def bfs(x,y):
    q = deque()
    q.append((x,y))
    while q:
        x,y = q.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            # 범위 넘어가면 무시
            if nx < 0 or ny <0 or nx >= n or ny >= m:
                continue
            # 괴물 만나면 무시
            if maze[nx][ny] == 0:
                continue
            # 최단거리 기록
            if maze[nx][ny] == 1:
                maze[nx][ny] = maze[x][y] + 1
                q.append((nx,ny))
    return maze[-1][-1]


# 시작지점
print(bfs(0,0))

```

