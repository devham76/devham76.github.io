---
title: "WEB, 실전jsp강좌, JSTL"
date: 2019-12-09 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP, JSTL]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### JSTL(JSP standard Tag Library)
- <u>JSP의 경우 HTML 태그와 같이 사용되서 전체적인 코드의 가독성이 떨어진다.</u>
- 이러한 단점을 보완하고자 만들어진 태그 라이브러리가 JSTL이다.
- JSTL은 Tomcat컨테이너에 포함되어 있지 않으므로 별도의 설치가 필요하다.

### 제공되는 라이브러리
1. Core , <c:tag
2. XML Processing , <x:tag
3. I18N formatting , <fmt:tag , 날짜형식이나 글자깨짐등에 사용
4. SQL , <sap:tag
5. Function, fn:functio()

### Core
- 기본적인 라이브러리로 출력,제어문,반복문 같은 기능이 포함되어있다

```java
<%@ taglib uri="http://jva.sun.com/jsp/jstl/core" prefix="c" %>
```

- prefix="c" 여기서부터는 Core라이브러리를 사용하겠다는 의미이다


---
## Reference
- <https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1184>
