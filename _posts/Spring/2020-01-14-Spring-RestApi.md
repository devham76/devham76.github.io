---
title: "Spring, RestAPI"
date: 2020-01-14 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- 다양한 환경들을 지원한다 (모바일, 웹..)
- 서로 다른 front-end를 이용하여 다양한 환경들을 지원한다, 하나의 back-end

- 이때 백엔드를 만드는 방법이 rest api이다
- resource를 처리하는 방법을 의미한다
crud

- post, get, put/patch, delete
- uri or url을 사용한다
- collection(read,create)
  읽기와 생성가능
 member는 read, update, delete할수있다

 - restaurant
collection : http://host/restaurants
개별적인 리소스는 : http://host/restaurants/{id}로 접근가능하다

- json포맷을 사용한다

- 가게목록 ; GET/restaurants
- 가게 상세; GET/restaurants/{id}
- 가게 추가; POST/restaurants
- 가게 수정; PATCH/restaurants/{id}
- 가게 삭제; DELETE/restaurants/{id}



---
## Reference
- [fastcampus] 스프링 부트 프로젝트
