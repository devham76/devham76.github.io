---
title: "Algorithm, BinarySearch & lower bound / upper bound"
date: 2020-03-24 15:30:28 -0400
categories: Algorithm
tags : [Algorithm, trie]
---

## BinarySearch 이분탐색
- 정렬되어있어야 한다
- O(n)(worst case) : 처음 부터 끝까지 원하는 값을 찾지 못할때
- O(long n) : 탐색 대상을 절반씩 줄여나가기 때문에 탐색의 횟수는 log2N이 된다.

```
1,2,3,4,5,6에서 6를 찾고싶으면

[1]
배열의 중간인 3과 비교한다.
6>3이므로 오른쪽에 위치한것들과 비교.
[2]
4,5,6 에서 6를찾는다
중간값인 5와 비교한다.
6>5이므로 오른쪽에 위치한것과 비교.
[3]
6에서 6을 찾는다.
끝.

```

> 이분탐색 : 원하는 값 K를 찾는 과정
> Lower Bound : 원하는 값 K이상이 처음 나오는 위치를 찾는 과정
> Upper Bound : 원하는 값 K를 초과한 값이 처음 나오는 위치를 찾는 과정

## Lower bound
### 글 풀이
```
arr= {1, 3, 5, 7, 8, 9, 11, 12, 13}에서, 10이상인 값이 처음 나오는 위치를 구하라.

[1]
arr [ (1+9)/2 ] = 8
10 > 8 이므로 시작위치를 5+1로 설정

[2]
arr [ (6+9)/2 ] = 7
10 < 11 이다.
이때, 이분탐색과 달리, 끝 위치를 중간위치인 7로 설정한다.

[3]
arr [ (6+7)/2 ] = 9
10 > 9 이므로 시작위치를 6+1로 설정.
시작위치 = 끝위치 = 6 이므로 6번째 값인 11이 Lower Bound가 된다.

```

### 코드

```java
int lower_bound(int arr[], int target){
  int mid, start, end;
  start =0; end = arr.length()-1;

  while(end > start){
    mid = (start+end) / 2;
    if(arr[mid] >= target)
      end = mid;
    else
      start = mid+1;
  }
  return end;
}
```

## Upper bound
- 초과하는 값을 찾는 것이므로 arr[mid] > target 로 변경하면 끝.

## 알고리즘 문제
- [합이 0인 네정수](https://www.acmicpc.net/problem/7453)
- [두 배열의 합](https://www.acmicpc.net/problem/2143)
- A+B = T / B = T-A 를이용
- 중복을 허용하는 배열에서 찾고자 하는 값의 개수를 구하는 방법 => __upper, lower bound를 이용__ 하면 이분법 이므로 O(log N) 빨리 찾을수있다.

```
배열에 중복된 값이 들어가있을수있으므로 upper, lower bound의 차이값으로
찾고자 하는 값의 개수를 구할수있다.

예시 )
upper bound = k초과인 값 발견 지점
lower bound = k이상인 값 발견 지점

1,2,3,5,5,6 배열
찾고싶은 값 ; 4
ub = 4
lb = 4
갯수 0개

찾고싶은 값; 5
ub = 6
lb = 4
개수 2개
```

```java
package org.baekjoon;

import java.io.*;
import java.util.*;

public class test2143_arrSum {

	static int[] A, B;
	static ArrayList<Long> sumA, sumB;
	static int N, M;
	static long T, cnt;

	public static void main(String[] args) throws IOException {

		// 데이터 입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = null;

		T = Long.parseLong(br.readLine());
		N = stoi(br.readLine());

		A = new int[N];
		st = new StringTokenizer(br.readLine());
		for(int i = 0 ; i < N ; ++i) {
			A[i] = stoi(st.nextToken());
		}

		M = stoi(br.readLine());
		B = new int[M];
		st = new StringTokenizer(br.readLine());
		for(int i = 0 ; i < M ; ++i) {
			B[i] = stoi(st.nextToken());
		}

		cnt = 0;
		sumA = new ArrayList<>();
		sumB = new ArrayList<>();

		// 합 리스트 만들기
		for(int i = 0 ; i < N ; ++i) {
			long sum = 0;
			for(int j = i ; j < N ; ++j) {
				sum += A[j];
				sumA.add(sum);
			}
		}

		for(int i = 0 ; i < M ; ++i) {
			long sum = 0;
			for(int j = i ; j < M ; ++j) {
				sum += B[j];
				sumB.add(sum);
			}
		}

		// 이진탐색(lower, upper bound)를 사용하기 위해서는 오름차순으로 정렬되어 있어야한다
		Collections.sort(sumA);
		Collections.sort(sumB);

		for(int i = 0 ; i < sumA.size() ; ++i) {
			long target = T - sumA.get(i);
			cnt += upper_bound(0, sumB.size(), target) - lower_bound(0, sumB.size(), target);
		}

		System.out.println(cnt);
	}

	// lower_bound는 list에서 target이상의 값이 있는 첫번째 index반환
	private static int lower_bound(int left, int right, long target) {
		while(left < right) {
			int mid = (left + right) / 2;
			if(sumB.get(mid) < target) {
				left = mid + 1;
			} else {
				right = mid;
			}
		}
		return right;
	}

	// upper_bound는 list에서 target초과의 값이 있는 첫번째 index반환
	private static int upper_bound(int left, int right, long target) {
		while(left < right) {
			int mid = (left + right) / 2;
			if(sumB.get(mid) <= target) { // target과 같을 때도 left를 갱신한다.
				left = mid + 1;
			} else {
				right = mid;
			}
		}
		return right;
	}

	private static int stoi(String s) {
		return Integer.parseInt(s);
	}
}

````


---

## Reference
- <https://velog.io/@hyeon930/BOJ-7453-%ED%95%A9%EC%9D%B4-0%EC%9D%B8-%EB%84%A4-%EC%A0%95%EC%88%98-Java>
