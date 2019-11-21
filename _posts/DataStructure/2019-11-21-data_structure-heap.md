---
title: "Data Structure, heap"
date: 2019-11-21 13:30:28 -0400
categories: DataStructure
tags : [DataStructure, heap, tree]
---

#### 들어가기 전
- 스택(stack) : 먼저들어온게 나중에 나간다
- 큐 (queue) : 먼저들어온게 먼저 나간다
- 우선순위 큐(priority queue) : 가장 우선순위가 높은게 먼저 나간다
- 우선순위 큐는 배열, 연결리스트, 힙으로 구현 가능하다.

---

### 힙'heap' 이란?
- 최댓값, 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 <b>완전 이진트리</b>를 기본으로 한 자료구조이다.
- 우선순위 큐를 위하여 만들어진 자료구조이다.
- 힙은 일종의 <b>반 정렬 상태(느슨한 정렬 상태)</b>를 유지한다.
    - 큰 값이 상위 레벨에 있고 작은 값이 하위 레벨에 있다는 정도
    - 간단히 말하면 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰 (작은) 이진 트리를 말한다.
- 힙 트리에서는 중복된 값을 허용한다. (이진 탐색 트리에서는 중복된 값을 허용하지 않는다.)

---
### 힙의 종류
![types-of-heap](https://user-images.githubusercontent.com/55946791/69312073-4cf23180-0c71-11ea-8e0e-51fcd6e9153f.png)

---
### 힙의 구현
- 힙을 저장하는 표준적인 자료구조는 <b>배열</b>
- 구현을 쉽게 하기 위해 index 0은 사용 안한다
- 힙에서의 부모 노드와 자식 노드의 관계
    - 왼쪽 자식 = 부모 * 2
    - 오른쪽 자식 = 부모 * 2 + 1
    - 부모 = 자식 / 2
    ![heap-index-parent-child](https://user-images.githubusercontent.com/55946791/69312190-9b9fcb80-0c71-11ea-97fa-f8dcc5ae078b.png)

---
### 힙의 삽입
![maxheap-insertion](https://user-images.githubusercontent.com/55946791/69312255-c558f280-0c71-11ea-90e4-30e44e1df2cd.png)

---
### 힙의 삭제
![maxheap-delete](https://user-images.githubusercontent.com/55946791/69312311-e0c3fd80-0c71-11ea-9ac3-60fc43538c15.png)



---
## Reference
<https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html>
