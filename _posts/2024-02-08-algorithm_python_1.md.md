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

