---
title: "Algorithm, kakao2018 프렌즈4블록(17679)"
date: 2020-01-03 13:00:28 -0400
categories: Algorithm
tags : [Algorithm , hard]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 어려웠던점
- 개념적으로 해결할 방법은 알아냈으나, 코드로 구현하기가 어려웠다.
- 맵을 새로 리뉴얼 하는 부분이 어려웠다 (해결 코드의 down()함수)
- 네개를 비교 하는 부분은 for문과 배열을 이용해서 쉽게 구현할 수 있었다

### 풀이
1. map전체를 돌며 하나씩 해당 위치의 네방향을 비교하여 삭제가능한지 알아낸다. 삭제가능하면 visited = true로 만든다<br>
- visited = true로 만드는 이유 : 삭제가능하다고 바로 삭제해버리면 예제처럼 겹치는 부분은 삭제가 되지 않기 때문에 일단, 삭제 가능 한 부분을 표시해준다.
- 처음 방문하는 위치라면 cnt++를 해주어 삭제할 개수를 세어준다

```java
for (int i = 0; i < m-1; i++) {
    for (int j = 0; j < n-1; j++) {
        char c = map[i][j];

        if(c == '.') continue;

        boolean same = true;
        for (int k = 0; k < 4; k++) {
            if(map[i+dx[k]][j+dy[k]] != c) {
                same = false;
                break;
            }
        }
        if(!same) continue;

        for (int k = 0; k < 4; k++) {
            int nx = i+dx[k];
            int ny = j+dy[k];

            if(!visited[nx][ny])
              cnt++;

            visited[nx][ny] = true;
        }
    }
}
```

2. 전체 map에서 삭제가능한것들을 visited 배열에 입력하면 map에 삭제 가능한것들을 '.' 으로 변경하여 삭제해버린다.

```java
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        if(visited[i][j])
            map[i][j] = '.';
    }
}
```

3. cnt == 0 이라는 의미는 더이상 2x2로 삭제할 것이 없으니까 그만 하라는 의미이다. 따라서 break로 while문을 나간다
- cnt == 0이 아니면 해당 라운드에서 삭제한 cnt값을 answer에 더한다

```java
if(cnt == 0) break;
answer += cnt;
```

4. down 메소드는 삭제할것들을 삭제하여 map을 다시 만드는 함수이다
- map의 맨아래 행에서 위로 올라가며 조사하는데
- 삭제할것이 있으면 ('.'이 있으면) 건너뛰고 삭제할것이 없으면 그 아래칸을 조사한다 ( map[nx+1][j] )  
  - 그 아래칸이 삭제할것이 아니라면 해당칸에 해당 문자를 넣고
  - 그 아래칸이 삭제할것 이라면 nx++;을 해서 삭제할것이 아닐때까지 더해주고(내려가고) , 더이상 삭제할칸이 없으면 그 위칸에  map[nx][j] = c; 문자를 넣어준다

```java
public static void down(int m, int n, char[][] map) {

    for (int i = m-1; i >= 0 ; i--) {
        for (int j = 0; j < n; j++) {
            if(map[i][j] == '.') continue;

            int nx = i;
            char c = map[i][j];
            map[i][j] = '.';
            while(true) {
                if(nx+1 >= m || map[nx+1][j] != '.') break;
                nx++;
            }
            map[nx][j] = c;
        }
    }
}
```

---

### 전체코드

```java
package org.programmers;

public class kakao_2018_17679_fiends4block_finish {

	static int[] dx = {0,0,1,1};
	static int[] dy = {0,1,0,1};

	public static int solution(int m, int n, String[] board) {
	    int answer = 0;
	    char[][] map = new char[m][n];
	    boolean[][] visited;
	    for (int i = 0; i < m; i++) {
	        map[i] = board[i].toCharArray();
	    }

	    while(true) {
	        visited = new boolean[m][n];
	        int cnt = 0;

	        for (int i = 0; i < m-1; i++) {
	            for (int j = 0; j < n-1; j++) {
	                char c = map[i][j];

	                if(c == '.') continue;

	                boolean same = true;
	                for (int k = 0; k < 4; k++) {
	                    if(map[i+dx[k]][j+dy[k]] != c) {
	                        same = false;
	                        break;
	                    }
	                }
	                if(!same) continue;

	                for (int k = 0; k < 4; k++) {
	                    int nx = i+dx[k];
	                    int ny = j+dy[k];
	                    if(!visited[nx][ny]) cnt++;
	                    visited[nx][ny] = true;
	                }
	            }
	        }

	        for (int i = 0; i < m; i++) {
	            for (int j = 0; j < n; j++) {
	                if(visited[i][j])
	                    map[i][j] = '.';
	            }
	        }

	        if(cnt == 0) break;
	        answer += cnt;

	        down(m,n,map);
	    }
	    return answer;
	}    

	public static void down(int m, int n, char[][] map) {

	    for (int i = m-1; i >= 0 ; i--) {
	        for (int j = 0; j < n; j++) {
	            if(map[i][j] == '.') continue;

	            int nx = i;
	            char c = map[i][j];
	            map[i][j] = '.';
	            while(true) {
	                if(nx+1 >= m || map[nx+1][j] != '.') break;
	                nx++;
	            }
	            map[nx][j] = c;
	        }
	    }
	}

}
```

---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/17679)

---
