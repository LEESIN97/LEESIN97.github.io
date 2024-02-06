---
layout: single
title:  "코테를 위한 파이썬 문법"
excerpt: "이것이 코딩테스트다"

categories: Useful code
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
print(a)

if a == 0.9:
	print(True)
else:
	print(False)
```



