---
layout: single
title:  "[알고리즘 Python] 그래프 이론"
excerpt: "이것이 코딩 테스트다 - 저자 나동빈"

categories: AlgorithmPython
tag: [Algorithm_Python, 그래프]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-22
last_modified_at: 2024-02-22
typora-root-url: ../
---

# 그래프 이론

[TOC]

------



## 서로소 집합 자료구조

서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조.

1. 합집합 연산, union 연산을 확인하여 연결된 두 노드 A, B (집합의 두 원소)를 확인한다.
2. A와 B의 루트 노드를 찾고 더 번호가 작은 루트 노드로 설정한다.
3. 1, 2의 과정을 반복한다.

노드의 개수 만큼 부모 테이블이 필요하고, 루트 노드를 찾기 위해서는 부모 테이블을 이용하여 재귀적으로 찾아야 한다.

```python
def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent,parent[x])
    return x

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
v, e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v + 1):
    parent[i] = i
    
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
print('각 원소가 속한 집합: ', end = ' ')
for i in range(1, v + 1):
    print(find_parent(parent, i), end = ' ')
    
print()

print('부모 테이블: ', end = ' ')
for i in range(1, v + 1):
    print(parent[i], end = ' ')
```

이 코드에서는 find 함수가 비효율적으로 동작한다. 최악의 경우 모든 노드를 확인해 시간 복잡도가 $O(V)$이다. union 혹은 find 연산의 개수가 M개라면 시간복잡도가 $O(NM)$이 된다.

이를 개선하기 위해서는 ''경로 압축 기법''을 적용한다. find함수를 재귀적으로 호출하면서 부모 테이블 값을 갱신하는 기법이다. 

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
v, e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v + 1):
    parent[i] = i
    
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
print('각 원소가 속한 집합: ', end = ' ')
for i in range(1, v + 1):
    print(find_parent(parent, i), end = ' ')
    
print()

print('부모 테이블: ', end = ' ')
for i in range(1, v + 1):
    print(parent[i], end = ' ')
```

시간복잡도 : $O(V + M(1 + log~2-M/V~V))$ 알아만 두자.

이 서로소 집합 알고리즘은 사이클 판별에서 이용이 가능하다. 무향 그래프에서 간선을 하나씩 확인하고, 매 간선에 대해여 union, find 함수를 호출하는 방식이다.

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
v, e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v + 1):
    parent[i] = i
    
cycle = False
    
for i in range(e):
    a, b = map(int, input().split())
    if find_parent(parent, a) == find_parent(parent, b):
    	cycle = True
    	break
	else:
    	union_parent(parent, a, b)
    
if cycle:
	print('cycle')
else:
	print('no')
```

------



## 신장 트리

'하나의 그래프가 있을 때 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프'  (트리에서 간선의 개수는 '노드의 개수 - 1')

### 크루스칼 알고리즘

최소 비용으로 만들 수 있는 신장 트리를 찾는 알고리즘이다. 이 알고리즘은 그리디 알고리즘으로 분류된다. 먼저 모든 간선에 대하여 정렬을 수행한 뒤에 가장 거리가 짧은 간선부터 집합에 포함시킨다. 

1. 간선 데이터를 오름차순으로 정렬한다.
2. 사이클이 발생하는지 확인해, 발생하지 않는 경우에만 최소 신장 트리에 포함한다.
3. 모든 간선에 대하여 2를 반복한다.

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
v, e = map(int, input().split())
parent = [0] * (v + 1)

edges = []
result = 0

for i in range(1, v + 1):
    parent[i] = i
    
for _ in range(e):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))
    
edges.sort()

for edge in edges:
    cost, a, b = edge
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
        
        
print(result)
```

시간 복잡도 : $O(ElogE)$ (모든 edge를 정렬하는 것이 가장 큰 작업이기 때문에)

------

## 위상 정렬

방향 그래프의 모든 노드를 '방향성에 거스르지 않도록 순서대로 나열하는 것'이다.

1. 진입차수가 0인 노드를 큐에 넣는다.
2. 큐가 빌 때까지 큐에서 원소를 꺼내 해당 노드에서 출발하는 간선을 그래프에서 제거하고, 새롭게 진입차수가 0이된 노드를 큐에 넣는다.

여기서 진입차수는 특정 노드로 들어오는 edge의 개수를 의미한다.

```python
from collections import deque

v, e = map(int, input().split())

indegree = [0] * (v + 1)
graph = [[] for i in range(v + 1)]

for _ in range(e):
    a, b = map(int, input().split())
    graph[a].append(b)
    indegree[b] += 1
    
def topology_sort():
    result = []
    q = deque()
    
    for i in range(1, v + 1):
        if indegree[i] == 0:
            q.append(i)
            
	while q:
        now = q.popleft()
        result.append(now)
        
        for i in grap[now]:
            indegree[i] -= 1
            if indegree[i] == 0:
                q.append(i)
                
	for i in result:
        print(i, end = ' ')
        
topology_sort()S
```

위상 정렬의 시간 복잡도 : $O(V + E)$ 노드와 간선을 모두 확인

