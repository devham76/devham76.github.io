---
title: "Algorithm, Knapsack Problem 배낭 채우기 문제(DP)"
date: 2020-03-28 15:30:28 -0400
categories: Algorithm
tags : [Algorithm, dp, Knapsack Problem ]
---

## 개념

```
N개의 물건과 최대 용량이 M인 배낭이 있다.
N개의 물건은 W무게와 v이익을 갖는다.
용량 M을 넘어가지 않으면서 물건을 max(p)가 되도록 채우는 문제를 말한다.

```

## 종류
### 1. 모든 경우의 수를 넣어본다(Brute-Force)
: O(n^) 느리다.

### 2. 가치가 좋은것 혹은 무게가 제일 적은것 부터 고른다. (Greedy)
: 최적의 답을 보장하지 못한다.

### 3. DP를 이용하여 해결한다.
: 큰 문제를 작은 문제로 쪼개서 해결.

---

> [평범한 배낭(12865)](https://www.acmicpc.net/problem/12865)

> [비슷한 문제 - 1 2 3 더하기 4](https://www.acmicpc.net/problem/15989)

> [비슷한 문제 - 동전1](https://www.acmicpc.net/problem/2293)

## 풀이
- 첫번째 물건을 골랐을때 가치를 구한다.
- 그 가치들에 두번째 물건을 넣었을때 최대값을 구한다
- 마지막 물건까지 반복

| 무게/가치 / 무게제한 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 / 13 | x | x | x | x | x | 13 | 13 | 13 | 13 | 13 |
| 4 / 8 | x | x | x | max(0,8) | max(0,8) |  max(13,8) | max(13,8) | max(13, 8) | max(13,8) | max(13, 13+8) |
| 3 / 7  | x | x | max(0, 7) | max(8,7) | max(8,7) | max(13,7) | max(13, 7+8) | max(13, 7+8) | max(8, 7+13) | max(21, 7+13) |

```java
package org.baekjoon;

import java.util.*;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Scanner;

public class test12865 {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		int k = sc.nextInt();

		// dp[idx][limit] : 0~idx번까지의 물건을 limit 무게까지 넣었을때 최대 가치
		int[][] dp = new int[n + 1][k + 1];
		int[][] product = new int[n + 1][2]; // 0:무게 1:가치
		for (int i = 1; i <= n; i++) {
			int weight = sc.nextInt();
			int value = sc.nextInt();
			product[i][0] = weight;
			product[i][1] = value;
		}

		for (int idx = 1; idx <= n; idx++) {
			for (int limit = 1; limit <= k; limit++) {
				// 현재 물건 전까지 물건들로 limit무게 까지 만들 수 있는 최대 가치 입력
				dp[idx][limit] = dp[idx - 1][limit];
				if (limit >= product[idx][0]) {

					int curWeight = product[idx][0];
					int curValue = product[idx][1];

					// 현재 물건을 넣기 이전의 가치 vs 현재 물건의 가치 + (limit-현재물건의 무게)일때 최대가치
					dp[idx][limit] = Math.max(dp[idx - 1][limit], curValue + dp[idx - 1][limit - curWeight]);
				}
			}

		}
		System.out.println(dp[n][k]);
	}

}

```



---

## 참고
- <https://gsmesie692.tistory.com/113>
