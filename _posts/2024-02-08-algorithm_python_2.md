---
layout: single
title:  "[알고리즘 Python] 구현"
excerpt: "이것이 코딩 테스트다 - 저자 나동빈"

categories: AlgorithmPython
tag: [Algoritm_Python, 구현]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-08
last_modified_at: 2024-02-08
typora-root-url: ../
---

# 구현

'풀이를 떠오리는 것은 쉽지만 소스코드로 옮기기 어려운 문제'

알고리즘은 간단하나 코드가 길거나 까다로운 코드를 작성해야 하는 문제.

완전탐색, 시뮬레이션이 구현 문제유형에 해당한다.

  

------

## 왕실의 나이트

**내 풀이**

```python
current_pos = list(input())
x = int(ord(current_pos[0]) - ord('a') + 1) 
y = int(current_pos[1])
move_dx = [-2, -2, 2, 2, -1, -1, 1, 1]
move_dy = [-1, 1, -1, 1, 2, -2, 2, -2]

cnt = 0

for i in range(8):
  if 1 <= (x + move_dx[i]) <= 8 and 1 <= (y + move_dy[i]) <= 8:
    cnt += 1
print(cnt)
```

x 좌표 행렬에서 열은 문자로 a~h로 주어지므로 이를 unicode를 바탕으로 1~8로 정수로 바꾸는 과정이 필요하다. 그 후 모든 경우에 대해서 차례대로 이동시킨다는 점에서 시뮬레이션 유형으로 분류된다.



**답변 예시**

```python
input_data = input()
row = int(input_data[1])
column = int(ord(input_data[0])) - int(ord('a')) + 1

steps = [(-2, -1), (-1, -2), (1, -2), (2, -1), (2, 1), (1, 2), (-1, 2), (-2, 1)]

result = 0
for step in steps:
	next_row = row + step[0]
	next_colum = column + step[1]
	if nex_row >=1 and next_row <= 8 and next_column >= 1 and nex_column <= 8:
		result += 1
print(result)
```

------



# 게임 개발

**내 풀이**

```python
n, m = map(int, input().split())
a, b, dir = map(int, input().split())
step = [(-1, 0), (0, -1), (1, 0), (0, 1)]
map = [list(map(int, input().split())) for _ in range(n)]
cnt = 1
cant_go = 0
while True:
  if cant_go >=8:
    break
  if cant_go == 4:
    map[a][b] = 2
    a -= step[dir][0]
    b -= step[dir][1]
  if dir == 3: 
    dir = 0
  elif dir != 3:
    dir += 1
  if map[a + step[dir][0]][b + step[dir][1]] == 1 or map[a + step[dir][0]][b + step[dir][1]] == 2:
    cant_go +=1
    continue
  elif map[a + step[dir][0]][b + step[dir][1]] == 0:
    map[a][b] = 2 # 방문 check
    a += step[dir][0]
    b += step[dir][1]
    cnt += 1
    cant_go = 0


print(cnt)
```

내가 짠 코드는 4방향이 모두 이미 가본 칸이거나 바다인 경우에서 바라보는 방향을 유지한 채 뒤로 가는 과정에서 하나를 간과하였다.

뒤로 가는 곳이 갈 수 없는 공간일 수도 있는 경우도 고려해줘야 한다.

근데 생각을 해보면 무조건 뒤로 가는 경우가 나오는 것 같기도? ..
이부분이 문제라기보다는 맵을 설정을 할 때 맵의 외곽은 항상 바다라고 돼있으므로 추가적으로 1로 padding을 시켜주는게 적합하다고 생각한다.





근데 아래의 답변 예시 처럼 map에서 방문한 곳인지를 기록해둘 때 새로 2차원 list를 만들어서 하는 것이 더 수월한 것 같다.

```python
n, m = map(int, input().split())

d = [[0] * m for _ in range(n)]

x, y, direction = map(int, input().split())
d[x][y] = 1

array = []
for i in range(n):
	array.append(list(map(int, input().split())))
	
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

def turn_left():
	global direction
	direction -= 1
	if direction == -1:
		direction = 3
count = 1
turn_time = 0
while True:
	turn_left()
	nx = x + dx[direction]
	ny = y + dy[direction]
	if d[nx][ny] == 0 and array[nx][ny] == 0:
		d[nx][ny] = 1
		x = nx
		y = ny
		count += 1
		turn_time = 0
		continue
	else:
		turn_time += 1
	if turn_time == 4:
		nx = x - dx[direction]
		ny = y - dy[direction]
		if array[nx][ny] == 0:
			x = nx
			y = ny
		else:
			break
		turn_time = 0
print(count)
```

