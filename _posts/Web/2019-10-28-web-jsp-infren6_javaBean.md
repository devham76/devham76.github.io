---
title: "WEB, 실전jsp강좌, 자바빈"
date: 2019-10-28 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 빈(bean) 이란?
- 반복적인 작업을 효율적으로 하기 위해 사용
- java언어의 데이터(속성)와 기능(메소드)으로 이루어진 클래스
- jsp 페이지를 만들고, 엑션태그를 이용하여 빈을 사용한다
- 빈을 만든다 : getter,setter있는 class파일을 만든다
![bean](https://user-images.githubusercontent.com/55946791/67659317-5accd380-f99f-11e9-978f-15d9777fec4c.JPG)

### 빈을 사용하는 이유
- JSP페이지에 뷰 부분과 로직 부분을 같이 작성하게되면 굉장히 복잡해지게 됩니다.

- 그런 것을 피하기 위해 JSP 페이지의 로직부분을 모듈화해서 분리함으로써 프로그램의 효율을 높이는 것이 사용하는 목적입니다.

![javabean](https://user-images.githubusercontent.com/55946791/70423002-0cd3e100-1ab0-11ea-8b49-17cec74be359.jpg)

---
### 빈의 사용
#### <jsp:useBean>
- 특정 Bean을 사용한다고 명시 할때 사용

```java
<jsp:useBean id="student" calss="com.javalec.ex.Student" scope="page" />

// 위의 액션태그를 코드로 바꾸면 아래와 같다

Student student = (Student)reqeust.getAttribute("student");
if (student == null){
	student = new Student();
	request.setAttribute("student", student);
}
```

- id : jsp페이지에서 자바빈 <u>객체에 접근 할때 사용하는 이름</u>
- class : 패키지 이름을 포함한 자바빈 클래스의 완전한 이름을 입력
- scope : 자바빈 <u>객체가 저장될 영역</u>을 지정

#### scope
- page : 생성된 페이지 내에서만 사용 가능
- request : 요청된 페이지 내에서만 사용 가능
- session : 웹브라우저 생명주기와 동일하게 사용가능
- application : 웹 어플리케이션 생명주기와 동일하게 사용 가능

#### <jsp:setProperty>
- 데이터 값 설정시 사용

```java
<jsp:setProperty name="student" property="name" value="로꼬" />
// name : 빈이름, property : 속성이름, value : 데이터 값

<jsp:setProperty name="student" property="*" />
```
- property속성의 값을 *로 지정하면 프로퍼티의 값을 같은 이름을 갖는 파라메터의 값으로 설정한다.


#### <jsp:getProperty>
- 데이터 값을 가져올때 사용
```java
<jsp:getProperty name="student" property="name"/>
// name : 빈이름, property : 속성이름
```
---
### 예제
- beanEx.jsp
```java
<jsp:useBean id="student" class="com.javalac.ex.Student" scope="page"></jsp:useBean>


<jsp:setProperty name="student" property="name" value="로꼬" />
<jsp:setProperty name="student" property="age" value="26" />
<jsp:setProperty name="student" property="grade" value="4" />
<jsp:setProperty name="student" property="studentNum" value="10" />

이름 : <jsp:getProperty name="student" property="name" /><br>
나이 : <jsp:getProperty name="student" property="age" /><br>
학년 : <jsp:getProperty name="student" property="grade" /><br>
번호 : <jsp:getProperty name="student" property="studentNum" />
```
- Student.java
```java
package com.javalac.ex;

public class Student {

	private String name;
	private int age;
	private int grade;
	private int studentNum;

	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public int getGrade() {
		return grade;
	}
	public void setGrade(int grade) {
		this.grade = grade;
	}
	public int getStudentNum() {
		return studentNum;
	}
	public void setStudentNum(int studentNum) {
		this.studentNum = studentNum;
	}
}
```

---
## Reference

- <https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1175>

- <https://all-record.tistory.com/105>
