---
layout: single
title:  "정렬"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Python, Sort]

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



