---
title: "Algorithm, JAVA, 퀵정렬"
date: 2019-10-01 17:30:28 -0400
categories: Algorithm
tags : [Algorithm, 퀵정렬]
---
## **퀵정렬**
- 리스트 가운데서 하나의 원소를 고름(pivot 선정)
- pivot 앞에는 pivot보다 작은 값이 오고, pivot 뒤에는 pivot보다 큰 값들이 오도록 리스트를 둘로 분할한다.
- 분할된 두 개의 리스트에 대해 재귀함수를 통해 이 과정을 반복한다.
- 시간복잡도 : 최악 O(n^2), 평균 O(nlogn)

![퀵정렬](https://user-images.githubusercontent.com/55946791/65944688-3c8db980-e46d-11e9-8cda-f306bab7ba80.JPG)
```java
	static void swap(int[] a, int idx1, int idx2) {
		int tmp = a[idx1]; a[idx1] = a [idx2]; a[idx2] = tmp;
	}

	static void quickSort(int[] a, int left, int right) {
		int pl = left;			//왼쪽 커서
		int pr = right;			//오른쪽 커서

		int x = a[ (pl+pr)/2 ];	//피벗

		do {
			while(pl < x) pl++;
			while(pr > x) pr--;
			if(pl <= pr)
				swap(a, pl++, pr--);
		}while( pl<= pr ); 		// pl과 pr이 교차되면 중지.

		// 배열을 반복해서 나눠서 정렬한다.
		if(left < pr)	quickSort(a, left, pr);
		if(right > pl)	quickSort(a, pl, right);
	}
```
---

## Reference
[do it 자료구조와 함께 배우는 알고리즘 입문 자바 편](http://book.interpark.com/product/BookDisplay.do?_method=detail&sc.prdNo=283580014&gclid=Cj0KCQjw8svsBRDqARIsAHKVyqEKmI3030BpfA7WAFrW163sLmdXDpJxoT6Dex9SIQZkFdYVPZ7tz4QaAo95EALw_wc)


---
