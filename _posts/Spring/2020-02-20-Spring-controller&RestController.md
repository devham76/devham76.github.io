---
title: "Spring, @Contorller & @RestController 차이"
date: 2020-02-03 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 기존의 MVC 컨트롤러   (@Controller)
- 주용도 : view(화면)를 리턴
- @ResponseBody를 사용하여 객체 리턴 가능
### Restful 웹서비스 컨트롤러 (@RestController)
- 주용도 : 데이터 리턴
- view필요 없이 객체를 반환하기만 하면 객체 데이터는 json/xml 형식의 http 응답을 직접 작성하게 된다

### @ResponseBody
- @ResponseBody를 사용하면, Spring은 HTTP응답에 리턴값을 자동으로 반환해준다

### @RestController
- @ResponseBody를 추가하지 않아도 기본으로 적용된다
- 별도의 view를 제공하지 않으므로 문제 발생시 개발자가 직접 제어해야한다



---
## Reference
- <https://doublesprogramming.tistory.com/105>
