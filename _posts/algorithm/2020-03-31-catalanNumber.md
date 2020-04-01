---
title: "Algorithm, Catalan Number"
date: 2020-03-31 15:30:28 -0400
categories: Algorithm
tags : [Algorithm, dp, catalan number]
---

## 카탈란 수
### 1. 잘 짜인 괄호

- 괄호 ()를 잘 짜였다고한다. n쌍의 ()를 잘 짜인 모양으로 늘어 놓는 방법은 몇가지인가?
```
n=0 , *
n=1 , ()
n=2 , ()(), (())
...
```

### 2. 산만들기
- 오르막과 내리막을 n쌍으로 산을 만들수있는 방법의 수는?
```
n=0 , *
n=1 , /\
             /\
n=2 , /\/\, /  \
```

### 3. 대각선 피해가기
- 정사각형으로 이루어진 nxn개의 정사각형의 변을 따라 이동할때 대각선과 만나지 않고 이동하는 방법의 수? ( 산만들기과 같은 문제이다 )

### 4. 다각형을 삼각형으로 나누기
- n+2개 변으로 이루어진 볼록 다각형을 서로 만나지 않는 대각선을 사용해서 n개의 삼각형으로 나누는 방법의 수

## 점화식 찾기
- AB가 n-1쌍의 괄호를 가질때 n쌍의 괄호로 만들수있는 방법은
()AB, (A)B, A(B), (AB)가 있다.
- A가 k쌍이면, B는 n-k-1쌍이 있어야 한다.

```
C1 = C0C0
C2 = C0C1 + C1C0
C3 = C0C2 + C1C1 + C2C0
...
```

### [boj 10422 괄호](https://www.acmicpc.net/problem/10422)

```java
package org.baekjoon;

import java.util.Scanner;

public class test10422 {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int T = sc.nextInt();

		long[] dp = new long[2501];	// dp[i] : 괄호 i쌍의 개수. 길이6은 3쌍을 만들수있다.
		dp[0] = 1;
		dp[1] = 1;
		for (int i = 2; i <= 2500; i++) {
			for (int j = 0; j < i; j++) {
				dp[i] += (dp[j] * dp[i - j - 1]) ;
				dp[i] %= 1000000007;
			}
		}
		while (T-- > 0) {

			int n = sc.nextInt();

			if (n % 2 != 0) {
				System.out.println(0);
				continue;
			}

			System.out.println(dp[n/2]);
		}

	}

}

```


## 코드표현


```java
package org.study;

public class CatalanNumber {

	static int[] dp;

	public static void main(String[] args) {
		int N = 10;
		for (int i = 1; i <= N; i++) {
			System.out.println(catalan(i));
		}

		System.out.println();

		dp = new int[N + 1];
		dp[0] = 1;
		dp[1] = 1;
		for (int i = 2; i <= N; i++) {
			for (int j = 0; j < i; j++) {
				dp[i] += dp[j] * dp[i - j - 1];
			}
			System.out.println(dp[i]);
		}
	}

	static int catalan(int n) {
		int res = 0;

		// base case
		if (n <= 1) {
			return 1;
		}

		for (int i = 0; i < n; i++) {
			res += catalan(i) * catalan(n - i - 1);
		}
		return res;
	}
}

```

```
1, 2, 5, 14, 42, 132, 429, 1430, 4862, 16796
```


---
## 참고

- <https://www.geeksforgeeks.org/program-nth-catalan-number/>
- <https://suhak.tistory.com/77>
