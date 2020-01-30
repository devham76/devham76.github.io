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
- client가 호출하는 <u>모든 비즈니스 메소드</u>
- ex) BoardServiceImpl, UserServiceImpl 클래스의 모든 메소드

### 포인트컷(Pointcut)
- 필터링된 조인트 포인트
- <u>비즈니스 메소드들 중에서 우리가 원하는 특정메소드</u>
- 이 메소드에서 횡단관심이 발생한다

```xml
<aop:pointcut id="allPointcut" expression="execution(* com.springbook.biz..*Impl.*(..))"/>
```

- '*' : 리턴타입
- com.springbook.biz. . : 패키지정보
- '*Impl' : 클래스명
- *(..) : 메소드명 및 매개 변수

### 어드바이스(Advice)
- <u>횡당 관심에 해당하는 공통 기능의 코드</u>
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
- <u>어떤 포인트컷 메소드에 대해서 어떤 어드바이스 메소드를 실행할지 결정한다</u>

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
|동작시점| 설명|
|--|--|
|Before|  비즈니스 메소드 실행 전 동작|
|After| - After Returning : 비즈니스 메소드가 <u>성공적으로 리턴<u>되면 동작<br>
- After Throwing : 비즈니스 메소드가 실행 중 <u>예외가 발생</u>하면 동작 (try~catch 블록에서 catch블록에 해당)<br>
- After : 비즈니스 메소드가 <u>실행된 후, 무조건 실행</u>(try~catch~finally에서 finally에 블록에 해당)|
|Around| <u>비즈니스 메소드 실행 전후</u>에 처리할 로직을 삽입할 수 있음|

- 예제

```xml
<bean id="afterThrowing" class="com.springbook.biz.common.AfterThrowingAdvice"></bean>
<bean id="after" class="com.springbook.biz.common.AfterAdvice"></bean>
<aop:config>
	<aop:pointcut id="allPointcut" expression="execution(* com.springbook.biz..*Impl.*(..))"/>
	<aop:aspect ref="afterThrowing">
		<aop:after-throwing pointcut-ref="allPointcut" method="exceptionLog"/>
	</aop:aspect>
	<aop:aspect ref="after">
		<aop:after pointcut-ref="allPointcut" method="finallyLog"/>
	</aop:aspect>
</aop:config>
```

- Around 예제
	- ProceedingJoinPoint객체의 proceed()를 통해 비즈니스 메소드를 호출할 수 있다.

```java
import org.aspectj.lang.ProceedingJoinPoint;

public class AroundAdvice {
	public Object aroundLog(ProceedingJoinPoint pjp) throws Throwable {
		System.out.println("[Before] : 비즈니스 메소드 수행 전에 처리내용...");
		Object returnObj = pjp.proceed();
		System.out.println("[After] : 비즈니스 메소드 수행 후에 처리내용...");
		return returnObj;
	}
}
```

## 애노테이션으로 AOP 설정
- @Service : 횡단관심의 기능을 가진 클래스의 객체를 생성시킨다(어드바이스)
- @Aspect : 어드바이스 + 포인트컷
- @Pointcut : 횡단관심 발생 메소드 위치
- @Before, @After, @AfterReturing, @AfterThrowing, @Around : 횡단관심 발생시점

## 예제

- xml 설정

```xml
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

### Before

```java
@Service	// 해당 클래스의 객체가 생성되어야 사용할 수 있으므로 @Service를 이용해 생성해준다.
@Aspect		// LogAdvice 어드바이스(공통횡단관심의 기능) + allPointcut 포인트컷(어디서 발생시킬지) 둘을 연결시켜준다
public class LogAdvice {
	@Pointcut("execution(* com.springbook.biz..*Impl.*(..))")
	public void allPointcut() {}

	@Before("allPointcut()")
	public void printLog() {
		System.out.println("[공통 로그] 비즈니스 로직 수행 전 동작");
	}
}
```

### After
- @AfterReturing (메소드 성공적 수행 후)
	- returning을 이용하여 메소드의 결과값을 받아 올 수 있다
- @AfterThrowing
	- throwing을 이용하여 예외값 받아올 수 있다
	- @AfterThrowing(pointcut="afterAllPointCut()", throwing="exceptObj")
- 예제

```java
@Service
@Aspect
public class AfterThrowingAdvice {

	@Pointcut("execution(* com.springbook.biz..*Impl.*(..))")
	public void afterAllPointCut() {}

	// 포인트컷 설정 및 (예외)결과값 받아오기
	@AfterThrowing(pointcut="afterAllPointCut()", throwing="exceptObj")
	public void exceptionLog(JoinPoint jp, Exception exceptObj) {
		String method = jp.getSignature().getName(); // 실행된 메소드 이름 가져오기
		System.out.println(method + "() 메소드 수행 중 예외 발생");

		if(exceptObj instanceof IllegalArgumentException) {
			System.out.println("부적합한 값이 입력되었습니다");
		} else if(exceptObj instanceof NumberFormatException) {
			System.out.println("숫자 형식의 값이 아닙니다");
		} else if(exceptObj instanceof Exception) {
			System.out.println("문제가 발생했습니다");
		}
	}
}
```

### Around

```java
@Service
@Aspect
public class AroundAdvice {
// ProceedingJoinPoint객체의 proceed()를 통해 비즈니스 메소드를 호출할 수 있다.
	@Pointcut("execution(* com.springbook.biz..*Impl.*(..))")
	public void aroundAllPointCut() {}

	@Around("aroundAllPointCut()")
	public Object aroundLog(ProceedingJoinPoint pjp) throws Throwable {
		String method = pjp.getSignature().getName();

		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		System.out.println("[Before] : 비즈니스 메소드 수행 전에 처리내용...");
		Object returnObj = pjp.proceed();

		stopWatch.stop();
		System.out.println(method + "() 메소드 수행 시간 : "+ stopWatch.getTotalTimeMillis()+"(ms)초");
		return returnObj;
	}
}
```

---
## Reference
- 스프링 퀵 스타트-채규태 지음
