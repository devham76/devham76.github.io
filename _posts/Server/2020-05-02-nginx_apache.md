---
title: "Nginx와 Apache"
date: 2020-05-02 20:00:28 -0400
categories: etc
tags : [Apache, Nginx]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 웹 서버
- 웹 서버는 HTTP 프로토콜을 통해 읽힐수 있는 문서를 처리하며 일반적으로 웹 애플리케이션의 앞단에 배치되곤 한다.
- 동적인 리소스는 WAS에게 처리하도록 하고 정적인 리소스를 보다 효율적으로 처리하기 위한 방법일 수 있다.


## 1. Apahce
![apache 클라이언트 처리 동작](https://user-images.githubusercontent.com/55946791/80852123-ff86e100-8c60-11ea-9f70-f18240ba42c2.png)

### 1-1.스레드/프로세스 기반 구조
- 클라이언트 요청 하나당 스레드 하나가 처리하는 구조. 사용자가 많으면 스레드 생성, 메모리 및 CPU 낭비가 심하다.
- 요청을 받으면 MPM(Multi Processing Module :다중처리 모듈) 방식으로 처리한다.
### Apahce문제점
- __1개의 클라이언트당 1개의 스레드(or 프로세스)구조__ 였기 때문에 클라이언트가 맺은 __접속이 완전히 끝나지 않으면 한 스레드/프로세스가 죽지 않는 방법을 사용했다. (keep alive)__
- 서버의 프로세스가 blocking되면 요청 처리 못하고, 완료 될때까지 대기
- 그러므로 __대량 접속에서 효율이 떨어지는__ 문제점이 있다.
- Apahce 2.4부터는 Event MPM을 사용해서 해결하고있다.


### 1-2-1. Prefork MPM
![prefork mpm](https://user-images.githubusercontent.com/55946791/80852141-35c46080-8c61-11ea-9e1a-fd125a5ba64a.png)
- __1개의 자식 프로세스가 1개의 스레드를__ 갖는 구조로, 자식 프로세스는 최대 1024개 까지 가능
- 실행 중인 프로세스를 복제해서 실행한다.(메모리까지 같이 복제)
- 응답프로세스를 미리 띄워놓고 클라이언트 요청 시 자식 프로세스가 반응하게 되는 방식.
- 스레드 간 __메모리 공유X__ (독립적이기 때문에 안정적이나, 메모리를 많이 사용한다. 왜냐, 프로세스1:스레드1 이니까, 각기다른 프로세스의 스레드)
- 디버깅이 빈약한 플랫폼에서 쉬운 디버깅 가능
- 일반적으로 single CPU또는 Dual CPU에서 성능이 좋다

### 1-2-2. Worker MPM
![worker](https://user-images.githubusercontent.com/55946791/80852222-c9962c80-8c61-11ea-8b70-0d32b594bd31.gif)
- __1개의 프로세스가 각각 여러 쓰레드를__ 사용하게 된다.
- 쓰레드간의 __메모리를 공유한다.__
- prefork보다 메모리 사용량 적고, 통신량이 많은 서버에 적절하다.

### prefork vs worker
- 둘의 속도는 비슷하다.

|prefork | worker|
|--|--|
|안전하지 않은 제 3자가 만든 모듈 사용가능 | 통신량이 많은 서버에 적합|
|디버깅이 빈약한 플랫폼에서 쉽게 디버깅| prefork에 비해 적은 메모리 사용|

### event MPM
- 아파치 2.4.x 버전부터 생성된 방식
– worker 방식을 기반으로 함

## 2.Nginx (엔진엑스)
- 웹 서버 s/w로 __가벼움과 높은 성능을__ 목표로 한다.
- 웹서버, 리버스 프록시, 캐싱, 로드 밸런싱, 미디어 스트리밍 등을 위한 오픈소스 s/w
- Nginx는 요청에 응답하기 위해 __비동기 Event-driven 기반 구조를__ 가진다.

### 특징
![Nginx 클라이언트 처리 동작](https://user-images.githubusercontent.com/55946791/80852441-90f75280-8c63-11ea-9573-c8ba1d433f9e.png)
- 스레드를 많이 사용하지 않기 때문에 문맥교환 비용이 적고 cpu소모도 적다.
- Event-driven 처리 방식으로 모든 IO를 전부 Event-Listener로 미루기 대문에 흐름이 끊기 지 않고 __빠르게 응답이 가능하다.__


### 프록시+로드밸런싱

```
# Load Balancing
upstream target-server {
  least_conn;
  server [서버주소1] weight=5 max_fails=3 fail_timeout=10s;
  server [서버주소2] weight=10 max_fails=3 fail_timeout=10s;
}

server {
  listen 80;
  listen [::]:80;

  server_name front.local;

  access_log /var/log/nginx/access.log;
  error_log /var/log/nginx/error.log;

  location / {
    proxy_next_upstream error http_503;
    proxy_pass http://target-server;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-NginX-Proxy true;
    proxy_set_header Host $host;
    proxy_redirect off;
  }
}
```

- 로드 밸런싱
  - upstream이라는 옵션으로 설정가능
  - least_conn은 연결이 가장 적은 서버로 트래픽 전달
  - (유료)Nginx Plus만 Health check지원
  - ※HAProxy
    - L4,L7 H/W 로드밸런서 대체하기 위한 오픈소스 S/W
    - (High Availabilty 고가용성). Nginx와 달리 health check, 특정 api에서 서버상태 점검 가능
    - [참고 글](https://seokjun.kim/haproxy-and-nginx-load-balancing/)

---
## 참고
- <https://taetaetae.github.io/2018/06/27/apache-vs-nginx/>
- <https://bkjeon1614.tistory.com/23>
- <https://cntechsystems.tistory.com/24>
