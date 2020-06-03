---
title: "JAVA, 디자인 패턴, 싱글톤/전략/어댑터/템플릿메소드/팩토리메소드"
date: 2020-06-03 13:40:28 -0400
categories: JAVA
tags : [JAVA, 디자인패턴]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

> [내 코드 확인하기](https://github.com/devham76/AlgorithmPS/tree/master/studyJava_factCampus/src)

## Singleton Patteren
- __인스턴스가 프로그램 내에서 오직 하나만 생성__
- 프로그램 어디에서든 이 인스턴스에 접근할 수 있다.

### 장점
- 전체 클래스에서 한개만 생성되므로 메모리 아낄수있다
- 다른 객체들과 공유 용이
### 단점
- 싱글톤으로 만든 객체가 복잡하다면, 객체간 결합도가 높아진다.

### 예시
```
  //Calendar cal = new Calendar();
  // 컴파일 에러. 달력은 이미 만들어진 한개의 달력을 참조만할수있다.
  Calendar calendar = Calendar.getInstance();
  calendar.getTime();	// Calendar의 여러 메소드 사용 가능
```

### 구현

```
public class Company {

	private static Company instance = new Company();
	// 전체에서 사용될 유일한 인스턴스
	// 함부로 변경되면 안되므로 private로 선언
	// 단 하나의 값만을 가져야 하므로 static으로 선언

	// private 이므로 해당 클래스에서만 생성가능하다
	private Company() {}

	// 객체를 생성하지 않고 해당 인스턴스를 부르고 싶어서 static으로 선언한다
	public static Company getInstace() {
		if (instance == null)
			instance = new Company();

		return instance;
	}

}

public class CompanyTest {

	public static void main(String[] args) {
		Company c1 = Company.getInstace();
		Company c2 = Company.getInstace();

		// 주소 값이 같다
		System.out.println(c1+" "+c2);
	}
}
```


## Strategy Patteren
- OOP 5원칙의 Open-Close 법칙의 대표적인 예
- __기존코드는 변경X, 쉽게 확장O__
- 객체들의 공통점을 캡슐화 , 객체의 행위를 변경하기 원하면 전략을 바꿔 유연하게 확장
![전략패턴](https://user-images.githubusercontent.com/55946791/83636754-73f6cc00-a5e1-11ea-87b9-fae61eb3a6c5.jpg)

> [전략패턴 참고](https://victorydntmd.tistory.com/292?category=719467)


## Adapter Patteren
- 어댑터를 이용하면 __호환될수 없던 클래스를 연결해서__ 사용가능
- 기존시스템 + 어댑터 + 업체에서 제공한 클래스
- 기존 클래스의 코드 수정X , 타겟 인터페이스에 맞춰 동작을 가능하게 한다.
![어댑터패턴](https://user-images.githubusercontent.com/55946791/83639859-482a1500-a5e6-11ea-8c34-3a049a2bcda1.JPG)

> [어댑터패턴 참고](https://niceman.tistory.com/141)


## Template Method Patteren
- 코드의 중복을 줄이기 위해, __하위class에서 빈번,공통으로 나타나는 부분을 별도의 추상 클래스에__ 정의해서 사용
- 구현별로 달라질 수 있는 메소드를 구현 클래스에서 선언 후 호출
- 추상 클래스를 이용한다 (하위 클래스에서 기능의 확장에 용이 !)

### 장점
- 코드 중복 감소
- 자식 class의 역할 감소, 핵심로직 관리 용이
- 객체 추가 및 확장 용이

### 단점
- 추상메소드가 많아지면 클래스 관리 복잡
- 추상클래스와 구현클래스간 복잡성 증대

### 구조
![템플릿메소드패턴](https://user-images.githubusercontent.com/55946791/83640047-8f180a80-a5e6-11ea-95a5-7d147be43831.JPG)
### 결과
![템플릿메소드패턴2](https://user-images.githubusercontent.com/55946791/83641398-71e43b80-a5e8-11ea-9ab7-8f7ab230fc35.JPG)


> [템플릿 메소드 패턴 참고](https://niceman.tistory.com/142?category=940951)

## Factory Method Patteren
- __객체 생성을 대신 수행해주는 공장__ (간접적으로 객체 생성 후 반환)
- 기반 클래스 코드에 구체 클래스의 이름을 감추는 방법
### 장점
- 생성할 클래스를 미리 몰라도 팩토리 클래스가 객체 생성
- 객체의 자료형이 하위클래스에 의해 결정

### 단점
- 객체가 늘어날 때 마다 하위클래스 재정의로 인한 불필요한 많은 클래스 생성 가능

![팩토리 메서드 패턴](https://user-images.githubusercontent.com/55946791/83642002-3eee7780-a5e9-11ea-95d5-ed766502e4c3.JPG)

```java
package FactoryMethod;

public class ShapeFactory {

	// 팩토리 메소드 - 객체 생성 후 반환
	public Shape getShap(String shapeType) {
		if(shapeType==null)
			return null;

		if(shapeType.equalsIgnoreCase("CIRCLE")){
			return new Circle();
    }  
		else if(shapeType.equalsIgnoreCase("RECTANGLE")){
			return new Rectangle();
    }

		return null;

	}
}
```

> [팩토리 패턴 참고](https://niceman.tistory.com/143?category=940951)
