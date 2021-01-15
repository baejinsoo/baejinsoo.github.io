---
title: "BAEKJOON - 럭키 스트레이트"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-16

---

### BAEKJOON - 럭키 스트레이트

https://www.acmicpc.net/problem/18406



##### 해결방법 

S를 반으로 나누고 앞과 뒤의 합을 구해서 비교하는 간단한 문제

```python
n = int(input())

# 인덱스로 나눠서 확인하기 위해 int -> string
n = str(n)
front_sum = 0
back_sum = 0
for i in range(len(n)):
    if i < len(n)/2:
        front_sum += int(n[i])
    else:
        back_sum += int(n[i])

if front_sum == back_sum:
    print("LUCKY")
else:
    print("READY")
```

