---
title: "Algorithm, programmers, 42842(카펫)"
date: 2019-10-15 12:30:28 -0400
categories: Algorithm문제풀이
tags : [Algorithm, JAVA, 문제풀이, 완전탐색]
---
#### 완전탐색
- BP라고 불리는 완전탐색은 단어 그대로 모든 경우의 수를 다 해보는 것이다.
- 알고리즘을 풀때 강력한 방식이지만, 시간은 최대로 들어간다.

1. for문 사용
2. 순열, 조합 사용
3. 재귀함수 사용
4. 비트마스크 사용

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
