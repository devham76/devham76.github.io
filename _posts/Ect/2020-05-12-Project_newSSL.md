---
title: "프로젝트 관리2 - AWS에서 SSL인증 발급하고 등록하기"
date: 2020-05-12 20:00:28 -0400
categories: etc
tags : [project]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

> [완성된 사이트 보러가기](https://www.devham76.com)

## HTTP와 HTTPS차이
평문의 HTTP 문서는 SSL 레이어를 통과하면서 암호화 돼서 목적지에 도착하고, 목적지에서는 SSL 레이어를 통과하면서 복호화 돼서 웹 브라우저에 전달된다.

![https3](https://user-images.githubusercontent.com/55946791/81721497-e8df5600-94ba-11ea-919f-52f3814b60ab.png)
- HTTPS URL은 "https://"로 시작한다. 기본 포트번호는 __443__ 이다. HTTP URL은 "http://"로 시작한다. 기본 포트번호는 __80__ 이다.
- HTTP는 평문 데이터를 기반으로 하기 때문에, 유저정보와 같은 민감한 정보가 인터넷 상에 그대로 노출된다. 이 정보는 수집되거나 변조될 수 있다. HTTPS는 이러한 공격을 견딜 수 있도록 설계돼 있다.
- __HTTPS는 인증서를__ 이용해서, 접속 사이트를 신뢰할 수 있는지 평가할 수 있다.
- 일반적으로 __HTTPS는 HTTP에 비해서 (매우 많이)느리다.__ 많은 양의 데이터를 처리할 경우 성능의 차이를 체감할 수 있다. 많은 웹 사이트들이 __민감한 정보를 다루는 페이지(로그인 혹은 유저정보) 페이지를 HTTPS로__ 전송하고, 기타 페이지는 HTTP로 전송하는 방법을 사용한다. 하드웨어 SSL 가속기를 이용해서 암/복호화 성능을 높이는 방법을 사용하기도 한다.

> [참고](https://www.joinc.co.kr/w/Site/Network_Programing/AdvancedComm/HTTP#s-5.)


## SSL등록 방법
1. Let's Encrypt 설치 후 SSL 등록
	- EC2 내부에 SSL인증서를 설치하고 서비스하는 방법 (일반적인 기존 방식)
	- 보통 서비스가 소규모라면 1대의 서버에 Nginx설치후 Let's Encrypt를 설치해서 SSL등록한다
	- 다만, 이럴 경우 트랙픽이 늘어 로드밸런서 + 여러 서버 구성으로 확장하기 쉽지 않다.


2. AWS에서 제공하는 인증서 관리 서비스인 ACM(AWS Certificate Manager)을 ACM 통합서비스와 연동하여 적용하는 방법
(참고 : ACM이란? https://docs.aws.amazon.com/ko_kr/acm/latest/userguide/acm-overview.html)
- 이 방법은 AWS에서 제공하는 인증서 관리 서비스로 갱신에 대한 신경을 개발자가 쓸 필요가 없다. 유효기간은 13개월이며, ACM 통합서비스와 연동해서 쓰면 무료이다.
- ACM 통합서비스라 함은 AWS의 ELB, CloudFront, API Gateway 등의 서비스이다.

## 1. ACM(AWS Certificate Manager) 이용 하여 SSL발급
- ACM으로 접속해서 인증서 요청, 도메인 등록 후 완성된 인증서에 "Route 53에서 레코드 생성" 클릭

![ssl인증서 발급중](https://user-images.githubusercontent.com/55946791/81703227-410c5d00-94a7-11ea-98fa-c141fd4e3018.JPG)

## 2. Elastic Load Balancer 사용

- 현재 사용중인 EC2인스턴스를 ELB에 넣는다.
- Certificate manager로 발급한 인증서는 ELB 또는 cloudfront로 배포되는 사이트에만 적용 가능하기 때문이다.

1. ec2 설정 화면의 왼쪽 탭에 로드밸러스 추가하는 부분으로 접속

2. 로드 밸러서 구성에 https를 반드시 추가한다
![로드밸러스 추가](https://user-images.githubusercontent.com/55946791/81705720-4f0fad00-94aa-11ea-8fe4-5ef800f368d4.JPG)

3. 보안그룹 설정시 ec2에 있는 내 프로젝트를 반드시 선택한다
![로드밸러스 - 보안그룹](https://user-images.githubusercontent.com/55946791/81705727-5040da00-94aa-11ea-91dd-4eef41b93a62.JPG)

4. 완성화면
![로드밸러스 위치](https://user-images.githubusercontent.com/55946791/81705723-4fa84380-94aa-11ea-9d67-1866ebaffd80.JPG)


5. Route 53 유형A 설정 변경
![Rout 53 a](https://user-images.githubusercontent.com/55946791/81719774-72d9ef80-94b8-11ea-86d1-3004c4db4569.JPG)

6. 그리고 503에러...

- ELB에 SSL 인증서를 등록할 때 502에러나 503에러 때문에 고생하는 경우에는 인스턴스의 Security Groups과 ELB의 Listenr가 제대로 등록되었는지 확인해보셔야 합니다.

- 라는 글을 발견해서 이 두가지를 한참을 보다가 ELB를 지우고 새로 생성을 여러번 반복했다


- Target is in an Availability Zone that is not enabled for the load balancer 을 발견했다.

![ELB 오류원인](https://user-images.githubusercontent.com/55946791/81720310-2fcc4c00-94b9-11ea-8cd4-559f953e194d.JPG)

- 이 화면을 유심히 보다가 가용영역에 __ap-northeast-2c__ 라고 쓰여있는게 거슬렸다.

- 처음 ELB를 생성할때 가용영역을 설정하는것이 있었고, 이것이 의미하는 바를 몰라서 ap-northeast-2a, ap-northeast-2b에만 지정했던것이 생각났다.

![elb오류해결](https://user-images.githubusercontent.com/55946791/81720728-c1d45480-94b9-11ea-9bfc-baaf4fb3de57.JPG)

- 서브넷을 편집해주었더니 오류해결 !!

## 완성화면
![https 완성](https://user-images.githubusercontent.com/55946791/81720899-fba55b00-94b9-11ea-889d-06bfe51275e7.JPG)


## SSL보안 취약점
- SSL/TLS는 인터넷 상에서 주고받는 민감정보를 보호하는 역할을 하고 있으나 관련 보안 이슈로 위협 지속 발생
- 보안에 취약한 __SSL 2.0과 SSL 3.0의 사용을 자제하고 TLS 1.0 이상 사용 권장__
- SSL/TLS와 관련된 소프트웨어 문제로 인해 민감정보 유출 가능성을 염두에 두고 최신 보안 패치 적용 필요
- 보안 점검 툴로 __SSL/TLS 보안 취약점 여부를 정기적으로 모니터링해야 함__

> [참고](https://spri.kr/posts/view/19827?code=industry_trend)

- SSL은 보안에 취약할수 있다고해서 인증서를 선택할때 TLS가 적혀있는것을 선택해서 ELB를 다시 만들어주었다.
![tls 선택](https://user-images.githubusercontent.com/55946791/81723019-2fce4b00-94bd-11ea-866a-82d643099b2a.JPG)

- 인터넷 검색결과 TLS도 취약점이 있다고 나와있다...TLS 1.3을 사용하라고 하는데 지원하지 않으므로 여기까지 하겠다.

---
## 참고
- <https://yunzema.tistory.com/264>
- <>https://jojoldu.tistory.com/434
- <https://velog.io/@minholee_93/AWS-ELB-SSL-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-mfk4dpjrd6>
- <https://brunch.co.kr/@poin2lab/5>
