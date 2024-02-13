---
layout: single
title:  "[Python] 코테를 위한 파이썬 문법"
excerpt: "이것이 코딩테스트다"

categories: Useful_code
tag: [Python]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-06
last_modified_at: 2024-02-06
typora-root-url: ../
---

# 자료형









## 실수형



컴퓨터는 실수를 처리할 때 2진수로 처리하며, 부동 소수점 방식을 이용한다.

0.9와 같은 이진수를 분수로 표현하려고 하면 무한히 반복되는 이진수가 발생하고, 이를 컴퓨터 메모리에 저장하거나 계산에 사용하는 데에는 실질적인 한계가 있다. 

따라서 0.9와 같은 값은 정확히 표현되지 않고 근사값으로 처리된다.



소수점 값을 비교하는 작업이 필요한 문제라면 실수 값을 비교하지 못해서 원하는 결과를 얻지 못할 수 있으므로 이럴 때는 round()함수를 이용한다.



```python
a = 0.3 + 0.6
print(round(a, 4))

if round(a,4) == 0.9: #넷째 자리에서의 반올림
    print(True)
else:
    print(False)
    
```







## 리스트 자료형

- 코딩 테스트 문제에서 크기가 N인 1차원 리스트를 초기화해야하는 경우가 많은데 다음과 같이 한다.

```python
n = 10
a = [0] * n # 모든 값이 0인 크기가 N인 1차원 리스트 초기화
```



- 리스트 컴프리헨션을 이용한다면 간단하게 리스트를 초기화 할 수 있다.

```python
array = [i for i in range(20) if i % 2 == 1]

# N X M 크기의 2차원 리스트 초기화
n = 3
m = 4
array = [[0] * m for _ in range(n)]

# N X M 크기의 2차원 리스트 초기화(잘못된 방법)
n = 3
m = 4
array = [[0] * m] * n

array[1][1] = 5
```



- 관련 메서드

| 매서드명  | 사용법                                             | 설명                                                | 시간 복잡도 |
| --------- | -------------------------------------------------- | --------------------------------------------------- | ----------- |
| append()  | 변수명.append()                                    | 원소 삽입                                           | O(1)        |
| sort()    | - 변수명.sort()<br />- 변수명.sort(reverse = True) | - 오름차순 정렬<br />- 내림차순 정렬                | $O(NlogN)$  |
| reverse() | 변수명.reverse()                                   | 리스트의 원소를 뒤집기                              | $O(N)$      |
| insert()  | 변수명.insert(인덱스, 삽입할 값)                   | 특정 위치에 원소를 삽입                             | $O(N)$      |
| count()   | 변수명.count(특정 값)                              | 특정 데이터의 개수를 셈                             | $O(N)$      |
| remove()  | 변수명.remove(특정 값)                             | 특정 값을 갖는 원소 제거, 여러개면 하나만 제거한다. | $O(N)$      |

insert()와 remove()의 시간복잡도에 주목해야 한다.

각 메서드는 대입하거나 삭제한 후에 리스트의 위치를 조정해야 하기 때문이다.



- 특정한 값을 가지는 모든 원소 제거

리스트 컴프리헨션을 이용한다. 

```python
a = [1, 2, 3, 4, 5, 5, 5]
remove_set = [3, 5]

result = [i for i in a if i not in remove_set]

```







## 튜플

- 튜플은 그래프 알고리즘을 구현할 때 자주 사용된다.
- 튜플은 리스트에 비해 상대적으로 공간 효율적이고, 일반적으로 각 원소의 성질이 서로 다를 때 주로 사용한다.







## 사전

내부적으로 Hash Table을 이용하기 때문에 검색 수정에 있어서 시간 복잡도가 $O(1)$이다.

```python
data = dict()
data['사과'] = 'Apple'

if '사과' in data:
	print('sdsd')
```

파이썬에서 리스트, 문자열, 튜플 등 원소들을 차례대로 반복할 수 있는 자료형을 iterable 자료형이라고 하며. 이 자료형들은 내부에 원소들을 포함하는 역할을 하기 때문에 이러한 자료형들도 in 문법이 사용이 가능하다.



- key 와 value데이터 분리

```python
data = dict()
data['사과'] = 'apple'

key_list = data.keys()
value_list = data.values()

# 이런 식으로 사용
for key in key_list:
	print(data[key])
```







## 집합

- 중복을 허용하지 않는다.
- 순서가 없다, 즉, 인덱싱, 슬라이싱이 되지 않는다. 
- 특정 원소가 존재하는지 검사하는 연산의 시간 복잡도는 $O(1)$



- 집합 자료형의 연산 및 관련 함수

```python
a = set{[1, 2, 3, 4, 5]} 
b = set{[3, 4, 5, 6, 7]}
print(a | b) # 합집합
print(a & b) # 교집합
print(a - b) # 차집합



# 관련 함수
data = set{[1, 2, 3]}

data.add(4) # 집합 원소 추가

data.update([5, 6]) # 새로운 원소 여러개 추가

data.remove(3) # 특정 값 원소 제거
```







------



# 조건문



```python
score = 85

if score >= 80:
	pass # 이런 식으로 pass를 이용하면 비워놓고 디버깅을 할 수 있다.
	
	
# 조건부 표현식
score = 85
result = "Success" if score >= 80 else "Fail"

# 파이썬 조건문 내에서의 부등식 아래의 두 조건문은 파이썬 내에서 같다.
if x > 0 and x < 20:
    pass
if 0 < x < 20:
    pass

```











# 입출력

```python
list(map(int, input().split())) # 문자열을 띄어쓰기로 구분하여 각각 정수 자료형의 데이터로 저장하는 코드


# 입력을 위한 전형적인 소스코드
n = int(input())
# 각 데이터를 공백으로 구분하여 입력
data = list(map(int, input().split()))



# 공백을 기준으로 구분하여 적은 수의 데이터 입력
n, m, k = map(int, input().split())

```





- 입력을 최대한 빠르게 받아야 하는 경우

```python
import sys
sys.stdin.readline().rstrip() # 한 줄 입력을 받고 공백 문자(엔터, 줄 바꿈 기호)를 제거한다.
```



- f-string 문법

```python
answer = 7
print(f"정답은 {answer}입니다.")
```







------





# 주요 라이브러리의 문법과 유의점

코딩 테스트에서는 대부분 표준 라이브러리를 사용가능하게 하므로 익히도록 하자.



## 내장 함수

import 명령어 없이 바로 사용할 수 있다.

가장 대표적인 함수는 input(), print()이다.

```python
# sum()함수는 리스트와 같은 iterable 객체가 입력으로 주어졌을 때, 모든 원소의 합을 반환한다.
result = sum([1, 2, 3, 4, 5])

# min()함수는 파라미터가 2개이상 들어왔을 때 가장 작은 값을 반환한다.
result = min(7, 3, 5, 2)

# max()함수는 파라미터가 2개 이상 들어왔을 때 가장 큰 값을 반환한다.
result = max(7, 3, 5, 2)

# eval()함수는 수학 수식이 문자열 형식으로 들어오면 해당 수식을 계산한 결과를 반환한다.
result = eval("(3 +5) * 7")

# sorted() 함수는 iterable 객체가 들어왔을 때, 정렬된 결과를 반환한다. key 속성으로 정렬 기준을 명시할 수도 있다.
# list와 같은 iterable 객체는 기본으로 sort() 함수를 내장하고 있어 이를 이용할 수도 있다.
result = sorted([9, 1, 8, 5, 4])
result = sorted([9, 1, 8, 5, 4], reverse = True) # 내림차순
result = sorted([('홍길동', 35), ('이순신', 75)], key = lambda x: x[1], reverse = True)



```







## itertools

코딩테스트에서 가장 유용하게 사용될 수 있는 클래스는 permutations, combinations (순열, 조합)이다.

```python
# permutations는 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 일렬로 나열하는 모든 경우를 계산해준다.
# permutations는 클래스이므로 객체 초기화 이후에는 리스트 자료형으로 변환하여 사용한다.
from itertools import permutations

data = ['A', 'B', 'C']
result = list(permutations(data, 3)) #모든 순열 계산


# combinations는 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우를 계산한다.
# 마찬가지로 combinations는 클래스이므로 객체 초기화 이후에 리스트 자료형으로 변환하여 사용한다.

from itertools import combinations

data = ['A', 'B', 'C']
result = list(combinations(data, 2)) # 2개를 뽑는 모든 조합 구하기


# product는 permutations와 비슷하지만 product는 중복해서 뽑을 수 있다.
# 마찬가지로 리스트 자료형으로 변환하여 사용

from itertools import product

data = ['A', 'B', 'C']
result = list(product(data, repeat = 2)) # 2개를 뽑는 모든 순열 구하기(중복 허용)

# combinations_with_replacement는 combinations와 같이 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우를 계산한다. (중복)
# 리스트 자료형으로 변환하여 사용한다.

from itertools import combinations_with_replacement

data = ['A', 'B', 'C']
result = list(combinations_with_replacement(data, 2))

```







## heapq

힙 기능을 위해 heapq 라이브러리를 제공한다.

파이썬의 힙은 최소 힙으로 구성되어 있으므로 단순히 원소를 힙에 넣었다가 빼는 것만으로도 시간복잡도 $O(NlogN)$에 오름차순 정렬이 된다. 

```python
import heapq

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for _ in range(len(h)):
        result.append(heapq.heappop(h))
    return result
result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])

```



- 최대 힙 : 최소힙에 부호를 변경하는 방식을 이용한다.

```python
import heapq

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for _ in range(len(h)):
        result.append(-heapq.heappop(h))
    return result
```





## bisect

'정렬된 배열'에서 특정한 원소를 찾아야 할 때 매우 효과적으로 사용된다.

혹은 '정렬된 리스트'에서 '값이 특정 범위에 속하는 원소의 개수'를 구하고자 할 때, 효과적으로 사용될 수 있다.

bisect_left(), bisect_right() 함수가 가장 중요하게 사용되며, 시간복잡도가 $O(logN)$이다.

- bisect_left(a, x) : 정렬된 순서를 유지하면서 리스트 a에 데이터 x를 삽입할 가장 왼쪽 인덱스를 찾는 메서드
- bisect_right(a, x) : 정렬된 순서를 유지하도록 리스트 a에 데이터 x를 삽입할 가장 오른쪽 인덱스를 찾는 메서드

```python
from bisect import bisect_left, bisect_right

a = [1, 2, 4, 4, 8]
x = 4

print(bisect_left(a, x))
print(bisect_right(a, x))

```



- counter_by_range(a, left_value, right_value)함수를 이용하면 정렬된 리스트에서 값이 [left_value, right_value]에 속하는 데이터의 개수를 반환한다. 원소의 개수를 $O(logN)$으로 빠르게 계산한다.

```python
from bisect import bisect_left, bisect_right

def cout_by_range(a, left_value, right_value):
	right_index = bisect_right(a, right_value)
	left_index = bisect_left(a, left_value)
	return right_index - left_index
	
a = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9]

print(count_by_range(a, 4, 4))
print(count_by_range(a, -1, 3))
```







## collections

deque, Counter를 코테에서 유용하게 사용한다.



- deque를 사용해 파이썬에서 큐를 구현한다.



|                            | **리스트** | deque  |
| -------------------------- | ---------- | ------ |
| 가장 앞쪽에 원소 추가      | $O(N)$     | $O(1)$ |
| 가장 뒤쪽에 원소 추가      | $O(1)$     | $O(1)$ |
| 가장 앞쪽에 있는 원소 제거 | $O(N)$     | $O(1)$ |
| 가장 뒤쪽에 있는 원소 제거 | $O(1)$     | $O(1)$ |

다만 인덱싱, 슬라이싱등의 기능은 사용할 수 없다. 데이터의 시작 부분이나 끝부분에 데이터를 삽입하거나 삭제할 때는 매우 효과적으로 사용될 수 있다.

파이썬에서 스택, 큐 자료구조의 대용으로 사용이 된다.

```python
from collections import deque

data = deque([2, 3, 4])
data.appendleft(1)
data.append(5)

print(data)
print(list(data))	
```







- Counter는 등장 횟수를 세는 기능을 제공한다.  리스트같은 iterable 객체가 주어졌을 때, 내부의 원소가 몇 번씩 등장했는지를 알려준다.

```python
from collections import Counter

counter = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])

print(counter['blue']) #횟수를 출력
print(counter['green'])

print(dict(counter)) # 사전 자료형으로 변환

```









## math

팩토리얼, 제곱근, 최대공약수 등을 제공해주는 기능을 포함하고 있다.

```python
import math

print(math.factorial(5)) # 5 팩토리얼을 출력

print(math.sqrt(7)) # 7의 제곱근을 출력

print(math.gcd(21, 14)) # 최대 공약수를 출력

print(math.pi) # pi를 출력
print(math.e) # 자연상수를 출력
```



