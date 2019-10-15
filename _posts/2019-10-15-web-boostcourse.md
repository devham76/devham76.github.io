---
title: "WEB, boostcourse, Servlet(Request, Response 객체)"
date: 2019-10-15 17:30:28 -0400
categories: WEB
tags : [WEB, boostcourse]
---

### 들어가기전에
1. HttpServletRequest : 클라이언트가 서버에게 보낸 요청을 추상화한 객체
2. HttpServletResponse : 서버가 클라이언트에게 응답하기 위한 정보를 추상화한 객체

---

![1_5_4_request_response](https://user-images.githubusercontent.com/55946791/66802408-475d4980-ef57-11e9-884f-926ad61ce9df.png)

### 요청과 응답
WAS는 웹 브라우저로부터 Servlet요청을 받으면,
- 요청할 때 가지고 있는 정보를 HttpServletRequest객체를 생성하여 저장한다
- 웹 브라우저에게 응답을 보낼 때 사용하기 위해 HttpServletResponse객체를 생성한다
- 생성된 HttpSerㄴvletRequest, HttpServletResponse 객체를 서블릿에게 전달한다

### HttpServletRequest
- http프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용
- 요청정보 (ex:헤더정보, 파라미터, 쿠키, URL, URI 등)의 정보를 읽어 들이는 메소드를 가지고 있다
- Body의 Stream을 읽어 들이는 메소드를 가지고 있다

### HttpServletResponse
- WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServletResponse객체를 생성하여 서블릿에게 전달한다
- 서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메시지등을 전송한다

### 헤더 정보 가졍오기
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  response.setContentType("text/html");
  PrintWriter out = response.getWriter();	// 요청 객체로 부터 응답을 보낼 통로를 알아온다
  out.println("<html>");
  out.println("<head><title>form</title></head>");
  out.println("<body>");

  Enumeration<String> headerNames = request.getHeaderNames();	// 모든 헤더의 이름을 문자열로 반환
  while(headerNames.hasMoreElements()) {
    String headerName = headerNames.nextElement();
    String headerValue = request.getHeader(headerName);
    out.println(headerName + " : " + headerValue + " <br> ");
  }		

  out.println("</body>");
  out.println("</html>");
}
```



### get
요청할때 가지고 온 파라메터값 가져오기
http://localhost:8080/firstweb/ParameterServlet?name=hyemi&age=20
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  response.setContentType("text/html");
  PrintWriter out = response.getWriter();	// 요청을 한 객체에게 응답할 연결통로
  out.println("<html>");
  out.println("<head><title>form</title></head>");
  out.println("<body>");

  String name = request.getParameter("name");
  String age = request.getParameter("age");

  out.println("name : " + name + "<br>");
  out.println("age : " +age + "<br>");

  out.println("</body>");
  out.println("</html>");
  }
```
---
## Reference

- [1) Servlet 이란?]<https://www.edwith.org/boostcourse-web/lecture/16686/>
