---
title: "JAVA, 인터페이스"
date: 2019-10-22 20:20:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 인터페이스 (interface)
- iterface implements
- <b>모든 메서드가 추상 메서드</b>로 이루어진 클래스
- 설계용으로 사용한다
- 형식적인 선언만 있고 구현은 없다
```java
interface 인터페이스 이름{
	// 인터페이스에 선언된 모든 변수는 public static final로 상수
	public static final float PI = 3.14f;
	// 인터페이스에 선언된 모든 메서드는 public abstract로 추상 메서드
	public void add();
}
```
- 목적
	- 함수의 껍데기만 있는 인터페이스의 함수를 <b>강제로 구현</b>하게 한다
	- 해당 인터페이스를 구현한 객체들에 대해서 <b>동일한 동작</b>을 보장한다
- 다중 상속 가능

---

# ★질문★ ) 인터페이스와 추상클래스의 차이점을 외관, 목적, 특징에 따라 설명해주세요

## 인터페이스
- 외관
	- interface , implements
	- 모든 메서드가 추상 메서드
- 목적
	- 함수의 껍데기만 있는 인터페이스의 함수를 <b>강제로 구현</b>하게 한다
	- 해당 인터페이스를 구현한 객체들에 대해서 <b>동일한 동작</b>을 보장한다
- 특징
	- 다중 구현 가능
## 추상클래스
- 외관
	- class extends
	- 추상메서드(구현코드가 없는 메서드)를 포함한 클래스
- 목적
	- 추상 클래스를 상속받아 기능을 <b>이용하거나 확장</b>시킨다
	- 상속 받은 클래스가 자신의 기능에 맞게 메서드를 재구현 한다 (책임 위임)
- 특징
	- <b>다중 상속 불가능</b> (다중 상속의 모호성)
	- car와 plane 두 클래스 모두 drive()메서드를 가지고 있다면 어떤걸 실행해야 될지 모호해진다.

	```java
	class MyVehicle extends car, 	plane{
		@Override
		public void goTo(){
			super.drive();
		}
	}
	```

	- <b>interface는 다중 구현</b>이 된다 (구현되어있지 않은 추상메서드만 있다)

	```java
	class car implements vehicle,engine{
		@Override
		public void drive(){
			@doSomething
		}
	}
	```

---

### 인터페이스의 요소
- <u>추상 메서드</u>
- <u>상수</u> (인터페이스에서 선언한 변수는 컴파일 과정에서 상수로 변환된다)
- 중복 구현을 막기위해 제공된다
	- <u>디폴트 메서드</u> (java8) : 기본 구현을 가지는 메서드, 구현하는 클래스에서 재정의 가능 / 인터페이스를 다중으로 구현했을때, 디폴트 메서드의 이름이 중복 되는 경우에는 재정의 한다
	- <u>정적 메서드</u> (java8) : 인스턴스 생성과 상관없이 인터페이스 타입으로 호출하는 메서드
	- <u>private 메서드</u>(java9) : 인터페이스 내에서만 사용하기 위해 구현한 메서드. 구현하는 클래스에서 재정의, 사용 x

### 인터페이스 상속
- 인터페이스 간에도 상속이 가능하다
- 구현이 없으므로 extends 뒤에 여러 인터페이스를 상속 받을 수 있다

### 인터페이스와 stratey Pattern
- 인터페이스를 활용하면 다양한 정책이나 알고리즘을 프로그램의 큰 수정 없이 적용/확장할 수 있다.
 - 예 ) sorting <- bubble sort, quick sort, heap sort / sorting이라는 인터페이스를 세가지 클래스가 구현되어있을때 또다른 sort클래스를 쉽게 추가하여 확장할수있다

---

### 인터페이스 구현과 형변환
- 인터페이스를 구현한 클래스는 <u>인터페이스 형으로 선언한 변수로 형 변환 할 수 있다</u>
- 형 변환시 사용할 수 있는 메서드는 인터페이스에 선언된 메서드만 사용할 수 있다
- 상속에서의 형 변환과 동일한 의미
	- Calc calc = new Caculator();
	- <u>Calc에서 선언된 메서드만 사용 가능</u>

- 단 클래스 상속과 달리 구현한 코드가없기 때문에 <u>여러 인터페이스를 구현 할 수 있다</u>
	- public class CompleteCalc extends Calculator implements Calc, Runnable
	- implements뒤에 여러 인터페이스가 올 수 있다

##### Calc 인터페이스
```java
package interfaceex;

public interface Calc {

	double PI = 3.14;
	// 앞에 선언된게 없지만 기본적으로 상수로 선언이 된다.
	// public static final double PI = 3.14;
	int ERROR = -99999999;

	int add(int num1, int num2);
	int substract(int num1, int num2);
	int times(int num1, int num2);
	int divide(int num1, int num2);
}
```

##### Calculator 추상메서드
```java
package interfaceex;

public abstract class Calculator implements Calc {
	// 인터페이스의 추상 메서드를 모두 구현하지 않으면
	// 추상메서드를 가지고 있기 때문에 추상클래스가 된다
	@Override
	public int add(int num1, int num2) {
		return num1 + num2;
	}

	@Override
	public int substract(int num1, int num2) {
		return num1 - num2;
	}
}
```

##### ComplateCalc 클래스
```java
package interfaceex;

public class ComplateCalc extends Calculator{

	@Override
	public int times(int num1, int num2) {
		return num1 * num2;
	}

	@Override
	public int divide(int num1, int num2) {
		if (num2 != 0)
			return num1 / num2;
		return ERROR;
	}
	public void showInfo() {
		System.out.println("Calc 인터페이스를 구현하였습니다.");
	}
}
```

##### CalculatorTest 실행 클래스
```java
package interfaceex;

public class CalculatorTest {

	public static void main(String[] args) {
		// Calc 클래스에 코드가 없는데 뭘 상속 받은거야?
		// 인터페이스를 implements 한것도 상속할 수 있다
		int num1 = 10;
		int num2 = 20;

		Calc calc =  new Calculator();
		System.out.println(calc.add(num1, num2));

		//Calc calc1 = new Cassslc();	// interface는 구현 안됨
		//Calc calc2 = new ComplateCalc();	// 추상 클래스는 구현 안됨

		ComplateCalc calc3 = new ComplateCalc();
		calc3.showInfo();
	}
}
```

---



---
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
