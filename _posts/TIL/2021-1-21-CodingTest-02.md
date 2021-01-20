---
title: "코딩테스트를 준비하면서..(2)"
excerpt: "알아두면 좋은 Tip"
categories:
  - Python
last_modified_at: 2021-01-21
toc: true
toc: true
toc_sticky: true
---

## 🤞코딩테스트를 준비하면서..(2)

이번에는 알아두면 도움이 되는 순열, 조합, 빈도계산, 덱에 대해 정리해두었다.

이 방법들을 몰랐을 때는 직접 구현하면서 시간을 많이 잡아먹었던 기억이 있다..



#### 조합, 순열

##### 조합 (nCr)

n까지의 수 중에서 `중복을 제외한` r개를 고르는 수열

```python
from itertools import combinations

data = [1, 2, 3, 4, 5, 6]
print(list(combinations(data, 2))) # nC2
print(list(combinations(data, 3))) # nC3
```

```
[(1, 2, 3), (1, 2, 4), (1, 3, 4), (2, 3, 4)]
```

##### 순열 (nPr)

```python
from itertools import permutations

data = [1, 2, 3, 4]
print(list(permutations(data, 2))) # nP2
```

```
[(1, 2), (1, 3), (1, 4), (2, 1), (2, 3), (2, 4), (3, 1), (3, 2), (3, 4), (4, 1), (4, 2), (4, 3)]
```



#### 빈도계산

```
data = [1,1,1,2,2,5,5,5,5,5,3]
```

위 처럼 리스트에 다양한 값들이 들어있을 때, 각 값들이 몇개씩 있는지 확인하기 위해서 우리는 `Counter`를 사용할 수 있다.

```python
from collections import Counter

data = [1,1,1,2,2,5,5,5,5,5,3]
result = Counter(data).most_common()
```

```
[(5, 5), (1, 3), (2, 2), (3, 1)]
```



#### 힙

##### 최소힙

`heap` 을 import해 사용하게 되면, 최솟값이 0번 인덱스, 즉 이진트리의 루트 값으로 들어가는 것을 볼 수 있다.

```python
import heapq

heap = []
heapq.heappush(heap, 3)  
heapq.heappush(heap, 1)  
heapq.heappush(heap, 4)  
heapq.heappush(heap, 5)  
heapq.heappush(heap, 2)
print(heap)

print(heapq.heappop(heap))
```

```
[1, 2, 4, 5, 3]
1
```



#### 덱 (deque)

덱은 데크 라고도 하며, 양방향에서 데이터를 처리할 수 있다.

기업 코딩테스트에서 자주 출제되는 유형인 bfs 문제를 풀때도 deque를 사용하면 쉽게 해결할 수 있다.

```python
from collections import deque

data = [1, 2, 4, 5, 3]
q = deque(data)

q.append(7) # [1, 2, 4, 5, 3, 7]
q.appendleft(8) # [8, 1, 2, 4, 5, 3, 7]
q.pop() # [8, 1, 2, 4, 5, 3]
q.popleft() # [1, 2, 4, 5, 3]
```



#### (+) 시간 측정

프로그래머스에서 문제를 풀다보면 효율성 테스트가 있는데, 이때 시간을 고려하면서 문제를 풀어야 한다. 나는 보통 문제를 풀때 `VScode` 환경에서 푸는데 실행시간이 얼마나 나오는지 궁금해서 알아보았다.

```python
# 시간 측정
import timeit
start = timeit.default_timer()
end = timeit.default_timer()
print("min len 측정     %f초 걸렸습니다." % (end - start))
```



