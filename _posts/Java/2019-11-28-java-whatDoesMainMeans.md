---
title: "JAVA, public static void main(String args[]) 의미"
date: 2019-11-28 20:30:28 -0400
categories: JAVA
tags : [JAVA, interview]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### public static void main(String args[])의미

### 1. public
- 모든 클래스에서 접근가능하다

#### 접근제어자
- public > protected > default > private
|종류| 클래스 | 하위클래스 | 동일패키지 | 모든 클래스
|---|:---:|:---:|:---:|:---:|
|private | o | x | x | x
|(default) | o | x | o| x
|protected | o | o | o | x
|public| o | o | o | o

### 2. static
- 정적 함수이다
- static으로 선언 되었기 때문에 해당 객체는 <u>자바가 컴파일 되는 순간 정의 되고 프로그램이 끝나고 메모리가 해제될때 소멸</u>된다

### 3. void
- 함수의 끝에 리턴되는 값이 없다

### 4. String args[]
- String형 배열을 매개변수로 받아온다
- 맨 처음 프로그램을 실행하는 데 있어 외부에서 값을 받아오기 위해서 사용하는 것이다.
- ex) java Example01.class 100 200 으로 시작한다면 args[0] = 100, args[1] = 200이 저장되어 프로그램이 실행된다.ㄴ

---
## Reference
- <https://m.blog.naver.com/crazydeicide/130114957734>
- <https://javacpro.tistory.com/11>
