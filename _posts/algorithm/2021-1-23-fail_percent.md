---
title: "프로그래머스 - 실패율"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 정렬"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-23
---

### 프로그래머스(Kakao 2020)- 실패율

[프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42889)

##### 해결방법 

이 문제는 정렬을 사용한 구현 유형의 문제라고 볼 수 있다.

각 스테이지의 실패율을 구하기 위해서 각 스테이지에서 몇 명이  실패했는지 찾기 위해 `Counter`를 사용하였다.

각 스테이지마다 실패율을 구한다음엔 ` result.sort(key=lambda x: -x[1])`를 써서 정렬하면 된다.

```python
from collections import Counter

def solution(N, stages):
    stages.sort()

    counter = Counter(stages).most_common()
    counter.sort()
    print(counter)

    size_stages = len(stages)
    result = []

    for i in range(1,N+1):
        result.append((i,0))

    for c in counter:
        if c[0] > N:
            break
        result.remove((c[0], 0))
        result.append((c[0], c[1]/size_stages))
        size_stages -= c[1]

    result.sort(key=lambda x: -x[1])
    fin = []
    for re in result:
        fin.append(re[0])
    return fin
```



##### 실행결과

```
테스트 1 〉	통과 (0.05ms, 10.2MB)
테스트 2 〉	통과 (0.20ms, 10.2MB)
테스트 3 〉	통과 (2.60ms, 10.6MB)
테스트 4 〉	통과 (14.50ms, 11.2MB)
테스트 5 〉	통과 (39.33ms, 15.6MB)
테스트 6 〉	통과 (0.31ms, 10.2MB)
테스트 7 〉	통과 (3.64ms, 10.3MB)
테스트 8 〉	통과 (14.51ms, 11.2MB)
테스트 9 〉	통과 (38.81ms, 15.7MB)
테스트 10 〉	통과 (12.91ms, 11.3MB)
테스트 11 〉	통과 (13.47ms, 11.2MB)
테스트 12 〉	통과 (18.41ms, 11.9MB)
테스트 13 〉	통과 (21.71ms, 12MB)
테스트 14 〉	통과 (0.06ms, 10.2MB)
테스트 15 〉	통과 (5.92ms, 10.6MB)
테스트 16 〉	통과 (3.42ms, 10.4MB)
테스트 17 〉	통과 (5.90ms, 10.6MB)
테스트 18 〉	통과 (3.12ms, 10.4MB)
테스트 19 〉	통과 (1.02ms, 10.2MB)
테스트 20 〉	통과 (4.96ms, 10.5MB)
테스트 21 〉	통과 (8.46ms, 11MB)
테스트 22 〉	통과 (14.88ms, 18.1MB)
테스트 23 〉	통과 (14.92ms, 12.1MB)
테스트 24 〉	통과 (21.64ms, 12.3MB)
테스트 25 〉	통과 (0.04ms, 10.2MB)
테스트 26 〉	통과 (0.05ms, 10.2MB)
테스트 27 〉	통과 (0.04ms, 10.2MB)
```

