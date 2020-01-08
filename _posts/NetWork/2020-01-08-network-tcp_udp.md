---
title: "NetWork, TCP & UDP"
date: 2020-01-08 15:05:28 -0400
categories: [network]
tags : [network, tcp, udp]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

![osi7layer](https://user-images.githubusercontent.com/55946791/71970381-f4401d80-324b-11ea-88ae-b25b0bdfc895.jpg)


## Transport Layer, TCP vs UDP
- 인터넷은 전송계층에 연결형/비연결형 프로토콜 두개의 주된 프로토콜을 갖는다.
- 데이터의 전달을 담당한다.

## 비교
|프로토콜 종류| TCP | UDP|
|--|--|--|
|연결 방식 | 연결형 서비스 | 비연결형 서비스|
|패킷 교환 방식| 가상 회선 방식 | 데이터그램 방식|
|전송순서| 전송 순서 보장| 전송 순서가 바뀔 수 있음|
|수신 여부 확인 | 수신여부확인 | 확인하지않음|
|통신 방식 | 1:1통신 | 1:1 or 1:N or N:N|
|신뢰성 | 높다 | 낮다|
|속도 | 느리다 | 빠르다|
|사용 | 대부분| DNS, streaming서비스


---
## TCP
:<b>Transmission Control Protocol, 전송제어 프로토콜, 연결형 프로토콜</b>
- TCP서비스를 하기 위해서는 송/수신자측에 소켓이라고 부르는 종단점을 생성,연결되어있어야 한다.

<img width="326" alt="tcp" src="https://user-images.githubusercontent.com/55946791/71972262-a9280980-324f-11ea-9c6f-e1be67a44063.png">

### [TCP 특징]
- <b>연결형</b> 서비스 , 가상 회선 방식 제공
  - 송/수진지를 연결하여 패킷을 전송하기 위한 논리적 경로를 배정한다.
- TCP는 일반적으로 IP와 함께 사용된다.
  - TCP : 패킷 추적 및 관리
  - IP : 데이터의 배달
- 3-way handshaking으로 연결을 설정, 4-way handshaking으로 연결 해제
  - 송/수진지를 확실히 하여 정확한 전송을 보장하기 위해 세션을 수립한다.
- 패킷에 순서를 부여하여 재조립하고, 흐름/혼잡 제어 기능이 있다
- <b>높은 신뢰성</b>을 보장
  - <b>TCP는 연속성보다 신뢰성있는 전송이 중요할때 사용하는 프로토콜</b>
- UDP보다 속도가 느리다
- 전이중(Full-Duplex), 점대점(Point to Point)방식


---

## UDP
:<b>User Datagram Protocol, 비연결형 프로토콜</b>
- 데이터를 데이터그램(독립적인 관계를 지니는 패킷) 단위로 처리하는 프로토콜

<img width="326" alt="udp" src="https://user-images.githubusercontent.com/55946791/71972269-a9c0a000-324f-11ea-9280-4666aa3b2ec9.png">


### [UDP 특징]
- 비연결형, 데이터그램 방식 제공
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다
- 신뢰성이 낮다
- TCP보다 속도가 빠르다
- <b>신뢰성보다는 연속성이 중요한 서비스에 사용된다</b>

- [ 유용한 분야 ]
  - 클라이언트-서버 상황에 유용하다
  - 종종 클라이언트는 서버로 짧은 요청을 보내고 짧은 응답을 기대한다
- [ 요청/응답이 손실된다면 ]
  - 클라이언트는 time out되고 다시 시도한다
  - 코드가 간단하고 TCP처럼 초기 설정에서 요구되는 프로토콜보다 적은 메세지가 요구된다.
- [ 사용되는 곳 ]
  - <b>DNS</b> : 도메인의 ip주소를 찾아주는 서버이며 DNS서버로 도메인을 포함한 UDP패킷을보낸다. 이 서버는 도메인의 IP주소를 포함한 UDP패킷으로 응답한다. 사전에 설정 필요X, 해제 필요X
  - <b>실시간 멀티미디어 / 실시간 트랜스포트 프로토콜(RTP : Real-time Transport Protocol)</b>: 오디오와 비디오 데이터 패킷 형식으로 전송한다.UDP패킷을 사용하기 때문에 전달,지연,손실 등에 대한 특별한 보장이없다 / 실시간 서비스 (streaming)

---



---
## Reference
- <https://mangkyu.tistory.com/15>
- <https://asfirstalways.tistory.com/327?category=685177>
