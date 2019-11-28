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
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
