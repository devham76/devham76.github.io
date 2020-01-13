---
title: "Spring, PSA"
date: 2020-01-13 13:40:28 -0400
categories: Spring
tags : [Spring, PSA]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## PSA
- Potable Service Abstraction
- 잘 만든 인터페이스(PSA)
- 내 코드는 변경하지 않아도 원하는 환경에 맞게 쉽게 변경할 수 있다


### 스프링 웹 MVC
- @Controller : 해당 에노테이션을 붙이면 요청을 매핑하는 controller클래스가된다
    - @RequestMapping (@GetMapping, @PostMapping) 을 사용한다
- 톰캣, 네티, 제티, 언더토우

### 스프링 트랜잭션
- @Transactional : 해당 에노테이션이 있으면 아래처럼 복잡하게 하지 않고 해당 메소드를 트랜젝션처리가 될 수 있도록 한다

- jdbc Transaction ex

```java
dbConnection.setAutoCommit(false);
// sql query가 들어와도 커밋하지 않고있다가
...
// 한꺼번에 커밋한다
dbConnection.commit();
```

- OwnerRepository.java

```java
@Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE %:firstName%")
@Transactional(readOnly = true)
Collection<Owner> findByFirstName(@Param("firstName") String firstName);
```

- 내 코드는 변경하지 않아도 JpaTrasaction, Hibernate..등으로 바꿔 사용할 수 있다(Potable 특성)


---
## Reference
- [fastcampus] 예제로 배우는 스프링 입문 | 백기선님 강좌
