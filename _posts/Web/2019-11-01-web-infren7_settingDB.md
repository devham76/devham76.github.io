---
title: "WEB, jsp & database 이용"
date: 2019-11-01 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### DB연결 순서
1. JDBC 드라이버 로드 / DriverManager
- 메모리에 mysqlDriver가 로드 된다
```java   
Class.forName("com.mysql.jdbc.Drvier");
```
2. 데이터베이스 연결 / Connection
- Connection 객체 생성
```java
Connection conn = DriverManager.getConnection(dbURL, dbID, dbPassword);
```
3. sql문 실행 / Statement
- Statement객체를 통해 sql문 실행
4. 데이터베이스 연결 해제 / ResultSet
```java
Statement stmt = null;
stmt = (Statement) con.createStatement();
rs = stmt.executeQuery("select * from user");
```

---
### Statement객체
- <interface> Statement
  - excuteQuery() / select
    - next(), previous(), first(), last(), get(getString, getInt)
  - executeUpdate() / insert, delete, update
---  

#### DAO
- 데이터 베이스 접근 객체 약자
- 실질적으로 db에서 회원정보를 불러오거나 입력,삭제시 사용 하는 클래스

---
### 예제
```java
package user;

import java.sql.*;

public class UserDAO {
	private Connection conn;
	private PreparedStatement pstmt;
	private ResultSet rs;

	// db 커넥션
	public UserDAO() {
		System.out.println("userdao !!");
		try {
			String dbURL = "jdbc:mysql://localhost:3306/studyweb";
			// 우리 컴에 설치된 mysql서버를 의미, bbs라는 데이터 베이스에 접속
			String dbID = "root";
			String dbPassword = "devham7676";
			//Class.forName("com.mysql.jdbc.Drvier");	// 주석처리하니까 실행됬음. 원인이 뭘까?
			// 드라이버 : mysql에 접속할 수 있도록 하는 하나의 메게체
			conn = DriverManager.getConnection(dbURL, dbID, dbPassword);
			System.out.println("1conn:"+conn);
		}catch(Exception e) {
			e.printStackTrace();
		}
	}

	public int login(String userID, String userPassword) {
		System.out.println("id : "+ userID+", pw: "+userPassword);
		String SQL = "Select userPw from user where userId = ? ";
		System.out.println("login conn:"+conn);
		try {
			pstmt = conn.prepareStatement(SQL);
			pstmt.setString(1, userID);
			rs = pstmt.executeQuery();
			if (rs.next()) {
				if(rs.getString(1).equals(userPassword)) {
					return 1; // 로그인 성공
				}
				else
					return 0; // 비밀번호 불일치
			}
			return -1; // 아이디가 없음
		} catch(Exception e) {
			System.out.println("error1");
			e.printStackTrace();
			System.out.println("error2");
		}
		return -2; // db오류
	}

	public int join(User user) {
		//System.out.println("id : "+ userId+", pw: "+userPw+", name :"+userName);
		String SQL = "Insert into user (userId, userPw, name) values (? ,? ,?) ";
		System.out.println("join conn:"+conn);
		System.out.println(SQL);
		try {
			pstmt = conn.prepareStatement(SQL);
			pstmt.setString(1, user.getUserId());
			pstmt.setString(2, user.getUserPw());
			pstmt.setString(3, user.getUserPw());
			return pstmt.executeUpdate();
		} catch(Exception e) {
			System.out.println("error1");
			e.printStackTrace();
			System.out.println("error2");
		}
		return -1; // db오류
	}
}
```

---
## Reference
<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1180>
