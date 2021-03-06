---
title: "JAVA, 변수유형"
date: 2019-10-22 20:30:28 -0400
categories: JAVA
tags : [JAVA]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### static
- <b>여러 개의 인스턴스가 같은 메모리의 값을 공유하기 위해 사용한다</b>
- 프로그램이 메모리에 load될때 데이터 영역의 메모리에 생성된다
---> <b>인스턴스의 생성과 관계없이 클래스 이름으로 직접 참조</b> 한다
- <b>클래스 변수</b> 라고도 한다

### 메모리
![memory](https://user-images.githubusercontent.com/55946791/67284805-43aa6380-f511-11e9-99fa-97b7d53f32fc.JPG)

|변수유형| 선언위치 | 사용범위 | 메모리 | 생성과 소멸
|---|:---:|:---:|:---:|:---:|
|지역변수(로컬변수) | 함수 내부에 선언| 함수 내부에서만 사용 | 스택 | 함수가 호출될 때 생성되고 함수가 끝나면 소멸함
| 멤버변수(인스턴스 변수)| 클래스 멤버 변수로 선언 | 클래스 내부에서 사용하고 private이 아니면 참조 변수로 다른 클래스에서 사용 가능 | 힙 | 인스턴스가 생성될 때 힙에 생성되고, 가비지 컬렉터가 메모리를 수거할 때 소멸됨
static변수(클래스 변수) | static 예약어를 사용하면 클래스 내부에 선언 | 클래스 내부에서 사용하고 private이 아니면 클래스 이름으로 다른 클래스에서 사용 가능 | 데이터 영역 | 프로그램이 처음 시작할 때 상수와 함께 데이터 영역에 생성되고 프로그램이 끝나고 메모리를 해제할 때 소멸됨

---
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
