---
layout: single
title:  "코테를 위한 파이썬 문법"
excerpt: "이것이 코딩테스트다"

categories: Useful_code
tag: [python]

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



<br/>



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

