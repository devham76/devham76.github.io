---
title: "Algorithm, programmers, 카카오2019(실패율-42889)"
date: 2019-11-02 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, comparable, 정렬]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- Comparable 인터페이스를 사용하여 정렬 한다
- int/double = int 로 나오기때문에 double로 형변환 필요


```java
package org.programmers;

import java.util.ArrayList;
import java.util.Collections;

public class kakao_2019_failPercentage {

	public static void main(String[] args) {
		int[] stages = {2, 1, 2, 6, 2, 4, 3, 3};
		solution(5, stages);
		int[] stages2 = {4,4,4,4,4};
		solution(4, stages2);
	}

    public static int[] solution(int N, int[] stages) {
        int[] answer = new int[N];
        int[] stagearr = new int[N+2];	// 스테이지별 사람을 구한다
        ArrayList<stage> stageArr = new ArrayList<>();	// 스테이지별 사람, 스테이지, 실패율 클래스
        int manAllCnt = 0;	 // 총 인원

        // 스테이지별 사람을 구한다.
        for (int i=0; i<stages.length; i++){
        	stagearr[ stages[i] ] ++;
        	manAllCnt++;
        }
        // 스테이지, 스테이지별사람, 실패율을 저장
        for( int i=1; i<stagearr.length-1; i++) {
        	// int/double = int 로 나오기때문에 double로 형변환 필요
        	stageArr.add( new stage(i, stagearr[i], (double)stagearr[i] / manAllCnt) );
        	manAllCnt -= stagearr[i];
        }

        // 실패율에 따라서 오름차순 정렬
        Collections.sort(stageArr);

        for (int i=0; i<stageArr.size(); i++){
        	answer[i] = stageArr.get(i).getSeq();
        }

        return answer;
    }
}
class stage implements Comparable<stage>{
	int seq;
	int manCnt;
	double percentage;
	public stage(int seq, int manCnt, double percentage){
		this.seq =seq;
		this.manCnt = manCnt;
		this.percentage = percentage;
	}

	public int getSeq() {
		return this.seq;
	}
	public double getPercentage() {
		return this.percentage;
	}
	// 실패율에 따라서 오름차순 정렬
    public int compareTo(stage s) {
        if (this.percentage > s.getPercentage()) {
            return -1;
        } else if (this.percentage < s.getPercentage()) {
            return 1;
        }
        return 0;
    }
}
```

---
## Reference
- [문제보러가기] : <https://www.welcomekakao.com/learn/courses/30/lessons/42889>
---
