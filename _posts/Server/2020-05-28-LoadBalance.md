---
title: "Server, Load Balancer"
date: 2020-05-28 15:40:28 -0400
categories: [Server]
tags : [Load Balancer, Server]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

# 대규모 트래픽을 처리 할수 있는 방법

### Scale-up
- Server가 더 빠르게 동작하기 위해 __H/W성능을 올리는 방법__

### Scale-out
- 하나의 Server 보다는 __여러 대의 Server가 나눠서__ 일을 하는 방법
- h/w 향상 비용 > 서버 한대 추가 비용
- 여러 대의 Server 덕분에 무중단 서비스를 제공할 수 있다.


# 로드 밸런서란?
- 여러 대의 Server에게 균등하게 Traffic을 분산시켜주는 것
- 클라이언트와 서버풀 사이에 위치
- __한대의 서버에 부하가 집중되지 않도록 트래픽을 관리해서__ 각각의 서버가 최적의 퍼포먼스를 보일 수 있도록 한다.

![로드밸런서_아키텍처](https://user-images.githubusercontent.com/55946791/83122435-99ca2f80-a10e-11ea-9aa5-80ed8905cbbb.jpg)


## 로드밸런서 주요 기술
- NAT(Network Address Translation)
	- 사설 ip주소 -> 공인 ip주소로 변경, 주소변경의 역할
- DSR(Dynamic Source Routing protocol)
	- 서버에서 클라이언트로 되돌아가는 경우
	- 목적지 주소를 스위치의 IP주소가 아닌 클라이언트의 IP주소로 전달해서
	- N/W 스위치를 거치지 않고 바로 클라이언트를 찾아가는 개념
- Tunneling
	- 인터넷상에서 눈에 보이지 않는 통로를 만들어서 통신할 수 있게 하는 개념
	- 데이터를 캡슐화해서 연결된 상호 간에만 캡슐화된 패킷을 구별해 캡슐화를 해제



## 네트워크 로드밸런서 종류
- L2(Data Link Layer)
	- Mac Address Load Balancing
	- 브릿지, 허브 등
	- 장점 : 구조가 간단, 신뢰성높다, 가격저렴, 성능좋다
	- 단점 : Broadcast 패킷에 의해 성능저하 발생, 라우팅 등 상위레이어 프로토콜 기반 스위칭 불가
- L3(Network Layer)
	- IP Address Load Balancing
	- L2 + Routing
	- Router, ICMP 프로토콜, IP
	- 장점 : Broadcast 트래픽으로 전체 성능 저하 방지, 트레픽 체크
	- 단점 : 특정 프로토콜을 이용해야 스위칭 가능
- __L4(Transport Layer)__
![L4-로드밸런싱](https://user-images.githubusercontent.com/55946791/83123692-317c4d80-a110-11ea-869c-e62c4cff2fae.jpg)

	- Transport Layer(IP+PORT) Load Balancing
	- TCP, UDP Portocol
	- 장점 : port기반 스위칭 지원, VIP를 이용하여 여러대를 한대로 묶어 부하분산
	- 주로 Round Robin 방식 사용

- __L7(Application Layer)__
![L7-로드밸런싱](https://user-images.githubusercontent.com/55946791/83123689-304b2080-a110-11ea-8089-6674d04d831b.jpg)

	- Application Layer(사용자 Request) Load Balancing
	- HTTP, FTP, SMTP Protocol
	- HTTP헤더, 쿠키 등과 같은 사용자의 요청을 기준으로 특정 서버에 트래픽 분산 가능
	- __패킷 내용 확인 후, 내용에 따라 로드를 특정 서버에 분배하는 것이 가능__
		- ex) url에 따라 부하 분산 or http 헤더의 쿠키값에 따라 부하 분산
	- 특정 패턴을 지닌 바이러스 감지해 N/W보호 가능, DoS/DDoS와 같은 비정상 트래픽 필터링 가능

![웹_1920_–_1](https://user-images.githubusercontent.com/55946791/83124062-a9e30e80-a110-11ea-9075-a91b798bc0e1.png)


## 로드밸런서 알고리즘 종류
- 로드 밸런서는 어떤 기준으로 Server를 선택할까?
- Round Robin(순차방식)
	- 요청을 순서대로 각 서버에 균등하게 분배하는 방식
	- 서버 커넥션 수나 응답시간에 상관없이 모든 서버를 동일하게 처리
	- 다른 알고리즘에 비해서 가장 빠르다
- Least Connetion(최소 연결 방식)
	- 서버에 연결되어 있는 Connection 개수가 가장 적은 서버에 트래픽 분배
	- 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합
- Least Response Time(응답 시간방식)
	- 서버의 현재 연결 상태와 응답시간을 모두 고려하여 트래픽을 배분한다
	- 응답시간 : Response Time, 서버에 요청을 보내고 최초 응답을 받을 때까지 소요되는 시간
	- 가장 적은 연결 상태 + 가장 짧은 응답시간을 보이는 서버에 우선적으로 로드를 배분한다
- IP 해시 방식(IP Hash Method)
	- 클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식
	- 사용자의 IP를 해싱해(Hashing, 임의의 길이를 지닌 데이터를 고정된 길이의 데이터로 매핑하는 것, 또는 그러한 함수) 로드를 분배하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장합니다.


## 로드 밸런서 장애 대비는 어떻게 할까?
	- 로드 밸런서를 이중화해서 장애를 대비할 수 있다.
![로드밸런서 장애 대비](https://user-images.githubusercontent.com/55946791/83124800-a734e900-a111-11ea-987e-54490e6bd655.gif)
	1. 이중화 된 로드 밸런서들은 서로 Health Check를 한다
	2. Main Load Balancer가 동작하지 않으면 가상 ip(VIP, Virtual IP)는 여분의 로드 밸런서로 변경된다
	3. 여분의 로드 밸런서로 운영하게 된다

## Health Check
- Active 장비의 장애 탐지시 사용
- Server에 일정한 간격으로 신호를 보내고 응답이 오는지 체크해서 정상 가동 중인지 판단
- 레이어가 높을 수록, 정확도 高, 서버 부하 多
- 종류
	- ICMP 체크 (L3) : Ping등으로 응답 확인
	- Port 체크 (L4) : 웹일경우, 80번 포트로 응답 확인
	- Service 체크 (L7) : HTTP통신을 확인하는 경우, 특정 페이지가 제대로 표시되는지 확인

### 보통 로드밸런서의 설정 시 서버들에 대한 주기적인 health Check를 통해 장애 여부를 판단할 수 있다.



---
## 참고

- <https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903>
- <https://medium.com/@pakss328/%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%84%9C%EB%9E%80-l4-l7-501fd904cf05>
- <https://nesoy.github.io/articles/2018-06/Load-Balancer>
- <https://jins-dev.tistory.com/entry/L4-L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1Load-Balancing-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC>
