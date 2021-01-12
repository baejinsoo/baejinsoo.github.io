---
title: "무지의 먹방 라이브"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-12

---

### 프로그래머스(kakao 2019) - 무지의 먹방 라이브

https://programmers.co.kr/learn/courses/30/lessons/42891

처음부터 k번째까지 하나씩 이동하면서 풀면 효율성 테스트에서 실패했던 문제이다.

문제에서 설명하는대로 구현하면 효율성 테스트 제한 사항 중 k는 `2 x 10^13`이하의 자연수 이므로

`2 x 10^13`번 확인해야 되서 시간초과 오류가 발생한다.

풀이를 보고 문제를 해결하는 방법을 알아도 코드로 구현하는데 많이 까다로운 문제였다.

이 문제는 시간이 적게 걸리는 음식부터 확인하는 Greedy 접근 방식으로 해결해야 한다.

모든 음식을 시간을 기준으로 정렬한 뒤, 시간이 적게 걸리는 음식부터 제거해 나가는 방식을 이용하며 이 때 우선순위 큐를 사용해 구현해 보았다.

##### 해결방법 

1. 우선순위 큐에 (음식을 먹는데 필요한시간, 음식 번호)의 형태로 삽입한다.

2. (가장 적게 걸리는 음식) * (남아있는 음식의 개수)가 k보다 작거나 같다면 가장 적게 걸리는 음식을 pop 해주고, times에 (가장 적게 걸리는 음식) * (남아있는 음식의 개수)를 더해준다.

   그리고 남아있는 음식들에는 pop해준 음식의 시간만큼 빼줘야 하므로 count_times에 시간을 저장해둔다. 그리고 마지막으로 남아있는 음식의 개수에서 1을 빼주면 된다.

3. 그 다음부터 계속 (적게 걸리는 음식)*(남아있는 음식의 개수) 가 k보다 클때까지 반복해준다.
4. 남아있는 음식을 음식 번호 순서대로 정렬해 준 뒤 남은 음식 중에서 몇 번째 음식인지 확인해서 결과를 출력해주면 된다.

```python
import heapq

def solution(food_times, k):
    if sum(food_times) <= k:
        return -1
    
    q = []
    for i in range(len(food_times)):
        heapq.heappush(q, (food_times[i],i+1))
    
    times = 0
    count_times = 0
    food_num = len(food_times)
    while times + (q[0][0] - count_times)*food_num <= k:
        now = heapq.heappop(q)[0]
        times += (now - count_times)*food_num
        count_times = now
        food_num -= 1

    result = sorted(q, key=lambda x: x[1])
    return result[(k-times)%food_num][1]

# food_times = [3,1,2]
# k = 5

# print(solution(food_times, k))
```

