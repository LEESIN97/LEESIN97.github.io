---
layout: single
title:  "알고리즘 - 그리디 알고리즘"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Python, Algorithm, Greedy]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-08
last_modified_at: 2024-02-08
typora-root-url: ../
---

# 큰 수의 법칙

**내 풀이**

```python
n, m, k = map(int, input().split())
num_list = list(map(int, input().split()))

num_list.sort(reverse=True)

# m번을 더하여 가장 큰 수를 출력 하는 문제
# 똑같은 인덱스는 k번 연달아 더하는 것만 가능
ans = 0
ans = (num_list[0] * k + num_list[1]) * (m // (k+1)) + (m % (k+1)) * num_list[0]


print(ans)


```

가장 큰 수를 k번 더하고 두번째로 큰 수를 한번 더하는 연산을 반복하면 된다.



**답안 예시**

```python
n, m, k = map(int, inpu().split())
data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

count = int(m/(k+1)) * k
count += m % (k + 1)

result = 0
result += (count) * first
result += (m - count) * second

print(result)
```

------





# 숫자 카드 게임

**내 풀이**

```python
n, m = map(int, input().split())

card_table = [list(map(int, input().split())) for _ in range(n)]

row_min = [min(card_table[i]) for i in range(n)]

print(max(row_min))
```



**답안 예시**

```python
import time

n, m = map(int, input().split())

result = 0
start_time = time.time()
for i in range(n):
  data = list(map(int, input().split()))
  min_value = min(data)
  result = max(result, min_value)
end_time = time.time()
spended_time = end_time - start_time
print(result)
print(spended_time)
###################################################
result = 0
start_time = time.time()
for _ in range(n):
  data = list(map(int, input().split()))
  min_value = 10001
  for a in data:
    min_value = min(min_value, a)

  result = max(result, min_value)
end_time = time.time()
spended_time = end_time - start_time

print(result)
print(spended_time)

```

두가지의 방법이 있다. 두 방법의 시간을 측정한 결과는 아래의 사진과 같다.

![Screenshot from 2024-02-08 18-20-07](/images/2024-02-08-algorithm_python_1.md/Screenshot from 2024-02-08 18-20-07.png)

------





# 1이 될 때까지

**내풀이**

```python
n, k = map(int, input().split())
cnt = 0
while n != 1:
  if n % k == 0:
    n = n // k
    cnt += 1
  else:
    n -= 1
    cnt += 1
print(cnt)
```

최대한 많이 나눠줌으로써 최적의 해를 보장한다.



**답안 예시**

```python
n, k = map(int, inpu().split())
result = 0

while n >= k:
	while n % k != 0:
		n -= 1
		result += 1
	n //= k
	result += 1
	
while n > 1:
	n -= 1
	result += 1
print(result)
```

위의 두 코드는 n의 범위가 10만 이하의 경우에만 제한시간에 만족되게 동작할 수 있다.



```python
n, k = map(int, input().split())
result = 0

while True:
	target = (n // k) * k
	result += (n - target)
	n = target
	if n < k:
		break
	result += 1
	n //= k
result += (n - 1)
print(result)
```



