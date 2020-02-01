---
title: "Spring, DI, IoC"
date: 2020-01-10 13:40:28 -0400
categories: Spring
tags : [Spring, DI, IoC]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---



## Dependency Injection
- 컨테이너가 직업 객체들 사이에 의존관계를 처리하는 것.
- Setter Injection , Constructor(생성자) Injection
- 의존성이 삽입된다는 의미로 IoC를 DI라는 표현으로 사용합니다.
### Dependency ( 의존성 )
- <b>객체지향언어에서 두 클래스 간의 협력하는 관계</b>
- 일반적으로 둘 중 하나가 다른 하나를 어떤 용도를 위해 사용함

### Dependency는 위험하다
- 하나의 모듈(클래스)이 바뀌면 다른 모듈까지 변경이 이루어지 지기 때문에 위험하다
- 테스트 가능한 어플을 만들때 의존성이 있으면 유닛테스트 작성이 어렵다
    - 유닛테스트의 목적 자체가 다른 모듈로부터 독립적으로 테스트하는 것을 요구하기 때문이다(Mock객체로 대체가능하다)
- Controller는 Repository에 의존한다 (ioc 구현전)


---

## IoC
- Inversion of Control ; 뒤바뀐 제어권

### IoC란
- 객체의 생성이나 객체사이의 의존관계를 개발자가 직접 자바 코드로 처리해야했었다. 이런 상황에서는 의존관계에 있는 객체를 변경하려면 반드시 자바코드를 수정해야 한다.
- 하지만 IoC가 적용되면 객체 생성과 의존관계를 컨테이너가 처리하게 된다
- 결과적으로 소스에 의존관계가 명시되지 않으므로 결합도가 떨어져서 유지보수가 편리해진다.

### 구현방법
- 스프링은 두가지( @Component, @Autowired ) 어노테이션을 지원해서 IoC를 구현한다
- @Component
- @Autowired
- 의존성이 삽입된다는 의미로 IoC를 DI라는 표현으로 사용합니다.

```java
@RestController
public class RestaurantController {

    // ★ IoC사용 전 ★
    // Contorller에서 Restaurant Repository를 직접 만들어준다
    //private RestaurantRepository repository = new RestaurantRepository();

    // ★ IoC사용 후 ★
    @Autowired  // RestaurantController를 만들어줄때 spring이 알아서 RestaurantRepository의 객체를 만들어준다
    private RestaurantRepository repository;

    // ...이하 생략
}
```

```java
// RestaurantRepository를 스프링이 직접 관리하도록 해당 애노테이션을 붙인다
@Component
public class RestaurantRepositoryImpl implements RestaurantRepository {

    // 이하 생략
}
```

```java
//RestaurantRepository를 다른 형태로 쉽게 변경할수있다
public interface RestaurantRepository {
    List<Restaurant> findAll();
    Restaurant findById(Long id);
}
```

- 이렇게 IoC를 사용하는것으로 변경하고 Test를 돌리면 오류가 발생한다
- 해당 오류는 RestaurantControllerTest 클래스에 객체를 직접주입하여 해결할 수 있다

```java
@SpyBean(RestaurantRepositoryImpl.class)   // 컨트롤러에 원하는 객체를 주입할수있다
private RestaurantRepository restaurantRepository;
```

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
- 각 객체들의 강한 의존성을 유연하게 한다

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
- [inflearn] 예제로 배우는 스프링 입문 | 백기선님 강좌
- <https://jongmin92.github.io/2018/02/11/Spring/spring-ioc-di/>
