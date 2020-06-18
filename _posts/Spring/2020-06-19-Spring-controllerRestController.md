---
title: "Spring, @Controller @RestController 차이"
date: 2020-06-19 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## @Controller @RestController 차이
- 주요한 차이점 : HTTP Response Body가 생성되는 방식

### @Controller
- 전통적인 Spring MVC의 컨트롤러
- __View 기술사용__
- @ResponseBody를 사용하면 View를 리턴하지 않고 Controller에서 직접 데이터 리턴 가능

> Spring4.0부터 @RestController를 통해 더 단순화 되었다.

### @RestController
- Restful 웹서비스의 컨트롤러
- 반환 되는 객체 데이터 타입 : __JSON/XML 타입의 HTTP 응답을 직접 리턴__

## 실행 흐름
### @Controller의 실행 흐름
Client -> Request -> Dispatcher Servlet -> Handler Mapping -> __Controller__ -> View -> Dispatcher Servlet -> Response -> Client

### @ResponseBody의 실행 흐름
Client -> Request -> Dispatcher Servlet -> Handler Mapping -> __Controller (ResponseBody)__ -> Response -> Client

### @RestController의 실행 흐름
Client -> HTTP Request -> Dispatcher Servlet -> Handler Mapping -> __RestController (자동 ResponseBody 추가)__ -> HTTP Response -> Client

## 1. @Controller(Spring MVC Controller)

### [Controller - View]
__Spring MVC Restful 전통적인 Work Flow__
![controller view](https://user-images.githubusercontent.com/55946791/85137406-1ff41480-b27c-11ea-8112-aac5b225c775.png)
- 전통적인 Spring MVC Controller인 @Controller는 주로 View를 반환하기 위해 사용한다.

1. Client는 URI형식으로 웹 서비스에 요청 전송
2. Mapping되는 Handler와 그 Type을 찾는 DispatcherServlet이 요청을 인터셉트
3. Controller가 요청을 처리한 후 응답을 DispatcherServlet으로 반환하고
DispatcherServlet은 __View를 사용자에게 반환.__

### [Contoller - Data]
__Spring 3.x MVC Restful Web Service Work Flow__
![controller data](https://user-images.githubusercontent.com/55946791/85137927-e8399c80-b27c-11ea-9407-9f87b104e749.png)
- @ResponseBody로 Spring MVC의 컨트롤러에서는 _데이터를 반환하기 위해_ 사용
1. Client는 URI형식으로 웹 서비스에 요청 전송
2. Mapping되는 Handler와 그 Type을 찾는 DispatcherServlet이 요청을 인터셉트
3. __@ResponseBody를__ 사용하여 Client에게 __Json형태로 데이터를 반환.__

## 2. @RestController(Spring Restful Controller)
__Spring 4.x MVC Restful Web Service Work Flow__
![restcontroller](https://user-images.githubusercontent.com/55946791/85138367-9cd3be00-b27d-11ea-9ad4-6340aa66c079.png)

- RestController = Spring MVC Controller + __@ResponseBody__
- 주용도 : Json/XML형태로 객체 데이터 반환
1. Client는 URI형식으로 웹 서비스에 요청 전송
2. Mapping되는 Handler와 그 Type을 찾는 DispatcherServlet이 요청을 인터셉트
3. RestController는 해당 요청을 처리하고 데이터를 반환.





--
## 참고
- <https://mangkyu.tistory.com/49>
- <https://lkg3796.tistory.com/58>
- <https://doublesprogramming.tistory.com/105>
