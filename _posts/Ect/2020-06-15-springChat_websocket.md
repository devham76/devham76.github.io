---
title: "Spring, chatting 프로그램 만들기, websocket"
date: 2020-06-15 20:00:28 -0400
categories: etc
tags : [project, websocket, spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 채팅 서비스 구현하기
팀원들과 velog를 클론코딩하기로 했다. 큰 도메인은 게시물, 개인페이지였고 팀원은 백엔드 개발자 세명이여서 일 분배가 어려웠다. 따라서 나는 그 동안 구현 해보고 싶었던 채팅 서비스를 구현해서 붙여보기로 했다.


- 일반적인 http통신을 하는 서버들과 달리 __채팅 서버는 socket통신을 하는 서버가__ 필요하다.

### http통신
- __client의 요청이 있을 때만 서버가 응답하고 연결을 종료하는 단방햔 통신__ 이다.
- 따라서 client가 server에 접속해 콘텐츠를 요청하고 결과를 받아 소비하는 구조의 서비스에서 많이 사용된다.

### socket통신
- __server와 client가 특정 port를 통해 지속적으로 연결유지 하여 실시간으로 양방향 통신을 하는 방식__
- 주로 채팅 같은 실시간성을 요구하는 서비스에서 많이 사용된다.

### Websocket
- Websocket은 기존의 단방향 __HTTP프로토콜과__ 호환되어 __양방향 통신을__ 제공하기 위해 개발된 프로토콜
- 일반 Socket통신과 달리 __HTTP 80 port를 이용하므로 방화벽에 제약이 없다__
- __접속까지는 HTTP 프로토콜을__ 이용하고 그 이후의 통신은 자체적인 Websocket 프로토콜로 통신하게 된다.

## 실습
### build.gradle

```java
implementation 'org.springframework.boot:spring-boot-starter-websocket'
```

### WebSocketChatHandler

```java
@Slf4j
@Component
public class WebSockChatHandler extends TextWebSocketHandler {

    protected void handleTextMessage(WebSocketSession session, TextMessage message) throws Exception{
        String payload = message.getPayload();
        log.info("payload {}", payload);
        TextMessage textMessage = new TextMessage("Welcome chatting server !!");
        session.sendMessage(textMessage);
    }
}
```

### WebSockConfig

```java
@RequiredArgsConstructor
@Configuration
@EnableWebSocket
public class WebSockConfig implements WebSocketConfigurer {
    private final WebSocketHandler webSocketHandler;

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(webSocketHandler, "/ws/chat").setAllowedOrigins("*");
    }
}
```

### 확장프로그램 설치
- <https://chrome.google.com/webstore/search/websocket>

### 결과화면

![websocket](https://user-images.githubusercontent.com/55946791/84656452-a8f20f80-af4d-11ea-93b4-ab6cc49026b4.JPG)


---
## 참고
- [Websocket>Spring websocket chatting server(1) – basic websocket server
](https://daddyprogrammer.org/post/4077/spring-websocket-chatting/)
- [Http 통신과 Socket 통신 차이](https://mangkyu.tistory.com/48)
