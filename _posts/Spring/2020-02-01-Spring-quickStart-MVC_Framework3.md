---
title: "Spring, Spring MVC, 애노테이션 이용하기 2"
date: 2020-02-01 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## @RequestParam

### Command객체
- Command 객체를 이용하면 클라이언트에서 넘겨준 요청 파라메터 정보를 받아낼 수 있다.
- 그러려면 반드시 요청 파라메터(BoardVO vo), 매핑될 변수(vo.seq), Setter메소드(SetSeq())가 Command(=DTO)클래스에 선언되어있어야 한다.

### @RequestParam
- <u>HttpServletRequest.getParameter() 와 같은 기능</u>
-
```java
@RequestParam(value="searchCondition", defaultValue="TITLE", required=false)
// value : 파라메터이름 , defaultValue : 기본 설정값, required : 파라메터 생략 여부
```

- 이 애노테이션을 이용하면 Command(=DTO) 객체에 없는 파라메터를 Controller클래스에서 사용할 수 있다.

### 예시
- 글 목록 화면에서 검색 조건, 검색 키워드를 설정하고 검색하는 상황
- <u>검색 조건과 키워드는 BoadVO의 변수가 아니다</u>
- /getBoardList.do에 매핑된 getBoard()가 실행될때 BoardVO를 Command객체로 사용할 수 없다.

```java
@RequestMapping("/getBoardList.do")
public String getBoardList( @RequestParam(value="searchCondition", defaultValue="TITLE", required=false) String condition,
    @RequestParam(value="searchKeyword", defaultValue="", required=false) String keyword,
    BoardDAO boardDao, BoardVO vo, Model model) {
  // 매개변수로 선언하면 컨테이너가 자동으로 객체생성해준다

  System.out.println("검색 조건 : "+ condition);
  System.out.println("검색 키워드 : " + keyword);
  // 3. 결과값을 model에 저장, 이동할곳(view)을 리턴
  model.addAttribute("boardList", boardDao.getBoardList());
  return "getBoardList.jsp";
}
```


---
## Reference
- 스프링 퀵 스타트-채규태 지음
