---
title: "Spring, Spring Framework IoC XML파일로 설정하기"
date: 2020-01-29 13:40:28 -0400
categories: Spring
tags : [Spring,IoC]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## IoC
![IOC](https://user-images.githubusercontent.com/55946791/73336539-6fc64500-42b5-11ea-85c5-43153dabd93d.JPG)

## 생성자 인젝션 이용하기(Constructor Injection)
- 자바 소스코드는 변경하지 않고 컨테이너 설정파일만 변경해서 객체를 생성할수있다.
- 아래 xml파일에서 bean의 id값에 해당하는 값을 constructor-arg(생성자 매개변수)태그의 ref에 적절하게 넣으면 된다

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="tv" class="com.springbook.biz.polymorphism.SamsungTV">
		<constructor-arg index="0" ref="apple"></constructor-arg>
		<constructor-arg index="1" value="20000000"></constructor-arg>
	</bean>
	<bean id="sony" class="com.springbook.biz.polymorphism.SonySpeaker"></bean>
	<bean id="apple" class="com.springbook.biz.polymorphism.AppleSpeaker"></bean>
</beans>
```


- SamsungTV.java

```java
package com.springbook.biz.polymorphism;

public class SamsungTV implements TV{
	private Speaker speaker;
	private int price;

	public SamsungTV() {
		System.out.println("SamsungTV(1) 객체 생성");
	}
	public SamsungTV(Speaker speaker, int price) {
		System.out.println("SamsungTV(2) 객체 생성");
		this.speaker = speaker;
		this.price = price;
	}
 //  중략
}
```

### 결과 화면
- <constructor-arg index="0" ref="apple"></constructor-arg> 에 apple을 넣었으므로 AppleSpeaker클래스의 객체가 매개변수로 들어갔으므로 노란줄에 출력된다
- 빨간줄은 <bean id="apple" class="com.springbook.biz.polymorphism.AppleSpeaker"></bean> bean 태그로 설정하여 처음에 객체를 만들어줬기 때문에 출력되었다
![ioc ex](https://user-images.githubusercontent.com/55946791/73336346-ed3d8580-42b4-11ea-9559-f95dc6858cef.JPG)

---

## Setter 인젝션 이용하기
- 대부분 Setter인젝션을 사용하며, Setter메소드가 제공되지 않는 클래스에 대해서만 생성자 인젝션을 사용한다

### 예제
- 컨테이너 설정
- property태그를 이용하여 name에 있는 함수를 실행한다.
  - name="speaker" 이면 앞에 set을 붙인 함수가 실행된다(setSpeaker())

```xml
<bean id="tv" class="com.springbook.biz.polymorphism.SamsungTV">
  <property name="speaker" ref="apple"></property>
  <property name="price" value="200000000"></property>
</bean>
<bean id="sony" class="com.springbook.biz.polymorphism.SonySpeaker"></bean>
<bean id="apple" class="com.springbook.biz.polymorphism.AppleSpeaker"></bean>
```

- SamsungTV

```java
package com.springbook.biz.polymorphism;

public class SamsungTV implements TV{
	private Speaker speaker;
	private int price;

	public SamsungTV() {
		System.out.println("SamsungTV(1) 객체 생성");
	}

	public void setSpeaker(Speaker speaker) {
		System.out.println("---> setSpeaker() 호출");
		this.speaker = speaker;
	}
	public void setPrice(int price) {
		System.out.println("---> setPrice() 호출");
		this.price = price;
	}
  // 중략
}
```

### 결과화면
- property태그로 인해 함수가 호출된것을 확인할수있다
![ioc ex2](https://user-images.githubusercontent.com/55946791/73337005-c1bb9a80-42b6-11ea-8bde-e8184096b8e5.JPG)



---
## Reference
- 스프링 퀵 스타트-채규태 지음
