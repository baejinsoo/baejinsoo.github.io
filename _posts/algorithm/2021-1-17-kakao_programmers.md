---
title: "프로그래머스 - 기둥과 보 설치"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - 구현"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-17
---

### 프로그래머스(Kakao 2020)- 기둥과 보 설치

[프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/60061)

##### 해결방법 

이 문제는 시간제한이 5초로 넉넉한 편이므로 O(N^3) 으로 해결이 가능하다.

건축물을 설치하거나 철거할 경우를 일일이 확인하는 함수를 구현하는 방법으로 해결했다.

```python
# 현재 설치되거나 삭제할 건축물이 가능한지 판별하는 함수
def check(answer):
    for x, y, a in answer:
        if a == 0: # 기둥인 경우
            # '바닥위' or '보의 한쪽 끝부분 위' or '다른 기둥위' 라면 가능
            if y == 0 or [x-1,y,1] in answer or [x,y,1] in answer or [x,y-1,0] in answer:
                continue
            else:
                return False
        elif a == 1: # 보 인경우
            # '한쪽 끝부분이 기둥 위' or '양쪽 끝부분이 다른 보와 동시에 연결'
            if [x,y-1,0] in answer or [x+1,y-1,0] in answer or ([x-1,y,1] in answer and [x+1,y,1] in answer):
                continue
            else:
                return False
    return True

def solution(n, build_frame):
    len_build = len(build_frame)
    answer = []
    
    for frame in build_frame:
        x, y, a, b = frame
        if b == 1: # 설치하는 경우
            answer.append([x,y,a])
            if check(answer) is not True:
                answer.remove([x,y,a])
        elif b == 0: # 철거하는 경우
            answer.remove([x,y,a])
            if check(answer) is not True:
                answer.append([x,y,a])
    answer = sorted(answer) # 정렬
    return answer


n = 5
build_frame = [[0,0,0,1],[2,0,0,1],[4,0,0,1],[0,1,1,1],[1,1,1,1],[2,1,1,1],[3,1,1,1],[2,0,0,0],[1,1,1,0],[2,2,0,1]]
print(solution(n, build_frame))
```

