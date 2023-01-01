---
layout: single
title:  "unhatched linux(1)"
excerpt: "Networking academy Winter 2022 Linux Unhatched - MY Engineering Camp"

categories: etc
tag: [linux, os, linux_command_syntax]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true
 
date: 2022-12-30
last_modified_at: 2023-01-02

---

<br/>

# Basic Command Syntax

<br/>

<br/>

## command

<br/>



```c
sysadmin@localhost:~$ ls
-bash: /usr/games/LS: Permission denied
```

다음과 같은 형식을 따른다.

command [options...] [arguments...] 

* arguments  : 명령이 수행할 항목을 지정.
* options : 옵션을 사용하여 명령의 동작을 변경한다.

ex) ls is displays a listing of information about files. command를 설정된 options에 따라 directory가 argument인 곳에서 실행 

 만약 options와 arguments를 입력하지 않았다면 현재의 directory의 list of files를 display한다.

**대문자와 소문자는 다른 명령을 가진다는 점을 유의하자.**



<br/>

<br/>



## options

<br/>

options을 설정해 command의 동작을 변경할수가 있다.

```c
sysadmin@localhost:~$ ls
-bash: /usr/games/LS: Permission denied
```

 ex) command ls는 default값으로 알파벳 순서로 한행에 길게 listing 한다.

이 명령어 ls를 다음과 같이 option을 변경할 수 있다.

```
ls -l -r //long display, 알파벳순서를 거꾸로
ls -rl //long display, 알파벳순서를 거꾸로 
ls -lr //long display, 알파벳순서를 거꾸로
```

<br/>



# Printing working directory

<br/>



