---
title: "Server, Kafka"
date: 2020-06-03 15:40:28 -0400
categories: [Server]
tags : [Kafka, Server]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 기존 메시징 시스템 vs Kafka
|기존|Kafka|
|--|--|
|producer 메시지 전송시, 메시지 개별전송 | 다수의 메시지를 batch형태로 한번에 전달 (tcp/ip라운드트립 횟수 줄임)|
|메시지 메모리에 저장<br>처리 안된 메시지가 많을 수록 성능 감소 | 파일시스템에 저장<br> 메시지 남아도 성능 괜찮.  |
|consumer가 메시지 사용후 바로 삭제| 바로 삭제 안하고 일정 기간 저장<br>consumer장애발생시 복구 후 메시지 사용가능|
|broker->consumer push<br>consumer는 어떤 메시지 처리해야 하는지 tracking,계산| pull<br>consumer가 처리가능한 만큼 pull하기 때문에 성능 최적<br>broker는 message,consumer 관리에 대한 부담이 줄어듬|


### 공통점
  - 비동기 시스템
  -
### 기존 메시싱 시스템
- 목적
  - 메시지 보관,교환,전달의 신뢰성 보장 -> 따라서 내부 프로세스 복잡,  / 속도, 용량 小

### 카프카
- 목적
  - 실시간 대량 전송 , 따라서 신뢰성관리는 pub/sub에게 넘긴다.
- 큐에서 consumer로 push하는 기능은 부하가 많이 걸리는데
consumer가 pull해서 메시지 전달성능에 집중시켜 고성능화 했다

## 카프카
![카프카 기본](https://user-images.githubusercontent.com/55946791/83614255-e951a500-a5bf-11ea-9cf9-5fa338eeeb7e.jpg)
1. __producer,consumer는 각자의 역할이 정확하게 분리__
- 카프카를 사용하지 않고 분리한다면,
	- 하나의 웹서버+모니터링 서버, 로그분석 서버, 데이터 저장 서버...
	- 새로운 웹서버를 추가한다면, 연동해야할 시스템이 많아진다
	- 만약, 모니터링 서버에 문제가 생긴다면 모니터링 서버와 관련된 다른 서비스에도 문제발생가능
- 카프카를 사용한다면,
	- __새로운 웹서버 추가 용이__
	- 서버 장애발생시, __연쇄 작용 발생 확률 낮다__

2. multi producer,consumer
- producer는 하나이상의 토픽에서 메시지 전송 가능
- consumer는 하나이상의 토픽에서 메세지 수집 가능

3. 디스크에 메세지 저장
- 일반메시징 시스템 : consumer가 message읽으면 바로 삭제
- __일정 기간동안 disk에 메시지 저장__
- 활용 방법
  - 트래픽이 일시적으로 폭주해서 consumer처리가 늦어져도 disk에 안전하게 보관되어있어 message손실없다
  - consumer에 장애 발생시, 잠시 중단 후 재실행 해도 message는 disk에 저장되어있어서 손실 없이 작업가능

4. 확장성
- 카프카 클러스터는 무중단으로 손쉽게 확장 가능하다

5. 높은 성능
- 고성능을 유지 하기 위해 내부적으로 분산처리, 배치 처리 등 하고있다
  - __분산 시스템__
    - 카프카는 분산 시스템이므로 유동적으로 서버를 늘릴수 있다.
    - 서버를 늘려서 서버당 처리량 줄이고, 장애발생시 연쇄작용 없앤다
  - 배치처리
    - server&client가 data주고 받을때 I/O작업이 실행된다.
    - __I/O작업을 최소화 하기 위해 작은 메시지는 묶어서 한번에__ 보낸다.

## 카프카 용어
### 브로커
	- 카프카가 설치되어 있는 서버 또는 노드

### 프로듀서
  - 메시지 생산, 브로커에 토픽이름으로 보내는 서버 또는 애플리케이션
### 컨슈머
  - 브로커의 토픽 이름으로 저장된 메시지 가져가는 서버 또는 애플리케이션

### 토픽
![카프카 토픽](https://user-images.githubusercontent.com/55946791/83614252-e8b90e80-a5bf-11ea-8b3c-03c5caa48711.jpg)
- producer,consume가 카프카로 보낸 자신들의 __메시지를 구분하기 위한 네임__
- 메시지를 받을 수 있도록 __논리적으로 묶은 개념__
- 토픽이라는 이름으로 구분해서 사용

### 파티션
![카프카 파티션](https://user-images.githubusercontent.com/55946791/83614249-e8207800-a5bf-11ea-98ab-caad9d30f811.jpg)
- 메시지 순서를 보장해야 해서, __관련이 없는 메시지를 동시에 많이 전송하려면 파티션에 병렬로 보낸다.__
- 토픽을 구성하는 데이터 저장소, 수평 확장이 가능한 단위

- _무조건 파티션 수를 늘리면안된다_
  - 파티션은 브로커의 디렉토리와 매핑되고 , 데이터마다 2개의 파일을 갖게 되므로 리소스 낭비

### 오프셋
![카프카 오프셋](https://user-images.githubusercontent.com/55946791/83614246-e787e180-a5bf-11ea-8194-1b4e4ff9eff7.jpg)
- 오프셋으로 메시지 __순서 보장__
- 각 파티션마다 메시지가 __저장되는 위치__
- 오프셋은 __파티션 내에서 유일하고, 순차적으로 증가하는 숫자__


## 카프카의 고가용성 & 파티션 리플리케이션
![카프카 파티션 복제](https://user-images.githubusercontent.com/55946791/83614242-e656b480-a5bf-11ea-9194-cf35b28b7c51.jpg)
- 서버의 물리적 장애 발생을 대비해 토픽을 이루는 __각각의 파티션을 리플리케이션한다__
- 리더(원본 - 읽기,쓰기) & 팔로워(복사본 - 복사만함.)
- 리더가 있던 브로커 장애 발생시, 팔로워가 새로운 리더가 된다

---
## 로컬에서 실습
1. 주키퍼 시작
- zookeeper-server-start.bat ../../config/zookeeper.properties
![카프카-주키퍼화면](https://user-images.githubusercontent.com/55946791/83629354-e7461100-a5d4-11ea-8855-1c3036bc8364.JPG)
- 주키퍼 종료
  - bin/windows/zookeeper-server-stop.bat config/zookeeper.properties
2. 카프카 서버시작
- kafka-server-start.bat ../../config/server.properties
![카프카-서버시작 화면](https://user-images.githubusercontent.com/55946791/83629352-e614e400-a5d4-11ea-80c9-9b9f323e2244.JPG)
- kafka 종료
  - bin/windows/kafka-server-stop.bat config/server.properties


3. 카프카 토픽생성 후 producer에서 메시지 생성
- 토픽생성
  - kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
- producer topic에 메세지 생성
  - kafka-console-producer.bat --broker-list localhost:9092 --topic test
- 메세지 조회
  - kafka-console-producer.bat --broker-list localhost:9092 --topic REQ-LOG
![카프카-토픽생성 producer](https://user-images.githubusercontent.com/55946791/83629357-e8773e00-a5d4-11ea-9249-af190b8e4f31.JPG)

4. 카프카 컨슈머측에서 확인
![카프카-컨슈머](https://user-images.githubusercontent.com/55946791/83629356-e7dea780-a5d4-11ea-8561-b1c1aa8ddde8.JPG)

5. 카프카 토픽리스트
kafka-topics.bat --list --zookeeper localhost:2181
![카프카-토픽리스트](https://user-images.githubusercontent.com/55946791/83629355-e7dea780-a5d4-11ea-9956-785afc696558.JPG)


---
## 참고
- [카프카, 데이터 플랫폼의 최강자]<http://www.yes24.com/Product/Goods/59789254>
- <https://epicdevs.com/17>
- <https://soul0.tistory.com/498?category=755055>
- <https://d2.naver.com/helloworld/7731491>
