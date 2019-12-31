---
title: "JAVA, Collections Framework"
date: 2019-12-15 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념, CollectionsFramework]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
# 1.컬렉션 프레임웍
- Collection : 데이터 그룹
- Framework : 표준화된 프로그래밍 방식
- JDK1.2부터 다양한 종류의 컬렉션 클래스가 추가되고 <u>모든 컬렉션 클래스를 표준화된 방식으로 다룰</u> 수 있도록 체계화되었다.

![collection](https://user-images.githubusercontent.com/55946791/71610408-1abee280-2bd4-11ea-8a3a-fea2d9bfd4bf.jpg)

## 1.1 컬렉션 프레임웍의 핵심 인터페이스
![컬렉션 프레임워크 핵심 인터페이스 상속계층도](https://user-images.githubusercontent.com/55946791/70857702-04a7f580-1f37-11ea-8273-437fb72f97ce.jpg)
- 인터페이스 List와 Set을 구현한 컬렉션 클래스들은 서로 많은 공통부분이 있어서 공통부분을 뽑아 Collection인터페이스를 정의 할 수있었다.
- 컬렉션 프레임웍의 핵심 인터페이스와 특징

|인터페이스|특징| 구현 클래스
|--|--|--|
|List| <b>순서가 있는</b> 데이터의 집합, <b>데이터 중복</b>을 허용한다. <br>예) 대기자 명단| ArrayList, Vector, LinkedList, Stack
|Set| <b>순서를 유지하지 않는</b> 데이터의 집합. <b>데이터의 중복을 허용하지 않는다</b> <br>예) 양의 정수 집합, 소수의 집합 |HashSet, TreeSet
|Map|<b>key와 value의 쌍</b>으로 이러우진 데이터의 집합. <b>순서 유지 x, 키 중복 x, 값 중복 o</b> <br>예) 우편번호, 지역번호(전화번호) | HashMap, TreeMap, Hashtable, Properties

### Collection 인터페이스
- List와 Set의 조상인 Collection 인터페이스에는 컬렉션을 다루는데 가장 기본적인 메서드를 정의하고 있다

### List 인터페이스
- 중복 허용, 저장순서 유지 되는 컬렉션을 구현하는데 사용된다
![List의 상속계층도](https://user-images.githubusercontent.com/55946791/70857792-703e9280-1f38-11ea-9e01-25c8fd0e41a6.jpg)

### Set 인터페이스
- 중복 x, 저장순서 유지 x
![set의 상속계층도](https://user-images.githubusercontent.com/55946791/70857797-abd95c80-1f38-11ea-8fe1-50dd0e8adca3.jpg)

### Map 인터페이스
- 키 중복x, 값 중복 허용
![MAP의 상속계층도](https://user-images.githubusercontent.com/55946791/70857811-ef33cb00-1f38-11ea-827e-1a5a9ffd64b7.jpg)

---
## 1.2 ArrayList
- 저장순서 유지, 중복을 허용한다
- 배열에 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장된다.
- 모든 종류의 객체를 담을 수 있다
- <u>데이터를 읽고 저장하는데는 효율이 좋다</u>
- <u>용량을 변경해야할 때는 효율이 떨어진다</u> , 새로운 배열을 생성하여 기존의 배열 데이터를 복사해야 하기때문에.


## 1.3 LinkedList
- <b>배열의 특징</b>
  - 접근시간이 빠르다
  - 크기를 변경할수 없다, 배열 중간에 데이터를 추가/삭제하는데 시간이 많이 걸린다
- 배열의 단점을 극복하려고 나온것이 LinkedList이다
- <u>불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다</u>
- <u>단점 : 이동방향이 단방향이기 때문에 다음 요소에 대한 접근은 쉽지만 이전에 대한 접근은 어렵다.</u> (더블 링크드 리스트로 단점 해결)
- 실제로 LinkedList클래스는 이름과 달리 '더블 링크드 리스트'로 구현이 되어 있는데, 이는 링크드 리스트의 단점인 낮은 접근성을 높이기 위한것이다.
- 큐, 양방향 큐, 스택 만들때 사용

## ArrayList vs Vector
- Vector : 데이터에 동시 접속이 발생했을때 처리할 수 있다 (ArrayList의 구형버전, 잘 안쓰임)

## ArrayList vs LinkedList
- 순차적으로 추가/삭제 하는 경우 : ArrayList 가 빠르다
- 중간 데이터를 추가/삭제 하는 경우 : LinkedList가 빠르다

|컬렉션| 읽기(접근시간) | 추가/삭제 | 비고
|--|--|--|--|
|ArrayList | 빠르다 | 느리다 | 순차적인 추가삭제는 더 빠르다. <br>비효율적인 메모리 사용
|LinkedList| 느리다 | 빠르다 | 데이터가 많을수록 접근성이 떨어진다

---
## 1.4 Stack 과 Queue
- stack : <u>순차적으로 데이터를 추가/삭제하므로 ArrayList</u>와 같은 배열 기반의 컬렉션 클래스가 적합하다
- queue : 배열기반의 컬렉션 클래스 x ; 첫번째 데이터를 삭제하므로 빈공간을 채우기 위한 데이터 복사 때문에 비효율적이다. => 데이터의 <u>추가/삭제가 쉬운 LinkedList로 구현</u>하는것이 더 적합하다  

### PriorityQueue
- <u>저장한 순서에 관계없이 우선순위(priority)가 높은 것부터</u> 꺼내게 된다
- <u>null은 저장할 수 없다</u>
- 저장공잔으로 <u>배열</u>을 사용하며, 각 <u>요소를 힙(heap)이라는 자료구조의 형태로 저장</u>한다
- 힙 : 이진 트리의 한 종류로 가장 큰 값이나 가장 작은 값을 빠르게 찾을 수 있다

### Deque(Double-Ended Queue)
- Queue의 변형으로, 양쪽 긑에 추가/삭제가 가능하다

---
## 1.5 Iterator, ListIterator, Enumeration
- 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스
- <b>Iterator를 이용해서 컬렉션의 요소를 읽어오는 방법을 <u>표준화 함으로써 코드의 일관성을 유지하여 재사용성을 극대화</u> 한다.</b>


### Iterator
- 컬렉션 프레임워크에서는 <u>컬렉션에 저장된 요소들을 읽어오는 방법을 표준화</u>하였다.
- 인터페이스

```java
pulic iterface Iterator {
  boolean hasNext();  // 읽어올 요소가 남아있는지?
  Object next();  // 다음 요소 읽어오기
  void remove();  // next()로 읽어온 요소를 삭제
}
public interface Collection {
  ...
  public Iterator Iterator();
  ...
}
```

- 사용예시

```java
List list = new ArrayList();
Iterator it = list.iterator();

while(it.hasNext()){
  System.out.println(it.next());
}

Map map = new HashMap();
...
Iterator it = map.keySet().iterator();
```

### Enumeration
:  Iterator의 구버전

### ListIterator
:  Iterator에 <u>양방향 조회기능추가</u> (List를 구현한 경우만 사용가능)
- Iterator는 단방향으로만 이동하기 때문에 컬렉션의 마지막 요소에 다다르면 더이상 사용x
- ListIterator는 양방향으로 이동하기 때문에 요소간의 이도잉 자유롭다. <u>hasNext()나 hasPrevious()</u>를 호출해서 이동 할 수 있는지 확인해야 한다.

---
## SET
: 집합을 정의 하며 요소의 중복을 허용하지 않는다.

### HashSet
- 가장 빠른 임의 접근속도
- 순서를 예측할 수 없다

### LinkedHashSet
- 추가된 순서, 또는 가장 최근에 접근한 순서대로 접근 가능

### TreeSet
- 정렬된 순서대로 보관하며 정렬 방법을 지정할 수 있다

---

## MAP
:key,value 의 쌍으로 연관지어 저장, 순서없음

### HashMap
- 중복x 순서x
- key,value null허용o
- 멀테쓰레드에서 사용x, 멀티쓰레드에서는 HashTable을 쓴다

### HashTable
- HashMap보다 느리지만, 동기화 지원
- key,value null허용x
- 멀티쓰레드에서 사용

### TreeMap
- 이진검색트리 형태로 key,value쌍으로 이루어짐
- 정렬된 순서로 저장(오름차순, 저장시간 다소 길다)하므로 빠른 검색
- <b>key를 기준으로 정렬할 경우 유용</b>, 정렬기준 : 숫자> 대문자 > 소문자 > 한글

### LinkedHashMap
- HashMap과 유사
- Map에 있는 엔트리들의 연결 리스트를 유지하므로 입력한 순서대로 반복 가능

---
## Reference
- 자바의 정석(남궁성)
- <https://hackersstudy.tistory.com/26>
