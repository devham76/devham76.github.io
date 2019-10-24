---
title: "WEB, jsp, 액션태그"
date: 2019-10-24 15:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
---
#### 액션태그
- jsp페이지 내에서 어떤 동작을 하도록 지시하는 태그
- ex. 페이지 이동, 페이지 포함(include) 등

##### foward
- 현재페이지에서 다른 페이지로 전환할 때 사용
```java
<jsp:forward page="action_forward.jsp" />
```
##### include
- 페이지내에 다른 페이지 삽입시 사용
```java
<jsp:include page="includeex.jsp" flush="true" />
```

---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1171>
