---
title: "Algorithm, Union Find "
date: 2020-03-23 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, find-union ]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## Uionn Find
- 서로소 집합 그리고 병합 찾기 집합 이라고도 불리며 __여러 서로소 집합의 정보를 저장__ 하고 있는 자료구조를 의미한다

- 예시
```
[1,2,3,4,5,6,7,8]
[1,2,5,6,8] [3,4] [7]
```

## 구현
![Tree](https://user-images.githubusercontent.com/55946791/77328498-f4868a00-6d5f-11ea-964a-1f908b69db71.png)


### 초기화
- 처음에는 각각의 원소들은 연결된 정보가 없기 때문에 자기 자신이 부모가 된다

```java
for(int i=1; i<7; i++){
  parent[i] = 1;
}
```

### Find
- 집합의 부모 원소를 찾는 함수
- 원소 x의 부모를 찾는다.

```java
int find(int x){
  // 자신이 부모인 경우 x반환
  if(x == parent[x])
    return x;
  else {
    // 자신의 부모의 부모를 찾는다
    return parent[x] = find(x);
  }
}
```

### Uion
- 주어진 두 원소 또는 집합을 합하는 함수

```java
void union(int x, int y){
  x = find(x);
  y = find(y);

  // root가 다르다면 서로 연결
  // y의 루트를 x의 루트로 만들어서
  // x집합에 y집합을 붙인다.
  if(x != y){
    parent[y] = x;
  }
}
```

### 관련문제
- [바이러스](https://www.acmicpc.net/problem/2606)
- [집합의 표현](https://www.acmicpc.net/problem/1717)
- [친구네트워크](https://www.acmicpc.net/problem/4195)
- [ABCDE](https://www.acmicpc.net/problem/13023)


### 친구네트워크 풀이
```java
package org.baekjoon;

import java.util.*;

public class test4195_nw {

	static int[] parent ;
	static int[] count;
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int test_case = sc.nextInt();
		while(test_case > 0) {
			test_case--;

			// 친구관계
			int F = sc.nextInt();
			// 사람수의 최대 = 친구관계 x 2
			parent = new int[F*2];
			// 네트워크속 사람 수
			count = new int[F*2];

			for(int i=0; i<F*2; i++) {
				parent[i] = i;
				count[i] = 1;
			}
			int num = 0;
			Map<String, Integer> hm = new LinkedHashMap<>();	//key순서보장
			for(int i=0; i<F; i++){
				String f1 = sc.next();
				String f2 = sc.next();

				// 새로운 사람이라면, 사람에게 번호 부여
				if (!hm.containsKey(f1))
					hm.put(f1, num++);

				if (!hm.containsKey(f2))
					hm.put(f2, num++);

				// 사람의 번호로 부모찾기
				int f_num1 = hm.get(f1);
				int f_num2 = hm.get(f2);

				union(f_num1, f_num2);
				for(Integer p:parent) {
					System.out.print(p+" ");
				}
			}

			Iterator<String> keys = hm.keySet().iterator();
			while(keys.hasNext()) {
				String key = keys.next();
				System.out.println(key+", "+hm.get(key));
			}

			for(Integer p:parent) {
				System.out.print(p+" ");
			}
		}
	}

	private static void union(int f_num1, int f_num2) {
		f_num1 = find(f_num1);
		f_num2 = find(f_num2);

		// 부모가 같으면 같은 네트워크에 속해있으므로
		// 부모의 네트워크 개수 반환
		// 그게 아니라면 두 네트워크 합쳐서 반환
		if(f_num1 != f_num2) {
			parent[f_num2] = f_num1; // f_num1이 부모가된다.
			count[f_num1] += count[f_num2];	// f_num1은 f_num2의 네트워크를 차지한다.
			count[f_num2] = 1; // f_num2는 꼬리가 되므로 자기 자신하나.
		}
		System.out.println(count[f_num1]);
	}

	private static int find(int f_num) {
		// 내 부모가 나이면 나를 반환
		if(parent[f_num] == f_num) {
			return f_num;
		}
		// 내 부모의 최종 부모를 찾아 반환
		else {
			return parent[f_num] = find(parent[f_num]);
		}
	}

}

```

---
## Reference
<https://twpower.github.io/115-union-find-disjoint-set>
