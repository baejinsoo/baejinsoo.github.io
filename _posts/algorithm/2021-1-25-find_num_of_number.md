---
title: "정렬된 배열에서 특정 수의 개수 구하기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 이진 탐색"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-25
---

### 정렬된 배열에서 특정 수의 개수 구하기

##### 해결방법 

해당하는 특정 수를 찾은 후 왼쪽 오른쪽 인덱스를 비교하면서 몇개인지 확인하면 된다.

```python
n, x = map(int, input().split())
sorting = list(map(int, input().split()))

def search(sorting, val, start, end):
    while start < end:
        mid = (start + end) // 2
        print(mid)
        if sorting[mid] == val:
            return mid
        elif val < sorting[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return False

result = search(sorting, x, 0, len(sorting))
if result == False:
    print(-1)

else:
    left = 0
    left = result
    right = 0
    right = result
    while sorting[left] == x:
        left -= 1
    while sorting[right] == x:
        right += 1
    print(right - left - 1)
```



##### 파이썬에 내장된 `bisect`를 사용해서 푸는 방법

파이썬으로 코딩테스트를 준비하면서 느끼는 거지만, 정말 이점이 많은 것 같다고 다시한번 느낄수 있었다.

[python - bisect](https://docs.python.org/ko/3/library/bisect.html)

```python
n, x = map(int, input().split())
array = list(map(int, input().split()))

def count_by(array, left, right):
    right = bisect_right(array, right)
    left = bisect_left(array, left)
    return right - left

count = count_by(array, x, x)

if count == 0:
    print(-1)
else:
    print(count)
```