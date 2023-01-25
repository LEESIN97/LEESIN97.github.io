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

```python
# example
def square(x):
    return x*x
f = square
f(5)

def cube(x):
    return x*x*x

def formula(method, argument_list):
    return [method(value) for value in argument_list]
```

위의 예시에서 formula 함수는 필요한 함수를 매개변수로 받아와 매핑해서 이용할수 있다.

* 클로저

inner function을 return값으로 반환한다.

이해하기 위해 예시를 들면

```python
def outer_func(tag): 
    tag = tag 

    def inner_func(txt): 
        text = txt  
        print('<{0}>{1}<{0}>'.format(tag, text))  

    return inner_func 

h1_func = outer_func('h1') 
p_func = outer_func('p') 

h1_func('h1 태그의 안입니다.') 
p_func('p 태그의 안입니다.')

```

클로저는 하나의 함수로 여러가지의 함수를 간단히 만들어낼 수 있게 도와준다.

이때 tag라는 변수는 프리변수이고, inner_func에서 tag라는 변수를 참조하여 사용한다.

<br/>

이 두개의 특성을 데코레이터는 가진다.

<br/>

사용하는 이유? : 기존의 코드를 수정하지 않고 wrapper 함수를 이용하여 여러가지 기능을 추가할 수가 있다.

```python
def star(func):
    def inner(*args, **kwargs):
        print("*"*30)
        func(*args, **kwargs)
        print("*"*30)
    return inner

def percent(func):
    def inner(*args, **kwargs):
        print("%"*30)
        func(*args, **kwargs)
        print("%"*30)
    return inner

@star
@percent
def printer(msg):
    print(msg)

printer("hello")
```

