---
title: "JAVA, Object 클래스"
date: 2020-01-07 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념, ObjectClass]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## Object 클래스
- 모든 클래스의 최상위 클래스
- java.lang.Object 안에 있는 클래스이다
- 모든 클래스는 Object클래스를 상속받음
- 모든 클래스는 Object클래스의 메서드를 사용할 수 있음
- 모든 클래스는 Object클래스의 일부 메서드를 재정의 하여 사용할 수 있음
- import하지 않아도 컴파일러가 자동으로 import해준다

- 예제: toString(), equals(), hashCode(), clone()
	- equals() : 논리적으로 동일 / cf) == : 물리적으로 동일(주소)
	- hashCode() : 인스턴스 저장된 가상머신의 주소를 10진수로 반환


---
### 예제

```java
package ObectPart;

class Book{
	String title;
	String author;
	Book(String title, String author){
		this.title = title;
		this.author = author;
	}

	// 마우스 오른쪽 -> source -> overriding
	// Object classd의 toString()메서드를 오버라이딩 한다
	@Override
	public String toString() {
		//return super.toString(); (부모의 원형 호출)
		return title + ", " + author;
	}

}
public class ToStringTest {
	public static void main(String[] args) {
		Book book = new Book("해리포터", "j.k.롤링");
		System.out.println(book.toString());
	}

}
```

---
## Reference
-[fast capmus](https://www.fastcampus.co.kr/online/#/courses/200748/clips/11438)
