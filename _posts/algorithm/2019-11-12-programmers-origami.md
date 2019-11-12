---
title: "Algorithm, programmers, 종이접기(62049))"
date: 2019-11-12 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, recursive]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 풀이
- 재귀 함수로 해결
- 기저사례 : 현재 접은 횟수 == 접어야 되는 횟수
- 한번 접으면
    - 현재 접힌 왼쪽 부분 = 이전에 접은 부분과 같고
    - 현재 접힌 오른쪽 부분 = 이전에 접은 부분과 반대
    - 현재 접힌 부분의 가운데는 무조건 0
    
---

```java
package org.programmers;
// https://www.welcomekakao.com/learn/courses/30/lessons/62049
public class witercoding_2019_origami {

	public static void main(String[] args) {
		//solution(3);
		solution(4);

	}
	static int[] answer;
	public static int[] solution(int n) {
		int[] design = {0};
		getDesign(n, 1, design);
		return answer;
	}
	public static void getDesign(int goal, int count, int[] prevDesign) {

		if (goal == count) {
			makeAnswer(prevDesign);
			return;
		}
		int[] design = new int[ prevDesign.length*2 + 1 ];
		for (int i = 0; i < prevDesign.length; i++) {
			// 현재 값의 오른쪽은 이전값과 같고
			design[i] = prevDesign[i];
			// 현재 값의 왼쪽은 이전값의 반대이다
			design[ design.length -1 -i] = ( prevDesign[i] == 1) ? 0 : 1 ;
		}
		// 가운데 값은 무조건 0
		design[ prevDesign.length / 2] = 0;
		// 다 접을 때 까지 반복
		getDesign( goal, count+1, design);
	}
	public static void makeAnswer(int[] arr) {
		answer = new int[arr.length];
		answer = arr.clone();
	}
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/62049>
---
