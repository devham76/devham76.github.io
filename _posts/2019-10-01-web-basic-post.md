---
title: "WEB, 기본적인 인터넷, 네트워크 그리고 서버"
date: 2019-10-01 15:30:28 -0400
categories: WEB
tags : [WEB, webproject]
---
---
## 인터넷 접속 과정
1. 내 노트북 웹 브라우저( client )에서 google.com( domain )을 입력하고 엔터를 친다.
2 .DNS server가 도메인을 ip address로 변환하여 내 노트북으로 전달해준다.
3. 그 ip 주소로  구글에 접속(request)하게된다.
4. google.com( server )에서 답장을 내 컴퓨터로 보낸다(response)
5. 내 노트북에 구글 페이지가 보인다.

---
## 공인ip & 사설ip

친구를 초대하려면 내 집주소를 알아야 하고
누군가가 나에게 전화하려면 내 전화번호를 알아야 한다.
누군가가 내 서버에 접속 하려면 나의 ip주소를 알아야 한다.

curl https://ipinfo.io/ip 로 검색 => ipinfo.io온라인 서비스 입장에서 본 내 컴퓨터 주소
ip addr : 명령어를 통해 => 이 컴퓨터의 실제 ip주소

실제ip 와 이 컴퓨터가 외부에 접속할 때 사용하는 ip는 다르다

통신사 - 공유기 - 여러대의 컴퓨터
- public address / 공인 ip : 
  통신사가 제공하는 ip는 공유기(router)가 갖게된다 / 컴퓨터가 외부에 접속할 때 사용하는 ip
- private address / 사설 ip :
  여러대의 컴퓨터도 ip를 반드시 가져야 하므로 사설 ip를 갖게된다 / 실제 ip

예 ) 
회사 마케팅부서에 연락을 하고싶을때, 
회사 대표 번호(공유기, 공인 ip)에 전화를 하면
내선 번호(사설 ip)를 이용하여 마케팅부서에 연결이 된다.

공인ip와 사설ip가 다르다면 내 컴퓨터를 client로 사용할 수는 있어도 server로 사용할 수 없다.
단, 같은 공유기를 사용하고 있는 컴퓨터들끼리는 사설ip가 달라도 서로 통신가능하다

---
## Reference 
[생활코딩](https://opentutorials.org/course/2598/14427)


---
