---
title: "WEB, servlet, servlet-form태그"
date: 2019-10-24 14:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, SERVLET]
---
### HTML FORM 태그
- form태그는 서버쪽으로 정보를 전달할 때 사용
1. input
- type : 태그 종류 지정 (ex. text, submit, checkbox...)
- name : input 태그 이름
- value : name에 해당 하는 값 (ex.name=value)
2. input , submit
- form내의 데이터를 전송할 때 사용
- ex. \<input type="submit" value="전송">
3. form태그
- \<form action="요청하는 컴포넌트 이름" method="요청을 처리하는 방식">

---
#### 예제 코드
- form태그의 submit 버튼을 클릭하여 데이터를 서버로 전송하면
- 해당파일(servlet)에는 HttpServletRequest객체를 이용하여 Parameter값을 얻을 수 있다

```html
<form action="FormEx" method="post">
아이디 : <input type="text" name="id" size="10"><br/>
비밀번호 : <input type="password" name="pw" size="10"><br/>
</form>
```
```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  String id = request.getParameter("id");
  String pw = request.getParameter("pw");

  response.setContentType("text/html; charset=utf-8");
  PrintWriter writer = response.getWriter();

  writer.print("<html><head></head><body>");
  writer.print("id : "+id+"<br/>");
  writer.print("pw : "+pw+"<br/>");
  writer.print("</body>");
}
```
---
#### 한글처리
- GET 방식
  - server.xml 수정
  - <Connector URIEncoding="UTF-8" ....>
- POST 방식
  - request.setCharacterEncoding("UTF-8");

---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1166>
