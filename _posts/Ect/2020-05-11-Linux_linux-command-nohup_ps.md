---
title: "Linux, 명령어 - nohup, ps"
date: 2020-05-11 20:00:28 -0400
categories: etc
tags : [Linux]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## ps(Process Status)
- 리눅스 프로세스 확인 명령어

|옵션| 설명|
|--|--|
|-e| 모든 프로세스 출력|
|-f| 풀 포맷 출력 (uid, pid)|
|-l | 긴 포맷으로 출력 |
|p, -p| 특정 pid의 프로세스 출력|
|-u| 특정 사용자의 프로세스 출력|

- ps -ef | grep apache(모든 프로세스의 출력값을 grep을 이용하여 apache가 포함된 라인들을 출력)

```
[ec2-user@springboot2-webservice ~]$ ps -ef | grep java
ec2-user   543   462  0 19:41 pts/0    00:00:00 grep --color=auto java
ec2-user 21347     1  0 May04 ?        00:09:20 java -jar -Dspring.config.location=classpath:/application.properties,classpath:/application-real.properties,/home/ec2-user/app/application-oauth.properties,/home/ec2-user/app/application-real-db.properties -Dspring.properties.active=real /home/ec2-user/app/step2/springboot2-webservice-1.0.1-SNAPSHOT.jar

```

## nohup
* 리눅스, 유닉스에서 쉘스크립트파일(*.sh)을 데몬형태로 실행시키는 프로그램
* nohup은 리눅스에서 쉘스크립트파일을 데몬형태로 실행시키는 명령어이다.


## 실행 시키기

```
$nohup [실행파일]
$nohup [실행파일] & // 백그라운드 실행
```

## nohup 종료하기

```
1. "ps -ef | grep 쉘스크립트파일명" // 명령으로 데몬형식으로 실행
2. "kill -9 PID번호" // 명령으로 해당 프로세스 종료
```

- ex)

```
//-- 실행
$ nohup php daemon1.php &

//-- 확인
$ ps -ef | grep daemon1.php
root      5376 49641  0 Apr18 pts/3    00:02:22 php daemon1.php

//-- 종료
$ kill 5376

```

---
## 참고
- <https://arer.tistory.com/150>
- <https://jasontody.tistory.com/113>
