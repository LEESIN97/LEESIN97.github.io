---
layout: single
title:  "[Python] 시간과 메모리 측정"
excerpt: "이것이 코딩테스트다"

categories: Useful_code
tag: [Python, time]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-08
last_modified_at: 2024-02-08
typora-root-url: ../
---

# 시간과 메모리 측정

알고리즘의 소요 시간을 확인하고 싶을 때, 효율성을 측정하고 싶을 때 다음과 같은 코드로 시간을 측정할 수 있다.

```python
import time
start_time = time.time() # 측정 시작
(어떤 알고리즘의 코드)
end_time = time.time() # 측정 종료
print("time:", end_time - start_time) # 수행시간 출력
```

