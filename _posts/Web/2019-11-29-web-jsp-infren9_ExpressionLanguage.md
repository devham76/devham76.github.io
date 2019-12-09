---
title: "WEB, 실전jsp강좌, ExpressionLanguage"
date: 2019-11-29 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Experssion Language
- EL이란, 표현식 또는 액션 태그를 대신해서 값을 표현하는 언어이다
- ex) 액션태그 : <jsp:forward page="action_forward.jsp" />
- ex) (표현식) : <%= value %>, (EL) : ${value}


#### 1. EL연산자
- 산술 : +, -, *, /, %
- 관계형 : ==, !=, >, <
- 조건 : a ? b: c
- 논리 : &&, ||
- ex.
```java
<%= 1>3 ? true:false %> <br>
${ 1 > 3 ? true : false}
```
### 2. 액션태그 EL

```java
<jsp:useBean id="student" class="com.javalac.ex.Student" scope="page"></jsp:useBean>
<jsp:setProperty name="student" property="name" value="로꼬" />
<jsp:setProperty name="student" property="age" value="26" />
<jsp:setProperty name="student" property="grade" value="4" />
<jsp:setProperty name="student" property="studentNum" value="10" />

이름 : <jsp:getProperty name="student" property="name" /><br>
나이 : <jsp:getProperty name="student" property="age" /><br>
학년 : <jsp:getProperty name="student" property="grade" /><br>
번호 : <jsp:getProperty name="student" property="studentNum" /><br>
-----<br>
이름 : ${student.name}<br>
나이 : ${student.age}<br>
학년 : ${student.grade}<br>
번호 : ${student.studentNum}<br>
```

---
### 3. 내장객체

|내장객체|설명|
|----|----|
|pageScope| page객체를 참조하는 객체
|requestScope | reqeust객체를 참조하는 객체
|sessionScope| session객체를 참조하는 객체
|applicationScope | application객체를 참조하는 객체
|---|---
|param| 요청 파라미터를 참조하는 객체
|paramValues| 요청 파라미터(배열)를 참조하는 객체
|initParam| 초기화 파라미터를 참조하는 객체
|cookie| cookie객체를 참조하는 객체


#### objectEl.jsp
```java
<form action="ObjectElOk.jsp" method="get">
아이디 : <input type="text" name="id">
비밀번호 : <input type="password" name="pw">
<input type="submit" value="로그인">
</form>

<%
application.setAttribute("application_name", "application_value");
session.setAttribute("session_name", "session_value");
pageContext.setAttribute("page_name", "page_value");
request.setAttribute("request_name", "request_value");
%>
```

#### ObjectElOk.jsp
```java
<%
	String id = request.getParameter("id");
	String pw = request.getParameter("pw");
%>

	아이디 : ${param.id}<br>
	비밀번호: ${param.pw}<br>
	아이디 : ${ param["id"] }<br>
	비밀번호 : ${ param["pw"] }<br>
<hr>

	applicationScope : ${applicationScope.application_name}<br>
	sessionScope : ${sessionScope.session_name}<br>
	pageScope : ${pageScope.page_name}<br>
	requestScope : ${requestScope.request_name}<br>

```


---
## Reference
- <https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1183>
