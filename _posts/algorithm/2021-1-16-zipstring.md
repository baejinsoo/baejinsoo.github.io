---
title: "프로그래머스 - 문자열 압축"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-16
---

### 프로그래머스(kakao 2019) - 문자열 압축

https://programmers.co.kr/learn/courses/30/lessons/60057

##### 해결방법 

요구사항을 하나씩 이행해서 구현하면 풀리는 문제

입력으로 주어지는 문자열의 길이가 1,000 이하이므로 가능한 모든 경우의 수를 탐색하는 완전 탐색 방법으로 수행하면 된다.

문자열을 자를 수 있는 최대의 크기는 문자열/2 이고,

나머지는 요구사항에 맞춰서 배열을 인덱스별로 나타내기만 하면 되는 문제

```python
def solution(s):
    answer = len(s)
    check_size = int(len(s)/2)+1
    for i in range(1,check_size):
        count = 1
        len_check = []
        times = 0
        for j in range(i,len(s),i):
            times += 1
            if  s[j-i:j] == s[j:j+i]:
                count += 1
                if (len(s)-1) // i == times:
                    len_check.append(str(count))
                    len_check.append(s[j:j+i])
                    count = 1
            elif count == 1 and s[j:j+i] != s[j-i:j]:
                len_check.append(s[j-i:j])
                if (len(s)-1) // i == times:
                    len_check.append(s[j:j+i])
            elif count > 1 and s[j:j+i] != s[j-i:j]:
                len_check.append(str(count))
                len_check.append(s[j-i:j])
                count = 1
                if (len(s)-1) // i == times:
                    len_check.append(s[j:j+i])
        res = "".join(len_check)
        answer = min(answer, len(res))
    return answer
```

