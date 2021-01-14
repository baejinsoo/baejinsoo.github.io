---
title: "곱하기 혹은 더하기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-11
---

##### 해결방법

- 문자열을 순서대로 확인함
- 곱해서 0 이 되면 더함
- 그 외의 값은 곱함

```python
s = input()

result = 0
for text in s:
    if result * int(text) == 0:
        result += int(text)
    else:
        result *= int(text)

print(result)
```

##### 코드 수정

코딩 테스트 스터디를 진행하면서 

0일때만 더하는게 아니라 1일 경우에도 더해야하는 사실을 간과한 것을 확인 후 코드수정

```python
s = input()

result = 0
for text in s:
    if result * int(text) == 0 or result * int(text) == 1 or text == 1:
        result += int(text)
    else:
        result *= int(text)

print(result)
```

