---
title: "Server, Blocking-NonBlocking-Synchronous-Asynchronous"
date: 2020-05-28 15:40:28 -0400
categories: [Server]
tags : [Blocking,Synchronous]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

> [최고 짱짱 이해 잘되는 블로그](https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)

## Blocking
- I/O 작업은 유저레벨에서 직접 수행 X, 커널레벨에서 가능하다
- I/O에서 Blocking 형태의 작업은 유저 프로세스가 커널에게 I/O를 요청하는 함수를 호출하고,
- 커널이 작업을 완료하면 함수가 작업 결과를 반환한다.

- __I/O 작업이 진행되는동안 유저 프로세스는 자신의 작업을 중단한채 대기해야 한다__
- I/O작업이 CPU자원을 거의 사용하지 않기 때문에 리소스 낭비가 심하다

![block non-block](https://user-images.githubusercontent.com/55946791/83138729-34823880-a126-11ea-9d77-f6805ddb9448.png)


## Blocking / non-Blocking
> Blocking / non-Blocking은 호출되는 함수가 바로 리턴하느냐 마느냐가 관심사
> Blocking/NonBlocking은 호출한 입장에서의 특징

- non-Blocking
	- __호출된 함수가 바로 리턴해서__ 호출한 함수에게 제어권을 넘겨주고
	- 호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있는것
  - 제어문 수준에서 지체없이 반환하는 것
- Blocking
  - __바로 리턴 안함__
	- 호출된 함수가 자신의 작엄을 모두 마칠 때까지 호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만든다
  -

## Synchronous / Asynchronous (동기/비동기)
> Synchronous/Asynchronous는 호출되는 함수의 작업 완료 여부를 누가 신경쓰냐가 관심사
> Sync/Async는 처리되는 방식의 특징

- Asynchronous(비동기)
	- 호출되는 함수에게 callback을 전달해서, 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 callback을 실행하고
	- __호출하는 함수는 작업완료 여부를 신경쓰지 X__
  - 별도의 쓰레드로 빼서 실행하고, 완료되면 호출하는 측에 알려주는 것

- Synchronous(동기)
	- 호출하는 함수가 호출되는 함수의 작업 완료 후 리턴을 기다리거나
	- 호출되는 함수로부터 바로 리턴 받더라도 __작업 완료 여부를 호출하는 함수 스스로 계속 확인하며 신경쓴다__

> 성능과 자원의 효율적 사용 관점에서 가장 유리한 모델은 Async-NonBlocking 모델이다.

## NonBlocking-Sync
![non blocking 동기화](https://user-images.githubusercontent.com/55946791/83138727-32b87500-a126-11ea-8c35-625ebb58aa20.png)

- 호출되는 함수는 바로 리턴하고, 호출하는 함수는 작업 완료 여부를 신경쓴다.(기다리거나 묻거나)
- NonBlocking함수를 호출했기 때문에, 기다리진 않고 계속 물어보기만한다

- NonBlocking 메서드 호출 후, 바로 반환 받아서 다른 작업을 할 수 있게 되지만
- 메서드 호출에 의해 수행되는 작업이 완료된것 아니고,
- 호출하는 메서드가 호출되는 메서드 쪽에 작업 완료 여부를 계속 문의한다.

```java
Future ft = asyncFileChannel.read(~~~);
while(!ft.isDone()) {
    // isDone()은 asyncChannle.read() 작업이 완료되지 않았다면 false를 바로 리턴해준다.
    // isDone()은 물어보면 대답을 해줄 뿐 작업 완료를 스스로 신경쓰지 않고,
    //     isDone()을 호출하는 쪽에서 계속 isDone()을 호출하면서 작업 완료를 신경쓴다.
    // asyncChannle.read()이 완료되지 않아도 여기에서 다른 작업 수행 가능
}

// 작업이 완료되면 작업 결과에 따른 다른 작업 처리
// 실무에서는 CompletableFuture를 쓰거나,
// Future를 쓴다면 위의 while 블록은 별도의 쓰레드로 빼서 실행하는 것이 좋다
```

## Blocking-ASync
![block 비동기](https://user-images.githubusercontent.com/55946791/83151524-a151fe80-a137-11ea-89f7-ebc2c8374fd7.png)
- 호출되는 함수가 바로 리턴하지 않고
- 호출하는 함수는 작업 완료 여부를 신경쓰지 않는것
- 대표 조합
	- Node.js(싱글 쓰레드 루프 기반) + MySQL
	- Node.js에서 Async(비동기)로 진행해도, db작업 호출시 MySQL에서 제공하는 드라이버 호출, 이것은 blocking방식
	- Java의 Servlet(멀티 쓰레드 기반) + JDBC
> Blocking-Async 는 별다른 장점이 없어 일부러 사용할 필요는 없지만
NonBlocking-Async 방식을 사용중에 Blocking으로 동작하는 것이 포함되어있다면
의도하지 않게 Blocking-Async로 동작할 수 있다.

<br>

- 동기 : call하고 응답이 올 때까지 기다렸다가 다음 로직을 실행한다.
 * 장점 : 안전성이 보장된다. 순서가 보장된다.
 * 단점 : 느리다.



- 비동기 : call하고 응답이 오지 않아도 다음 로직을 실행한다.
 * 장점 : 빠르다
 * 단점 : 처리 하기가 까다롭다. 순서가 보장이 되지 않는다.
 ---

synchronous blocking IO : syscall 이 완료될 때 까지 기다림
synchronous non-blocking IO : blocking 이 될 상황에서 EWOULDBLOCK 반환 (에러 처리 필요)
asynchronous blocking IO : IO는 non-blocking 이지만, 알림을 blocking 함 (select)
asynchronous non-blocking IO : IO를 background 에서 실행 callback 으로 처리
