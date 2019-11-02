---
title: "Algorithm, programmers, 카카오2020(오픈채팅방-42888)"
date: 2019-11-02 13:00:28 -0400
categories: Algorithm
tags : [Algorithm]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

- 아이디와 닉네임을 key, value로 묶어 해시를 이용했다

### 내 풀이
```java
package org.programmers;

import java.util.ArrayList;
import java.util.HashMap;

public class kakao_2020_openchat {

	public static void main(String[] args) {
		String[] record = {
				"Enter uid1234 Muzi",
				"Enter uid4567 Prodo",
				"Leave uid1234",
				"Enter uid1234 Prodo",
				"Change uid4567 Ryan"
		};

		solution(record);

	}
	public static String[] solution(String[] record) {
		ArrayList<String> answer = new ArrayList<String>();
		HashMap<String, String> user = new HashMap<>();
		for (int i=0; i<record.length; i++) {
			String[] splitRecord = record[i].split(" ");
			// 명령문 비교
			switch (splitRecord[0]) {
			//아이디, 닉네임
			case "Enter" :
				//if ( !user.containsKey(splitRecord[1]) )
				user.put(splitRecord[1], splitRecord[2]);
				break;
			case "Change" :
				user.put(splitRecord[1], splitRecord[2]); break;
			}
		}

		for (int i=0; i<record.length; i++) {
			String[] splitRecord = record[i].split(" ");
			String nickName = user.get( splitRecord[1] );
			switch (splitRecord[0]) {
			case "Enter" :
				answer.add(nickName+"님이 들어왔습니다."); break;
			case "Leave" :
				answer.add(nickName+"님이 나갔습니다."); break;
			}}

		String[] array = new String[answer.size()];

		for (int i=0; i<answer.size(); i++)
			array[i] = answer.get(i);

		return array;
	}
}
```

### 다른 사람 풀이
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

public class Solution {
    public String[] solution(String[] record) {
        HashMap<String, String> codeMap = new HashMap<String, String>();
        codeMap.put("enter","들어왔습니다.");
        codeMap.put("leave","나갔습니다.");

        HashMap<String, String> uidMap = new HashMap<String, String>();
        List<String> list = new ArrayList<String>();
        for(String str:record){
            String[] split = str.split("\\s+");
            String code = split[0];
            String uid = split[1];
            if(split.length > 2) {
                String name = split[2];
                uidMap.put(uid, name);
            }
            if(!"Change".equalsIgnoreCase(code)){
                list.add(code +" "+uid);
            }

        }
        String[] answer = new String[list.size()];
        for(int i=0;i<answer.length;i++){
            String[] split = list.get(i).split("\\s+");
            String name = uidMap.get(split[1]);
            answer[i] = name+"님이 "+ codeMap.get(split[0].toLowerCase());
        }

        return answer;
    }
}
```

### 깨달은점
- 헉, 명령어와 출력을 key와 value 값으로 묶을 생각은 못했다.


---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/42888)
