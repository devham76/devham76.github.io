---
title: "Algorithm, programmers, 42576(완주하지못한선수), 해싱"
date: 2019-10-30 12:30:28 -0400
categories: Algorithm문제풀이
tags : [Algorithm, 문제풀이, 해싱]
---

##### 빠른 풀이
```java
public static String solution(String[] participant, String[] completion) {
  Arrays.sort(participant);
  Arrays.sort(completion);
  int i;
  for (i=0; i<completion.length; i++) {
    if(!participant[i].equals(completion))
      return participant[i];
  }
  return participant[i];
}
```
##### 해시 풀이
```java
package org.programmers;

import java.util.HashMap;
import java.util.Map;

public class marathon {

	public static void main(String[] args) {
		String[] p = {"leo", "kiki", "eden"};
		String[] c = {"eden", "kiki"};

		solution(p,c);
	}
    public static String solution(String[] participant, String[] completion) {
        String answer = "";
        int val = 0;

        Map<String, Integer> hm = new HashMap<>();

        for (String part:participant) {
        	// 해시맵에 해당 key에대한 value값이 없다면
        	if(hm.get(part) == null)
        		hm.put(part,1);
        	else {
        		val = hm.get(part) + 1;
        		hm.put(part, val);
        	}
        }

        // 참여자중에 완주자는 value를 0으로 한다
        for (String comp:completion) {
        	val = hm.get(comp) -1;
        	hm.put(comp, val);
        }

        // value가 1이면 완주자가 아니다
        for (String key:hm.keySet()) {
        	if(hm.get(key)==1) answer = key;
        }
        return answer;
    }
}
```
---
## Reference
[문제로 가기](https://www.welcomekakao.com/learn/courses/30/lessons/42576)
[문제 풀이](https://dreamhollic.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C-%ED%92%80%EC%9D%B45-%EC%99%84%EC%A3%BC%ED%95%98%EC%A7%80-%EB%AA%BB%ED%95%9C-%EC%84%A0%EC%88%98-JAVA)
