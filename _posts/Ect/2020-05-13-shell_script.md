---
title: "쉘 스크립트란?, 쉘 스크립트 작성하기"
date: 2020-05-12 20:00:28 -0400
categories: etc
tags : [shell script]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 개요
- 요새 면접 스터디를 하면서 스터디 과제를 깃허브에 정리하고 있다.
- 스터디 전후에도 계속 공부하려고 정리하고 있는데, 정리하는 것이 굉장히 __단순 반복 작업이라__ 귀찮아 죽겠다..
- 제일 귀찮은게 구글시트에서 스터디 주제를 복사 -> 복사한것에 공백을 하나씩 제거 후 제목마다 * 달기 -> 과목 파일에 제목들 넣고, 링크 만들어주기 -> 내용마다 ### 달아주기
- 이 부분을 __쉘 스크립트를 이용해서 제목들만 입력하면 알아서 만들어주고, 나는 copy&paste__ 할수있게 하려고한다.

## 스크립트란?
- 일반적으로 Interpret 방식으로 동작하는 __컴파일 되지 않는 프로그램__
- text형식으로 저장되는 프로그램, __한 줄씩 순차적으로 읽어서 실행__ 되도록 작성된 프로그램
- 종류 : 쉘 스크립트, 자바 스크립트, 펄 스크립트 등
	- 스크립트를 읽어 __실행해주는 인터프리트 엔진__ 에 따라 나뉜다.
	- __쉘 스크립트 : 운영체제의 쉘(bash, ksh, csh..)__
	- 자바 스크립트 : 웹브라우저
	- 펄 스크립트 : perl


## 코드

```shell script
#! /bin/bash

########################
## 과목별로 실행 해준다
########################

function solution(){

	# 1. 목록에 * 달아 주기
	i=0
	for list in "${lists[@]}"; do
		if [ $i -ne "0" ]
		then
			echo "* $list"
		fi
		i=$((i+1))
	done

echo ""

	# 2. * 제목 입니다(#제목-입니다) ; 형태로 만들기
	i=0
	answer=""
	for list in "${lists[@]}"; do
		# 공백 정확히 입력해야 if문 오류안난다
		if [ $i -ne "0" ]
		then
			# tr은 치환한것을 echo만 해줄뿐, 치환한것을 변수에 저장 못한다
			# 따라서 echo한것을 answer에 입력
			answer=$(echo "(#$list)" | tr ' ' '-')
			echo "* [$list]${answer}"
		fi
		i=$((i+1))
	done

echo ""

	# 3. ### 달아주기
	i=0
	for list in "${lists[@]}"; do
    	if [ $i -ne "0" ]
       	then
            echo "## $list";
    	fi
    	i=$((i+1))
	done

echo ""

	# 4. 태그 달아주기

	type=${lists[0]}

tag="> :arrow_double_up:[Top](#${type})
\n:leftwards_arrow_with_hook:[Back](https://github.com/devham76/tech-interview-studyw#${type})
\n:information_source:[Home](https://github.com/devham76/tech-intervie-studyw#tech-interview)"

echo -e $tag  # 줄바꿈유지
echo ""
echo "-------------------------------------"
echo ""
}


########################
## 1. 파일 돌면서 공백이 나오기 전까지 실행
########################

# 1. file.txt 파일에 있는 목록 읽기
lists=()
i=0
while read LINE; do
	# 해당 줄이 공백이 아니면 계속 읽는다
	if [ -z "$LINE" ];
	then
		solution $lists[@]
		lists=()
		i=0
	else
        	# 공백 포함시, 따옴표 필수
		lists[$i]="${LINE}"
        	i=$((i+1))
	fi

done < file.txt



```

## 결과

```shell
$ cat file2.txt
3-os
this 키워드
자바에서 tcp udp 소켓 생성 방법
리틀엔디안 빅엔디안
Reflection
oop 5대 원칙

2-network
iocp
http keep alive / tcp keep alive
ssl
tcp udp 패킷구조 차이점
리피터, 허브, 브릿지, 라우터와 L2, L3, L4, L7 스위치 차이점

//----------------------------


$ sh start.sh
* this 키워드
* 자바에서 tcp udp 소켓 생성 방법
* 리틀엔디안 빅엔디안
* Reflection
* oop 5대 원칙

* [this 키워드](#this-키워드)
* [자바에서 tcp udp 소켓 생성 방법](#자바에서-tcp-udp-소켓-생성-방법)
* [리틀엔디안 빅엔디안](#리틀엔디안-빅엔디안)
* [Reflection](#Reflection)
* [oop 5대 원칙](#oop-5대-원칙)

## this 키워드
## 자바에서 tcp udp 소켓 생성 방법
## 리틀엔디안 빅엔디안
## Reflection
## oop 5대 원칙

> :arrow_double_up:[Top](#3-os)
:leftwards_arrow_with_hook:[Back](https://github.com/devham76/tech-interview-studyw#3-os)
:information_source:[Home](https://github.com/devham76/tech-intervie-studyw#tech-interview)

-------------------------------------

* iocp
* http keep alive / tcp keep alive
* ssl
* tcp udp 패킷구조 차이점
* 리피터, 허브, 브릿지, 라우터와 L2, L3, L4, L7 스위치 차이점

* [iocp](#iocp)
* [http keep alive / tcp keep alive](#http-keep-alive-/-tcp-keep-alive)
* [ssl](#ssl)
* [tcp udp 패킷구조 차이점](#tcp-udp-패킷구조-차이점)
* [리피터, 허브, 브릿지, 라우터와 L2, L3, L4, L7 스위치 차이점](#리피터,-허브,-브릿지,-라우터와-L2,-L3,-L4,-L7-스위치-차이점)

## iocp
## http keep alive / tcp keep alive
## ssl
## tcp udp 패킷구조 차이점
## 리피터, 허브, 브릿지, 라우터와 L2, L3, L4, L7 스위치 차이점

> :arrow_double_up:[Top](#2-network)
:leftwards_arrow_with_hook:[Back](https://github.com/devham76/tech-interview-studyw#2-network)
:information_source:[Home](https://github.com/devham76/tech-intervie-studyw#tech-interview)

-------------------------------------

```
