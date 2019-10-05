---
title: "Algorithm, programmers, 49993(윈터코딩_스킬트리)"
date: 2019-10-05 13:30:28 -0400
categories: Algorithm문제풀이
tags : [Algorithm, JAVA, 문제풀이]
---
난이도 중 / 문제 풀이 완료 못함.

```java
package org.programmers;

public class wintercoding_2018_49993 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		// "CBD"	["BACDE", "CBADF", "AECB", "BDA"]	2
		String skill = "CBD";
		String[] skill_trees = {"BACDE", "CBADF", "AECB", "BDA"};
		solution(skill, skill_trees);
	}
    public static int solution(String skill, String[] skill_trees) {
        int answer = 0;
        
        for ( int i=0; i<skill_trees.length; i++ ) {
        	System.out.println(skill_trees[i]);
        	boolean isOk = true;
        	
        	for ( int j=0; j<skill.length()-1; j++ ) {
        		int s1 = skill_trees[i].indexOf( skill.charAt(j) );
        		int s2 = skill_trees[i].indexOf( skill.charAt(j+1) );
        		System.out.println("j : "+j+" / s1:"+s1+" s2:"+s2);
        		
        		// case 1: 마지막 원소가 -1일땐 마지막 안본다.
        		if (j == skill.length()-2 && s2 == -1) {
        			isOk = true;
        		} 
        		// case 2: 첫번째 원소가 -1일땐 거짓.
        		else if (j==0 && s1 == -1 && s1 < s2) {
        			isOk=false; break;
        		}
        		// case 3: 위치를 비교한다.
        		else {
        			if ( s1 > s2 ) {	
        				isOk=false; break;
        			}
        			else {
        				isOk=true;
        			}
        		}
        	}
        	
        	if(isOk == true) { 
        		System.out.println("--->"+skill_trees[i]);
        		answer++;
        	}
        }
        System.out.println(answer);
        return answer;
    }
}
```


---
## Reference 
[문제로 가기](https://programmers.co.kr/learn/courses/30/lessons/49993#fn1)
[문제풀이 참고](https://m.blog.naver.com/PostView.nhn?blogId=yongyos&logNo=221572139348&categoryNo=39&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
