---
title: "Spring, 2-Layered 아키텍쳐 스타일"
date: 2020-02-03 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## Service
- <u>Controller는 DAO객체를 직접 이용해서는 안되며, 반드시 비즈니스 컴포넌트를 이용하여 사용자의 요청을 처리해야 한다.</u>
- DAO객체를 직접 사용하면 문제가 발생한다

### 변경 전
![게시판프로그램수행흐름](https://user-images.githubusercontent.com/55946791/73634082-b5af4e80-46a3-11ea-9634-a220dcf998d2.jpg)
### 변경 후
- Business Layer가 추가되었고 Controller는 DAO를 직접 이용하지 않는다
![게시판프로그램수행흐름2](https://user-images.githubusercontent.com/55946791/73634581-d4faab80-46a4-11ea-9cd8-e4e522d4e9ba.jpg)


### (1) DAO 클래스 교체하기
- 이유 1. DAO클래스를 다른 클래스로 쉽게 교체하기 위해서이다
- 비즈니스 컴포넌트가 변경되거나 새로운 요소가 추가될 때마다 이를 사용하는 Controller의 소스를 매번 수정한다면 유지보수는 어려울 수밖에 없다

### (2) AOP 설정하기
- 이전에 설정한 AOP의 포인트컷은 Service구현 클래스의 메소드에 설정했다
- 따라서 Controller메소드에서 Service클래스의 인터페이스를 통해 비즈니스 객체의 메소드를 호출하여, AOP로 설정한 어드바이스들이 동작하게한다.

### (3) 비즈니스 컴포넌트 의존성 주입하기
- Controller 객체들이 생성되기 전에 비즈니스 컴포넌트 객체를 생성해야 (@Autowired BoardService)의존성 주입이 가능하다
- 의존성 주입을 해야 Controller는 직접 DAO를 이용하지 않고 BoardService클래스의 메소드를 이용하게된다
- 따라서 <u>Controller 객체들이 생성되기 전에 applicationContext.xml 파일을 읽어 비즈니스 컴포넌트들을 메모리에 생성해야한다</u>

### web.xml
: <u>ContextLoaderListener는 클라이언트의 요청이 없어도 컨테이너가 구동될때 Pre-Loading 되는 객체이다</u>
- ContextLoaderListener는 applicationContext.xml을 읽는다
- applicationContext.xml의 context:component-scan 태그에 의해서 @Component, @Autowired 가 붙은 클래스, 변수의 객체를 생성한다

```xml
<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:applicationContext.xml</param-value>
</context-param>

<listener>
  <listener-class>
    org.springframework.web.context.ContextLoaderListener
  </listener-class>
</listener>
```

## 스프링 구동순서와 관계
![스프링 구동순서](https://user-images.githubusercontent.com/55946791/73637441-a46a4000-46ab-11ea-9e2a-f2b328f71f95.jpg)

### 1. 서블릿 컨테이너 구동
web.xml 파일을 로딩하여 서블릿 컨테이너가 구동된다

### 2. ContextLoaderListener 객체 생성
- 서블릿 컨테이너는 web.xml 파일에 등록된 ContextLoaderListener객체를생성 (pre loading)한다.
- 이때 ContextLoaderListener 객체는 src/main/resources 소스 폴더에 있는 applicationContext.xml 파일을 로딩하여 스프링 컨테이너를 구동한다 (<b>이를 Root 컨테이너라고한다</b>)
- <u>이때 Service구현 클래스나 DAO객체들이 메모리에 생성된다</u>


### 3. 사용자 요청
- 사용자의 액션에 의해 "*.do" 요청이 서버에 전달되면 서블릿 컨테이너는 DispatcherServlet 객체를 생성하고
- /WEB-INF/config 콜더에 있는 presentation-layer.xml(controller,viewResolver 정보) 파일을 로딩하여 두번째 스프링 컨테이너를 구동한다.

- 이 두번째 스프링 컨테이너가 Controller 객체를 메모리에 생성한다



---
## Reference
- 스프링 퀵 스타트-채규태 지음
