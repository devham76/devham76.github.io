---
title: "WEB, jsp, 태그/동작원리/내부객체"
date: 2019-10-24 14:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, SERVLET]
---
- Servlet : <b>JAVA언어</b>로 문서를 작성, 출력객체를 이용해여 HTML코드 삽입 (<b>CONTROLLER</b>)
- JSP : <b>HTML코드</b>에 JAVA언어를 삽입해서 동적 문서를 만들수 있다 (<b>VIEW</b>)
### JSP태그 종류
||표현|설명|
|---|:----:|:---:|
|지시자| <%@ %> | 페이지 속성
|주석| <%-- --%>|
|선언|  <%! %> | (전역)변수, 메소드 선언
|표현식| <%= %> | 결과값 출력
|스크립트릿|  <% %> | java코드
|액션태그| <jsp:action></jsp:action> | 자바빈 연결

---
### JSP 동작 원리
1. 웹브라우저로 jsp파일 요청
2. jsp 컨테이너가 jsp파일->servlet파일(.java)로 변환
3. servlet파일(.java)은 컴파일 되어 클래스 파일로 변환
4. 요청한 클라이언트에게 html파일 형태로 응답

---
### JSP 내부 객체
- 개발자가 객체를 생성하지 않고 바로 사용 가능한 객체
- JSP에서 제공되는 내부객체는 JSP컨테이너에 의해 servlet으로 변환될 때 자동으로 객체가 생성된다

#### 내부 객체 종류
1. 입출력 객체
  - request, response, output
2. 서블릿 객체
  - page, config
3. 세션 객체
  - session
4. 예외 객체
  - exception
---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1168>
