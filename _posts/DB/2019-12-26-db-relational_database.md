---
title: "DATABASE, 관계형 데이터베이스(relational database)"
date: 2019-12-26 15:30:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 관계형 데이터베이스란
- table로 이루어져 있으며, 이 table은 key와 value의 관계를 나타낸다
- 이처럼 데이터의 종속성을 관계로 표현하는 것이 데이터베이스의 특징이다
- 관계형 데이터베이스의 table 구성
![img_mysql_table](https://user-images.githubusercontent.com/55946791/71457747-cfc35a80-27e2-11ea-8b3c-2d5c0028e106.png)

- <b>관계형 데이터베이스는 위와 같이 구성된 다른 테이블가 관계를 맺고 모여있는 집합체로 이해할 수 있다</b>

## 관계형 데이터베이스 용어
1. 열(column)
- 각각의 열은 유일한 이름을 가지고 있고 자시만의 타입을 가지고 있다
- field 또는 attribute(속성)이라고도 불린다

2. 행(row)
- 관계된 데이터의 묶음을 의미한다
- 한 테이블의 모든 행은 같은 수의 열을 가지고 있다
- 행은 tuple 또는 record라고도 불린다

3. 값(value)
- 테이블은 각각의 행과 열에 대응하는 값을 가지고 있다
- 이러한 값은 열의 타입에 맞는 값이어야 한다

4. 키(key)
- 테이블에서 행의 식별자로 이용되는 열을 key 또는 primary key(기본 키)라고 한다

5. 관계(relationship)
- 테이블 간의 관계는 관계를 맺는 테이블의 수에 따라 다음과 같이 나눌 수 있다
  - 일대일 관계
  - 일대다 관계
  - 다대다 관계
- 이러한 관계를 나타내기 위해 foreign key(외래키)라는 것을 사용한다
- 외래키는 한 테이블의 키 중에서 다른 테이블의 행을 식별할 수 있는 키를 의미한다

6. 스키마(schema)
- 스키마는 테이블을 디자인하기 위한 청사진이라고 할 수 있다
- 이러한 스키마는 각 열에 대한 항목,타입 , 기본키, 외래키를 나타내야 한다
- 문법
  - Reservation(ID, Name, Date, RoomNum)
- 개체-관계 다이어그램
  - ![img_mysql_diagram](https://user-images.githubusercontent.com/55946791/71458376-d901f680-27e5-11ea-8b40-945f21e46bc7.png)




---
## Reference
- <http://tcpschool.com/mysql/mysql_intro_relationalDB>
