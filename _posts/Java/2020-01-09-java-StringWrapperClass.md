---
title: "JAVA, String Wrapper class"
date: 2020-01-09 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## String 클래스

### String클래스 선언하기
  - String str1 = new String("abc"); //인스턴스로 생성됨, 힙메모리에 생성
  - String str2 = "abc"; // 상수풀에 있는 문자열을 가르킴, 상수풀에 있는 문자열은 공유한다

  ![strig](https://user-images.githubusercontent.com/55946791/72039283-cb6d6600-32e7-11ea-8976-1ae81704135a.JPG)

- 예제코드

```java
String s1 = new String("abc");
String s2 = new String("abc");
System.out.println(s1==s2); // 메모리의 주소가 다르므로 false

String s3 = "abc";
String s4 = "abc";
System.out.println(s3==s4); // 상수풀에 있는것을 공유하므로 true
```

### String은 immutable
  - String 클래스의 concat() or + 를 이용하여 String을 연결하면 <u>문자열은 새로 생성</u> 된다.
  - 원래 s1과 수정된 s1의 메모리 주소값다르다!

```java
String s1 = "abc";
String s2 = "def";
System.out.println(s1.hashCode());	//96354

s1 = s1.concat(s2);
System.out.println(s1.hashCode());	//-1424385949 -> s1은 다시 생성된 string을 가르킨다
```
  - 메모리가 낭비 되므로 이를 해결하기 위해서는 즉, <u>String을 계속 연결해서 사용</u>할 일이 있다면 <b>StringBuilder & StringBuffer</b>을 사용하자

### StringBuffer & StringBuilder
- 가변적인 char[]배열을 멤버변수로 가지고 있는 클래스
- 문자열을 변경하거나 연결하는 경우 사용하면 편리
<br>
- <b>StringBuffer는 멀티 쓰레드프로그래밍에서 동기화</b>가 보장된다
- 단일 쓰레드프로그래밍에서는 StringBuilder를 사용하는 것이 더 좋다
<br>
- toString()으로 String으로 변경

### Wrapper 클래스
- 기본 자료형에 대한 클래스
- ex) boolean(기본형) -> Boolean(Wrapper클래스)


---
## Reference
- fastcampus
