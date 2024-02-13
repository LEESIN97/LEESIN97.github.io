---
layout: single
title:  "[리눅스] unhatched linux(3)"
excerpt: "Networking academy Winter 2022 Linux Unhatched - MY Engineering Camp"

categories: linux
tag: [linux, os, linux_command_syntax]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2023-01-08
last_modified_at: 2023-01-08
---

## Network Configuration

<br/>

```C
ifconfig [OPTINS]
```

ifconfig command는 일시적으로 네트워크 세팅을 바꿀수 있다. 하지만 드물게 사용한다.

ping command는 두개의 컴퓨터 사이의 연결확인을 할 수 있다.

ping command는 계속해서 지정된 ip주소에 packets을 보낸다.

<br/><br/>

## Viewing Processes

<br/>

```C
ps [OPTIONS]
ps -e //view every process
ps -ef //view more detail
```

<br/><br/>

## Package Management

<br/>

Package management 는 시스템이 설치되거나 업데이트되거나 등등 하게 할수있는 시스템이다.

많은 Package managemnet는 administrative access가 필요하다.

패키지를 선택하고 업데이트(설치), 제거할 수 있다.
