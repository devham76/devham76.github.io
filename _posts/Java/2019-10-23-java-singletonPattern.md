---
title: "JAVA, singleton패턴(static 응용)"
date: 2019-10-22 20:30:28 -0400
categories: JAVA
tags : [JAVA, 패턴]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### static 응용 : singleton 패턴
![singleton](https://user-images.githubusercontent.com/55946791/67358304-eeb32f80-f59a-11e9-8a05-d26274c84bec.JPG)
- 자동차 회사는 단 한개만 존재해야 한다
<br>
#### [singleton패턴 이란]
- <b>전 시스템에 단 하나의 인스턴스만이 존재</b>하도록 구현하는 방식
- ex)날짜, 서울의 날짜는 단한개. 뉴욕의 날짜는 단한개.

#### [코드 예시]
##### CompanyTest
```java
package singlton;
import java.util.Calendar;
public class CompanyTest {

	public static void main(String[] args) {
		Company c1 = Company.getInstace();
		Company c2 = Company.getInstace();

		// 주소 값이 같다
		System.out.println(c1+" "+c2);

		// 예시
		//Calendar cal = new Calendar();
		// 컴파일 에러. 달력은 이미 만들어진 한개의 달력을 참조만할수있다.
		Calendar calendar = Calendar.getInstance();
		calendar.getTime();	// Calendar의 여러 메소드 사용 가능
	}
}
```

##### Company
```java
package singlton;
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
```

---

### 문제
- 카드 회사가 있습니다. 카드회사는 유일한 객체이고, 이 회사에서 카드를 발급하변 항상 고유번호가 자동으로 생성됩니다
- 10001부터 시작해서 카드가 생성될 때 마다 10002,10003식으로 증가됩니다
- 다음 코드가 수행 되도록 Card 클래스,CardCompany 클래스를 구현하세요

### CardCompanyTest

```java
package classPart;

public class CardCompanyTest {

	public static void main(String[] args) {

		// 싱글톤 패턴
		CardCompany company = CardCompany.getInstance();


		// 카드 회사는 하나만 있고, 카드회사에서 카드를 발급한다.
		// 메서드에서 Card 생성
		Card myCard = company.createCard();
		Card yourCard = company.createCard();

		System.out.println(myCard.getCardNumber());	// 10001 출력
		System.out.println(yourCard.getCardNumber()); // 10002 출력
	}
}
```

### CardCompany

```java
package classPart;


public class CardCompany {


	// 카드회사는 유일하다
	// 함부로 변경되면 안되므로 private
	// 단 하나의 값만 가져야 하므로 static
	private static CardCompany company = new CardCompany();

	// private이므로 해당 클래스에서만 생성가능
	private CardCompany() {}

	// 객체를 생성하지 않고 해당 인스턴스를 부르고 싶어서 static으로 선언한다
	public static CardCompany getInstance() {
		if (company == null) {
			company = new CardCompany();
		}
		return company;
	}

	// 카드회사에서 카드를 발급한다.
	// Card가 생성된다
	public Card createCard() {
		Card card = new Card();
		return card;
	}
}

```

### Card

```java
package classPart;

public class Card {

	// 카드 번호는 카드마다 하나 있다
	// static을 사용하면 모든 카드가 공유하므로 쓰면안된다
	// private로 외부에서 함부로 바꾸지 못하게 보호한다.
	//private static int cardNumber;
	private int cardNumber;

	// serialNum 카드 회사에서 제공되고 그 값음 공유 되므로 static으로 설정한다
	private static int serialNum = 10000;

	Card(){
		// card가 발급될때마다 (인스턴스화 될때마다) seialNum은 +1 되고, 그값은 유지 된다.
		serialNum++;
		cardNumber = serialNum;
	}

	public int getCardNumber() {
		return cardNumber;
	}

	public void setCardNumber(int cardNumber) {
		this.cardNumber = cardNumber;
	}

}

```


---
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
