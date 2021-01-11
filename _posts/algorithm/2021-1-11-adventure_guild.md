---
title: "모험가 길드"
excerpt: "이것이 취업을 위한 코딩테스트다 with 파이썬 - Greedy"
categories:
  - 알고리즘 문제풀기
last_modified_at: 2021-01-11
---

##### 해결방법

- Counter 이용해서 공포도값 카운팅

- Counter.most_common() 사용시 많은 순으로 정렬되기 때문에, 1,2,3, 순으로 정렬시키고

  튜플을 리스트로 바꿔줌(튜플은 값 수정이 안되기 때문)

- 리스트를 확인하면서 공포도 값이 해당 공포도 인원보다 작거나 같으면 결과값에 몫을 더하고

  그 외에는 나머지 값은 다음 차례의 인원수 쪽으로 넘겨서 계산함

```python
from collections import Counter

n = int(input())
fear_data = list(map(int, input().split()))

result = 0
count_data = Counter(fear_data).most_common()
count_data.sort()
print(count_data)

new_list = []
for data in count_data:
    new_list.append(list(data))

for i in range(len(new_list)-1):
    if new_list[i][1] >= new_list[i][0]:
        result += new_list[i][1] // new_list[i][0]
        new_list[i+1][1] += (new_list[i][1] % new_list[i][0])
    else:
        new_list[i+1][1] += new_list[i][1] % new_list[i][0]
if new_list[-1][1] >= new_list[-1][0]:
    result += new_list[-1][1] // new_list[-1][0]

print(result)
```

