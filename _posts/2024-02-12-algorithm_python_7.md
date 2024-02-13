---
layout: single
title:  "[알고리즘 Python] 이진 탐색"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Python, Binary Search]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-12
last_modified_at: 2024-02-12
typora-root-url: ../

---

# 이진 탐색

[TOC]



## 순차 탐색

N개의 데이터가 있을 때 말 그대로 순차적으로 탐색하는 방법이다.

리스트의 데이터의 원소에 순차적으로 방문하며 탐색한다. 

ex) 리스트에 원하는 원소가 있는지 찾고 싶을 때, 리스트 객체 method인 count()

```python
def sequential_search(n, target, array):
	for i in range(n):
		if array[i] == target:
			return i + 1

input_data = input().split()
n = int(input_data[0])
target = inpu_data[1]

array = input.split()

print(sequential_search(n, target, array))
```

- 순차 탐색의 시간 복잡도

맨 처음의 데이터부터 총 데이터 N개를 탐색하므로 시간복잡도는 $O(N)$이다.

------





## 이진 탐색

이진 탐색은 배열이 **정렬**되어 있어야만 사용할 수 있다.

시작점, 끝점, 중간점을 이용하고, 중간점 위치에 있는 원소와 ````반복적으로 비교하면서 탐색한다.

target의 값보다 중간점에 있는 원소가 더 크다면, 끝점을 중간점 바로 왼쪽에 둔다.

target의 값보다 중간점에 있는 원소가 더 작다면, 시작점을 중간점 바로 오른쪽에 둔다.

중간점을 새로운 시작점과 끝점을 이용하여 구한다. 

- 이진 탐색의 시간 복잡도 

한 번 확인할 때마다 확인하는 원소의 개수가 절반씩 줄어든다는 점에서 시간 복잡도가 $O(logN)$이다.

문제에서 탐색 범위가 1000만 이상, 혹은 2000만 이상이라면 이진 탐색이 필요한 경우가 많다.

```python
def binary_search(array, target, start, end):
	if start > end:
		return None
	mid = (start + end) // 2
	if array[mid] == target:
		return mid
	elif array[mid] > target:
		return binary_search(array, target, start, mid - 1)
	else:
		return binary_search(array, target, mid + 1, end)
		
n, target = map(int, input().split())
array = list(map(int, input().split()))

result = binary_search(array, target, 0, n-1)
if result == None:
	print('doesn't exist)
else:
	print(result + 1)
```



```python
def binary_search(array, target, start, end): 
	while start <= end:
		mid = (start + end) // 2
		if array[mid] == target:
			return mid
		elif array[mid] > target:
			end = mid - 1
		else:
			start = mid + 1
	return None

n, target = map(int, input().split())
array = list(map(int, input().split()))

result = binary_search(array, target, 0, n - 1)
if result == None:
	print('doesn't exist)
else:
	print(result + 1)
```



### 트리 자료구조 - 이진 탐색 트리

데이터 정렬이 전제조건이다. 

트리 자료구조는 그래프 자료구조의 일종으로 데이터베이스 시스템이나 파일 시스템과 같은 곳에서 많은 양의 데이터를 관리하기 위한 목적으로 사용한다. 

트리 구조는 큰 데이터 (계층적이고 정렬된 데이터)를 다루기에 적합하다.  이때 이진 탐색 기법을 이용하여 빠르게 탐색한다. 



**이진 탐색 트리**

트리 자료구조 중 이진 탐색이 가능한 가장 간단한 형태이며 다음의 특징을 가진다.

1. 부모 노드보다 왼쪽 자식 노드가 작다.
2. 부모 노드보다 오른쪽 자식 노드가 크다.

이진 탐색 트리가 구현이 되있을 때 이진 탐색은 루트 노드부터 왼쪽 자식 노드 혹은 오른쪽 자식 노드로 이동하며 반복적으로 방문한다.

------



## 문제

### 부품 찾기

```python
def binary_search(target, array, start, end):
  mid = (start + end) // 2
  if start > end:
    return 'no'

  if array[mid] == target:
    return 'yes'
  elif array[mid] > target:
    return binary_search(target, array, start, mid - 1)
  elif array[mid] < target:
    return binary_search(target, array, mid + 1, end)


n = int(input())
product = list(map(int, input().split()))

m = int(input())
target = list(map(int, input().split()))

product.sort()

start_index = 0
end_index = n - 1

for target_element in target:
  print(binary_search(target_element, product, start_index, end_index),
        end=' ')

```

**게수 정렬**을 이용한 풀이

```python
n = int(input())
array = [0] * 1000001

for i in rnput().split():
	array[int(i)] = 1

m = int(input())
x = list(map(int, input().split()))
for i in x:
	if array[i == 1:
		print('yes', end = ' ')
	else:
		print('no', end = ' ')
		
```

**집합 자료형**을 이용한 풀이

```python
n = int(input())
array = set(map(int, input().split()))

m = int(input())

x = list(map(int, input().split()))

for i in x:
	if i in array:
		print('yes', end = ' ')
	else:
		print('no', end = ' ')
```

 리스트(list)나 튜플(tuple) 자료형을 사용해도 기능적으로는 동일한 결과를 낳지만, set 자료형이 내부적으로 해시 테이블을 기반으로 하기 때문에 멤버십 테스트가 빠르다.



### 떡볶이 떡 만들기

```python
def binary_search(target, array, start, end):
  result = 0
  while start <= end:
      mid = (start + end) // 2
      sum = 0
      for x in array:
          if x > mid:
              sum += x - mid
      if sum < target:
          end = mid - 1
      else:
          result = mid
          start = mid + 1
  return result

n, m = map(int, input().split())
rcake_array = list(map(int, input().split()))
rcake_array.sort()
print(binary_search(m, rcake_array, 0, rcake_array[n - 1]))


```

