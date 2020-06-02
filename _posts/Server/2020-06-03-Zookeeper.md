---
title: "Server, ZooKeeper"
date: 2020-06-03 15:40:28 -0400
categories: [Server]
tags : [ZooKeeper, Server]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### 코디네이션 시스템
- 분산 시스템 설계의 문제점을 해결하는 서비스 시스템
	- 1.분산된 시스템간 정보를 어떻게 공유할것이고
	- 2.클러스터에 있는 server들의 상태를 확인할 필요가 있고
	- 3.분산된 server간 동기화를 위한 lock을 처리하는 것

- 분산 시스템은 각각의 어플리케이션이 돌아가는 환경, N/W가 달라 장애 발생시 정확한 진단을 내리기 어렵다

- 분산 시스템 내에서 중요한 상태 정보나 설정 정보 등을 유지한다.
- 고가용성을 제공
	- 코디네이션 서비스의 장애는 전체 시스템의 장애를 유발할수 있으므로,  이중화등을 통해 고가용성을 제공
- 종류
	- ZooKeeper가 있고 ( NoSQL의 한종류인 Apache, 대용량 분산 큐 시스템 Kafka ) 에 사용된다

## 주키퍼(Zookeeper)
- 오픈소스

- 목적
	- 분산 처리 시스템을 이루는 수많은 프로세스들이 안전하고 원활하게 서비스 할 수 있도록 도와준다
	- 개발자가 분산 코디네이션 로직보다 __비즈니스 핵심 로직에__ 집중 하게끔 지원하는 역할을 한다
- 특징
	- 분산 시스템을 코디네이션 하는 용도로 디자인
	- data access가 빠르다
	- 자체적으로 장애에 대응성 가진다 (장애애도 data 유실없이 fail over/fail back가능)
	- 주키퍼는 직접 어플리케이션의 작업을 조율하지 않는다. 구성 요소들을 조율하는건 서버 개발자의 책임, 주키퍼는 이를 쉽개 개발 할수 있도록 도와줌
	- 분산 시스템에서 동시성으로 인해 생기는 잘못된 동작 차단

- 주키퍼가 다루는 정보
	- 서버들의 설정 정보, 클러스터 구성시 마스터 서버
	- 각각의 작업에 할당되어 있는 서버가 무엇인지 등의 정보

### 주키퍼가 사용되는 서비스
1. Apache HBase
	- Hadoop에서 사용되는 HBase는 cluster master를 선출하기 위해 주키퍼를 사용
	- 현재 __이용 가능한 서버가 어떤 것들이 있는지__ 정보 저장, cluster의 메타 데이터 보관에 쓰인다
2. Apache Kafka
	- kafka server 크래시를 감시하기 위해 사용된다
	- 새로운 토픽생성시 , __토픽의 생성과 소비 상태를 저장하기__ 위해 주키퍼 도입

### 구성
- Leader Follower로 구성되는 __Master-Slave__ 아키텍처
- 디렉토리 형태의 data 저장소
- znode라는 data 저장 객체(key,value)식.
- 이 객체에 data를 넣고 빼는 기능만 제공
- watcher
	- 특정 znode에 watch걸어놓으면, 해당 znode가 변경시 client에게 callback호출날린다
	- client가 해당 znode가 변경된걸 알게도고, watcher 삭제된다

### ZooKeeper 활용 시나리오
- 큐
	- watcher와 sequence node를 이용하면 큐 생성가능
	- queue라는 node를 만들고, 이 노드의 chide node를 sequence node로 구성하면, 새롭게 생성되는 메시지 들은 sequence node로 순차적으로 생성
	- 이 큐를 읽는 client가 큐node를 watch하도록 설정하면,
	- 메시지가 들어올 때 마다 call back을 받아서, 마치 메시지 queue의 pub/sub 형태
	- 대용량 메시지&애플리케이션은 MQ(Rabbit MQ등)을 활용하고
	- ZooKeeper는 클러스터간 통신용 큐로 활용하는것 고려

---
## 참고
- [분산 코디네이터 Zookeeper(주키퍼) 소개](https://bcho.tistory.com/1016)
- [Zookeeper](https://brunch.co.kr/@timevoyage/77)
