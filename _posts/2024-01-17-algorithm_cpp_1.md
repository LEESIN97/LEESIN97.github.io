---
layout: single
title:  "[알고리즘 C++] 준비"
excerpt: "Do it! 알고리즘 코딩 테스트 - C++편"

categories: AlgorithmCpp
tag: [Algoritm_C++]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-01-17
last_modified_at: 2024-01-17
---

## 시간 복잡도

<br/>

모든 테스트 케이스를 염두에 둬야 하기 때문에 빅-오 표기법(O(n))을 기준으로 수행 시간을 계산한다. 

빅-오 표기법으로 시간복잡도를 계산해 데이터의 최대 크기를 대입하여 대략적인 시간을 계산할 수 있다. (이 떄 1초에 1억번 연산으로 기준을 잡는다.)

<br/><br/>

## 수정렬하기

<br/>

- 시간 제한 2초
- 백준 온라인 저지 2750번

버블 정렬 : $$(1000000)^2 > 200000000  부적합$$

병합 정렬 : $$1000000log_2(1000000) < 200000000  적합$$

<br/><br/>

## 시간 복잡도 도출



<br/>

- 상수는 시간 복잡도 계산에서 제외한다.
- 가장 많이 중첩된 반복문의 수행 횟수가 시간 복잡도의 기준이 된다.

