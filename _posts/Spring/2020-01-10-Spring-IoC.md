---
title: "Spring, IoC"
date: 2020-01-10 13:40:28 -0400
categories: Spring
tags : [Spring, IoC]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## Dependency ( 의존성 )
- <b>객체지향언어에서 두 클래스 간의 관계</b>
- 일반적으로 둘 중 하나가 다른 하나를 어떤 용도를 위해 사용함

### Dependency는 위험하다
- 하나의 모듈(클래스)이 바뀌면 다른 모듈까지 변경이 이루어지 지기 때문에 위험하다
- 테스트 가능한 어플을 만들때 의존성이 있으면 유닛테스트 작성이 어렵다
    - 유닛테스트의 목적 자체가 다른 모듈로부터 독립적으로 테스트하는 것을 요구하기 때문이다(Mock객체로 대체가능하다)

---

## IoC
- Inversion of Control ; 뒤바뀐 제어권


### 일반 제어권 vs IoC
- 일반적인 (의존성에 대한) 제어권 : 내가 사용할 <u>의존성은 내가 만든다</u>

```java
class OwnerController {
  private OwnerRepository repository = new OwnerRepository();
}
```

<br>
- IoC : 내가 사용할 <u>의존성을 누군가 알아서 주겠지</u>
  - 내가 사용할 의존성의 타입(또는 인터페이스)만 맞으면 어떤거든 상관없다
  - 그래야 내 코드 테스트 하기도 편하지

```java
class OwnerController{

  // ★★★해당 객체를 사용을 하지만 여기서는 만들지 않는다.★★★
  // 밖에서 누군가 만들겠지. -> 의존성 역전
  private OwnerRepository repo;

  public OwnerController(OwnerRepository repo) {
    this.repo = repo; // 의존성을 누군가 알아서 주겠지
  }
  public doSomething(){

  }

  // repo를 사용한다

}

class OwnerControllerTest {
  @Test
  public void create(){
    // OwnerRepository의 객체 없이는 OwnerController의 doSomething()을 호출할수없다.
    // 즉, OwnerController는 안전하다
    OwnerRepository repo = new OwnerRepository();
    OwnerController controller = new OwnerController(repo);
    controller.doSomething();
  }
}
```

---
## IoC 컨테이너
- ApplicationContext or Bean Factory 가 있다
- <b>빈(Bean , spring에서 사용할 객체)을 만들어 제공하고 , 빈들 사이의 의존성을 엮어준다</b>

<br>
- 빈 설정
    - 이름 or ID
    - 타입
    - 스코프
- but 컨테이너를 직접 쓸 일은 많지 않다

- 의존성 주입은 빈끼리만 가능하다, 즉 spring IoC컨테이너 안에 들어있는 객체끼리만 컨테이너가 의존성 주입을 해준다

- 객체 하나를 매번 새로 만들지 않고 계속 해서 사용한다. IoC컨테이너에 등록되어있는 Bean은 객체 하나이고 그것을 계속 사용한다

---
## Bean(빈)
- <b>스프링 IoC컨테이너가 관리하는 객체</b>
- 개발자가 일반적으로 생성한 객체(new 사용)은 bean이 아니다 !!
- 이런 Bean들만 의존성 주입이 된다

### 빈 등록방법
1. Component Scaning
    - 해당 <b>에노테이션</b>이 있으면 빈으로 등록해준다
    - @Component
    - @Repository
    - @Service
    - @Controller
    - @Configuration
2. 또는 <b>직접 일일히 XML이나 자바 설정 파일</b>에 등록

### 예제
- 직접 빈 설정파일 만들어주기

```java
@Configuration
public class SampleConfig{

  @Bean
  public SampleController sampleController(){
    return new SampleController();
  }
}
```

### 빈을 꺼내는 방법
- <b>@Autowired</b> 사용
- IoC컨테이너안에 있는 빈을 주입받아서 사용할 수 있다
```java
@Autowired
private OwnerRepository owners;
```

---
## 의존성 주입
: 필요한 의존성을 어떻게 받아올것인가
- 두 클래스가 서로 관계있게 어떻게 만들어줄수있는지
- 빈이 있어야 의존성을 주입한다
- @Autowired / @Injection 을 어디에 붙일까?
    - 생성자 (권장 !)
    - 필드
    - Setter
- <b>생성자에게 의존성을 주입하는것을 권장한다 , 해당객체가 생성되지 않으면 해당 클래스를 사용할수 없게 만들어버린다</b>
```java
@Controller
class OwnerController {

  private VisitRepository visits;

	private final OwnerRepository owners;    // 빈 껍데기

  /*
    1. 이 클래스에 있는 OwnerRepository는 빈 껍데기 이다
    2. 이 클래스의 객체를 만들고 싶으면 OwnerRepository객체가 필요하다
    3. 따라서 OwnerController클래스의 객체를 만들고자 하는 곳에서 OwnerRepository객체를 만들어서 파라메타로 전달해줘야 객체 생성이 가능하다
  */
  @Autowired
	public OwnerController(OwnerRepository clinicService, VisitRepository visits) {
		this.owners = clinicService;
		this.visits = visits;
	}

  /*
    ... 이하 생략
  */
}
```



---
## Reference
- [fastcampus] 예제로 배우는 스프링 입문 | 백기선님 강좌
