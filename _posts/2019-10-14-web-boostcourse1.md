---
title: "WEB, boostcourse, Servlet&Lifecycle"
date: 2019-10-14 17:30:28 -0400
categories: WEB
tags : [WEB, boostcourse]
---
### Servlet
- URL 요청을 처리하는 프로그램
- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- 서블릿을 정의 해보면
  1. 서블릿은 WAS에서 동작하는 JAVA 클래스이다
  2. 서블릿은 HttpServlet 클래스를 상속받아야 한다
  3. 서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두가지(JSP, 서블릿)를 조화롭게 사용해야 한다.
--> ex: 웹 페이지를 <u>구성하는 하면(HTML)은 <b>JSP</b></u>로 표현하고, <u>복잡한 프로그래밍은 <b>서블릿</b></u>으로 구현
- jsp vs servlet
  - jsp : javs server page, html 파일 내에 java언어를 삽입한 문서
  - servlet : server applet, java언어로 이루어진 웹 프로그래밍 문서
---
### Servlet 라이프 사이클
![servlet_lifecycle](https://user-images.githubusercontent.com/55946791/66801806-5d6a0a80-ef55-11e9-9cef-c5db37578d64.png)

- WAS는 서블릿 요청을 받으면 해당 서블릿이 메모리에 있는지 확인합니다.
- if (메모리에 없음) {
  + 해당 서블릿 클래스를 메모리에 올림
  + init() 메소드를 실행
}
  + service()메소드를 실행
- was가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 메소드가 실행됩니다.

## service(request, response) 메소드는
- WAS는 매번 service()만 호출한다.
- 즉, service()를 오버라이드 하지 않았다면, 해당 서블릿의 부모인 HttpServlet의 service() 메서드가 실행된다.

## HttpServlet의 service()는 템플릿 메소드 패턴으로 구현
- 클라이언트의 요청이 GET일 경우, 자신이 가지고 있는 doGet(response, request)을 호출
- 클라이언트의 요청이 POST일 경우, 자신이 가지고 있는 doPost(response, request)를 호출

```java
package examples;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class LifeCycleServlet
 */
@WebServlet("/LifeCycleServlet")
public class LifeCycleServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

    public LifeCycleServlet() {
        System.out.println("LifeCycleServlet 생성");
        // TODO Auto-generated constructor stub
    }

	public void init(ServletConfig config) throws ServletException {
		System.out.println("init test 호출");
	}

	public void destroy() {
		System.out.println("destroy 호출");
		// 서블릿을 수정하면 현재 메모리에 올라가있는 서블릿 객체는 더이상 사용 될수없다
		// 이때 destory()가 호출
	}
	/*
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("service 호출");
		// 서블릿은 서버에 서블릿 객체를 여러개 만들지 않는다
		// 요청이 여러번 들어오면 요청된 객체가 메모리에 있는지 체크하고
		// 있다면 service()만 호출한다
	}
	*/

	@Override
	// 정적인 페이지
	protected void doGet(HttpServletRequest req, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		out.println("<html>");
		out.println("<head><title>form</title></head>");
		out.println("<body>");
		out.println("<form method='post' action='/firstweb/LifeCycleServlet'>");
		out.println("name : <input type='text' name='name'><br>");
		out.println("<input type='submit' value='ok'><br>");                                                 
		out.println("</form>");
		out.println("</body>");
		out.println("</html>");
		out.close();
	}

	@Override
	// 동적인 페이지
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		String name = request.getParameter("name");
		out.println("<h1> hello " + name + "</h1>");
		out.close();
	}
}
```
---
## Reference

- [1) Servlet 이란?]<https://www.edwith.org/boostcourse-web/lecture/16686/>
- [3) Servlet 라이프 싸이클]<https://www.edwith.org/boostcourse-web/lecture/16688/>
