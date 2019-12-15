---
title: "JAVA, Comparable / Comparator"
date: 2019-10-09 13:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- 배열이나 Collection 프레임워크 등에서 sort()를 사용하면 컴퓨터가 알아서 정렬 해준다.
 - Arrays.sort(), Collection.sort()
- 여기서 사용되는 sort()는 Comparable 구현에 의해 정렬 된것이다.

*Comparable* : 기본 정렬기준을 구현하는데 사용
*Comparator* : 기본 정렬기준 외에, <u>다른 기준으로 정렬</u>하고자 할 때 사용

----
## 1. Comparable
- 기본 정렬기준 구현
![comparable](https://user-images.githubusercontent.com/55946791/66453747-6dd73c80-eaa0-11e9-8106-d0edf696e32b.png)

- 다른 기준으로 정렬 시
: <u>Comparable을 implements</u> 하고 하단에 <u>compareTo를 Override</u>하며 비교코드 생성해야함.

![comparable2](https://user-images.githubusercontent.com/55946791/66454201-18039400-eaa2-11e9-9531-3a62738b123a.JPG)


## 2. Comparator
- 객체내의 어떤 변수를 기준으로 정렬할지 정해야 한다.

![comparator](https://user-images.githubusercontent.com/55946791/66454677-75e4ab80-eaa3-11e9-86dd-a18abc6eb3f4.JPG)

---
## Reference
<https://cwondev.tistory.com/15>
