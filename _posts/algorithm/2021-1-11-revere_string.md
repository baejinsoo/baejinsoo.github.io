---
title: "문자열 뒤집기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-11
---

##### 해결방법

- 1로 만들때의 횟수, 0으로 만들때의 횟수를 각각 구해서 둘 중 최소값을 출력

- 중복된 값 제거후 리스트에 추가

- 1로 만드는 경우에는 리스트 값이 0이면 +1

  0으로 만드는 경우에는 리스트 값이 1이면 +1

  두 결과값 중 작은 값 출력

```python
s = input()

make_1 = 0
make_0 = 0

list_1 = []
list_0 = []

# 1로 만들때 횟수 구하기
for i in range(len(s)):
    if i == 0:
        list_1.append(int(s[i]))
    else:
        if int(s[i-1]) != int(s[i]):
            list_1.append(int(s[i]))
for num in list_1:
    if num == 0:
        make_1 += 1
# 0으로 반들때 횟수 구하기
for i in range(len(s)):
    if i == 0:
        list_0.append(int(s[i]))
    else:
        if int(s[i-1]) != int(s[i]):
            list_0.append(int(s[i]))
for num in list_0:
    if num == 1:
        make_0 += 1
# 둘중 최소값 출력
print(min(make_0, make_1))
```

