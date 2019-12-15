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

|인터페이스|특징
|--|--|
|List| <b>순서가 있는</b> 데이터의 집합, <b>데이터 중복</b>을 허용한다. <br>예) 대기자 명단 <br>구현클래스 : ArrayList, LinkedList, Stack, Vector등
|Set| <b>순서를 유지하지 않는</b> 데이터의 집합. <b>데이터의 중복을 허용하지 않는다</b> <br>예) 양의 정수 집합, 소수의 집합 <br>구현클래스 : HashSet, TreeSet
|Map|<b>key와 value의 쌍</b>으로 이러우진 데이터의 집합. <b>순서 유지 x, 키 중복 x, 값 중복 o</b> <br>예) 우편번호, 지역번호(전화번호) <br>구현 클래스 : HashMap, TreeMap, Hashtable, Properties등

#### Collection 인터페이스
- List와 Set의 조상인 Collection 인터페이스에는 컬렉션을 다루는데 가장 기본적인 메서드를 정의하고 있다

#### List 인터페이스
- 중복 허용, 저장순서 유지 되는 컬렉션을 구현하는데 사용된다
![List의 상속계층도](https://user-images.githubusercontent.com/55946791/70857792-703e9280-1f38-11ea-9e01-25c8fd0e41a6.jpg)

#### Set 인터페이스
- 중복 x, 저장순서 유지 x
![set의 상속계층도](https://user-images.githubusercontent.com/55946791/70857797-abd95c80-1f38-11ea-8fe1-50dd0e8adca3.jpg)

#### Map 인터페이스
- 키 중복x, 값 중복 허용
![MAP의 상속계층도](https://user-images.githubusercontent.com/55946791/70857811-ef33cb00-1f38-11ea-827e-1a5a9ffd64b7.jpg)

---
### 1.2 ArrayList
- 저장순서 유지, 중복을 허용한다
- 배열에 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장된다.
- 모든 종류의 객체를 담을 수 있다
- <u>데이터를 읽고 저장하는데는 효율이 좋다</u>
- <u>용량을 변경해야할 때는 효율이 떨어진다</u> , 새로운 배열을 생성하여 기존의 배열 데이터를 복사해야 하기때문에.


### 1.3 LinkedList
- <b>배열의 특징</b>
  - 접근시간이 빠르다
  - 크기를 변경할수 없다, 배열 중간에 데이터를 추가/삭제하는데 시간이 많이 걸린다
- 배열의 단점을 극복하려고 나온것이 LinkedList이다
- <u>불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다</u>
- <u>단점 : 이동방향이 단방향이기 때문에 다음 요소에 대한 접근은 쉽지만 이전에 대한 접근은 어렵다.</u> (더블 링크드 리스트로 단점 해결)
- 실제로 LinkedList클래스는 이름과 달리 '더블 링크드 리스트'로 구현이 되어 있는데, 이는 링크드 리스트의 단점인 낮은 접근성을 높이기 위한것이다.

### ArrayList vs LinkedList
- 순차적으로 추가/삭제 하는 경우 : ArrayList 가 빠르다
- 중간 데이터를 추가/삭제 하는 경우 : LinkedList가 빠르다



---
## Reference
- 자바의 정석(남궁성)
