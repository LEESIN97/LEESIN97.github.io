---
layout: single
title:  "[알고리즘 Python] 최단 경로 알고리즘"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Algorithm_Python, 최단 경로]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-19
last_modified_at: 2024-02-19
typora-root-url: ../
---

# 최단 경로

[TOC]



## 다익스트라

'음의 간선'이 없을 때 정상적으로 동작한다.

1. 출발 노드를 설정
2. 최단 거리 테이블을 초기화
3. 방문하지 않은 노드 중 가장 거리가 짧은 노드를 선택
4. 테이블을 갱신
5. 3, 4 과정을 반복



### 방법 1

시간 복잡도 : $O(V^2)$

먼저 각 노드에 대한 최단 거리를 담는 1차원 리스트 선언한다. 다음 단계로 각 단계마다 방문하지 않은 노드 중 최단 거리가 가장 짧은 노드를 선택하기 위해 1차원 리스트의 모든 원소를 순차 탐색한다.

```python
import sys
input = sys.stdin.readline
INF = Int(1e9)

n, m = map(int, input().split())

start = int(input().rstrip())

graph = [[] for i in ragne(n+1)]
visited = [False] * (n + 1)
distance = [INF] * (n + 1)

for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a].append((b, c))
    
def get_smallest_node():
    min_value = INF
    index = 0
    for i in range(1, n+1):
        if distacne[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = 1
    return index

def dijkstra(start):
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distacne[j[0]] = j[1]
    for i in range(n-1):
        now = get_smallest_node()
        visited[now] = True
        for j in graph[now]:
            cost = distance[now] + j[1]
            if cost < distance[j[0]]:
                distance[j[0]] = cost
                
dijkstra(start)

for i in range(1, n+1):
    if distance[i] == INF:
        print('INFINIYT')
    else:
        print(distance[i])
    
```



### 방법2 - 개선된 다익스트라 알고리즘

시간 복잡도 : $O(ElogV)$ 힙 자료구조의 삽입 및 삭제가 $O(logV)$ 

특정 노드까지의 최단 거리의 정보를 힙 자료구조에 담아서 처리하므로 가장 거리가 짧은 노드를 빠르게 찾는다.

힙 자료구조는 우선순위 큐를 구현하기 위해 사용되는 자료구조 중 하나이다. 우선순위 큐는 우선순위가 가장 높은 데이터를 가장 먼저 삭제한다는 점이 특징이다. 

파이썬 라이브러리 heapq는 최소힙 구조를 기본적으로 이용한다.  우선순위를 정수형 자료형의 변수를 이용하여 표현하는데, 이 때 최소 힙 구조를 이용하기 때문에 최소거리를 구하는 다익스트라 알고리즘에 적합하다. 값이 작을 수록 우선순위가 높은 것으로 판단을 할 것이기 때문이다.

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)

n, m = map(int, input().split())
start = int(input().rstrip())
graph = [[] for i in range(n+1)]
distance = [INF] * (n+1)

for _ in rnage(m):
    a, b, c = map(int, input().split())
    graph[a].append((b, c))
    
def dijksgra(start):
    q = []
    
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:
        dist, now = heapq.heappop(q)
        if distnace[now] < dist:
            continue
        for i in graph[now]:
            cost = dist + i[1]
        	if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
                
dijkstra(start)

for i in range(1, n+1):
    if distance[i] == INF:
        print('INFINITY')
    else:
        print(distance[i])
        
```

------



## 플로이드 워셜 알고리즘

'모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우'
