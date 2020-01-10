---
title: "Spring, TDD & Unit test 개념"
date: 2019-12-16 15:30:28 -0400
categories: [testcode]
tags : [testcode]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## TDD의 정의
- Test Driven Development
  - 테스트 주도 개발 : <b>테스트가 개발을 이끌어 나간다</b>
### TDD의 개념
- 테스트를 먼저 만들고 테스트를 통과하기 위한 코드를 작성하는 것.

### 레드 그린 사이클
- RED 항상 실패하는 테스트를 먼저 작성하고
- GREEN 테스트가 통과하는 프로덕션 코드를 작성하고
- Refactor 테스트가 통과하면 프로턱션 코드를 리팩토링한다

---
## Unit Test
- TDD의 첫번째 단계인 <b>기능 단위의 테스트 코드를 작성</b>하는 것을 이야기한다.
- 테스트 코드를 먼저 작성 x , 리팩토링 포함 x
### 단위 테스트의 장점
1. <b>톰캣을 내렸다가 다시 실행하는 일 반복 하지 않아도 된다.</b>
2. System.out.println()을 통해 눈으로 검증하지 않아도 된다.
  - 테스트 코드를 작성하면 더는 사람이 눈으로 검증하지 않게 <b>자동검증</b>이 가능하다
3. <b>개발자가 만든 기능을 안전하게 보호</b>해준다
  - 하나의 기능을 추가할 때마다 <b>서비스의 모든 기능을 테스트 할수는 없다</b> 따라서 <b>기존 기능이 잘 작동되는 것을 보장</b>하게 해준다.


---
## Reference
- 스프링 부트와 AWS로 혼자 구현하는 웹 서비스
- <https://gmlwjd9405.github.io/2018/06/03/agile-tdd.html>
