---
title: "백준 - 카드 정렬하기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 정렬"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-23
---

### 백준(BOJ) - 카드 정렬하기

[BOJ](https://www.acmicpc.net/problem/1715)

##### 해결방법 

이 문제의 핵심은 항상 가장 작은 두 카드 묶음을 합쳐가면서 결과를 찾는 것 이다.

이 해법을 찾으려고 문제를 이해하는 것도 꽤 애먹었다. 

가장 작은 크기의 수를 효과적으로 찾을 수 있는 자료구조는 우선순위 큐를 사용하는 것이고 파이썬에 내장되어있는 `heapq`를 사용하면 된다.

```python
import heapq

n = int(input())
cards = []
for _ in range(n):
    heapq.heappush(cards, int(input()))

result = 0

while len(cards) != 1:
    a = heapq.heappop(cards)
    b = heapq.heappop(cards)
    result += (a+b)
    heapq.heappush(cards, (a+b))

print(result)
```



아래는 heapq를 사용하지 않고 함수로 매차례마다 `sort()`함수를 써서 런타임 에러를 발견한 실패한 코드이다. 

```python
n = int(input())
cards = []
for _ in range(n):
    cards.append(int(input()))

total = 0
def cal(cards):
    global total
    # print(cards, total)
    if len(cards) == 1:
        return cards
    cards.sort()
    cards.append(cards[0] + cards[1])
    total += (cards[0] + cards[1])
    cards.remove(cards[0])
    cards.remove(cards[0])
    cal(cards)

cal(cards)
print(total)
```

