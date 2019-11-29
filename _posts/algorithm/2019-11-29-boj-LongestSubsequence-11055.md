---
title: "Algorithm, boj, 가장 큰 증가 부분 수열(11055)"
date: 2019-11-29 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, dp]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### 풀이
- 입력 배열의 길이와 같은 dp배열을 생성한다
- dp[i]에는 arr[i]값이 가장 큰 값으로 하는 부분배열의 길이가 입력된다
- 가장 작은 부분배열의 크기는 1이 되므로 dp배열의 초기값을 1로 해준다
- i는 두번째 수부터 마지막 수가 되고, 각각의 수의 이전수가 해당수보다 작은지 확인하고, 작다면 수열의 길이를 확인하여 입력한다.



```java
package org.baekjoon;

import java.util.Scanner;

public class test11055_dp_LongestSubsequence {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		int[] arr = new int[num];
		int[] dp = new int[num];
		for (int i = 0; i < num; i++) {
			arr[i] = sc.nextInt();
			dp[i] = 1;
		}

		int max = 1;
		for (int i = 1; i < num; i++) {
			for (int j = 0; j < i; j++) {
				if ( arr[i] > arr[j] ) {
					dp[i] = Math.max(dp[i], dp[j]+1);
					max = Math.max(max, dp[i]);
				}
			}
		}
		System.out.println(max);
	}
}

```

---

### 가장 큰 증가 부분 수열 (11055)

```java
package org.baekjoon;

import java.util.Scanner;

public class test11055_dp_BiggesSubsequence {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		int[] arr = new int[num];
		int[] dp = new int[num];
		for (int i = 0; i < num; i++) {
			arr[i] = sc.nextInt();
			dp[i] = arr[i];
		}

		int max = 0;
		for (int i = 1; i < num; i++) {
			for (int j = 0; j < i; j++) {
				if ( arr[i] > arr[j] ) {
					dp[i] = Math.max(dp[i], dp[j]+arr[i]);
				}
				max = Math.max(max, dp[i]);
			}
		}
		System.out.println(max);
	}
}

```

---
## Reference
- [문제보러가기](https://www.acmicpc.net/problem/11055)
- [영상 풀이](https://www.youtube.com/watch?v=CE2b_-XfVDk)
- [글 풀이](https://stack07142.tistory.com/56)

---
