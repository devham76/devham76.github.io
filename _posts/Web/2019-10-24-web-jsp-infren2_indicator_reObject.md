---
title: "WEB, jsp, 지시자/request,response객체"
date: 2019-10-24 14:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
---
#### 지시자
- jsp 페이지의 전체적인 속성을 지정할 때 사용한다
- ex)page : 해당 페이지 전체적인 속성 지정
    - 사용되는 언어, import문 등을 많이 사용

```java
<%@page import = "java.util.*" %>
<%@ page language="java" contentType="text/html; charset="EUC-KR"
    pageEncoding="EUC-KR"%>
```


2. include : 별도의 페이지를 현재 페이지에 삽입
```java
<%@ include file="include.jsp"%>
```

3. taglib : 태그라이브러리의 태그 사용

---

#### requset 객체
| 메소드 | 설명|
|---|:---:|
|getMethod() | get,post방식 구분
|getSession() | 세션 객체 얻기
|getRequestURL() | 요청 url얻기

#### parameter 메소드 (request 객체)
| 메소드| 설명|
|---|:---:|
| getParameter(String name) | name에 해당하는 파라메터값 구함
| getParameterNames() | 모든 파라메터값 구함
| <b>getParameterValues(String name)</b>| name에 해당하는 파라메터 값 구함

#### reponse 객체
| 메소드| 설명
|:---:|:---:|
|getCharacterEncoding()| 응답할때 문자 인코딩 지정
|addCookie(Cookie)| 쿠키지정
|<b>sendRedirect(URL)</b> | 지정한 URL로 이동

- sendRedirect() 이용 : 로그인할때 로그인 성공하면 성공 페이지로, 실패하면 실패페이지로 이동한다.


---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1169>
<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1170>
