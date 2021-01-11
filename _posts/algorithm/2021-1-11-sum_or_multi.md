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

