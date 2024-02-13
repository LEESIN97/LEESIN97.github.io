---
layout: single
title:  "[리눅스] unhatched linux(1)"
excerpt: "Networking academy Winter 2022 Linux Unhatched - MY Engineering Camp"

categories: linux
tag: [Linux]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2022-12-30
last_modified_at: 2023-01-02

---

<br/><br/>

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

```c
ls -l -r //long display, 알파벳순서를 거꾸로
ls -rl //long display, 알파벳순서를 거꾸로
ls -lr //long display, 알파벳순서를 거꾸로
```

<br/>



## printing working directory

<br/>

파일시스템안에 현재 어디위치 하는지 찾기 위해서 pwd 명령어를 사용한다.

```c
sysadmin@localhost:~$ //여기에서 ~가 현재 directory를 의미 한다.
```



<br/>

<br/>



## Changing Directories

<br/>

```c
cd [options] [path]
```

현재의 directory에서 path로 directory를 변경한다.

Linux directory structure에서 root directory는 /로 표현된다.



path는 단계별 방향이다.

* absolute path

​		filesystem의 root에서 시작한다. (/부터 시작)

```c
sysadmin@localhost:/$ cd /home/sysadmin
sysadmin@localhost:~$ pwd // /home/sysadmin 출력
```



* relative path :

​		current location에서 시작한다. 현재의 directory에서 순차적으로 ex) 다음 directory/그 다음 directory

```c
sysadmin@localhost:~$ cd Documents
sysadmin@localhost:~/Documents/$ cd School/Art
```



short cut)

```c
cd .. //상위 directory로 이동
cd ~ // home directory인 /home/sysadmin으로 바로 이동
```

<br/><br/>

## Listing Files

<br/>

```c
ls [options] [file]
```

 ```c
 ls -l /var/log //file을 long listing
 ```

위에서와 같이 file을 long listing 하게 되면 여러파일들이 출력되는데 그중 하나는 다음과 같이 출력이 된다.

```
-rw-r--r-- 1 root   root  18047 Dec 20  2017 alternatives.log

```

맨앞의 symbol은 filetype을 의미한다.

* d, directory  : 다른 파일들을 저장하는데 쓰인다.
* -, regular file : 읽기 가능한 파일, 이미지 파일, 바이너리 파일, 압축파일을 포함한다.
* l, symbolic link : 다른 하나의 파일을 가리킨다.
* s, socket : 프로세스간의 통신을 허용
* p, pipe : 프로세스간의 통신을 허용
* b, block file : 하드웨어와 커뮤니케이션에 사용
* c, character file : 하드웨어와 커뮤니케어션에 사용

<br/>

맨 앞의 symbol 이후의 문자들을 자세히 살펴보면

* -**rw-r--r--** 1 root   root  18047 Dec 20  2017 alternatives.log

  rw-r--r--1 : permissions (특정 사용자가 파일을 액세스할 수 있는 방법)

* -rw-r--r-- **1** root   root  18047 Dec 20  2017 alternatives.log

  1 :  Hard Link Count

* -rw-r--r-- 1 **root**   root  18047 Dec 20  2017 alternatives.log

  root : User Owner, 자동적으로 생성될 때 만든 이에게 배정이 된다.

* -rw-r--r-- 1 root   **root**  18047 Dec 20  2017 alternatives.log

  root : 어떠한 그룹이 이 파일을 가지고 있는지 나타낸다.

* -rw-r--r-- 1 root   root  **18047** Dec 20  2017 alternatives.log

  18047 : 파일 사이즈를 나타내는데, 큰 파일이나 디렉토리는 킬로바이트로 나타난다. 그래서 실제로는 디렉토리에 경우 block size(파일 시스템에서 사용되는 데이터의 크기) 의 배수로 표현

* -rw-r--r-- 1 root   root  18047 **Dec 20  2017** alternatives.log

  Dec 20 2017 : 타임스탬프

* -rw-r--r-- 1 root   root  18047 Dec 20  2017 **alternatives.log**

  alternatives.log : 파일 이름



마지막에 -> 화살표가 있는 경우가 있는데 다른 하나의 파일을 가리키는 것이다.

화살표로 표시하고 original file의 pathname을 표시한다.

<br/>



### sorting

<br/>

```
ls -lt /var/log // timestamp 순으로 long listing
ls -l -S /var/log // size순으로 long listing
ls -lSr /var/log // size역순으로 long listing

```



