---
title: "왕실의 나이트"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 구현"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-13
toc = true
---

#### 해결방법

나이트가 이동할 수 있는 경로를 모두 확인해서 리스트에 넣어 놓고, 

현재 위치에서 이동했을 때 8*8 판 안에 있다면 count 하는 방법으로 구현했다.

좌표를 알파벳으로 받기 때문에 `ord()` 를 사용해 알파벳을 아스키 코드 값으로 변환하여 좌표 값을 받았다.

```python
now = input()

possible_move = [(2,1), (2,-1), (-2,1), (-2,-1), (1,2), (-1,2), (1,-2), (-1,-2)]
a = 'a'
now_x = int(now[1])-1
now_y = ord(now[0]) - ord(a)

print(type(now_x),now_x, type(now_y), now_y)

result = 0
for move in possible_move:
    dx = now_x + move[0]
    dy = now_y + move[1]
    if 0 <= dx < 8 and 0<= dy < 8:
        result += 1

print(result)
```

