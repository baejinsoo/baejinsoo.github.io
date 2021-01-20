---
title: "코딩테스트를 준비하면서..(1)"
excerpt: "알아두면 좋은 Tip"
categories:
  - Python
last_modified_at: 2021-01-21
toc: true
toc: true
toc_sticky: true
---

## 🤞코딩테스트를 준비하면서..(1)

개발자로 취준을 한다면 피할 수 없는 코딩테스를 대비하면서 자주 접하는 기본기에 대해서 정리를 하고자 이 글을 쓰고 있다.

복습과 정리를 위한 글이지만 나처럼 `파이썬`으로 코딩테스를 준비한다면 이 글을 읽는 분들에게 많은 도움이 되었으면 좋겠다.



#### 입출력

##### map

`1 2` 와 같이 공백으로 입력값이 주어졌을 때, 원하는 변수에 입력을 받는 방법이다.

```python
a, b = map(int, input().split())
```



##### sys

간혹가다가 입력 값이 많은 경우`input()`을 사용하면 pypy3로 제출했더라도 시간 초과를 경험한 적이 있다. 이럴 때는 `sys`를 import 해서 입력을 받아야 한다.

```python
import sys
n = int(sys.stdin.readline()) # 입력
sys.stdout.write(n) # 출력
```

이 방법으로 시간초과가 나진 않지만 제한시간에 문제를 풀어야하는 코딩 테스트에서 입력을 받을때마다 `sys.stdin.` 을 사용하기에는 너무 귀찮다. 

```python
from sys import stdin 
input = sys.stdin.readline 
print = sys.stdout.write
```

위와 같은 코드를 맨 위에 작성하게 되면 평소에 사용하는 print()함수를 호출하듯 사용하면된다.



#### 배열, 리스트

##### 1. pythonic한 배열 입력

요즘에 풀고잇는 '이것이 취업을 위한 코딩 테스트다 with 파이썬'  에서의 문제나 백준 사이트의 문제를 보면 첫 번째 줄에 입력되는 숫자, 다음줄 부터는 공백을 기준으로 배열을 입력받는 문제들을 자주 볼 수 있다.

```python
n = int(input())
data = []
for _ in range(n):
	data.append(list(map(int, input().split())))
```

이 방법이 내가 계속 쓰던 코드인데 아래처럼 `pythonic`한 코드로 바꿀 수 있다.

```python
data = [list(map(int, input().split())) for _ in range(int(input()))]
```



##### 2. 정수와 배열이 같은 줄에 들어오는 경우

```
3 1 2 3
5 1 2 3 4 5
4 1 2 3 4
```

위처럼 한줄에 첫번째는 갯수 n, 두번째 부터 n개의 수를 배열을 입력받아야 하는 경우가 있다.

```python
n, *data = map(int, input().split())
```

data 변수 앞에 *을 붙이면 뒤이어 나오는 값이 data 배열에 저장되는 것을 확인할 수 있다.



##### 3. 문자열을 한글자씩 배열에 저장

```
dfajlaifjlaj
```

이 처럼 문자열이 주어졌을 때 각 문자마다 배열에 저장하고 싶다면 `list(input())`을 사용하면 된다.

```python
data = [list(input()) for _ in range(n)]
```



##### 4-1. 리스트를 문자열로 출력

문제를 풀다보면 정답을 출력할 때 문자열로 출력하는 경우를 많이 보았다. 문제를 풀때는 리스트로 풀다가 마지막에 문자열로 출력하기위해서 매번 구글링을 한 후 출력을 했었다.

```python
data = ['h','e','l','l','o']
print("".join(data))
```

data안의 문자가 숫자인 경우

```python
arr = [1, 2, 3, 4] 
print("".join(map(str, arr)))
```



##### 4-2 공백을 포함해 출력

```python
1 2 3 4 #원하는 출력 결과
```

```python
print(*arr)
```



#### 문자열

##### 문자열을 거꾸로

```python
data = "dkjlaf"
print(data[::-1])
```

##### 아스키코드

```python
ord() # 문자를 아스키코드로 변환
chr() # 아스키코드를 문자로 변환
```

