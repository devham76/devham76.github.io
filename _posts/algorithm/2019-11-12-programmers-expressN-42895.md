---
title: "Algorithm, programmers, N으로 표현(42895)"
date: 2019-11-12 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, dfs]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- 못풀어서 다른 분의 풀이 봄
### 풀이
- 기저사례
    - 연산횟수 8 초과
    - 연산결과 == number
- 이전까지의 연산결과와 주어진 N또는 NN, NNN, NNNN, NNNN...의 사칙연산을 반복적으로 한다.
#### 구현
- 연산회수 (count) : 이전까지의 연산횟수 + 현재 이루어질 사칙연산 횟수(1) + nn을 만들어서 발생한 횟수(i)
- 맨처음의 nn은 N, 그 다음은 NN, NNN, NNNN..... ; 언제까지? 8 - 이전 연산 횟수 만큼 만들어서 연산한다.

---
```java
package org.programmers;

public class Level1_experessN_42895 {

	public static void main(String[] args) {
		solution(5 ,12);
	}
    public static int solution(int N, int number) {
    	dfs (N, number, 0, 0);
        return answer;
    }
    static int answer = -1;
    public static void dfs(int N, int number, int count, int current){

    	if (count > 9) {
    		answer = -1;
    		return ;
    	}
    	if (current == number) {
    		// answer 값이 안정해져 있거나 answer보다 count가 더 최솟값이면
    		if (answer == -1 || answer > count)
    			answer = count;
    		return ;
    	}
    	int nn = N;
    	for (int i = 0; i < 8 - count; i++) {
    		// 이전까지의 연산횟수 + 현재 이루어질 사칙연산 횟수(1) + nn을 만들어서 발생한 횟수(i)
    		// 맨처음의 nn은 N, 그 다음은 NN, NNN, NNNN..... ; 언제까지? 8 - 이전 연산 횟수 만큼 만들어서 연산한다.
    		dfs(N, number, count+1+i, current+nn);
    		dfs(N, number, count+1+i, current-nn);
    		dfs(N, number, count+1+i, current/nn);
    		dfs(N, number, count+1+i, current*nn);

    		nn = N*10 + N;
    	}
    }
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/42895>
- [다른분의 풀이] : <https://jayrightthere.tistory.com/entry/DFSJAVA-N%EC%9C%BC%EB%A1%9C-%ED%91%9C%ED%98%84>
---
