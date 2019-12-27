---
title: "Algorithm, programmers, 카카오2019(길 찾기 게임-42892)"
date: 2019-11-02 13:00:28 -0400
categories: Algorithm
tags : [Algorithm, 트리, 이진트리, Comparator ]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 배운점
- 트리를 직접 구현해본적이 없어서 어려웠다 자료구조를 구현해보는 공부가 필요하다
- Comparator 구현을 많이 해봐야 겠다

### 풀이
1. 노드를 생성한다
  - id : 입력되는 순서
  - x,y : 입력되는 좌표값
  - left, right : 트리를 구현하기 위한 변수

```java
class Node{
  int id;
  int x,y;
  Node left;
  Node right;

  Node(int id, int x, int y){
    this.id = id;
    this.x = x;
    this.y = y;
  }
}
```
2. 입력받은 노드들을 y좌표에 따라 레벨을 나누고, x좌표에 따라 왼쪽/오른쪽 자식으로 구분하기 위해 우선 리스트에 입력한다

```java
List<Node> Nodes = new ArrayList<Node>();

for (int i=0; i<size; ++i) {
  Nodes.add(new Node(i+1, nodeinfo[i][0], nodeinfo[i][1]));
}
```

3. y,x값에 따라서 노드들을 정리해준다

```java
// y의 내림차순, y가 같으면 x의 오름차순으로 정리한다
Nodes.sort(Comp);
// y값이 작은게 우선이고, y값이 같다면 x값이 작은게 우선이다
Comparator<Node> Comp = new Comparator<Node>() {
  public int compare(Node a, Node b) {
    if(a.y == b.y)
      return a.x - b.x;	// x가 작은 값이 앞으로 온다

    return b.y - a.y;
  }
};
```

4. 정리된 노드리스트를 가지고 이진 트리를 만들어준다
- 자식의 x값이 부모의 x값보다 작을때 부모의 왼쪽 자식이 된다
- <b>그런데 부모의 왼쪽 자식이 이미 있다면 부모의 왼쪽 자식의 자식으로 만든다</b>

```java
// 노드들로 트리를 만들어준다
void addNode(Node parent, Node child) {
  if(child.x < parent.x) {
    if(parent.left == null)
      parent.left = child;
    else	// 이미 자식이있으므로 해당 자식의 자식으로 만든다 !!! (이부분이 어려웠음)
      addNode(parent.left, child);
  }
  else {
    if(parent.right == null)
      parent.right = child;
    else
      addNode(parent.right, child);
  }
}
```

5. 전위,후위 순회

```java
int idx; // 전역변수
void preorder(int[][] answer, Node node) {
  if (node == null) return;
  answer[0][idx++] = node.id;
  preorder(answer, node.left);
  preorder(answer, node.right);
}
void postorder(int[][] answer, Node node) {
  if (node == null) return;
  postorder(answer, node.left);
  postorder(answer, node.right);
  answer[1][idx++] = node.id;
}
```

---

### 소스

```java
package org.programmers;

import java.util.*;
public class kakao_2019_Tree_findWay {

	public static void main(String[] args) {

		int[][] nodeinfo = {{5, 3}, {11, 5}, {13, 3}, {3, 5}, {6, 1},{1, 3}, {8, 6}, {7, 2}, {2, 2}};
		kakao_2019_Tree_findWay k = new kakao_2019_Tree_findWay();
		k.solution(nodeinfo);
	}

	// 노드의 생성 / id:삽입된 순서, x,y값을 각각 입력한다
	class Node{
		Node(int id, int x, int y){
			this.id = id;
			this.x = x;
			this.y = y;
		}
		int id;
		int x,y;
		Node left;
		Node right;
	}

	// answer에 순회하는 노드들을 담을때 순서를 지정해준다.
	int idx;
	// List : 순서가 있다
	List<Node> Nodes = new ArrayList<Node>();

	// y값이 작은게 우선이고, y값이 같다면 x값이 작은게 우선이다
	Comparator<Node> Comp = new Comparator<Node>() {
		public int compare(Node a, Node b) {
			if(a.y == b.y)
				return a.x - b.x;	// x가 작은 값이 앞으로 온다

			return b.y - a.y;
		}
	};

	// 노드들로 트리를 만들어준다
	void addNode(Node parent, Node child) {
		if(child.x < parent.x) {
			if(parent.left == null)
				parent.left = child;
			else	// 이미 자식이있으므로 해당 자식의 자식으로 만든다 !!! (이부분이 어려웠음)
				addNode(parent.left, child);
		}
		else {
			if(parent.right == null)
				parent.right = child;
			else
				addNode(parent.right, child);
		}
	}

	void preorder(int[][] answer, Node node) {
		if (node == null) return;
		answer[0][idx++] = node.id;
		preorder(answer, node.left);
		preorder(answer, node.right);
	}
	void postorder(int[][] answer, Node node) {
		if (node == null) return;
		postorder(answer, node.left);
		postorder(answer, node.right);
		answer[1][idx++] = node.id;
	}

	//-------
	//-- 구현
	//-------
    public int[][] solution(int[][] nodeinfo) {
    	int size = nodeinfo.length;

    	//-- 1. x,y값을 토대로 노드를 리스트에 넣는다
    	// 입력되는 값을 리스트에 입력한다
    	// 정렬되지 않은 상태로 list가 생성된다
    	for (int i=0; i<size; ++i) {
    		Nodes.add(new Node(i+1, nodeinfo[i][0], nodeinfo[i][1]));
    	}

    	// y의 내림차순, y가 같으면 x의 오름차순으로 정리한다
    	Nodes.sort(Comp);

    	//-- 2. 노드들로 트리를 생성한다
    	// 트리의 루트는 첫번째 노드가 된다.
    	Node root = Nodes.get(0);
    	for (int i=1; i<size; ++i) {
    		// 부모노드 , 새로운 노드
    		addNode(root, Nodes.get(i));
    	}

    	int[][] answer = new int[2][size];
    	preorder(answer, root);
    	idx = 0;
    	postorder(answer, root);


    	//------
    	// 값 확인용
    	for (int i=0; i<size; ++i) {
    		System.out.print(Nodes.get(i).id+ " ");
    	}
    	System.out.println();
    	for (int j=0; j<2; ++j) {
    		for (int i=0; i<size; ++i) {
    			System.out.print(answer[j][i]+ " ");
    		}
    		System.out.println();
    	}

        return answer;
    }

}
```

---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/lessons/42892)
- [동영상풀이](https://www.youtube.com/watch?v=J8YxDIauh1g)

---
