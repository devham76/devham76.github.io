---
title: "Algorithm, programmers, 12932(자연수 뒤집어 배열로 만들기)"
date: 2019-10-04 13:30:28 -0400
categories: Algorithm문제풀이
tags : [Algorithm, JAVA, 문제풀이]
---
난이도 하

```java
package org.programmers;
// https://programmers.co.kr/learn/courses/30/lessons/12932
import java.util.*;
public class Level_1_12932 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		long n = 1234567;
		solution(n);
	}
	public static int[] solution(long n) {
	      
	      Queue<Integer> queue = new LinkedList<Integer>();
	      do {
	    	  queue.offer( (int) (n%10) );
	    	  n = n / 10;
	      }while( n != 0 );
	      
	      int[] answer = new int[ queue.size() ];
	      int i = 0;
	      while (!queue.isEmpty()) {
	    	  int a = queue.poll();
	    	  answer[i++] = a;
	      }
	      return answer;
	 }
}
```


---
## Reference 
[문제로 가기](https://programmers.co.kr/learn/courses/30/lessons/12932)
