---
title: "Algorithm, JAVA, Permutation (순열)"
date: 2019-10-01 19:30:28 -0400
categories: Algorithm
tags : [Algorithm]
---
순열이란 n 개의 값 중에서 r 개의 숫자를 모든 순서대로 뽑는 경우를 말합니다.
예를 들어 [1, 2, 3] 이라는 3 개의 배열에서 2 개의 숫자를 뽑는 경우는

[1, 2]
[1, 3]
[2, 1]
[2, 3]
[3, 1]
[3, 2]

arr배열에서 r개 뽑기
- output   = r개 사이즈의 배열
- visited  = 중복해서 뽑지 않기 위해 체크하는 배열

1. DFS를 돌면서 모든 인덱스에 방문하여 output배열에 값을 넣습니다
2. 이미 들어간 값은 visited 값을 true로 바꾸어 중복하여 넣지 않도록 합니다.
3. depth값 = output에 들어간 숫자의 길이
4. depth값이 r만큼 되면 output에 들어있는 값을 출력하면 됩니다.

![Permutation](https://user-images.githubusercontent.com/55946791/65956241-e593de80-e484-11e9-84f7-39d8d818e53f.png)

```java
package org.study;

import java.util.*;
/*
 *  순열 : n 개 중에서 r개 선택
 *  시간복잡도는 O(n!)
 *  연습 문제 : https://www.acmicpc.net/problem/10974
 */

public class Permutation {

	public static void main(String[] args) {
		int[] arr = {1,2,3};
		int[] output = new int[arr.length];
		boolean[] visited = new boolean[arr.length];
		perm(arr, output, visited, 0, arr.length, 3);

	}

	// 순서를 지키면서 n개중 r개를 뽑는 경우
	// 사용 예시 : perm(arr, output, visited, 0, n, 3);
	static void perm(int[] arr, int[] output, boolean[] visited, int depth, int n, int r) {

		//- 현재 깊이는 뽑은 개수이다
		//- 즉, 뽑은 개수와 뽑을 개수가 같다면 종료.
		if(depth == r) {
			print(output,r);
			return;
		}

		// 1. 모든 원소를 순회한다.
		for (int i=0; i<n; i++) {
			// 2. 방문하지 않은 원소를 찾는다
			if(visited[i] == false) {
				visited[i] 		= true;			// 방문표시
				output[depth]	= arr[i];		// 결과값 배열의 해당 깊이 자리에 방문하지 않는 원소를 삽입
				// 삽입 후에 한단계 깊은 노드로 이동 하여 output에 값추가
				perm(arr, output, visited, num, depth+1, pick);
				visited[i] 		= false;		// 한단계 깊은 노드 삽입이 끝나고 부모노드로 왔을때 arr[]의 다음 원소를 해당 자리에 넣을수 있다.
			}

		}
	}

	// 배열 출력
	static void print(int[] arr, int r) {
        for(int i=0; i<r; i++)
            System.out.print(arr[i] + " ");
		System.out.println();
	}
}
```
---

### reference
[참고](https://bcp0109.tistory.com/14)
[백준 문제](https://www.acmicpc.net/problem/10974)
