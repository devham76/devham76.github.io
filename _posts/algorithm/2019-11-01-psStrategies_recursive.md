---
title: "Algorithm, 알고리즘 문제해결 전략, brute-force"
date: 2019-11-01 13:00:28 -0400
categories: Algorithm
tags : [Algorithm,  brute-force, 알고리즘 문제해결 전략]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### brute-force
- 무식하게 푼다
- 완전탐색
- 컴퓨터의 빠른 계산을 이용해 가능한 경우의 수를 일일이 나열하면서 답을 찾는 방법
- ex. 재귀호출
---
### 방법
1. 가능한 모든 답의 후보를 만드는 과정을 여러 개의 선택으로 나눕니다. 각 선택은 답의 후보를 만드는 과정의 한 조각이 됩니다.
2. 그 중 하나의 조각을 선택해 답의 일부를 만들고, 나머지 답을 재귀 호출을 통해 완성합니다.
3. 조각이 하나 밖에 남지 않은 경우, 혹은 하나도 남지 않은 경우에는 답을 생성 했으므로, 이것을 기저 사례로 선택해 처리합니다.
- [<b>팁!!</b>] 기저사례 : 입력이 잘못되거나, 범위에서 벗어난 경우도 기저사례로 택해서 맨 처음에 처리한다.
``` java
// 필수조건: n>=1
// 결과 : 1부터 n까지의 합을 반환
int recursiveSum(int n) {
  if (n == 1) return 1; // 더이상 쪼개지지 않을때
  return n + recursiveSum(n-1);
}
```

---
#### 문제
* 문제 ID:BOGGLE, 난이도:하
* 5x5 크기의 알파벳 격자에 상하좌우/대각선으로 인접한 칸들의 글자를 이어서 단어를 찾아내는 게임이다.
* 입력받은 단어를 찾으면 true, 그렇지 못하면 false를 반환하라

```java
package org.psStrategies;

public class Chapter6_boggle {

	public static void main(String[] args) {
		char[][] board = {
				{'N','N','N','N','S'},
				{'N','E','E','E','N'},
				{'N','E','Y','E','N'},
				{'N','E','E','E','N'},
				{'N','N','N','N','N'},
		};
		String word = "YES";
		boolean answer = false;
		// 게임판 위에서 단어의 첫글자가 시작되는 곳을 찾는다.
		for( int x = 0; x < board.length; x++) {
			for ( int y = 0; y < board.length; y++) {
				if (board[x][y] == word.charAt(0)) {
					if( hasWord(x, y, board, word) )
						answer = true; break;
				}
			}
		}

		System.out.println(answer);
	}
	// 인접 8칸
	static int[] dx = {-1, -1, -1, 1, 1, 1, 0, 0};
	static int[] dy = {-1, 0, 1, -1, 0, 1, -1, 1};
	public static boolean hasWord(int x, int y, char[][] board, String word) {

		// 기저 사례 : 입력이 잘못되거나 / 범위를 벗어나면 기저사례!!!!!
		// 기저 사례 1 : 검색 범위가 게임 판을 벗어날때 실패
		if (x < 0 || x >= board.length || y < 0 || y >= board.length)
			return false;
		// 기저 사례 2 : 입력이 잘못 됬을때 실패
		if (board[x][y] != word.charAt(0))
			return false;
		// 기저 사례 3 : 입력이 잘됐고, 단어 길이가 1이라면 성공.
		if (word.length() == 1)
			return true;
		// 인접한 8칸을 검색한다
		for (int direction = 0; direction < 8; direction++) {
			int nextX = x + dx[direction], nextY = y + dy[direction];
			if ( hasWord(nextX, nextY, board, word.substring(1)) )
				return true;
		}
		return false;
	}
}
```

---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/parts/12230)
- 알고리즘 문제해결 전략
