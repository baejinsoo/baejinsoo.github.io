---
title: "문자열 재정렬"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 구현"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-16
---

### 문자열 재정렬



##### 해결방법 

S를 순차적으로 확인하면서 문자와 숫자를 따로 나누고 합치는 비교적 간단했던 문제

join을 써서 리스트를 문자열로 바꿔주는 것도 필요

```python
s = input()

str_data = []
int_data = []

# print(ord('A'), ord('Z'))
for data in s:
    # 알파벳이면 str에 append
    if 65 <= ord(data) <= 90:
        str_data.append(data)
    else: # 숫자면 int에 append
        int_data.append(data)

result = str_data + int_data
# 두 배열 합친 후 리스트를 문자열로 변환 후 출력
print(''.join(result))
```

