---
title: "JAVA, 알고리즘, 조합"
date: 2019-10-01 15:30:28 -0400
categories: Algorithm
tags : [Algorithm, JAVA]
---
## **조합**
- 숫자 n개에서 r개를 중복되지 않게 뽑자.
- 예) 
{1,2,3} 에서 2개 뽑기
{1,2} {1,3} {2,3}

- 상세 설명
start변수를 기준으로 start보다 작으면 뽑을 후보에서 제외, 크면 뽑을 후보가 됩니다.

- ex) {1,2,3} 배열이 있고 start가 0 부터 시작합니다.
함수에 들어오면 i=start로 시작 하는 for문에 들어갑니다.
i=0일때 즉, 인덱스 0 인 값 1을 선택 했다면, 
더이상 1은 고려 대상에서 제외 되고
다음 for문은 무조건 i+1=1 부터 시작합니다.

```java
import java.util.*;
public class Combination {
/*
 * 조합 : n 개 중에서 r 개 선택
 * 참고 : https://bcp0109.tistory.com/15?category=848939
 * */
	
	public static void main(String[] args) {
		int[] arr = {1,2,3,4};
		boolean[] visited = new boolean[arr.length];
		
		/*
		 * 시작 기준점은 인덱스  0 
		 * arr.length개 중에서 
		 * i=1 ; 1개 부터 arr.length개 까지 뽑을 것이다.
		 */
		for(int i=1; i<arr.length; i++)
			combination(arr, visited, 0, arr.length, i);		
	
	}
	
	/*
	 * 백트레킹 사용
	 * combination(뽑을 배열, 뽑혔는지 확인하는 배열, 시작 기준점, n개중, r개 선택)
	 * */
	static void combination(int[] arr, boolean[] visited, int start, int n, int r) {
		
		// 뽑기로 한 개수 만큼 다 뽑앗다면 print
		if(r==0) {
			print(arr, visited, n);
			return;
		}
		else {
			// 기준점 인덱스 부터 배열의 끝까지 뒤진다
			for(int i=start; i<n; i++) {
				// 방문 후 true 표시.
				visited[i] = true;						
				
				// i+1; 방문한 인덱스 이 후의 값을 뒤진다 / n개중에 좀 전에 방문 한개 했으므로 r-1개를 뽑는다
				combination(arr, visited, i+1, n, r-1);	
				
				// 방문 완료 후 false 표시.
				visited[i] = false; 					
			}
		}
	}
	
	// 배열 출력
	static void print(int[] arr, boolean[] visited, int n) {
		for(int i=0; i<n; i++) {
			if(visited[i] == true)
				System.out.print(arr[i]+ " ");
		}
		System.out.println();
	}
	
}

```
---

## Reference 

(https://bcp0109.tistory.com/15?category=848939)<br>


---
