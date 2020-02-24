---
title: "Spring, JPA 기본키 매핑"
date: 2020-02-24 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## @Id
- 기본키 할당하는 방법은 _직접할당_, _자동생성_ 두가지 방법이 있다.
- __DBMS마다 sequence, auto_increment등 기본키를 자동생성 방법이 다르다__
- Spring Data JPA는 이를 해결하기 위해 4가지 자동 생성 방법을 제공한다.

## 기본키 자동생성 방법
### IDENTITY
- 기본 키 생성을 DB에 위임하는 방법(DB에 의존적)
- MySQL, PostgresSQL, SQL Server, DB2

### SEQUENCE
- DB 시퀀스를 사용해서 기본 키를 할당하는 방법 (DB에 의존적)
- 주로 시퀀스를 지원하는 Oracle, PostgresSQL, DB2, H2에서 사용
- @SequenceGenerator를 사용하여 시퀀스 생성기를 등록하고, 실제 db에 생성될 시퀀스이름을 지정해줘야 한다

### TABLE
- 키 생성 테이블을 사용하는 방법
- 키 생성 전용 테이블을 하나 만들고 여기에 이름과 값으로 사용할 컬럼을 만드는 방법
- 테이블을 사용하므로, DBMS종류에 상관없이 모든 DBMS에 적용가능

### AUTO
- DBMS에 의존하지 않고 기본키를 할당하는 방법
- DBMS에 따라 위의 세가지 방법 중 하나를 자동으로 선택해준다

```java
// lombok의 어노테이션
@Getter // 클래스 내 모든 필드의 Getter 메소드를 자동생성
@NoArgsConstructor // 파라메터 없는 기본 생성자 자동추가, entity는 기본생성자가 꼭 있어야 한다

// 테이블과 링크 될 클래스임을 알린다
@Entity
public class Posts extends BaseTimeEntity {
    @Id // pk필드
    @GeneratedValue(strategy = GenerationType.IDENTITY) // pk생성규칙, auto_increment
    private Long id;

    @Column(length = 500, nullable = false)
    private String title;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String content;

    private String author;

    // 해당 클래스의 빌더 패턴 클래스를 생성
    @Builder
    public Posts(String title, String content, String author) {
        this.title = title;
        this.content = content;
        this.author = author;
    }

    public void update(String title, String content) {
        this.title = title;
        this.content = content;
    }
}

```

---
## Reference
- <https://ithub.tistory.com/24>
