---
layout: single
title:  "[알고리즘 Python] 정렬"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Algorithm_Python, Sort]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-09
last_modified_at: 2024-02-09
typora-root-url: ../
---

# 정렬



## 선택 정렬

가장 작은 데이터를 선택해 맨 앞에 있는 데이터를 바꾸는 과정을 반복한다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
	min_index = i
	for j in range(i+1, len(array)):
		if array[min_index] > array[j]:
			min_index = j
	array[i], array[min_index] = array[min_index], array[i] # swap
	
print(array)
```



- 선택 정렬의 시간 복잡도

매번 가장 작은 수를 찾기 위해서 비교 연산이 필요하다. i = 0 일때 N-1번 비교 연산 ~ i = N-1일때 1번 비교연산
따라서 근사치로 대략적으로 $O(N^2)$라고 표현할 수 있다.

------



## 삽입 정렬

두번째 데이터 부터 시작해서 그 앞의 데이터와 비교해 적절한 위치로 삽입을 한다. 그 앞의 데이터는  이미 정렬이 돼 있다고 가정한다.

선택 정렬에 비해 실행 시간 측면에서 더 효율적이고 구현 난이도가 더 높다.

데이터가 거의 정렬이 되어 있을 때 더 효율적이다.

- 삽입 정렬의 시간 복잡도

기본적으로 $O(N^2)$인데, 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작한다.

최선의 경우에는 $O(N)$의 시간복잡도를 가진다.

```python
array =[7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
	for j in range(i, 0, -1):
		if array[j] < array[j - 1]:
			array[j], array[j - 1] = array[j - 1], array[j]
		else:
			break
print(array)
```

------



## 퀵 정렬

정렬 알고리즘 중 가장 많이 사용되는 알고리즘

호어 분할 방식을 이용하면 리스트에서 첫번째로 피벗을 설정한 뒤에 왼쪽에서부터 pivot보다 큰 데이터를 찾고, 오른쪽에서부터 피벗보다 작은 데이터를 찾아서 서로 위치를 교환해준다. 찾는 과정에서 큰 데이터의 위치와 작은 데이터의 위치가 엇갈렸다면 작은 데이터와 피 pivot의 위치를 바꿔준다. 그럼으로써 pivot의 오른쪽에는 pivot보다 큰 데이터들이 왼쪽에는 작은 데이터들이 이루어지고 이는 분할이라고 한다. 이제 분할된 각 데이터에서의 pivot을 설정하고 (맨 앞) 앞에서의 과정을 반복한다.

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    if start >= end:
        return
    pivot = start
    left = start + 1
    right = end
    while left <= right:
        while left <= end and array[left] <= array[pivot]:
            left += 1
        while right > start and array[right] >= array[pivot]:
            right -= 1
        if left > right:
            array[right], array[pivot] = array[pivot], array[right]
        else:
            array[left], array[right] = array[right], array[left]
    
    quick_sort(array, start, right - 1)
    quick_sort(array, start + 1, end)
    
quick_sort(array, 0, len(array) - 1)
print(array)
    
```





파이썬에서의 퀵 정렬 (시간적으로는 비효율적)

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quic_sort(array):
	if len(array) <= 1:
		return array
	pivot = array[0]
	tail = array[1:]
	
	left_side = [x for x in tail if x <= pivot]
	right_side = [x for x in tail if x > pivot]
	
	return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
	
```

당연히 리스트 컴프리헨션 부분을 보면 tail 리스트 전체에 대해서 비교연산을 하면서 left_side, right_side를 나누기 때문에 앞에서의 코드보다 비효율적임을 알 수 있다.



- 퀵 정렬의 시간 복잡도

퀵 정렬의 **평균** 시간 복잡도는 $O(NlogN)$이다. (여기서 로그는 밑이 2인 로그를 의미한다.)

러프하게 보면 재귀함수가 호출이 될 때마다 분할이 되는데, 분할의 횟수가 로그함수를 따라 비선형적으로 감소하는 것을 의미한다.

하지만, **최악의 시간 복잡도는 $O(N^2)$이다**. '이미 데이터가 정렬이 돼 있는 경우' 매우 느리게 동작한다. (pivot 값을 맨 처음 원소로 했을 때)



------



# 계수 정렬

특정한 조건이 부합할 때만 사용할 수 있는 빠른 정렬 알고리즘이다. '데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때만' 사용이 가능하다.

일반적으로 최소와 최대의 차이가 1,000,000이 넘지 않을 때 사용

계수 졍렬 방식은 별도의 리스트를 선언해서 사용하는 방식이다. 

먼저 가장 큰 데이터 ~ 가장 작은 데이터를 포함하는 범위의 리스트를 초기 값 0을 가지도록 생성한다.

주어진 리스트를 확인하면서 앞에서 생성한 리스트에서 동일한 인덱스를 가지는 원소의 값에 +1을 해준다.

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]
count = [0] * (max(array) + 1)

for i in range(len(array)):
	count[array[i]] += 1
	
for i in range(len(count)):
	for j in range(count[i]):
		print(i, end = ' ')
```



- 계수 정렬의 시간 복잡도

계수 정렬은 데이터의 개수 N만큼 을 확인 해야 하고 0부터 최대까지의 길이만큼의 리스트를 확인해야 하기 때문에 시간복잡도가 $O(N + K)$이다.

- 계수 정렬의 공간 복잡도

계수 정렬은  때로는 매우 비효율 적일 수도 있다. 0과 999,999만 있는 경우가 그렇다.

데이터의 개수가 10,000,000개 미만이면서, 동일한 값을 가지는 데이터가 여러 개 등장할 때 적합하다.(리스트에서 10,000,000개의 원소는 약 40MB) 

------





## 파이썬의 정렬 라이브러리

- sorted() : 병합 정렬을 기반으로 만들어진 파이썬 내장 함수이다. 최악의 경우에도 $O(NlogN)$의 시간 복잡도를 제공한다. sorted함수는 집합이나, 딕셔너리 자료형을 입력 받아도 리스트로 반환한다.

```python
array = [7, 5, 9, 3]

result = sorted(array)

array = [('바나나', 2), ('사과', 5)]
def setting(data):
    return data[1]
result = sorted(array, key=setting)

result = sorted(array, key=lambda x: x[1])

```



- sort() : 리스트 객체의 내장 함수이다. 내부 리스트를 바로 정렬한다. 이때 반환되는 리스트는 없다.

```python
array = [7, 5, 9, 3]

array.sort()
```



- 시간 복잡도

정렬 라이브러리는 최악의 경우에도 시간 복잡도 $O(NlogN)$를 보장한다. 





------



## 문제



### 위에서 아래로

**내 풀이**

```python
n = int(input())
num_list = []
for _ in range(n):
  num_list.append(int(input()))

num_list.sort(reverse = True)
for i in range(n):
  print(num_list[i], end = ' ')
```





###  성적 낮은 순서로 출력

```python
n = int(input())
score_list = []
for _ in range(n):
  name, score = input().split()
  score_list.append((name, int(score)))

score_list.sort(key=lambda x: x[1])

for i in range(n):
  print(score_list[i][0], end=' ')
```





### 두 배열의 원소 교체

```python
n, k = map(int, input().split())
a = list(map(int, input().split()))
b = list(map(int, input().split()))


a.sort(reverse=True)
b.sort()
for i in range(n-1, n-1-k, -1):
  b[i], a[i] = a[i], b[i]

print(sum(a))
         
```

------

