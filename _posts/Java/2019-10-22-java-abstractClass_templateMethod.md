---
title: "JAVA, 추상 클래스&템플릿 메서드"
date: 2019-10-22 15:20:28 -0400
categories: JAVA
tags : [JAVA,java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
--- 

### 추상 클래스란 ? (abstract class)
- 추상 메서드를 포함한 클래스
- 추상 메서드는 구현코드 없이 메서드의 선언만 있음
- <b>동일한 메서드를 클래스의 상태에 따라 다르게 구현</b>하게 될때 <b>추상 클래스</b>를 사용한다

```java
// 선언만 있는 추상 메서드
abstract int add(int x, int y);

// {}부분이 구현 내용임, 추상 메서드 아님
int add(int x, int y){}
```

- abstract 예약어 사용
- <b>추상 클래스는 new (인스턴스 화)할 수 없음</b>
- 상속을 하기 위해 만든다 (혼자 돌아가기 위한 클래스는 아니다)
- 구체적인 기능을 모를때 추상메서드로 해준다
- 하위 클래스는 상위클래스의 메서드를 구현해야 할 의무가 있다

```java
package abstractex;

public class ComputerTest {

	public static void main(String[] args) {

		//Computer c1 = new Computer();	// 추상클래스는 인스턴스 화 할 수 없다.
		Computer c2 = new DeskTop();	// 상위 클래스로 선언 할 수 있다.
		//Computer c3 = new NoteBook();	// 추상클래스는 인스턴스 화 할 수 없다.
		Computer c4 = new MynoteBook();

		c2.display();
		c4.display();
	}
}
/*
결과 :
DeskTop display
NoteBook display
*/
```
---

### 추상 클래스와 템플릿 메서드
##### 템플릿 메서드
- 추상 메서드나 구현된 메서드를 활용하여 <b>전체 기능의 흐름(시나리오)를 정의하는 메서드</b>
- 전체의 흐름은 변경되면 안되므로 <b>final</b>로 선언하여 하위 클래스에서 재정의 할 수 없게한다
<br>
- 프레임 워크에서 많이 사용되는 설계 패턴, 설계단계에서 많이 사용한다
- 추상 클래스로 선언된 상위 클래스에 <u>템플릿 메서드를 활용하여 <b>전체적인 흐름</b>을 정의</u> 한다
  - ex) Car.run()
- <u>하위 클래스에서 <b>다르게 구현</b>되어야 하는 부분은 추상 메서드로 선언</u>해서 하위 클래스가 구현하도록 함
  - ex) Car.drive(), Car.stop()

```java
package template;

public abstract class Car {

	// 차가 멈추고, 달리는 것은 차의 종류에 따라 다르기 때문에 여기서 구현할 수 없다
	public abstract void drive();
	public abstract void stop();
	public abstract void horn();

	// 하위 클래스에서 필요에 의해서 재정의해서 사용하는 메서드, 항상 사용해야 하는 것은 아니다
	public void washCar() {}

	public void startCar() {
		System.out.println("시동을 켭니다");
	}
	public void turnOff() {
		System.out.println("시동을 끕니다");
	}

	// 차가 달려가는 시나리오는 항상 똑같다
	// 하위 클래스에서 메서드를 변경할 수 있기 때문에 final로 선언해준다
	public final void run() {
		startCar();
		drive();
		horn();
		stop();
		washCar();
		turnOff();
	}
}
```

```java
public class CarTest {

	public static void main(String[] args) {
		Car myCar = new ManualCar();
		myCar.run();
		System.out.println();
		Car yourCar = new AICar();
		yourCar.run();
	}
}
/*결과
시동을 켭니다
사람이 운전합니다
사람이 핸들을 조작합니다
사람이 경적을 울립니다.
사람이 브레이크로 정지합니다
자동차가 스스로 세차를 합니다
시동을 끕니다

시동을 켭니다
자율 주행합니다
자동차가 스스로 방향을 전환합니다
자동차가 스스로 경적을 울립니다.
자동차가 스스로 멈춥니다
시동을 끕니다
*/
```
---
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
