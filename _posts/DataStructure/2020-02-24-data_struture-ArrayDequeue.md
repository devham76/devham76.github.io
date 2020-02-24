

## Deque
- Double Ended Queue
- queue에 헤드와 테일 양쪽에 객체를 추가/삭제/검색 기능이 추가되어있다

## ArrayDeque
- queue, dequeue의 구현 클래스로서 배열을 이용하여 구현한다.

![arraydequeue](https://user-images.githubusercontent.com/55946791/75131191-2aaafc80-5715-11ea-80c0-797c108653a3.JPG)


## ArrayDeque 특징
- ArrayDeque는 Deque를 상속받는다
- Unlike Queue, we can add or remove elements from __both sides__.
- __Null elements are not allowed__ in the ArrayDeque.
- ArrayDeque is __not thread safe__, in the absence of external synchronization.
- ArrayDeque has __no capacity restrictions__.
- ArrayDeque is __faster than LinkedList and Stack__.

### 예제

```java
package org.study;

import java.util.ArrayDeque;
import java.util.Iterator;

public class ArrayDequeuTest {

	public static void main(String[] args) {

		ArrayDeque obj = new ArrayDeque();

		obj.add("네이버");
		obj.addFirst("라인");
		obj.offerFirst("카카오"); // t or f 반환
		obj.offerLast("쿠팡"); // t or f 반환

		// 검색
		System.out.println("retrieving first element : "+obj.peekFirst());
		System.out.println("retrieving last element : "+obj.peekLast());

		// 삭제
		System.out.println("Removing first element : "+obj.pollFirst());
		System.out.println("Removing last element : "+obj.pollLast());

		// reverse traversal	// 역 순회
		System.out.println("Remaining elements : ");
		Iterator it = obj.descendingIterator();
		while(it.hasNext()) {
			System.out.println(it.next());
		}
	}

}

```

```
retrieving first element : 카카오
retrieving last element : 쿠팡
Removing first element : 카카오
Removing last element : 쿠팡
Remaining elements :
네이버
라인
```

---
- <http://theageofjava.blogspot.com/2011/11/deque-and-arraydeque.html>
- <https://m.blog.naver.com/PostView.nhn?blogId=horajjan&logNo=220311167791&proxyReferer=https%3A%2F%2Fwww.google.com%2F>
