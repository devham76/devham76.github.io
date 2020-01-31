---
title: "Spring, JDBC"
date: 2020-01-30 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## JdbcTemplate 클래스
- JDBC 프로그램을 이용하려면 작성해야할 코드가 너무 많다
- <u>DB연동에 필요한 자바 코드를 처리해주고 개발자는 SQL 구문만 관리</u>할 수 있도록 지원한다
- GoF디자인 패턴 중 템플릿 메소드 패턴이 적용된 클래스이다
- 템플릿 메소드 패턴 : 복잡,반복되는 알고리즘을 캡슐화해서 재사용하는 패턴으로 정의할 수 있다

### 예제
- maven등록

```xml

<!-- DBCP관련 설정 -->
<dependency>
  <groupId>commons-dbcp</groupId>
  <artifactId>commons-dbcp</artifactId>
  <version>1.4</version>
</dependency>

<!-- Spring -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-jdbc</artifactId>
  <version>${org.springframework-version}</version>
</dependency>
```

- spring container 설정

```xml
<!-- DB로부터의 커넥션 -->
<!-- DataSource설정 -->
<context:property-placeholder location="classpath:config/database.properties"/>
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
  <property name="driverClassName" value="${jdbc.driver}" />
  <property name="url" value="${jdbc.url}" />
  <property name="username" value="${jdbc.username}" />
  <property name="password" value="${jdbc.password}" />
</bean>

<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
  <property name="dataSource" ref="dataSource" />
</bean>
```

- config/database.properties

```xml
jdbc.driver=org.h2.Driver
jdbc.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1
jdbc.username=sa
jdbc.password=
```

- BoardDAOSpring.java
  - @Repository : 객체 생성
  - @Autowired : JdbcTemplate 클래스 의존성 주입

```java
// DAO(Data Access Object)
@Repository // 객체 생성 @Component와 비슷한일을 하지만 데이터 관리에 더 특화되어있다
public class BoardDAOSpring {

	@Autowired // 의존성주입  해당 객체는 설정파일에서 bean으로 만들어줬다
	private JdbcTemplate jdbcTemplate;

	// SQL 쿼리문
	private final String BOARD_INSERT 	= "insert into BOARD (seq, title, writer, content) values ( (select nvl(max(seq), 0)+1 from board), ?,?,?)";

	//-- CRUD 기능 메소드 구현
	// 글 등록
	public void insertBoard(BoardVO vo) {
		System.out.println("==>SPRING JDBC로 insertBoard() 기능 처리");
		jdbcTemplate.update(BOARD_INSERT, vo.getTitle(), vo.getWriter(), vo.getContent());
	}    
  // ...중략
```



---
## Reference
- 스프링 퀵 스타트-채규태 지음
