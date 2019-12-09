---
title: "WEB, 실전jsp강좌 & DAO/DTO"
date: 2019-11-02 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### DAO (Data Access Object)
- <u>DB에 접속해서 데이터를 추가/삭제/수정 등의 작업을 하는 클래스</u>
- 일반적인 JSP, Servlet 페이지내에서 DB작업을 함께 기술할 수 있지만, 유지보수 및 코드의 모듈화를 위해 별도의 DAO클래스 만들어 사용한다

### DTO (Data Transfer Object)
- 데이터들을 하나로 묶는것
- DB에서 데이터를 관리할 때 데이터를 일반적인 변수에 할당하여 작업 할수도 있지만, 해당 <u>데이터의 클래스를 만들어 사용</u>한다

![dao dto](https://user-images.githubusercontent.com/55946791/68037628-7faca800-fd0b-11e9-80d9-9809dc09102d.JPG)

### prepareStatement객체
- sql문 실행을 위해 Statement객체를 사용
- Statement객체는 중복코드가 많아짐. 따라서 PreparedStatement객체를 사용한다.

- 사용 전 : 데이터가 많아지면 복잡하고 난잡해진다.
```java
Statement stmt = null;
stmt = (Statement) con.createStatement();
rs = stmt.executeQuery("Insert into user (userId, userPw, name, phone, gender) values ('hyemi', 'hyemi2', '이혜미', '0109999999',  'f' )");
rs = stmt.executeQuery("Insert into user (userId, userPw, name, phone, gender) values ('changho', 'changho22', '이창호', '0109999999',  'f' )");
```
- 사용 후 : 가독성이 좋다
```java
private PreparedStatement pstmt;
String SQL = "Insert into user (userId, userPw, name, phone, gender) values (?, ?, ?, ?, ?)";
pstmt = connection.prepareStatement(SQL);
pstmt.setString(1, "hyemi");
pstmt.setString(2, "hyemi12");
pstmt.setString(3, "이혜미");
pstmt.setString(4, "0109999999");
pstmt.setString(5, "f");
rs = pstmt.executeUpdate();
pstmt.setString(1, "changho");
pstmt.setString(2, "changho22");
pstmt.setString(3, "이창호");
pstmt.setString(4, "0109999999");
pstmt.setString(5, "f");
rs = pstmt.executeUpdate();

```

### 커넥션 풀(DBCP)
- 클라이언트에서 다수의 요청이 발생하면(커넥션 객체를 다수 생성해야 한다) DB에 부하가 발생한다
- 이 문제를 해결하기 위해 커넥션 풀(DataBase Connection Pool)기법을 이용 한다
- <u>커넥션객체를 미리 만들어 놓는다</u>
![dbcp](https://user-images.githubusercontent.com/55946791/68067525-5cc1d880-fd8b-11e9-828e-9bece4f4813d.JPG)

#### DBCP 사용
1. tomcat컨테이너가 db인증을 하도록 context.xml 파일을 열어 아래의 코드를 추가한다
(서버에서 커넥션풀을 만들어야 하기 때문에 서버에 작업한다)
```xml
<Resource
	auth="Container"
	driverClassName = "com.mysql.jdbc.Drvier"
	url = "jdbc:mysql://localhost:3306/studyweb";
	username = "root";
	password = "devham7676";
	name = "jdbc/Mysql8"
	type ="javax.sql.DataSource"
	maxActive = "50"
	maxWait = "1000"
	/>
```


---
### 예제
- MemberDAO.java
```java
package com.javalac.daotoex;

import java.sql.*;
import java.util.ArrayList;

import com.mysql.jdbc.Statement;
// db를 직접 관리/수정
public class MemberDAO {

	private String dbUrl = "jdbc:mysql://localhost:3306/studyweb";
	private String dbId = "root";
	private	String dbPw = "devham7676";

	public MemberDAO() {
		try {
			// 드라이브 로드
			Class.forName("com.mysql.jdbc.Drvier");
		}catch(Exception e) {
			e.printStackTrace();
		}
	}

	public ArrayList<MemberDTO> memberSelect() {
		ArrayList<MemberDTO> dtos = new ArrayList<MemberDTO>();

		Connection con = null;
		Statement stmt = null;
		ResultSet rs = null;

		try {
			// 드라이버 메니저에 커넥션을 한다
			con = DriverManager.getConnection(dbUrl, dbId, dbPw);
			stmt = (Statement) con.createStatement();
			rs = stmt.executeQuery("select * from user");

			while(rs.next()) {

				String id = rs.getString("userId");
				String pw = rs.getString("userPw");
				String name = rs.getString("name");

				MemberDTO dto = new MemberDTO(id, pw, name);
				dtos.add(dto);
			}

		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				if (rs != null) rs.close();
				if (stmt != null) stmt.close();
				if (con != null) con.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		return dtos;
	}
}
```

- MemberDTO.java
```java
package com.javalac.daotoex;
// db에서 가져온 데이터를 관리해주는 클래스
public class MemberDTO {

	private String userId;
	private String userPw;
	private String userName;

	public MemberDTO(String userId, String userPw, String userName) {
		this.userId = userId;
		this.userPw = userPw;
		this.userName = userName;
	}

	public String getUserId() {
		return userId;
	}
	public void setUserId(String userId) {
		this.userId = userId;
	}
	public String getUserPw() {
		return userPw;
	}
	public void setUserPw(String userPw) {
		this.userPw = userPw;
	}
	public String getUserName() {
		return userName;
	}
	public void setUserName(String userName) {
		this.userName = userName;
	}
}
```
- memberSelect.jsp
```java
<%
	// 데이터 작업
	MemberDAO memberDAO = new MemberDAO();
	// 데이터 모으기
	ArrayList<MemberDTO> dtos = memberDAO.memberSelect();

	for(int i=0; i<dtos.size(); i++) {
		MemberDTO dto = dtos.get(i);
		String name = dto.getUserName();
		String id = dto.getUserId();
		String pw = dto.getUserPw();

		out.println("이름 :"+name+", 아이디 :"+id+", 비밀번호 :"+pw+"<br>");
	}
%>
```


---
## Reference
<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1180>
