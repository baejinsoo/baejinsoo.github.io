---
title: "부품찾기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 이진 탐색"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-25
---

### 부품찾기

##### 해결방법 

이 문제는 이진탐색 알고리즘을 알고있으면 쉽게 풀 수 있는 문제다.

```python
n = int(input())
have = list(map(int, input().split()))

m = int(input())
needs = list(map(int, input().split()))


def check(val, have, start, end):
    while start <= end:
        mid = (start + end) // 2
        if have[mid] == val:
            return True
        elif val < have[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return False


have.sort() # 이진탐색 하기위해 정렬
for need in needs:
    if check(need, have, 0, len(have)):
        print("yes")
    else:
        print("no")

```



##### set()을  이용한 방법

```python
N = 5
parts = [8, 3, 7, 9, 2]
parts = set(all_parts)

M = 3
orders = [5,7,9]

for order in orders:
    if order in parts:
        print('yes', end=" ")
    else:
        print('no', end=" ")
```

