---
title: "Algorithm, programmers, 베스트 앨범(42579)"
date: 2019-12-28 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, hash, Comparator ]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 배운점
- 해시를 대충 알고있었는데 다시 공부해야겠다 공부의 연속...
- string은 == 으로 비교할수없고 equals로 구분해야한다. 실수금지

### 풀이
1. 노래를 구분하기 위해 id값을 추가한 song 클래스를 만들어준다

```java
 class song {
   int id;
   String genre;
   int plays;
   song(int id, String genre, int plays){
     this.id = id;
     this.genre = genre;
     this.plays = plays;
   }
 }
```

2. 장르별로 총 재생수를 해시로 구현하고, song객체를 ArrayList에 넣는다

```java
List<song> songList = new ArrayList<>();
Map<String, Integer> generPlay = new HashMap<>();

int play = 0;
for (int i=0; i<size; i++) {
  songList.add( new song(i, genres[i], plays[i]));
  if (generPlay.containsKey(genres[i]))
    play = generPlay.get(genres[i]) + plays[i];
  else
    play = plays[i];

  generPlay.put(genres[i], play);
}
```

3. 노래 리스트를 정렬한다
  - 장르가 같은것꺼리 묶고
  - 장르가 같다면 재생수가 큰순으로 정렬

```java
Comparator<song> Comp = new Comparator<song>() {
  public int compare(song a, song b) {
    // 장르가 같다면 재생수가 큰순으로 (int)
    if(a.genre.equals(b.genre))
      return b.plays - a.plays;
    // 장르별로 정리 (string)
    return a.genre.compareTo(b.genre);
  }
};
songList.sort(Comp);
```

4. 장르 - 총재생곡의 해시를 재생곡이 많은 순으로 정렬한다

```java
Iterator it = sortByValue(generPlay).iterator();	// 총재생수가 큰 장르순으로 정렬

public static List sortByValue(final Map map) {

    List<String> list = new ArrayList();
    list.addAll(map.keySet());

    Collections.sort(list,new Comparator() {

        public int compare(Object o1,Object o2) {
            Object v1 = map.get(o1);
            Object v2 = map.get(o2);

            return ((Comparable) v1).compareTo(v2);
        }

    });

    Collections.reverse(list); // 주석시 오름차순
    return list;
}
```

5. 장르 - 총재생곡의 해시를 돌며 각 장르당 2곡씩 정답 ArrayList에 담는다.

```java
Iterator it = sortByValue(generPlay).iterator();	// 총재생수가 큰 장르순으로 정렬
List<Integer> answer2 = new ArrayList<>();
while(it.hasNext()) {
      String key = (String) it.next();
      int num = 0;
      for (int i=0; i<size; i++) {
        // 장르별로 2곡까지만 뽑는다
        if (songList.get(i).genre.equals(key) && num < 2) {
          answer2.add(songList.get(i).id);
          ++num;
        }
      }
  }
```

---

### 전체코드

```java
package org.programmers;

import java.util.*;

import org.programmers.kakao_2019_Tree_findWay.Node;

public class test42579_bestAlbum {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		String[] genres = {"classic", "pop", "classic", "classic", "pop"};
		int[] plays = {500, 600, 150, 800, 2500};

		test42579_bestAlbum t = new test42579_bestAlbum();
		t.solution(genres, plays);

	}

	class song {
		int id;
		String genre;
		int plays;
		song(int id, String genre, int plays){
			this.id = id;
			this.genre = genre;
			this.plays = plays;
		}
	}

	Comparator<song> Comp = new Comparator<song>() {
		public int compare(song a, song b) {
			// 장르가 같다면 재생수가 큰순으로 (int)
			if(a.genre.equals(b.genre))
				return b.plays - a.plays;
			// 장르별로 정리 (string)
			return a.genre.compareTo(b.genre);
		}
	};


    public int[] solution(String[] genres, int[] plays) {

    	int size =  genres.length;

    	List<song> songList = new ArrayList<>();
    	Map<String, Integer> generPlay = new HashMap<>();

    	int play = 0;
    	for (int i=0; i<size; i++) {
    		songList.add( new song(i, genres[i], plays[i]));
    		if (generPlay.containsKey(genres[i]))
    			play = generPlay.get(genres[i]) + plays[i];
    		else
    			play = plays[i];

    		generPlay.put(genres[i], play);
    	}

    	songList.sort(Comp);

    	Iterator it = sortByValue(generPlay).iterator();	// 총재생수가 큰 장르순으로 정렬
    	List<Integer> answer2 = new ArrayList<>();
    	while(it.hasNext()) {
            String key = (String) it.next();
            int num = 0;
            for (int i=0; i<size; i++) {
            	// 장르별로 2곡까지만 뽑는다
            	if (songList.get(i).genre.equals(key) && num < 2) {
            		answer2.add(songList.get(i).id);
            		++num;
            	}
            }
        }

    	int[] answer = new int[answer2.size()];
    	for (int i=0; i<answer2.size(); i++) {
    		answer[i] = answer2.get(i);
    		System.out.print(answer[i]+" ");
    	}


        return answer;
    }

    public static List sortByValue(final Map map) {

        List<String> list = new ArrayList();
        list.addAll(map.keySet());

        Collections.sort(list,new Comparator() {

            public int compare(Object o1,Object o2) {
                Object v1 = map.get(o1);
                Object v2 = map.get(o2);

                return ((Comparable) v1).compareTo(v2);
            }

        });

        Collections.reverse(list); // 주석시 오름차순
        return list;
    }
}

```

---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/42579)

---
