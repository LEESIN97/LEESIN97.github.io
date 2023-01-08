---
layout: single
title:  "unhatched linux(2)"
excerpt: "Networking academy Winter 2022 Linux Unhatched - MY Engineering Camp"

categories: etc
tag: [linux, os, linux_command_syntax]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true
 
date: 2023-01-08
last_modified_at: 2023-01-08
---



## Access

<br/>

```C
su OPTIONS USERNAME
    
//logint shell option
su -
su -l
su --login
    
exit //logout
sl //administrative access
```

su command는 일시적으로 새로운 shell을 만들어 다른 유저처럼 행동할 수 있게 한다.

<br/>

```c
sudo [OPTIONS] COMMAND
sudo sl // administrative access
```

sudo command는 새로운 shell을 만들지 않고도 다른 유저처럼 행동할 수 있다.



 <br/><br/>



## Permissions

<br/>

user가 파일이나 directory와 상호작용할 수 있게하는 방법을 정한다.



### Perimissions Field

ex) -rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh

* -**rw**-r--r-- 1 **sysadmin** sysadmin 647 Dec 20  2017 hello.sh : Owner -> read, write 권한
* -rw-**r**--r-- 1 sysadmin **sysadmin** 647 Dec 20  2017 hello.sh : Groupt -> read 권한
* -rw-r--**r**-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh : Other -> read 권한

<br/><br/>



## Changing File Permissions

<br/>

chmod command를 이용해 파일의 Permission을 변경한다.

```C
chmod [<SET><ACTION><PERMISSIONS>]... FILE	
```

SET> 

* u : user who owns the file
* g : group who owns the file
* o : u와g가 아닌 것들
* a : all

ACTION>

* '+' : add
* '=' : Specify the exact permission
* '-' : remove

PERMISSION>

* r 
* w
* x

<br/><br/>

## Changing File Ownership

<br/>

chown command는 file과 directory의 ownership을 바꾼다.

```c
chown [OPTIONS] [OWNER] FILE
```

**먼저 administrative privileges를 얻기 위해 sudo prefix를 사용해야한다.**

ex)

```c
sudo chown root hello.sh //현재의 디렉토리에서 root로 owner를 바꾸는 명령어
```

<br/><br/>

## Viewing Files

<br/>

cat command는 전체 file의 내용을 보여준다. (주로 내용이 짧은 파일)

(긴 파일에 경우 head와 tail command를 사용)

```c
cat [OPTIONS] [FILE]
```

<br/>

<br/>

## Copying Files

<br/>

```C
cp [OPTIONS] SOURCE DESTINATION
CP /etc/passwd . // /etc/passwd 파일 전체를 현재 directory에 복사
dd [OPTIONS] OPERAND
// /dev/zero 파일을 읽어서 /temp/swapex 로 1M * 50 을 저장
dd if=/dev/zero of=/temp/swapex bs=1M counts=50
```

<br/><br/>

## Moving Files

<br/>

```C
mv SOURCE DESTINATION
```

mv command는 파일을 SOURCE 에서 DESTINATION 디렉토리로 옮긴다.

이 command를 이용해서 rename을 효율적으로 할 수 있다.

<br/><br/>

## Removing Files

<br/>

```C
rm [OPTINS] FILE	
```

rm Command 는 영구적으로 file을 삭제한다.

directory 전체를 삭제하려면 다음과 같다.

```c
rm -r Directory
```

<br/><br/>

## Filtering Input

<br/>

```c
grep [OPTIONS] PATTERN [FILE]
```

grep Command는 파일이 클 경우에 찾고자 하는 Pattern을 입력해 파일에서 그 부분의 결과를 출력한다.

여러가지 Expression이 있다. (basic, extended) 이를 참조할것.

<br/><br/>

## Shutting Down

<br/>

```C
shutdown [OPTIONS] TIME [MESSAGE]
// Example
shutdown 01:51
shutdown +1 "good bye"
shutdown now
```

시스템이 안전한 방법으로 중단되도록 한다.

default로 5분뒤, 시간을 설정할 수도 있다. (메시지도 추가적으로 넣을 수 있음)



