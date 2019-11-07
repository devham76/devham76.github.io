---
title: "Algorithm, programmers, 타겟넘버"
date: 2019-11-07 13:00:28 -0400
categories: Algorithm
tags : [Algorithm]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- 첫번째~마지막 숫자를 더하거나 빼는 경우의 수가 있으므로 두가지의 경우를 재귀적으로 실행한다
- 최종결과가 타겟과 같으면 answer+1

```java
package org.programmers;

public class Level2_targetNumber_43165 {

	public static void main(String[] args) {
		int[]  n = {1,1,1,1,1};
		int target = 3;
		solution(n, target);

	}
	static int answer = 0;
    public static int solution(int[] numbers, int target) {


        fun(numbers, target, 0, 0);
        System.out.println(answer);
        return answer;
    }
    public static void fun(int[] numbers, int target, int cnt, int current) {
    	if(cnt == numbers.length) {
    		if(current == target)
    			answer++;
    	}
    	else {
    	  fun(numbers, target, cnt+1, current+numbers[cnt]);
    	  fun(numbers, target, cnt+1, current-numbers[cnt]);
    	}
    }
}
```

### 다른사람 풀이
```java
class Solution {
    public int solution(int[] numbers, int target) {
        int answer = 0;
        answer = dfs(numbers, 0, 0, target);
        return answer;
    }
    int dfs(int[] numbers, int n, int sum, int target) {
        if(n == numbers.length) {
            if(sum == target) {
                return 1;
            }
            return 0;
        }
        return dfs(numbers, n + 1, sum + numbers[n], target) + dfs(numbers, n + 1, sum - numbers[n], target);
    }
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/43165>
