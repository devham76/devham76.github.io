---
title: "JAVA, StringBuilder"
date: 2019-11-08 20:30:28 -0400
categories: JAVA
tags : [JAVA, StringBuilder]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### StringBuilder를 사용하는 이유
#### String
- String객체를 서로 더하는 행위는 메모리 할당과 해제를 발생시키며 더하는 연산이 많아진다. 즉 성능적으로 좋지 않다
```java
String str1 = "ab"
String str2 = "cd"
System.out.println(str1 + str2);
// 새로운 String을 생성한다.
```
#### StringBuilder
- StringBuilder는 String과 문자열을 더할 때 <u>새로운 객체를 생성하는 것이 아니라, 기존의 데이터를 더하는 방식</u>을 사용한다
- <u>속도가 빠르고 상대적으로 부하가 적다</u>
- <u>긴 문자열을 더하는 상황</u>이 발생하면, StringBuilder를 적극적으로 사용하자

```java
StringBuilder sb = new StringBuilder();
sb.append("ab");
sb.append("cd");
System.out.println(sb.toString);
```


---
## Reference
<https://hardlearner.tistory.com/288>
