---
layout: single
title:  "[알고리즘 Python] 파이썬에서 리스트 크기, 1초당 연산 횟수"
excerpt: "이것이 코딩 테스트다"

categories: AlgorithmPython
tag: [Python, Algorithm]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-02-08
last_modified_at: 2024-02-08
typora-root-url: ../
---

# 파이썬에서 리스트 크기

| 데이터의 개수(리스트의 길이) | 메모리 사용량 |
| ---------------------------- | ------------- |
| 1,000                        | 약 4KB        |
| 1,000,000                    | 약 4MB        |
| 10,000,000                   | 약 40MB       |





------

# 1초당 연산 횟수

2020년 기준 파이썬 3.7 코드로 작성할 때 1초에 2,000만 번의 연산을 수행한다고 가정하고 문제를 풀면 안정적으로 풀 수 있다.



**Pypy3를 이용한다면 2000만번에서 1억 번 정도의 연산을 1초에 처리할 수 있다**