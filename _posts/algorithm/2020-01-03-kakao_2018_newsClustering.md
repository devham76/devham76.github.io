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
1. 내가 푼 풀이
 - 검색을 빨리 하기 위해 hashmap을 사용했고, str1, str2의 max,min을 구했다
 - 두개씩 쪼개는 부분이나 hashmap에 넣는것은 같은 동작이므로 함수로 구현하는게 좋을것같다
2. 다른 사람의 풀이
 - ArrayList로 구현했다. 합집합 = 전체집합 - 교집합 을 이용해서 빠르게 해결했다

---

### 내 풀이

```java
public int solution(String str1, String str2) {
  int answer = 0;

  HashMap<String, Integer> hm1 = new HashMap<>();
  HashMap<String, Integer> hm2 = new HashMap<>();

  List<String> stringArray1 = new ArrayList<>();
  List<String> stringArray2 = new ArrayList<>();

  str1 = str1.toLowerCase();
  str2 = str2.toLowerCase();

  // 두개씩 쪼개서 문자만 넣기
  String pattern = "^[a-zA-Z]*$";
  for (int i=0; i<str1.length()-1; i++) {
    String s1 = (String) str1.substring(i, i+2);
    if (Pattern.matches(pattern, s1) == true)
      stringArray1.add(s1);
  }
  for (int i=0; i<str2.length()-1; i++) {
    String s2 = (String) str2.substring(i, i+2);
    if (Pattern.matches(pattern, s2) == true)
      stringArray2.add(s2);
  }

  // <쪼갠것, 쪼갠것들 개수> 해쉬맵을 이용
  for (int i=0; i<stringArray1.size(); i++) {
    if ( hm1.containsKey(stringArray1.get(i)) ){
      hm1.put(stringArray1.get(i), hm1.get(stringArray1.get(i))+1 );
    }
    else
      hm1.put(stringArray1.get(i), 1);
  }

  for (int i=0; i<stringArray2.size(); i++) {
    if ( hm2.containsKey(stringArray2.get(i)) ){
      hm2.put(stringArray2.get(i), hm2.get(stringArray2.get(i))+1 );
    }
    else
      hm2.put(stringArray2.get(i), 1);
  }

  // str1, str2 각각에 중복된것이 있는지 찾기, 해쉬맵을 이용하여 검색을 빠르게 했다
  Iterator<String> keySetIterator = hm1.keySet().iterator();
  float max = 0, min = 0;
  while(keySetIterator.hasNext()) {
    String key = keySetIterator.next();
    // 중복된것이 있다면 최소, 최댓값을 찾고 str2에서 중복된것을 삭제한다
    if (hm2.containsKey(key) == true) {
      max += Math.max(hm1.get(key), hm2.get(key));
      min += Math.min(hm1.get(key), hm2.get(key));
      hm2.remove(key);
    }
    // 중복된것이 없다면 최소값은 0이고 최대값은 해당 값이다
    else {
      max += hm1.get(key);
    }
  }
  // 중복된것은 직전에 모두 삭제 했으므로 남은 것들을 돌며 최대값을 찾아준다
  keySetIterator = hm2.keySet().iterator();
  while(keySetIterator.hasNext()) {
    String key = keySetIterator.next();
      max += hm2.get(key);
  }

  if (min == 0 && max == 0)
    answer = 65536;
  else
    answer =  (int)Math.floor(min/max * 65536);

  return answer;
}
```

---

### 다른풀이

```java
public int solution(String str1, String str2) {

     List list1 = subset(str1.toLowerCase());
     List list2 = subset(str2.toLowerCase());

     int intersection = 0;

     List<Integer> check = new ArrayList<Integer>(); // 교집합 구할 떄, 중복제거

     for (int a = 0; a < list1.size(); a++) { // 교집합 개수 구하기
         String s1 = (String) list1.get(a);
         for (int b = 0; b < list2.size(); b++) {

             String s2 = (String) list2.get(b);
             // s1과 일치하는 s2가 있고, s2에 있는걸 넣은적이 없다면 추가한다
             if (s1.equals(s2) && !check.contains(b)) {
                 intersection++;
                 // s1과 일치 하는 s2를 찾으면 그 위치를 저장해서 다음 s1과 해당 값을 비교해서 같을때 또 다시 입력하지 않도록 한다.
                 check.add(b);
                 // s1과 일치하는 s2를 찾으면 교집합에 넣어주고 끝내고 다음 s1을 확인한다.
                 break;
             }

         }
     }

     // !!!!!!!!!왕충격....
     int union = list1.size() + list2.size() - intersection; // 합집합

     if (union == 0 && intersection == 0) {
         return 65536;
     }

     return (int) (((float) intersection / union) * 65536);
 }

 // 문자열 s의 다중집합
 public List subset(String s) {

     List<String> list = new ArrayList<String>();
     char[] arr = s.toCharArray();
     int size = arr.length - 1;
     String str;
     int start = 0;
     int end = 1;

     while (end <= size) {
         str = String.valueOf(arr[start]) + String.valueOf(arr[end]);
         boolean isMatch = Pattern.matches("^[a-z]*$", str); // 부분집합의 원소가 영어로만 구성되어 있는지 확인
         if (isMatch) {
             list.add(str);
         }
         start++;
         end++;

     }
     return list;
 }

```


---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/17677)
- [다른사람 풀이](https://kosaf04pyh.tistory.com/146)

---
