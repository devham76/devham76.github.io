---
title: "Spring, AOP"
date: 2020-01-10 13:50:28 -0400
categories: Spring
tags : [Spring, AOP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## AOP
- 흩어진 코드를 한 곳으로 모은다
<h3>[나온 배경]</h3>
똑같은일을 하는데 여러곳에 흩어져있는 코드가 있을때, 그 코드를 수정하려면 사용한곳을 모두 찾아서 수정해야한다
- 예제

```java
@GetMapping("/owners/find")
public String initFindForm(Map<String, Object> model) {
      // AOP 사용 전 , 불편하다!!!
      StopWatch stopWatch = new StopWatch();
      stopWatch.start();

  model.put("owner", new Owner());

      // AOP 사용 전 , 불편하다!!!
      stopWatch.stop();
      System.out.println(stopWatch.prettyPrint());

  return "owners/findOwners";
}
```

<br>
<h3>[해결]</h3>
똑같은 일을 하는 코드를 한데 묶어버린다


### AOP 구현 방법
- 컴파일
    - ex) A.java --(AOP끼어넣는다)-->A.class (기능이 생겨난다)
- 바이트코드 조작
    - A.java -> A.class --(AOP)--> 메모리 (기능이 생겨난다)
- <b>프록시 패턴 (스프링 AOP가 사용하는 방법)</b>
    - 기존코드 건들지 않고 새기능 추가하는방법
    - 참고로 어떤 내용인지만 알고있으면된다

```java
@Test
public void testPay(){
    // 스프링 부트가 하는일 ->
    // Cash만 만들어놔도 프록시 패턴인 CashPerf가 자동으로 빈에 등록되고 Cash대신에 사용된다
    Payment cashPerf1 = new CashPerf(); // stopwatch기능 있음 , proxy패턴 !
    Payment cashPerf2 = new Cash();     // stopwatch기능 없음
    Store store = new Store(cashPerf1);
    store.buySomething(100);
}
```

---
## AOP 적용 예제
<h2>@LogExecutionTime 으로 메소드 처리 시간 로깅하기</h2>

- @LogExecutionTime 에노테이션 (어디에 적용할지 표시 하는 용도) 생성

```java
// 이 에노테이션을 메소드에 사용하겠다
@Target(ElementType.METHOD)
// 이 정보를 언제까지 유지할것인가 , 런타임까지 유지한다
@Retention(RetentionPolicy.RUNTIME)
public @interface LogExecutionTime {
}
```

- 해당 애노테이션 정의

```java

@Component // Bean으로 등록해준다

@Aspect
public class LogAspect {
    Logger logger = LoggerFactory.getLogger(LogAspect.class);

    // 프록시패턴을 기반으로 동작한다
    // ★ LogExecutionTime 애노테이션이 하는일을 설정해준다 ★
    @Around("@annotation(LogExecutionTime)")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        // ProceedingJoinPoint : 애노테이션이 붙어 있는 메소드가 실행되면
        // 아래 일을 실행하겠다.
        StopWatch stopWatch = new StopWatch();
        stopWatch.start();

        // 애노테이션이 붙어있는 메소드를 실행해라
        Object proceed = joinPoint.proceed();

        stopWatch.stop();
        logger.info(stopWatch.prettyPrint());

        return proceed;
    }
}
```

- 사용

```java
@GetMapping("/owners/{ownerId}/edit")
  @LogExecutionTime
public String initUpdateOwnerForm(@PathVariable("ownerId") int ownerId, Model model) {
  Owner owner = this.owners.findById(ownerId);
  model.addAttribute(owner);
  return VIEWS_OWNER_CREATE_OR_UPDATE_FORM;
}
```


---
## Reference
- [fastcampus] 예제로 배우는 스프링 입문 | 백기선님 강좌
