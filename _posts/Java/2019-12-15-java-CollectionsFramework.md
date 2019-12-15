---
title: "JAVA, Collections Framework"
date: 2019-12-15 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념, CollectionsFramework]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 1.컬렉션 프레임웍
- Collection : 데이터 그룹
- Framework : 표준화된 프로그래밍 방식
- JDK1.2부터 다양한 종류의 컬렉션 클래스가 추가되고 모든 컬렉션 클래스를 표준화된 방식으로 다룰 수 있도록 체계화되었다.

### 1.1 컬렉션 프레임웍의 핵심 인터페이스
![컬렉션 프레임워크 핵심 인터페이스 상속계층도](https://user-images.githubusercontent.com/55946791/70857702-04a7f580-1f37-11ea-8273-437fb72f97ce.jpg)
- 인터페이스 List와 Set을 구현한 컬렉션 클래스들은 서로 많은 공통부분이 있어서 공통부분을 뽑아 Collection인터페이스를 정의 할 수있었다.
- 컬렉션 프레임웍의 핵심 인터페이스와 특징
|--|--|
|인터페이스|특징
|List| <b>순서가 있는</b> 데이터의 집합, <b>데이터 중복</b>을 허용한다.
<br>예) 대기자 명단
<br>구현클래스 : ArrayList, LinkedList, Stack, Vector등
|Set| <b>순서를 유지하지 않는</b> 데이터의 집합. <b>데이터의 중복을 허용하지 않는다</b>
<br>예) 양의 정수 집합, 소수의 집합
<br>구현클래스 : HashSet, TreeSet
|Map|<b>key와 value의 쌍</b>으로 이러우진 데이터의 집합. <b>순서 유지 x, 키 중복 x, 값 중복 o</b>
<br>예) 우편번호, 지역번호(전화번호)
<br>구현 클래스 : HashMap, TreeMap, Hashtable, Properties등 


---
## Reference
- 자바의 정석(남궁성)
