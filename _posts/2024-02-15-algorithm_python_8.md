---
layout: single
title:  "[알고리즘 Python] Dynammic Programming"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Algorithm_Python, Dynamic Programming]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-15
last_modified_at: 2024-02-15
typora-root-url: ../
---

# 다이나믹 프로그래밍

[TOC]

## 다이나믹 프로그래밍

큰 문제를 작게 나누고, 같은 문제라면 한번씩만 풀어 문제를 효율적으로 해결하는 알고리즘 기법이다.

1. 큰 문제를 작은 문제로 나눌 수 있을 때
2. 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일 한 경우

두 조건을 만족할 때 다이나믹 프로그래밍을 이용한다.



### Top-Down 방식 (메모제이션 혹은 캐싱 기법)

한 번 구한 결과를 메모리 공간에 저장해두고 호출하는 기법이다.

```python
d = [0] * 100

def fibo(x):
	if x == 1 or x == 2:
		return 1
	if d[x] != 0:
		return d[x]
	d[x] = fibo(x-1) + fibo(x-2)
	return d[x]
	
print(fibo(99))
```

재귀 함수를 함수를 다시 호출하는 과정에서 오버헤드가 발생한다. 반면에, 아래의 Bottom-Up 방식은 이러한 오버헤드가 없다.

**시간복잡도는 $O(N)$이다**



### Bottom-Up 방식

```python
d = [0] * 100

d[1] = 1
d[2] = 1
n = 99

for i in range(3, n+1):
	d[i] = d[i-1] + d[i-2]
	
print(d[n])

```

여기서 결과값이 저장되는 리스트를 'DP 테이블'이라고 한다.

------



## 문제



### 1로 만들기

Top-Down 방식의 풀이

```python
x = int(input())
d = [0] * (x + 1)

def top_down(x):
  if x == 2 or x == 3 or x == 5:
    return 1
  if d[x] != 0:
    return d[x]
  else:
    if x % 2 == 0:
      d[x] = 1 + min(top_down(x//2), top_down(x-1))
    elif x % 3 == 0:
      d[x] = 1 + min(top_down(x//3), top_down(x-1))
    elif x % 5 == 0:
      d[x] = 1 + min(top_down(x//5), top_down(x-1))
    else:
      d[x] = 1 + top_down(x-1)
  return d[x]

print(top_down(x))



```

Bottom-Up 방식의 풀이

```python
x = int(input())

d = [0] * 30001

for i in range(2, x + 1):
	d[i] = d[i - 1] + 1
	if i % 2 == 0:
		d[i] = min(d[i], d[i // 2] + 1)
	if i % 3 == 0:
		d[i] = min(d[i], d[i // 3] + 1)
	if i % 5 == 0:
		d[i] = min(d[i], d[i // 5] + 1)
print(d[x])
```





### 개미 전사

```python
n = int(input())
warehouse = list(map(int, input().split()))
d = [0] * 100
for i in range(n):
  d[i] = warehouse[i]

for i in range(2, n):
  d[i] = max(d[i] + d[i - 2], d[i - 1])

print(d[n - 1])

```



### 바닥 공사

```python
n = int(input())
d = [0] * 1001

d[1], d[2] = 1, 3
for i in range(3, n+1):
  d[i] = d[i-1] + 2 * d[i-2]

print(d[n] % 796796)
```



### 효율적인 화폐 구성

**틀린 풀이**

```python
n, m = map(int, input().split())
money_type = []
for _ in range(n):
  money_type.append(int(input()))

d = [0] * 10001
for money in money_type:
  d[money] = 1

min_money = min(money_type)

for i in range(min_money + 1, m + 1):
  if i in money_type:
    continue
  min = 999999999
  cnt = 0
  for money in money_type:
    if (i - money) % money == 0:
      cnt += 1
      if min > (d[i - money] + 1):
        min = d[i - money] + 1
    else:
      continue
  if cnt != 0:
    d[i] = min
  else:
    d[i] = -1

print(d[m])

```

**정답**

```python
n, m = map(int, input().split())

array = []
for i in range(n):
    array.append(int(input()))
                 
d = [100001] * (m + 1)

d[0] = 1
for i in range(n):
	for j in range(array[i], m + 1):
		if d[j - array[i]] != 10001:
			d[j] = min(d[j], d[j - array[i]] + 1)

if d[m] == 10001:
	print(-1)
else: print(d[m])
               
    
    
```

