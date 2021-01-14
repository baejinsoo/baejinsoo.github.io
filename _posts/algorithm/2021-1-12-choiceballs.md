---
title: "볼링공 고르기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-12
---

##### 해결방법 : 2가지 방법으로 풀었다.

1. 볼링들 중 2개를 뽑을 수 있는 조합을 모두 구한 후 중복값을 제거해준다.

```python
from itertools import combinations

n, m = map(int, input().split())
balls = list(map(int, input().split()))

# 2개를 뽑는 조합 수 구하기
result = list(combinations(balls, 2))

# 중복되는 무게가 있다면 count
for i in range(1,m+1):
    if balls.count(i) > 1:
        count += result.count((i,i))
# 갯수 출력      
print(len(result)-count)
```



2. A가 특정한 무게의 공을 뽑았을 때, B가 뽑을 수 있는 공의 갯수를 비교하며 해결

```python
n, m = map(int, input().split())
data = list(map(int, input().split()))
# 1부터 10 까지의 무게를 담을 수 있는 리스트(문제에서 공의 무게는 1~10까지로 정의)
array = [0] * 11

for x in data:
    array[x] += 1

result = 0
# 1부터 m까지의 각 무게에 대하여 처리
for i in range(1, m+1):
    n -= array[i]
    result += array[i] * n
print(result)
```


