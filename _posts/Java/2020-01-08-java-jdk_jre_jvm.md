---
title: "JAVA, SE,JDK,JRE,JVM"
date: 2020-01-08 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Java SE(Java Platform, Standard Edition)
- 자바의 표준안이며 어떤 문법적인 구성을 가졌는지와 같은 것들을 정의하고있다
- 구체적인 s/w가 아니며 <b>설계도</b>라고 할 수 있다. 이 명세서에 따라서 Java가 만들어지게 된다
- 최신; 13버전

### JDK(Java Development Kit)
- Java SE의 표준안에 따라서 만들어진 <b>구체적인 s/w</b>이다
- Java코드를 컴파일하는 컴파일러, 개발에 필요한 각종 도구, JRE가 포함
- 즉, <b>개발자를 위한</b> 자바 버전

### JRE(Java Runtime Environment)
- 자바가 실제로 동작하는데 필요한 JVM, 라이브러리, 각종 파일들이 포함
- 자바로 만들어진 프로그램을 구동하려면 이것을 설치한다
- <b>일반인을 위한</b> 자바 버전

### JDK & JRE
| JDK | JRE |
|--|--|
|자바개발도구 | 자바실행환경|
|JRE+개발에 필요한 실행파일 | JVM+클래스라이브러리|


---

### JVM(Java Virtual Machine)
- 자바가 실제로 구동하는 환경
- h/w나 o.s에 따라 달라질 수 있는 호환성의 문제를 JVM이 해결한다
- 컴퓨터를 사용해서 자바를 실행하기 위한 <b>가상 컴퓨터</b>

![JAVA 실행환경](https://user-images.githubusercontent.com/55946791/71958042-a5d25500-3232-11ea-804e-c5ae5af98f1e.jpg)



---
## Reference
- <https://devbox.tistory.com/entry/%EC%8B%A4%ED%96%89>
