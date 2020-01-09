---
title: "JAVA, 람다식"
date: 2020-01-09 13:50:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 람다식 (JAVA8 ~)
- 자바에서 함수형 프로그래밍을 구현하는 방식
- 함수형 프로그래밍이란
  - 외부 변수를 사용하지 않는다
  - 그렇기때문에 외부에 다른 영향을 주지 않는다. 따라서 병렬처리가 가능해진다
- 클래스를 생성하지 않고 함수의 호출만
<br>
- 함수를 변수처럼 사용하는 람다식

```java

interface PrintString{
	void showString(String str);
}

public class TestLambda {

	public static void main(String[] args) {
		PrintString lambdaStr = s->System.out.println(s);
		lambdaStr.showString("hi");

		showMyString(lambdaStr);

		// 구현부가 대입된다
		PrintString test = returnString();
		test.showString("hi3");
	}

	// 매개변수로 활용되었고, 바로 구현된것이 실행된다
	public static void showMyString(PrintString p) {
		p.showString("hi2");
	}

	// 함수의 구현부가 마치 변수 처럼 반환될수있다
	public static PrintString returnString() {
		return s->System.out.println(s+"!!!");
	}
}
```

<br>

- 예제

```java
package LambdaPart;

public class StringConcatTests {
	public static void main(String[] args) {
		StringConImpl impl = new StringConImpl();
		impl.makeString("ab", "cd");

		StringConcat concat = (s,v) -> System.out.println("[lambda] : "+s+v);
		concat.makeString("ab", "cd");
	}
}
/*
결과
[original] : abcd
[lambda] : abcd
*/
```

```java
package LambdaPart;

//함수형 인터페이스라고 지정
@FunctionalInterface
public interface StringConcat {
	// 함수형 인터페이스는 ★함수 하나만★ 선언
	public void makeString(String s1,String s2);
}
```

```java
package LambdaPart;

public class StringConImpl implements StringConcat {

	@Override
	public void makeString(String s1, String s2) {
		System.out.println("[original] : "+ s1 +s2);
	}
}
```


---
## Reference
- fastcampus
