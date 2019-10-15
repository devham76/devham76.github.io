---
title: "Algorithm, programmers, 42842(카펫)"
date: 2019-10-15 12:30:28 -0400
categories: Algorithm문제풀이
tags : [Algorithm, JAVA, 문제풀이, 완전탐색]
---
난이도 하

```java
package org.programmers;

import java.util.Arrays;

public class carpet {

	public static void main(String[] args) {
		solution(24, 24);
	}
	static int[] solution(int brown, int red) {
        int[] answer = new int[2];

        for (int i=1; i<=red; i++) {
        	if(red % i != 0)
        		continue;

        	int garo = red/i;	 // i는 세로, garo는 가로

					// 모든 둘레 + 네개의 모서리 를 둘러싼 개수 와 갈색 카펫이 같을때
        	if ( (garo+i)*2 + 4 == brown) {		
        		answer[0] = garo+2;
        		answer[1] = i+2;
        		break;
        	}
        }
        return answer;
    }
}
```
---
## Reference
[문제로 가기](https://programmers.co.kr/learn/courses/30/lessons/42842)
