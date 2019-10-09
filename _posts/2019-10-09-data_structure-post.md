---
title: "Data Structure, JAVA, array/arraylist/linkedlist"
date: 2019-10-09 13:30:28 -0400
categories: Data Structure
tags : [Data Structure, JAVA]
---
Array / ArrayList / LinkedList
=============
## 1. Array vs ArrayList
### 배열 (Array)
- 배열의 크기는 한번 정하면, 변경할 수 없다.
 - int[] arr = new inte[3];
- 배열 초기화시 메모리에 할당되어 ArrayList보다 속도가 빠르다.
- 다차원 생성이 가능하다.
 - int[][] multi = new int[2][2][2];
- 정렬 : Arrays.sort(arr);
### ArrayList
- *크기가 가변적이다.*
- *데이터 추가,삭제시 메모리를 재할당하기 때문에 속도가 배열보다 느리다.*
- 다차원 생성이 불가능하다.
- 정렬 : Collections.sort(arraylist);
 예제
- ArrayList<Integer> arraylist = new ArrayList<Integer>();
* *add*
 arraylist.add(1);
 두번 째 위치에 2 삽입 : arraylist.add(1, 2);
* *get*
 두번째 값을 구하고 싶다면 : arraylist(1);
* *size*
  ArrayList의 개수를 리턴한다. : arraylist.size();
* *contains*  
  contains 메소드는 리스트 안에 해당 값이 있는지 검색 후 boolean 값으로 리턴
* *remove*
  remove(객체) : 삭제결과 boolen으로 리턴
  remove(index) : 삭제 후 삭제된 항목 리턴
  
---
## 2. ArrayList vs LinkedList

![arraylist_linkedlist](https://user-images.githubusercontent.com/55946791/66452386-4467e200-ea9b-11e9-8c26-8e25ead10e62.JPG)

### ArrayList
- 구조 : 데이터들이 순서대로 쭉 늘어선 구조
- 삽입, 삭제시 자료의 최대 개수에 영향을 받는다. O(n)
- ArrayList는 크기가 한정되어있다
- <u>검색 : 무작위 접근이 가능해서 LinkedList보다 빠르다.</u>
### LinkedList
- 구조 : 자료의 주소 값으로 서로 연결되어 있는 구조
- <u>삽입,삭제를 빠르게 수행 할 수 있다.</u>
- 무한 개수의 자료 삽입 가능. (메모리 용량 무한정 이라면)
- 검색 : 순차 접근만이 가능해서 ArrayList보다 느리다.
---
## Reference
<http://blog.naver.com/PostView.nhn?blogId=sangrime&logNo=220622445166>
<http://www.nextree.co.kr/p6506/>
