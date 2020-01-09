---
title: "JAVA의 정석, Chapter 12 generics, annotation"
date: 2019-12-15 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념, generics, annotation]
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
1. <u>static멤버에 타입 변수 T를 사용할 수 없다</u>
    - 대입된 타입의 종류에 관계없이 동일한 것이어야 하기 때문이다.
2. <u>지네릭 배열을 생성 할 수 없다</u>
    - T[] tmpArr = new T[itemArr.length]; (x)
    - new 연산자 때문인데, 컴파일 시점에 타입 T가 뭔지 정확하게 알아야 한다
    - 그런데 컴파일 시점에는 T가 어떤 타입이 될지 알 수 없기 때문에 불가능 하다.

## 1.3 지네릭 클래스의 객체 생성과 사용
1. 참조변수와 생성자에 대입된 타입이 일치해야 한다
```java
Box<Apple> appleBox = new Box<Grape>(); // X
Box<Fruit> appleBox = new Box<Grape>(); // X

Box<Apple> appleBox = new Box<Apple>(); // O
Box<Apple> appleBox = new FruitBox<Apple>(); // O
```

## 1.4 제한된 지네릭 클래스(extends)
- 지네릭 타입에 'extends'를 사용하면, 특정 타입으이 자손들만 대입할 수 있게 제한할 수 있다.

```java
// Fruit의 자손만 타입으로 지정가능
class FruitBox<T extends Fruit> {
  ArrayList<T> list = new ArrayList<T>();
}

FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
fruitBox.add( new Apple() ); // Apple은 Fruit의 자손
fruitBox.add( new Grape() ); // Grape은 Fruit의 자손
```

## 1.5 와일드 카드
- 문제 코드
```java
class Juicer {
  static Juice makeJuice(FruitBox<T> Box){
    String tmp="";
    for (Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
  }
}
```
- <u>static메서드</u>에는 타입 매개변수 T를 매개변수에 사용할 수 없으므로 <u>지네릭스를 적용하지 않던가, 특정 타입을 지정</u>해 줘야 한다.

- 해결 시도 코드 (오류발생)
```java
  static Juice makeJuice(FruitBox<Fruit> Box){
    String tmp="";
    for (Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
  }

  static Juice makeJuice(FruitBox<Apple> Box){
    String tmp="";
    for (Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
  }
```
- <b>지네릭 타입이 다른 것만을는 오버로딩이 성립하지 않는다</b>. 따라서 오류 발생.

|사용 | 설명|
|--|--|
|<b> <? extends T> </b> | T와 그 자손들만 가능
|<b> <? super T> </b> | T와 그 조상들만 가능
|<b> <?> </b> | 모든 타입이 가능 <? extends Object>와 동일


## 1.6 지네릭 메서드
- 지네릭 <b>클래스</b>에 정의된 타입 메서드 != 지네릭 <b>메서드</b>에 정의된 타입 매개변수
- <b>static메서드에 지네릭 타입을 선언하고 사용하는 것 가능</b>하다
- <u>지역 변수를 선언한 것과 같다</u>고 생각하면 이해하기 쉬운데, 이 타입 매개변수는 메서드 내에서만 지역적으로 사용될 것이므로 메서드가 <u>static이건 아니건 상관없다</u>

---
## 예제 !

```java
package GenericPart;

public class GenericPrinterTest {

	public static void main(String[] args) {

		GenericPrinter<Powder> powderPrinter = new GenericPrinter<>();	// Powder 타입을 생성할 3d프린터를 만들었다
		Powder powder = new Powder();	// 타입을 생성했다
		powderPrinter.setMaterial(powder);	// 생성된 타입을 넣어줘야 한다
		System.out.println(powderPrinter);
		powderPrinter.doPrinting();

		GenericPrinter<Plastic> plasticPrinter = new GenericPrinter<>();
		Plastic plastic = new Plastic(); // 재료생성
		plasticPrinter.setMaterial(plastic); // 3d프린터에 재료 대입
		//plasticPrinter.setMaterial(powder); 오류발생 !! 처음에 3d프린터 생성시의 재료와 다르다
		System.out.println(plasticPrinter);
		plasticPrinter.doPrinting();

		// metrial을 상속받지 않았기 때문에 water은 재료로 사용 불가능
		//GenericPrinter<Water> waterPrinter = new GenericPrinter<>();		
	}
}
```

```java
package GenericPart;

// 3d프린터, 재료는 다양하다
// T -> 실제로 사용할때 재료를 정하자라는 의미 , 실제로 사용될때 재료가 정해진다

// 재료를 한정짓기 위해 extends Meterial한다, 상속받은 것만 사용가능!!!!!
public class GenericPrinter<T extends Meterial> {

	private T material;

	public T getMaterial() {
		return material;
	}

	public void setMaterial(T material) {
		this.material = material;
	}

	public String toString() {
		return material.toString();
	}

	public void doPrinting() {
		material.doPrinting();
	}

}
```

```java
package GenericPart;

public abstract class Meterial {

	public abstract void doPrinting();
}
```

```java
package GenericPart;

public class Plastic extends Meterial{

	// 오버라이딩, 부모 함수를 나에 맞게 재정의
	public String toString() {
		return "재료는 plastic입니다";
	}

	// 부모의 추상메서드는 무조건 구현해야한다
	@Override
	public void doPrinting() {
		System.out.println("plastic으로 프린팅한다");
	}
}
```


---
# 3. 애너테이션(annotation)
## 3.1 에너테이션이란?
- 프로그램의 소스코드안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨것
- 프로그래밍 언어에 영향 x
- 다른 프로그램에게 유용한 정보르 제공한다

---
## Reference
- 자바의 정석(남궁성)
