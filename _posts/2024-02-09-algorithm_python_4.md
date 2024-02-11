---
layout: single
title:  "파이썬에서 스택, 큐, 재귀함수"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Python, Algorithm, Stack, Queue, Recursive]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-09
last_modified_at: 2024-02-09
typora-root-url: ../
---

# 스택

파이썬에서 스택은 별도의 라이브러리를 사용하지 않고 리스트를 이용한다.

append()와 pop()을 이용하면 스택 자료구조와 동일하게 작동한다.

```python
stack = []

stack.append(5)
stack.append(3)
stack.pop()

print(stack)
print(stack[::-1])
```

------

# 큐

collections 모듈에서 제공하는 deque 자료구조를 활용한다.

deque는 스택과 큐의 장점을 모두 사용하는 자료구조이다. 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적이며 간단하다.

```python
from collections import deque

queue = deque()

queue.append(5)
queue.append(3)
queue.append(2)

queue.popleft()

print(queue)
queue.reverse()
print(queue)

list(queue) # 리스트 자료형으로 변환 
```

------





# 재귀 함수

재귀 함수의 수행은 스택 자료구조를 이용한다. 즉, 함수를 계속 호출했을 때 가장 마지막에 호출한 함수가 먼저 수행을 끝내야 그 앞의 함수 호출이 종료된다. 

```python

# 반복문으로 작성한 팩토리얼
def factorial_iterative(n):
	result += 1
	
	for i in range(1, n+1):
		result *= i
	return result
	
# 재귀함수로 작성한 팩토리얼
def factorial_recursive(n):
	if n<= 1:
		return 1
	return n * factorial_recursive(n-1)
	
	
```

반복문의 코드에 비해 재귀함수의 코드가 수학의 점화식을 그대로 나타내므로 더 간결하다.

재귀함수의 코드는 다음을 포함한다.

1. 종료 조건
2. 더 작은 변수에 대한 함수와의 관계