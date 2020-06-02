---
title: "WEB, Web에서 client의 요청은 server에서 어떻게 처리될까?"
date: 2020-06-02 15:40:28 -0400
categories: WEB
tags : [WEB, WS, WAS]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

> [생활코딩 내 질문](https://www.facebook.com/groups/codingeverybody/permalink/4163827110324460/)


## Spring MVC란?
- 웹 통신의 핵심은 Servlet API이며, 이를 구현하는 서블릿 컨테이너(Tomcat , Jetty)를 기반으로 한다.
- Servlet은 통신이 client->server로 이동하는 방법이 매우 엄격하다

### Servlet이란
- 웹프로그래밍에서 client의 요청을 처리 후 결과값 전송하는 Servlet 클래스의 구현 규칙을 지킨 자바 프로그래밍 기술

## Webflux
- spring mvc와 반대로 __servlet에 의존하지 않는다.__
- 즉 servlet을 기반으로 구축 및 구축되지 않은 서버(Netty, Undertow)를 모두 사용할수 있다.

## Netty
- __asynchronous event-driven network application framework__
- 신속한 개발과 유지 보수가 가능한 고성능기능을 위한 framework
- 2개의 이벤트 루프를 사용한다 ( non-blocking io ) -> 이벤트 루프 그룹
- boss & worker
	- boss는 들어오는 연결을 수락, worker에게 등록
	- data가 사용가능하면, worker에게 알리고 데이터 처리

---

## How a Server works
- 요청하기 전에, client와 server는 자신의 소켓(포트)에 바인딩하여 연결을 설정해야한다.
- 서버가 소켓에서 수신 대기 하는 동안, client가 연결 요청을 보낸다
- 연결이 설정되면, client가 data를 전송하기 시작하고, server는 이를 처리하고 response를 보낸다.
- 이후 연결을 닫는다.
- 대부분의 시간으 연결 설정, 데이터 수신 기다리는데 소요된다


### Blocking IO
![blocking-io-1](https://user-images.githubusercontent.com/55946791/83483625-08780600-a4de-11ea-9097-aa34ef1a2bc9.png)
- 스레드가 하나의 connection을 관리하고 있으므로, 하나의 open connection만 있을 수 있다.
- 다른 client는 연결을 시도 하는 동안, 이미 open된 connection이 닫힐 때까지 아무 일도 일어나지 않는다

### Threaded-Blocking IO (쓰레드 차단 IO)
![threaded-blocking-io-1](https://user-images.githubusercontent.com/55946791/83484222-5e997900-a4df-11ea-92cf-caeebb9eec89.png)
- 새로운 모든 연결을 새로운 소켓에 binding하고 data를 처리할 __새로운 thread를 만든다__
- clinet -> server socket에 연결 요청시, 통신 할 new socket를 다시 보낸다
- cpu, os 제한에 따라 상당히 많은 thread를 만들 수 있기 때문에 충분하다
- 최대 thread 수의 limit에 도달 할 때 까지 여러 연결을 처리 가능
- __각 thread는 memory할당이 필요해서, 동시에 연결이 진행동안 서버 성능이 저하된다.__

### Non-Blocking IO
![nio-1](https://user-images.githubusercontent.com/55946791/83486322-ebdecc80-a4e3-11ea-8d0d-1b64bb00e0e7.png)

- thread를 연결하기 위해 binding하는 대신, __data를 buffer에서 읽을 준비가 되면 알림이 전송된다 (이벤트 루프)__
- NIO는 data를 read/write할때 __스트림 대신 버퍼를 사용한다.__
	- 요청할 모든 data가 다 준비되어 수신하는것이 아니라, 생성이 될때마다 처리 되기 때문에
- 이 매커니즘을 사용하면 하나의 thread로 여러 연결을 처리할 수 있다.
- 이것이 IO를 기다리는 동안 thread가 차단되지 않는 방법이다.
- thread는 new data의 도착에 대한 알림을 받을 때만 buffer를 읽는다 (이벤트 루프)

- 몇개의 thread만으로 동시에 많은 연결을 처리할 수 있다.

### Callbacks, Reactive, Reactive Core
- 외부 리소스를 기다리는 동안, 요청되는 스레드를 차단하지 않는것
- data가 스트리밍되는 동안 대기하고, data가 도착했다는 알림을 받고싶을때 사용


## 요약
- non-blocking, asynchronous을 사용하면 동일한 양의 작업을 수행하는 데, 적은 스레드를 사용
- 더 많은 안정성과 확장성
- Webflux를 사용하면 구현가능
	- Webflux는 언제 쓰면 좋을까 ?
	- 원격 서버를 호출하는데 응답 시간이 높을때
	- 인터넷이 느릭 클라이언트 수가 많을때
	- Spring MVC를 사용할떄

- [Developers guide to Webflux](https://www.kotlindevelopment.com/kotlin-webflux/?fbclid=IwAR254xE9OpXJ3ytPgm-EoIYEbCDF4tVYcRhpsPdb-xJPMwnMgA_-EZJH2hw)

---

## 답변2
- 상용 서비스 구축시 : 로드밸런싱 및 서버 이중화 + 웹서버 + WAS
- 맨 앞단에 L4나 L7 스위치를 두어 로드밸런싱 및 서버 이중화를 지원
- 뒷단에는 보통 웹서버와 어플리케이션 서버를 분리하는 경우가 일반적

- __Web Server__
  - 보안문제 등으로 웹서버가 앞단에서 static resource(image, java script)를 처리

_ __WAS__
  - 어플리케이션 서버가 aps, jsp등의 api를 처리
  - 플랫폼에 따라 멀티쓰레드를 지원하거나 단일 쓰레드라도 event driven으로 여러 요청을 동시에 처리하도록 지원

## 답변3
- 언어나 프레임워크 따라서 다르긴 한데, __로드밸런서로 여러 서버에 부하를 분산하는 등의 기법을 사용하므로 병렬로__ 돌아간다고 보는게 편합니다.

- node.js는 싱글스레드 이벤트 루프(boss & work) 기반으로 돌아가지만, 여러 프로세스를 띄워 다중코어를 쓰기도 하고
- 자바는 요청마다 쓰레드를 띄우고 풀링하는 경우가 잦고, go는 코루틴 개념으로 경량스레드를 띄웁니다.

## 답변4
- 서버에 대한 정의가 명확하지 않으신 것 같습니다.
  - __서버는__ 어떤 컴퓨터를 지칭하는 것이 아닌 __프로그램입니다.__
  - 정확하게 __서버용으로 사용할 컴퓨터에 서버 프로그램을__ 실행하는 것이죠.
  - “어떤 서비스를 만들고 서버에 띄워놨을때”라는 질문을 하셨는데 어떤 서비스를 만든다는건 서버 프로그램도 만들었다는 것 입니다.
- 웹 : Apache등의 웹 서버를 이용해서 통신
- 게임 : 게임을 위한 서버 프로그램을 만들어야 합니다. 이때 다수의 요청을 동시에 처리해야 하므로 _통신 프로토콜을 설계/구현을 해서 멀티 프로세스 또는 멀티 스레드와 같은 방식을 사용하도록 프로그래밍을 합니다._

## 답변5
- 구현에 따라 다릅니다.
-  각 구현체마다 어떤 방법을 택했고 어떤 특징이 있는지를 알아보는 것도 재미있는 과정이 되실 것 같네요.

## WebServer

**Apache**
- 멀티프로세싱 또는 멀티스레딩

**Nginx**
- 비동기 처리
- 아파치가 멀티프로세싱을 함으로써 생기는 오버헤드를 줄이고자 하는 컨셉으로 나온 녀석이다 보니 정반대의 메커니즘으로 돌아갑니다.

## WAS

**Spring MVC**
  - 요청이 들어올 때마다 스레드를 새로 만들어서 동기적으로 처리합니다.

**Webflux**
 - 비동기 처리를 합니다.

**node.js express**
- 싱글스레드 비동기 처리를 합니다.
