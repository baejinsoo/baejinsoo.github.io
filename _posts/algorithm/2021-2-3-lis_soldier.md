---
title: "병사 배치하기"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 다이나믹 프로그래밍"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-02-02
---

### 병사 배치하기

#### 문제 설명

>전투력이 높은 병사가 앞쪽에 오도록 내림차순으로 배치를 하는 문제이다.

##### 해결방법 

>  LIS(Longest Increaing Subsequence) 최장 증가 부분 수열 알고리즘으로 풀 수 있다.

```python
n = int(input())
sol = list(map(int, input().split()))

dp = [1] * n

for i in range(1, n):
    for j in range(i):
        if sol[j] > sol[i]:
            dp[i] = max(dp[i], dp[j]+1)

print(n - max(dp))
```

