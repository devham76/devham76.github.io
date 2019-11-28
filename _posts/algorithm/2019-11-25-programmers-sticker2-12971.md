---
title: "Algorithm, programmers, 스티커2(12971)"
date: 2019-11-25 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, dp]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### 풀이
1. Math.max(현재 스티커 떼고 + 현재스티커-2의 dp , 현재스티커-1의 dp) 가 기본 점화식이 된다.
2. 원형이므로 첫번째 스티꺼를 떼거나 떼지않을때 두가지를 생각해야 한다.
3. 첫번재 스티커를 뗀다면, 마지막 스티커는 포함 하지 않는다.
4. 스티커틑 10만개 까지 있을수 있다.

### 배운점
- dp를 이용한 문제이므로 점화식을 먼저 구해야한다.
- 바텀업으로 예제를 적어보고 (실패함) 보이지않으면 탑다운으로 점화식을 구해보자
- 원형스티커 임을 조심하자

```java
// 풀이 참고 : https://aomee0880.tistory.com/94
// https://www.welcomekakao.com/learn/courses/30/lessons/12971
/*
 해결 방법 :
1. Math.max(현재 스티커 떼고 + 현재스티커-2의 dp , 현재스티커-1의 dp) 가 기본 점화식이 된다.
2. 원형이므로 첫번째 스티꺼를 떼거나 떼지않을때 두가지를 생각해야 한다.
3. 첫번재 스티커를 뗀다면, 마지막 스티커는 포함 하지 않는다.
4. 스티커틑 10만개 까지 있을수 있다.
*/
package org.programmers;

public class summercoding_2018_12971_sticker2 {

	public static void main(String[] args) {
		int[] s1 = {14, 6, 5, 11, 3, 9, 2, 10};
		int[] s2 = {1, 3, 2, 5, 4};
		// 36 8
		solution(s1);
	}
    public static int solution(int sticker[]) {
    	int[] dp1 = new int[100001];
    	int[] dp2 = new int[100001];

    	int len = sticker.length;
    	if (len == 1) return sticker[0];


    	// 첫번째 스티커를 뜯었다면
    	dp1[0] = sticker[0];
    	dp1[1] = dp1[0];
    	// 첫번째 스티커 뜯으면, 마지막 스티커는 사용할 수 없다
    	// 스티커 4개째 부터 유효 , dp1[2] => 스티커 4개째의 dp
    	for (int i = 2; i < len-1; i++)
    		dp1[i] = Math.max(sticker[i]+dp1[i-2], dp1[i-1]);

    	// 첫번째 스티커 안뜯는다면
    	dp2[0] = 0;	// 스티커 한개 있을때 못뜯으므로 0
    	dp2[1] = sticker[1]; // 스티커 두개 있을때 두번째 스터커 뜯는다.
    	// 스티커 세개째 부터 유효, dp2[2] => 스티커 3개째의 dp
    	for (int i = 2; i < len; i++)
    		dp2[i] = Math.max(sticker[i]+dp2[i-2], dp2[i-1]);

    	// 큰수반환 ( 첫번째스티커 뜯으면 마지막 스티커 못뗀다, 마지막 스티커의 dp)
    	return Math.max(dp1[len-2], dp2[len-1]);
    }

}
```

---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/12971)
- <https://aomee0880.tistory.com/94>
---
