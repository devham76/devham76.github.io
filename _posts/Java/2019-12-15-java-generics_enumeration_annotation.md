---
title: "JAVA, generics, enumeration(열거형), annotaion"
date: 2019-12-15 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념, generics]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
# 1. 지네릭스(Generics)

## 1.1 지네릭스란?
- <b>다양한 타입의 객체를 다루는 메서드나 클래스에 컴파일 시의 타입체크를 해주는 기능</b>
- 장점
  1. 객체의 타입 안정성을 높이고
  2. 형변환의 번거로움을 줄여준다
- 객체 타입을 미리 명시해줘서 번거로운 형변환을 줄여준다 !!

## 1.2 지네릭 클래스의 선언
```java
// 전
class Box{
  Object item;
  void setItem(Object item) {this.item = item;}
  Objecct getItem() { return item; }
}
// 후
// 클래스 옆에 <T>, Object를 T로 변경
class Box<T>{
  T item;
  void setItem(T item) {this.item = item;}
  T getItem() { return item; }
}
```
- 클래스 옆에 <T>, Object를 T로 변경
- 상황에 맞게 의미있는 문자를 선택해서 사용한다.
- 기호의 종류만 다를 뿐 <b>임의의 참조형 타입을 의미한다</b>
- 타입 T대신 String타입을 지정한다면
```java
// 전
Box<String> b = new Box<String>();
class Box{
  String item;
  void setItem(String item) {this.item = item;}
  String getItem() { return item; }
}
```

### 지네릭스의 용어
- class Box<T>
  - Box<T> : 지네릭스 클래스 T Box 라고 읽는다
  - T : 타입변수 또틑 타입 매개변수
  - Box : 원시타입 (row type)
- <b>컴파일 시의 타입체크</b>하고 <b>컴파일 후에 지네릭 타입이 제거</b>된다 즉, 컴파일 후에  Box<String>과 Box<Integer>는 이들의 원시타입인 Box로 바뀐다.

### 지네릭스의 제한
1. static멤버에 타입 변수 T를 사용할 수 없다
  - 대입된 타입의 종류에 관계없이 동일한 것이어야 하기 때문이다.
2. 지네릭 배열을 생성 할 수 없다
  - T[] tmpArr = new T[itemArr.length]; (x)
  - new 연산자 때문인데, 컴파일 시점에 타입 T가 뭔지 정확하게 ㅇ알아야 한다
  - 그런데 컴파일 시점에는 T가 어떤 타입이 될지 알 수 없기 때문에 불가능 하다.

---
## Reference
- 자바의 정석(남궁성)
