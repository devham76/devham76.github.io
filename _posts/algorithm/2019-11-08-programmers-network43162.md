---
title: "Algorithm, programmers, 네트워크(43162)"
date: 2019-11-08 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, dfs]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 풀이
- 0부터 n까지의 노드를 차례로 깊이우선으로 탐색한다.
- 탐색한 노드는 visited를 이용하여 true로 변경해준다.
- 탐색이 완료된 노드의 다음 노드를 방문했는지 visited로 확인하고, 방문하지 않았다면 해당 노드를 깊이우선으로 탐색한다.
- 깊이 우선으로 탐색할때 마다 network 는 +1 해준다.

---
```java
package org.programmers;

public class Level3_network_43162 {

	public static void main(String[] args) {
		int[][] c = { {1, 1, 0}, {1, 1, 0}, {0, 0, 1}};
		int[][] c2 = {	{1, 1, 0}, {1, 1, 1}, {0, 1, 1}};
		solution(3, c);
	}

	public static int solution(int n, int[][] computers) {
		int answer = 0;
		boolean[][] visited = new boolean[n][n];
		for(int i=0; i<computers.length; i++) {
			// 해당노드를 방문하지 않았다면, 해당노드의 네트워크를 모두 방문한 후에 +1
			if(visited[i][i] == false) {
				findWay(i, computers, visited);
				answer++;
			}
		}
		return answer;
	}

	// index노드와 인접한 모든 노드를 방문합니다
	public static void findWay(int index, int[][] computers, boolean[][] visited) {
		for(int j=0; j<computers.length; j++) { 			
			if( visited[index][j] == false && computers[index][j] == 1) {			
				visited[index][j] = visited[j][index] = true;
				findWay(j, computers, visited);
			}		
		}  			
	}
}
```

## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/43162>
