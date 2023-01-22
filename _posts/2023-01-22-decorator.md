---
layout: single
title:  "Decorator"

categories: Python
tag: [Python, pythonic code, syntax]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true
 
date: 2023-01-22
last_modified_at: 2023-01-22
---

## Decorator

<br/>

데코레이터를 이해하기 위해서 퍼스트 클래스 함수, 클로저를 이해해야한다.

<br/>

* 퍼스트클래스 함수

퍼스트클래스 함수란 함수자체를 인자(argument)로써 다른 함수에 전달하거나 다른 함수의 결과값으로 리턴 할 수 있고, 함수를 변수에 할당하거나 데이터 구조안에 저장할 수 있음을 의미한다.



* 클로저

이해하기 위해 예시를 들면

```python
def outer_func(tag):  # 1
    tag = tag  # 5

    def inner_func(txt):  # 6
        text = txt  # 8
        print('<{0}>{1}<{0}>'.format(tag, text))  # 9

    return inner_func  # 7

h1_func = outer_func('h1')  # 2
p_func = outer_func('p')  # 3

h1_func('h1 태그의 안입니다.')  # 4
p_func('p 태그의 안입니다.')  # 10
```

클로저는 하나의 함수로 여러가지의 함수를 간단히 만들어낼 수 있게 도와준다.

이때 tag라는 변수는 프리변수이고, inner_func에서 tag라는 변수를 참조하여 사용한다.

<br/>

이 둘을 이해했다면 데코레이터라는 것이 무엇인지 살펴보자.

<br/>

사용하는 이유? : 기존의 코드를 수정하지 않고 wrapper 함수를 이용하여 여러가지 기능을 추가할 수가 있다.

```python
def decorator_function(original_function):
    def wrapper_function(*args, **kwargs):  #1
        print('{} 함수가 호출되기전 입니다.'.format(original_function.__name__))
        return original_function(*args, **kwargs)  #2
    return wrapper_function


@decorator_function
def display():
    print('display 함수가 실행됐습니다.')


@decorator_function
def display_info(name, age):
    print('display_info({}, {}) 함수가 실행됐습니다.'.format(name, age))


display()
print()
display_info('John', 25)
```

