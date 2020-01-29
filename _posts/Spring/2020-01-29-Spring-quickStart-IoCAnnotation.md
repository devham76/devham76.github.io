---
title: "Spring, Spring Framework IoC 애노테이션으로 설정하기"
date: 2020-01-29 14:40:28 -0400
categories: Spring
tags : [Spring,IoC]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

- <bean>등록하지 않고 자동으로 생성하려면 <context:component-scan>을 정의해야한다
- 스프링 컨테이너는 클래스 패스에 있는 클래스들을 스캔하여 <u>@Component가 설정된 클래스들을 자동으로 객체 생성한다</u>

```xml
<!-- 방법1 어노테이션이용 -->
<context:component-scan base-package="com.springbook.biz.polymorphism"></context:component-scan>
```

### @Component
- @Component가 붙은 클래스는 자동으로 객체가 생성된다
- "tv"를 붙여서 요청시 사용할 아이디나 이름을 설정할수있다
```xml
<bean id="tv" class="com.springbook.biz.polymorphism.SamsungTV"/>
```

```java
@Component("tv")
public class SamsungTV implements TV{
}
```

### @Autowired
- 객체가 메모리에 존재하는지 확인 후에 <u>객체를 변수에 주입한다</u>
- 생성자, 메소드, 멤버변수(대부분)에 사용가능하다

### @Qualifer
- 만약 SonySpeaker와 AppleSpeaker객체가 모두 메모리에 생성되어있다면 컨테이너는 어떤 객체를 주입할지 판단할 수 없다
- 이떄 @Qualifer를 이용하여 객체의 이름으로 판단하여 의존성을 주입한다.

```java
public class SamsungTV implements TV{
	@Autowired
	@Qualifier("apple")
	private Speaker speaker;

  // ... 생략
}

// -- AppleSpeaker.java
@Component("apple")
public class AppleSpeaker implements Speaker {
  // 생략
}
```

### @Resource
- @Autowired는 변수의 타입을 기준으로 객체를 검색, 의존성 주입한다
- @Resource는 객체의 이름을 이용하여 객체를 검색, 의존성 주입한다

```java
@Component("tv")
public class SamsungTV implements TV{

	// 의존성 주입 방법 2.
	@Resource(name="apple")
	private Speaker speaker;
	private int price;
```


### 추가 어노테이션
![시스템구조](https://user-images.githubusercontent.com/55946791/73338617-5c69a880-42ba-11ea-8871-a9e84526079c.JPG)

1. Controller : 사용자의 요청을 제어
2. ServieImpl : 실질적인 비지니스 로직 처리
3. DAO : DB연동 담당

- 모든 클래스에 @Component를 할당하면 어떤 클래스가 어떤 역할을 수행하는지 파악하기 어렵다. 따라서 세개의 어토데이션을 추가로 제공한다




---
## Reference
- 스프링 퀵 스타트-채규태 지음
