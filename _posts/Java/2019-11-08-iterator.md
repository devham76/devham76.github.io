---
title: "JAVA, iterator"
date: 2019-11-08 20:30:28 -0400
categories: JAVA
tags : [JAVA, iterator]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Iterator
- 자바의 컬렉션 프레임웍에서 컬렉션에 저장되어 있는 요소들을 읽어오는 방법을 표준화 한것중 하나

```java
public interface Iterator {
  boolean hasNext();
  Object next();
  void remove();
}
```
- 장점 : 자동으로 index를 관리해주기 때문에 편리하다
- 단점 : 객체를 만들어 사용하기 때문에 느리다

```java
package org.study;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;

public class iteratorEx {
	public static void main(String[] args) {
		// 1.
		ArrayList<Integer> list = new ArrayList<>();
		for (int i=1; i<8; i++)
			list.add(i);
		Iterator it = list.iterator();

		while(it.hasNext()) {
			System.out.println(it.next());
		}
		// 2.
		HashMap<String, String> hm = new HashMap<>();
		for(int i=1; i<8; i++)
			hm.put("키"+i, "값"+i);
		Iterator<String> keys = hm.keySet().iterator();
		while( keys.hasNext() ) {
			String key = keys.next();
			System.out.println( String.format("키:%s, 값:%s", key, hm.get(key)));
		}
	}
}

```

---
## Reference

- <https://m.blog.naver.com/PostView.nhn?blogId=rwans0397&logNo=220622092974&proxyReferer=https%3A%2F%2Fwww.google.com%2F>
- <https://stove99.tistory.com/96>
