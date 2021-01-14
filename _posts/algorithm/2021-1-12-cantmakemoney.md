---
title: "만들수 없는 금액"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-12
---

##### 해결방법 : 2가지 방법으로 풀었다.

1. 조합을 이용해 가짓수를 구하고, 그 합들을 set에 넣고 최종 set에서 결과값 도출 하는 방법

```python
from itertools import combinations

n = int(input())
coins = list(map(int, input().split()))
result = set()

# nC1,nC2,nC3,...nCn개 의 조합으로 가능한 경우의 합을 set에 넣어감
for i in range(1, n+1):
    sum_coin = list(combinations(coins, i))
    for combi in sum_coin:
        result.add(sum(combi))
print(result)
# 1부터 (전체길이 +1) 까지 set안에 있는지 확인 없으면 출력
res = len(result) + 1
for i in range(1,len(result)+1):
    if i not in result:
        res = i
        print(res)
        break
print(result)
if res > len(result):
    print(res)
```

2.  1원부터 하나씩 금액을 만들 수 있는지 확인하며 증가해 나가는 방식

Greedy chapter의 문제이므로 이 방법이 더 올바른 방법이라고 생각한다.

```python
n = int(input())
data = list(map(int, input().split()))
data.sort()

target = 0
for x in data:
# 만들 수 없는 금액을 찾았을 때 반복 종료
	if target < x:
		break
	target += x

print(target+1)
```

#### 해설

문제의 입력 예시를 보면 data = [3, 2, 1, 1, 9] 이다.

1, 1, 2, 3, 9 순서대로 정렬 후 target의 값과 data내의 값을 비교하면서 for문을 순차적으로 확인한다.

| x  값 | target 값 | 만들 수 잇는 금액(이전 target값 +  현재x값) |
| ----- | --------- | ------------------------------------------- |
| 1     | 1         | 1                                           |
| 1     | 2         | (1+1) 1,2                                   |
| 2     | 4         | (2+2) 1,2,3,4                               |
| 3     | 7         | (4+3) 1,2,3,4,5,6,7                         |
| 9     |           |                                             |

9는 target 보다 크기 때문에 8을 만드는 것은 불가능하기 때문에 target = 8 이된다.