---
title: "Spring, Spring Framework AOP"
date: 2020-01-29 17:40:28 -0400
categories: Spring
tags : [Spring,AOP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## AOP
- 로깅, 예외, 트랜잭션 처리 같은 부가적인 코드(<b>횡단관심</b>)로 인해서 비즈니스 메소드가 복잡해질때가 있다
- <b>핵심관심</b> : 핵심 비즈니스 로직
- AOP를 이용하여 관심 분리를 하므로써 클래스의 응집도를 높일 수 있다

## 예제

- LogAdvice.java

```java
package com.springbook.biz.common;

public class LogAdvice {
	public void printLog() {
		System.out.println("[공통 로그] 비즈니스 로직 수행 전 동작");
	}
}
```

- 스프링컨테이너 설정파일
    - 현재 진행중인 메소드가 expresion의 설정범위에 있으면 method를 실행시킨다

```xml
<bean id="log" class="com.springbook.biz.common.LogAdvice"></bean>
<aop:config>
  <aop:pointcut id="allPointcut" expression="execution(* com.springbook.biz..*Impl.*(..))"/>
  <aop:aspect ref="log">
    <aop:before pointcut-ref="allPointcut" method="printLog"/>
  </aop:aspect>
</aop:config>
```

- BoardServiceClient.java
  - 해당클래스를 실행시키면 BoardServiceImpl클래스의 insertBoard()메서드가 실생된다.
  - aop:pointcut 태그의 expression에 의해서 aop:aspect에 설정된 printLog()가 실행된다

```java
public class BoardServiceClient {

	public static void main(String[] args) {
      //... 생략
		// 3. 글 등록 기능 테스트
		BoardVO vo = new BoardVO();
		vo.setTitle("제목 테스트얌");
		vo.setWriter("이혜미");
		vo.setContent("임시 내용이라능 spring boot 뿌셔버리자능~~");
		boardService.insertBoard(vo);
      //... 생략
    }
}
```

- 결과
![aop ex](https://user-images.githubusercontent.com/55946791/73356763-63a2ad80-42de-11ea-88bf-9eead64681e9.JPG)

### 의미
- 핵심 관심 메소드(insertBoard())와 횡단 관심 메소드(printLog())사이에서 <b>소스상의 결합은 발생하지 않았다</b>

---

## AOP용어 정리

### 조인트 포인트(JoinPoint)
- client가 호출하는 모든 비즈니스 메소드
- ex) BoardServiceImpl, UserServiceImpl 클래스의 모든 메소드

### 포인트컷(Pointcut)
- 필터링된 조인트 포인트
- 비즈니스 메소드들 중에서 우리가 원하는 특정메소드

```xml
<aop:pointcut id="allPointcut" expression="execution(* com.springbook.biz..*Impl.*(..))"/>
```

- '*' : 리턴타입
- com.springbook.biz. . : 패키지정보
- '*Impl' : 클래스명
- *(..) : 메소드명 및 매개 변수

### 어드바이스(Advice)
- 횡당 관심에 해당하는 공통 기능의 코드
- 독립된 클래스 메소드로 작성한다
- 동작 시점 : before, after, after-returning, after-throwing, around

```xml
<aop:before pointcut-ref="allPointcut" method="printLog"/>
```

### 위빙(Weaving)
- 핵심 관심 메소드(포인트컷)가 호출될 때, 어드바이스에 해당하는 횡단관심 메소드가 삽입되는 과정을 의미한다.
- 위빙을 통해서 비즈니스 메소드를 수정하지 않고도 횡단 관심의 기능을 추가,변경할 수 있다.

### 애스팩트(Aspect) 또는 어드바이저(Advisor)
- 포인트컷 + 어드바이스 를 이어준다
- 어떤 포인트컷 메소드에 대해서 어떤 어드바이스 메소드를 실행할지 결정한다

```xml
<bean id="log" class="com.springbook.biz.common.LogAdvice"></bean>
<aop:config>
  <aop:pointcut id="allPointcut" expression="execution(* com.springbook.biz..*Impl.*(..))"/>
  <aop:aspect ref="log">
    <aop:before pointcut-ref="allPointcut" method="printLog"/>
  </aop:aspect>
</aop:config>
```

- 어디서 ? execution에 해당하는 메소드를 실행하는 곳에서
- 무엇을 ? printLog()메소드를
- 언제 ? before, 포인트컷 메소드가 실행되기 전에 실행한다

### <aop:advisor> 엘리먼트
- aspect와 같은 기능을한다
- <u>트랜잭션</u> 설정 같은 특수한 경우는 advisor를 사용
- <u>advice 객체의 아이디를 모르거나 메소드 이름을 확인할 수 없는 경우 사용한다</u>

---
## 어드바이스 동작 시점



---
## Reference
- 스프링 퀵 스타트-채규태 지음
