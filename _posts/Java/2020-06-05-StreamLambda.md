---
title: "JAVA, Stream, Lambda"
date: 2020-06-05 13:40:28 -0400
categories: JAVA
tags : [JAVA, Stream, Lambda]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## Stream (java.util)
- __Collection의 요소를 하나씩 참조하여 Lambda식으로 처리할 수 있게 해주는 일종의 반복자__

> Input/Output Stream (java.io)  

```
- 스트림
: 프로그램(파일, n/w 등)과 I/O객체를 연결하여 데이터를 송수신 하는 길
: InputStream : data를 읽어 들이는 객체, OutputStream : data를 써서 보내는 객체

바이트 스트림 : binary data 입출력 , 이미지 동영상 송수신에 사용
문자스트림 : text data 입출력하는 스트림 , html text파일 송수신 사용

직렬화/역직렬화 : 객체 <-> 데이터 스트림
```

### 예제

```java
List<String> names = Arrays.asList("hyemi", "haen", "minjun");

// 일반 방식
int count = 0;
for (String name : names) {
  if (name.contains("h"))
    count++;
}
System.out.println("count : " + count);

// 스트림 이용
count = 0;
count = (int) names.stream().filter(x -> x.contains("h")).count();
System.out.println("count (stream) : " + count);

// 차례로 실행된다
System.out.println(names.stream().filter(el -> {
		System.out.println("call filter...");
		return el.contains("h");
}).map(el -> {
	  System.out.println("call map...");
	  return el.toUpperCase();
}).findFirst());
// 결과 : Optional[HYEMI]
```

## Stream 사용법
- __Collections같은 객체 집합.스트림생성().중개연산().최종연산();__
- names.stream().filter(x -> x.contains("h")).count();
- "."으로 연계할 수 있게 하는 방법 : 파이프라인

## 중개연산
- Filter, Peek, Sorted, Limit, Distinct, Skip, map, mapToint, mapToLong, mapToDouble

### Filter
- 조건으로 거른다.
- names.stream().filter(x -> x.contains("h")).count();

### limit
- ages.stream().filter(x -> x > 3).limit(4).forEach(x -> System.out.println(x));

### map
- 특정 조건을 적용해서 변환

```java
	names.stream().map(n -> n.toUpperCase())
					  .forEach(n-> System.out.println(n));
```		

## 최종연산
- count(), min(), max(). sum(), average(), forEach, iterator...
- reduce()

  ```java
  List<Integer> ages = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
  System.out.println(ages.stream().reduce((b, c) -> b + c).get());  // 55
  ```

---

## Lambda
- __메소드를 하나의 식으로 표현한것__
- 익명메소드 생성 문법(이름과 반환값이 없어지기 때문)
- 메소드를 지칭하는 명칭없이 구현부만 선언

## Lambda 사용이유
- interface가 가지고 있는 method를 __간편,즉흥적으로 구현해서__ 사용하는 것이 목적

### 람다의 기본식

```
람다의 기본식 : (매개변수) -> {실행문}
```

- 람다식을 사용하기 위해서는 구현할 __인터페이스가 필요하다.__ (함수형 인터페이스)
- 람다식으로 구현하기 위한 인터페이스에는 __한개의 추상메소드만 가지고 있어야 한다__
- 이런 인터페이스를 미리 함수적 인터페이스 라고 부른다.

### 예시

```java
interface Calculator {
	int plusOne(int n);
}

public static void main(String[] args) {

	// 익명클래스
	Calculator calc = new Calculator() {

		@Override
		public int plusOne(int n) {
			return n + 1;
		}
	};

	System.out.println(calc.plusOne(3));

	// 람다식
	Calculator calc2 = (num1) -> {
		return num1 + 1;
	};
	System.out.println(calc2.plusOne(4));
}
```

### 예시2

```java
@FuntionalInterface
interface Calculator {
  int calc(int n);
}

class Driver {
  public static void main(String[] args) {
    int n = 2;

    // int n과 구별하기 위해 람다식에는 v라는 변수명을 사용.
    printCalc(n, v -> v + 1); // n + 1, 출력값 3
    printCalc(n, v -> v - 1); // n - 1, 출력값 1
    printCalc(n, v -> v * 2); // n * 2, 출력값 4
  }

  public static void printCalc(int n, Calculator cal) {
    System.out.println(cal.calc(n));
  }
}
```

---
## 참고

- [Java Stream](https://www.evernote.com/shard/s334/client/snv?noteGuid=d20aa8ef-53ab-4c6a-a67f-f143affce66f&noteKey=856dd29f14f79399c8b93eac4c20904f&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs334%2Fsh%2Fd20aa8ef-53ab-4c6a-a67f-f143affce66f%2F856dd29f14f79399c8b93eac4c20904f&title=Java%2BStream)
- <https://juyoung-1008.tistory.com/48>
- [예제로 배워보는 Stream & Lambda](https://sehun-kim.github.io/sehun/java-lambda-stream/#1)
