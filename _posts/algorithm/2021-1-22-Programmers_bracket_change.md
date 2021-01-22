---
title: "프로그래머스 - 괄호 변환"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - DFS/BFS"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-22

---

### 프로그래머스(Kakao 2020)- 괄호 변환

[프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/60058)

##### 해결방법 

문제를 이해하고 주어진 조건대로 구현만 하면 되는 문제이다.

조건이 여러개라 헷갈릴 수 있는 구현 문제라고 볼 수 있지만 재귀 함수를 활용해서 `DFS`로 문제를 해결할 수 있다.

```python

def check_valid(p):
    check = 0
    for elem in p:
        if elem == '(':
            check += 1
        else:
            check -= 1
        if check < 0:
            return False
    if check == 0:
        return True
    else:
        return False


def make_u_v(w):
    u = ""
    v = ""
    check = 0
    done = False
    for elem in w:
        if done:
            v += elem
        else:
            u += elem
            if elem == '(':
                check += 1
            else:
                check -= 1
            if check == 0:
                done = True
    return [u, v]


def step(p):
    if p == "":
        return ""
    u, v = make_u_v(p)
    if check_valid(u):
        result = u + step(v)
    else:
        result = '('
        result += step(v)
        result += ')'
        print("result=", result)
        u = u[1:-1]
        u_reversed = ""
        for elem in u:
            if elem == "(":
                u_reversed += ')'
            elif elem == ")":
                u_reversed += '('
        result += u_reversed

    return result


def solution(p):
    answer = ''
    answer = step(p)
    return answer
```



##### 실행결과

```
테스트 1 〉	통과 (0.01ms, 10.2MB)
테스트 2 〉	통과 (0.01ms, 10.3MB)
테스트 3 〉	통과 (0.01ms, 10.3MB)
테스트 4 〉	통과 (0.02ms, 10.3MB)
테스트 5 〉	통과 (0.01ms, 10.3MB)
테스트 6 〉	통과 (0.01ms, 10.2MB)
테스트 7 〉	통과 (0.02ms, 10.3MB)
테스트 8 〉	통과 (0.01ms, 10.3MB)
테스트 9 〉	통과 (0.02ms, 10.4MB)
테스트 10 〉	통과 (0.02ms, 10.3MB)
테스트 11 〉	통과 (0.05ms, 10.3MB)
테스트 12 〉	통과 (0.06ms, 10.3MB)
테스트 13 〉	통과 (0.09ms, 10.3MB)
테스트 14 〉	통과 (0.27ms, 10.3MB)
테스트 15 〉	통과 (0.42ms, 10.3MB)
테스트 16 〉	통과 (2.04ms, 10.3MB)
테스트 17 〉	통과 (0.93ms, 10.2MB)
테스트 18 〉	통과 (1.55ms, 10.3MB)
테스트 19 〉	통과 (3.16ms, 10.3MB)
테스트 20 〉	통과 (2.75ms, 10.2MB)
테스트 21 〉	통과 (0.98ms, 10.4MB)
테스트 22 〉	통과 (0.75ms, 10.2MB)
테스트 23 〉	통과 (1.76ms, 10.2MB)
테스트 24 〉	통과 (0.39ms, 10.2MB)
테스트 25 〉	통과 (1.00ms, 10.2MB)
```

