---
title: "WEB, jsp, 쿠키&세션"
date: 2019-10-24 15:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
---
### http프로토콜 특징
- 웹 브라우저에서 서버로 요청 후 서버는 웹 브라우저에 응답한다
- 응답 후에 <b>서버는 클라이언트와 관계를 끊어</b>버린다.
### 쿠키의 필요성
- <b>클라이언트의 정보를 유지</b>하기 위해
- <b>서버에서 생성, 클라이언트 측에 특정 정보 저장</b>한다
- 서버에 요청 할 때 마다 쿠키의 속성값을 참조 또는 변경 가능하다
  - ex. 로그인 페이지에서 로그인을 하고 <u>다른 페이지로 넘어갔을때 로그인 정보를 기억</u>한다
- 용량 제한, 300개 까지 데이터 저장가능

---
|메소드|설명
|:---:|:---:|
|response.setValue()|쿠키 값 설정
|request.getValue()|쿠키 값 얻기

1. 쿠키생성
2. 속성세팅
3. response 객체에 탑재
---
### 세션이란
  - 웹브라우저와 서버의 관계를 유지하기 위한 수단

|설명|쿠키|세션|
|:----|:----|:----|
|이용|생성:서버,저장:클라이언트| 서버상에 객체로 저장
|보안| 보안에취약 | 서버에서만 접근이 가능하여 보안이 좋다
|저장| 한계가 있다| 한계가 없다

---
### 세션문법
- 클라이언트 요청이 발생하면 <b>자동생성</b>된다
- session이라는 내부 객체를 지원하여 세션의 속성을 설정 할 수 있다

![session](https://user-images.githubusercontent.com/55946791/67656037-ff4a1800-f995-11e9-912a-1df5e2cc36e9.JPG)

- setAttribute() : 세션에 데이터 저장
- getAttribute() : 세션에 데이터 얻기
- getId() : 자동 생성된 세션의 유니크한 아이디를 얻는다
- removeAttribute()

---
##### login.html
```html
<form action="loginOk.jsp" method="post">
	아이디 : <input type=text name=id size=10><br>
	비밀번호 : <input type=password name=pw size=10><br>
	<input type=submit value="로그인 하기">
</form>
```
##### loginOk.jsp
```java
<%!
	String id,pw;
%>

<%
id = request.getParameter("id");
pw = request.getParameter("pw");

if (id.equals("hyemi") && pw.equals("hyemi123")){
  // cookie
  Cookie cookie = new Cookie("id", id);
  cookie.setMaxAge(60); // 1분간 기억
  response.addCookie(cookie);
  // session
  session.setAttribute("id", id);
  response.sendRedirect("welcome.jsp");
}else
  response.sendRedirect("login.html");
%>
```
##### welcome.jsp
```java
<h1>쿠키버전입니다</h1>
<%
	Cookie[] cookies = request.getCookies();
	if(cookies != null){
		for (int i=0; i<cookies.length; i++){
			if(cookies[i].getName().equals("id"))
				out.print(cookies[i].getValue()+"님 환영합니다!");
		}
	}
%>
<h1>세션버전입니다</h1>
<%

	Enumeration enumeration = session.getAttributeNames();
	while(enumeration.hasMoreElements()) {
		String sName = enumeration.nextElement().toString();
		String sValue = (String)session.getAttribute(sName);

		if(sValue.equals("hyemi")) out.println(sValue+"님 안녕하세요");
	}
%>
```
##### cookiedel.jsp
```java
<%
	Cookie[] cookies = request.getCookies();
	for(int i=0; i<cookies.length; i++){
		String str = cookies[i].getName();
		if(str.equals("cookieN")){
			out.println("name : "+cookies[i].getName() + "<br>");
			cookies[i].setMaxAge(0);
			response.addCookie(cookies[i]);
		}
	}
%>
```
---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1172>
