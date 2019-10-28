---
title: "WEB, jsp, 예외처리"
date: 2019-10-28 15:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
---
- 예외가 발생했을때 프로그램이 멈추면 안되기 때문에 예외 처리해준다
##### [방법1]
- 예외 발생
```jsp
<%@ page errorPage="errorPage.jsp" %>
```
- 예외 페이지
```jsp
// 예외 페이지임을 명시해준다
<%@ page isErrorPage="true" %>
// 해당페이지는 정상페이지임을 명시해줌
<% response.setStatus(200);%>
// exctption 객체 사용
<%= excetpion.getMessage()%>
```

##### [방법2]
```xml
<error-page>
  <error-code>404<error-code>
  <location>/error404.jsp<location>
<error-page>
  <error-page>
    <error-code>500<error-code>
    <location>/error500.jsp<location>
  <error-page>

```
---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1174>
