---
title: "기술 면접 준비-기본"
date: 2019-10-22 15:00:28 -0400
categories: [summary]
tags : [summary, JAVA]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

>JAVA 관련 예상 질문

#### 1. 객체지향에 대해 설명해보세요
- <b>캡상추다 (캡슐화 / 상속 / 추상화 / 다형성)</b>으로 코드의 <b>재사용성</b>을 높이고 코드의 <b>관리가 용이</b>하고 <b>제어자와 메서드를 이용하여 데이터를 보호</b>하는데 좋다
- <b>코드의 중복을 제거</b>하여 코드의 불일치로 인한 오류를 방지 할 수 있다

##### 캡슐화
- <u>데이터 보호</u> / 불필요한 부분을 감출 수 있다 (접근 제어자 / 인터페이스 등)

##### 상속
- 기존의 클래스를 <u>재사용</u>해서 새로운 클래스를 작성하는 것 (class 자손클래스 extends 조상클래스{...})

##### 추상화
- 추상클래스 / 추상메서드 / 인터페이스를 예로 설명

##### 다형성
- 하나의 참조변수로 여러 타입의 객체를 참조 할 수 잇는 것 (조상타입의 참조변수로 자손타입의 객체를 다룰 수 있는 것)

---
#### 2. 오버로딩 & 오버라이딩 차이?
- 오버로딩은 하나의 클래스에 같은 이름의 메서드를 여러개 정의 하는 것을 말하며, 오버라이딩은 조상클래스로부터 상속받은 메서드의 내용을 상속받는 클래스에 맞게 변경하는 것을 말한다

##### 오버로딩 조건
- 메서드의 이름이 같아야 한다
- 매개변수의 개수 or 타입이 달라야한다. (리턴타입은 오버로딩 구현과 관계 없다)

##### 오버라이딩 조건
- 선언부가 같아야 한다 (이름 / 매개변수 / 리턴타입)
- 접근제어자를 좁은 범위로 변경할 수 없다
- 조상클래스의 메서드보다 많은 수의 예외를 선언할 수 없다

---
#### 3. 접근제어자<br>
: 멤버 or 클래스에 사용되어, 외부로부터의 접근을 제한 (클래스 / 멤버변수 / 메서드 / 생성자)

##### public
: 접근 제한 없음
##### protected
: 같은 패키티 & 다른 패키지의 자손클래스에서 접근 가능
##### default
: <b>같은 패키지</b> 내에서만
##### private
: <b>같은 클래스</b> 내에서만 접근 가능

---
#### 4. 클래스 / 추상클래스 / 인터페이스 차이
- 클래스 : 설계도 , 추상클래스 : 미완성 설계도 , 인터페이스 : 밑그림
- 인스턴스 생성여부
  - 클래스 : 속성과 기능들로 완성된 설계도 이기 때문에 인스턴스 생성가능
  - 추상클래스 / 인터페이스 : 미완성 이기 때문에 인스턴스 생성 불가능
- 구성
  - 추상클래스 : 미완성 메서드 포함
  - 인터페이스 : 선언부만 있는 메서드와 상수를 가진다
- 인터페이스
  - 클래스를 작성하는데 도움을 줄 목적으로 사용
  - 인터페이스 추가 설명으로는 관계없는 클래스 간 관계를 맺어주고 표준화를 시킨다
  - 개인작업이 가능하게 해줘서 프로그래밍 시간을 단축 시킬 수 있다
  - 상속이 가능하며 다중상속까지 불가능하다
- (class 클래스명, abstract class 클래스명, interface 인터페이스명)

---
#### 5. 프로세스/쓰레드
- <b>프로세스 : 공장 / 쓰레드 : 일꾼</b>
##### 프로세스
: 실행중인 프로그램. 자원(resources)과 쓰레드로 구성
##### 쓰레드
: 프로세스 내에서 실제 작업을 수행하는 단위. 모든 프로세스는 하나의 쓰레드를 가지고 있다
##### 멀티쓰레드
: 하나의 프로세스에 하나 이상의 쓰레드를 생성하여 실행

---

> 데이터베이스 SQL문 관련 예상 질문과 문제

##### select문 만드는 방법
```sql
SELECT 컬럼명
FROM 테이블명
WHERE 조건식
ORDER BY 컬럼명 OR 표현식(ASC OR DESC);

*WHERE 절에 쓰이는 연산자*
- 논리 비교 연산자 : != <> ^=
- SQL비교 연산자 :
1. NOT BETWEEN ~ AND ~
2. NOT IN
3. NOT LIKE (% 사용할 경우 결과도 알아야함)
4. IS NOT NULL
```

##### GROUP BY와 HAVING 절
```sql
SELECT 컬럼명, GROUP 함수
FROM 테이블명
WHERE 조건식
GROUP BY 컬럼명
HAVING 조건식
ORDER BY 컬럼명이나 표현식 // 제일 마지막에 위치 !!

// 문제 1. 각 지역별로 몇 개의 부서가 있는지 나타내시오.
SELECT name, count(region_id)
FROM s_dept
GROUP BY site_name

// 문제 2. 각 부서별로 평균 급여를 구하되 평균 급여가 2000 이상인 부서를 나타내시오.
SELECT dept_id, AVG(salary)
FROM s_emp
GROUP BY dept_id
HAVING AVG(salary) >= 2000
```

##### JOIN


##### 서브 쿼리(SubQUERY)
: 하나의 SELECT문 안에 포함되어 있는 또 다른 SELECT 문장

---

> JSP & JAVA SCRIPT 관련 질문

##### request 객체 / response 객체란?
- request 객체는 클라이언트에서 서버로 넘어오는 데이트를 전달받기 위한 객체
- response 객체는 서버에서 클라이언트로 데이터를 전달하기 위한 객체

##### GET & POST 방식의 차이
- GET : URL로 값을 보내기 때문에 보안에 취약하고 길이 제한이 있다
- POST :  값을 전송하지만 URL에 노출되지 않아 보안에 강하고 많은 양의 데이터를 보내는데 적합하다

##### 쿠키(Cookie) & 세션(Session)의 특징
- 공통점 : 데이터를 저장하는 용도로 쓰임

|| 보안 | 속도 |
|---|:---:|---:
쿠키 | 물리적인 형태로 저장, 보안에 취약 | 빠르다
세션 | 서버에 보관, 보안에 좋다 | 느리다

##### 비동기식 & 비동기식 일처리
- 동기식 : 순차적으로 일을 스스로 끝내 나가는 방식으로 작업 당 페이지 이동이 있는 경우 이다
- 비동기식 : 해야 할 일을 위임하고 기다리는 방식으로 ajax를 이용하여 구현 할 수 있는데 페이지 이동없이 고정된 화면에서 어떠한 처리가 이뤄지는 것을 말한다

---
## Reference

- <https://blog.naver.com/vnemftnsska2/221428722368>