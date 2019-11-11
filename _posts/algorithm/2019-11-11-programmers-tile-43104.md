---
title: "Algorithm, programmers, 타일장식물(43104)"
date: 2019-11-11 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, dp]
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

public class Level1_tile_43104 {

	public static void main(String[] args) {
		System.out.println( solution2(5) );
	}    
	public static long solution(int N) {
        long answer = 0;
        long tile[] = new long[80];
        tile[0] = 1;
        tile[1] = 1;
        getTile(tile, 2, N);

        answer = tile[N-1] * 4 + tile[N-2] * 2;
        return answer;
    }

	public static void getTile(long tile[], int current, int goal) {
		if (current == goal)
			return;
		tile[current] = tile[current-1] + tile[current-2];
		getTile(tile, current+1, goal);
	}
	public static long solution2(int N) {
        long answer = 0;
        long tile[] = new long[80];
        tile[0] = 1;
        tile[1] = 1;
        for (int i = 2; i < N; i++)
        	tile[i] = tile[i-1] + tile[i-2];
        answer = tile[N-1] * 4 + tile[N-2] * 2;
        return answer;
	}
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/43104>
---
