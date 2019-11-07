---
title: "Algorithm, programmers, 단어변환(43163)"
date: 2019-11-08 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, bfs]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 풀이
- 시작이 같고, 시작으로 부터 가장 짧은 해결책을 찾는것이므로 넓이 우선탐색을 하여 답에 도달하면 끝내는 방법을 택해야 했다.
- 두 단어를 비교하는 방법이 여러가지가 있을수 있는데
    - 내 방법은 같은 위치에서 한 글자를 빼서 같은지 비교하는것
    - 다른 사람 방법은 두 단어의 차이가 1개 초과 인지 확인하는 법
    - 내 방법이 더 복잡하다 ㅠㅠ
- 내 풀이는 너무 직관적이다.. 어떤 자료 구조와 알고리즘을 사용할 수 있는지 더 고민해보자 !!

---
### 다른 사람 풀이
``` java
package org.programmers;
import java.util.LinkedList;
import java.util.Queue;

public class Level3_beginTarget_43163_2 {
	public static void main(String[] args) {
		String b = "hit";
		String t = "cog";
		String[] words = {"hot", "dot", "dog", "lot", "log", "cog"};

		solution(b,t,words);

	}

    static class Node {
        String next;
        int edge;

        public Node(String next, int edge) {
            this.next = next;
            this.edge = edge;
        }
    }

    public static int solution(String begin, String target, String[] words) {
        int n = words.length;
        int ans = 0;
        boolean[] visit = new boolean[n];

        Queue<Node> q = new LinkedList<>();
        q.add(new Node(begin, 0));

       //BFS
        while(!q.isEmpty()) {
            Node cur = q.poll();
            // 현재 고른 단어가 타겟과 같으면, 엣지를 반환하고 끝이난다.
            // 넓이 우선 탐색이므로 가장 짧은 값은 가장 먼저 반환 한 된 값이다!!!
            if (cur.next.equals(target)) {
                ans = cur.edge;
                break;
            }

            for (int i=0; i<n; i++) {
                if (!visit[i] && isNext(cur.next, words[i])) {
                    visit[i] = true;
                    q.add(new Node(words[i], cur.edge + 1));
                }
            }
        }
        System.out.println(ans);
        return ans;
    }

    static boolean isNext(String cur, String n) {
        int cnt = 0;
        for (int i=0; i<n.length(); i++) {
            if (cur.charAt(i) != n.charAt(i)) {
            	// 두 단어의 다른 글자가 1개 초과 이면 거짓을 반환.
                if (++ cnt > 1) return false;
            }
        }
        return true;
    }    
}
```

### 내 풀이
```java
package org.programmers;

public class Level3_beginTarget_43163 {

	public static void main(String[] args) {
		String b = "hit";
		String t = "cog";
		String[] words = {"hot", "dot", "dog", "lot", "log", "cog"};

		solution(b,t,words);
	}
	static int answer = 0;
	public static int solution(String begin, String target, String[] words) {

		boolean[] visited = new boolean[words.length];

		fun(begin, 0, visited, words, target);
		System.out.println(answer);
		return answer;
	}
	public static void fun(String begin, int cnt, boolean[] visited, String[] words, String target) {
		// 한 단어의 한글자씩 변경하므로, 글자수만큼 돈다.
		for (int i=0; i<begin.length(); i++) {

			String s1 = begin.substring(0, i) + begin.substring(i+1, begin.length());

			for(int j=0; j<words.length;  j++) {
				String s2 = words[j].substring(0, i) + words[j].substring(i+1, words[j].length());
				if(visited[j] == true)
					continue;
				// 한글자를 제외한 두단어가 같다면
				if(s2.equals(s1)) {
					// 비교하는 글자가 타겟이라면  비교 끝
					if(words[j].equals(target)) {
						answer = (answer == 0 ) ? cnt+1 : (answer > cnt+1) ? cnt+1 :answer;
						System.out.println("---->"+answer);
					}
					else {

						visited[j] = true;
						fun(words[j], cnt+1, visited, words, target);
						visited[j] = false;
					}
				}
			}
		}
	}
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/43163>
---
