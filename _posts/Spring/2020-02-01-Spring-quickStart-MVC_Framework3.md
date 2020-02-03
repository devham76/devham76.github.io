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

## @ModelAttribute
- @ModelAttribute가 설정된 메소드는 @RequestMapping 어노테이션이 적용된 메소드보다 먼저 호출된다.
- @ModelAttribute 메소드 실행 결과로 리턴된 객체는 <u>자동으로 Model에 적용</u>되고, <u>View 페이지에서 사용할 수 있다.</u>

### 예제
- BoardController.java
: 검색조건을 만들어서 view에서 사용한다

```java
@ModelAttribute("conditionMap")
public Map<String, String> searchConditionMap(){
  Map<String, String> conditionMap = new HashMap<>();
  conditionMap.put("제목", "TITLE");
  conditionMap.put("작성자", "WRITER");
  conditionMap.put("내용", "CONTENT");
  return conditionMap;
}

@RequestMapping("/getBoardList.do")
public String getBoardList( @RequestParam(value="searchCondition", defaultValue="TITLE", required=false) String condition,
    @RequestParam(value="searchKeyword", defaultValue="", required=false) String keyword,
    BoardDAO boardDao, BoardVO vo, Model model) {
  // 3. 결과값을 model에 저장, 이동할곳(view)을 리턴
  model.addAttribute("boardList", boardDao.getBoardList());
  return "getBoardList.jsp";
}
```

- getBoardList.jsp

```html
<select name="searchCondition">
<!-- @ModelAttribute활용 -->
<c:forEach items="${conditionMap}" var="option">
  <option value="${op tion.value}">${option.key}</option>
</c:forEach>
</select>
```

## @SessionAttributes
- <u>Model에 저장되어있는 데이터가 있다면 그 데이터를 세션(HttpSession)에도 자동으로 저장하라는 설정</u>

### 예제_글 update하기
- 글 상세 정보를 가져올때 Model에 board라는 이름으로 게시글의 정보를 입력한다
- <u>@SessionAttributes("board")에 의해서 Model에 저장되어있는 board데이터를 세션에 저장</u>한다
- 글 수정시에 @ModelAttribute("board") BoardVO vo 에서 세션에 저장되어있는 board를 vo에 할당한다


```java
@Controller
@SessionAttributes("board")
public class BoardController {
  @RequestMapping("/getBoard.do")
	public String getBoard(BoardVO vo, BoardDAO boardDao, Model model) {
		System.out.println("글 상세보기 처리");
		model.addAttribute("board", boardDao.getBoard(vo));		// Model 정보 저장
		return "getBoard.jsp";	// 이동할 View는 String으로 처리
	}

  @RequestMapping("/updateBoard.do")
public String updateBoard(@ModelAttribute("board") BoardVO vo, BoardDAO boardDao, ModelAndView mav) {
  System.out.println("글 수정 처리");
  boardDao.updateBoard(vo);
  return "getBoardList.do";
}

}
```



---
## Reference
- 스프링 퀵 스타트-채규태 지음
