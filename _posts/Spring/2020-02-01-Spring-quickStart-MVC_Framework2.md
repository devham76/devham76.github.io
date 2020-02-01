---
title: "Spring, Spring MVC, 애노테이션 이용하기 1"
date: 2020-02-01 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### 1. @Controller 이용 전
- 반드시 스프링이 제공하는 <b>Controller 인터페이스를 구현</b> 해야한다
- 사용자 요청을 받는 DispatcherServlet이 모든 Controller의 <b>handleRequest()메소드</b>를 호출할 수 있도록 해야한다.

```java
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

public class InsertBoardController implements Controller {

	@Override
	public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) {
		System.out.println("글 등록 처리");
		String title = request.getParameter("title");
		String writer = request.getParameter("writer");
		String content = request.getParameter("content");

		BoardVO vo = new BoardVO();
		vo.setTitle(title);
		vo.setWriter(writer);
		vo.setContent(content);

		BoardDAO boardDao = new BoardDAO();
		boardDao.insertBoard(vo);

		//
		ModelAndView mav = new ModelAndView();
		mav.setViewName("redirect:getBoardList.do");
		return mav;
	}
}
```

## @Controller
- @Controller는 <u>@Component를 상속</u>했기 때문에 @Contorller가 붙은 클래스의 <u>객체를 메모리에 생성</u>한다
- @Controller가 선언된 객체를 자동으로 <u>Controller객체로 인식</u>한다
- @Controller 을 붙여주면<b>스프링 설정파일에 의해서 스프링 컨테이너가 컨트롤러 객체들을 자동으로 생성</b>해준다
- 스프링 설정파일 :

```xml
<context:component-scan base-package="com.springbook.view"></context:component-scan>
```

### 2. @Controller 이용 후
- POJO 스타일로 구현한다
- 메소드 이름 : handleRequest -> insertBoard
- 리턴타입 : ModelAndView -> void
- 메개변수 HttpServletRequest, HttpServletResponse -> HttpServletRequest

```java
import org.springframework.stereotype.Controller;

@Controller
public class InsertBoardController {

	public void insertBoard(HttpServletRequest request) {
		System.out.println("글 등록 처리");
		String title = request.getParameter("title");
		String writer = request.getParameter("writer");
		String content = request.getParameter("content");

		BoardVO vo = new BoardVO();
		vo.setTitle(title);
		vo.setWriter(writer);
		vo.setContent(content);

		BoardDAO boardDao = new BoardDAO();
		boardDao.insertBoard(vo);
	}
}
```

## @RequestMapping사용하기
- 클라이언트의 "/insertBoard.do" 요청에 대해서 insertBoard()메소드가 실행되도록 한다

### 3. HandlerMapping -> @RequestMapping사용하기

- 방법 1.

```java
public class HandlerMapping {

	private Map<String, Controller> mappings;

	public HandlerMapping() {
		mappings = new HashMap<String,Controller>();
		mappings.put("insertBoard.do", new InsertBoardController());
	}

	public Controller getController(String path) {
		return mappings.get(path);
	}
}
```

- 방법 2.

```xml
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
  <property name="mappings">
    <props>
      <prop key="/insertBoard.do">/insertBoard</prop>
    </props>
</property>
</bean>
	<bean id="insertBoard" class="com.springbook.view.board.InsertBoardController"></bean>
```

- 방법 3.
```java
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class InsertBoardController {

	@RequestMapping(value="/insertBoard.do")
	public void insertBoard(HttpServletRequest request) {
		System.out.println("글 등록 처리");
    // 생략
	}
}
```

## 클라이언트 요청 처리
### 4. HttpServletRequest -> Command객체(DTO)이용하기
- 사용자의 요청을 HttpServletRequest 클래스로 받아서 일일히 설정하지 않고, Command객체를 이용한다
- Command객체 : Controller 메소드 매개변수로 받은 DTO객체
- <u>스프링 컨테이너</u>가 매개변수에 해당하는<u>BoardVO 객체를 생성하여 전달</u>한다.
- <u>Form 태그 안의 파라메터 이름과 Command 객체의 Setter메소드 이름이 반드시 일치</u>해야 한다.
- 그래야 Setter인젝션에 의해 자동으로 사용자 입력값이 저장된다.

### 그림 설명
![mvc framework4](https://user-images.githubusercontent.com/55946791/73587596-5dd8e200-4501-11ea-902d-ebe9836286a0.jpg)
1. 사용자가 글 등록을 요청하면
2. 스프링 컨테이너가 매개변수에 해당하는 BoardVO객체를 생성하고
3. 사용자가 입력한 파라메터 값을 추출해서 BoardVO 객체ㅔ 저장한다. 이때, BoardVO클래스의 Setter메소드들이 호출된다
4. insertBoard()메소드를 호출할때, 사용자 입력값들이 설정된 BoardVO객체가 인자로 전달된다


```java
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class InsertBoardController {

	@RequestMapping(value="/insertBoard.do")
	public void insertBoard(BoardVO vo) {
		System.out.println("글 등록 처리");

		BoardDAO boardDao = new BoardDAO();
		boardDao.insertBoard(vo);
	}
}
```

## Controller 통합
![mvc framework5](https://user-images.githubusercontent.com/55946791/73588557-08ef9880-450e-11ea-9cb3-4a3d54653051.JPG)

```java
@Controller
public class BoardController {

	@RequestMapping("/getBoard.do")
	public ModelAndView getBoard(BoardVO vo, BoardDAO boardDao, ModelAndView mv) {
		mv.addObject("board", boardDao.getBoard(vo));		// Model 정보 저장
		mv.setViewName("getBoard");		// View 정보 저장
		return mv;
	}

	@RequestMapping("/getBoardList.do")
	public ModelAndView getBoardList(BoardDAO boardDao, BoardVO vo, ModelAndView mav) {
		mav.addObject("boardList", boardDao.getBoardList());
		mav.setViewName("getBoardList");
		return mav;
	}

	@RequestMapping(value="/insertBoard.do")
	public String insertBoard(BoardVO vo, BoardDAO boardDao) {
		boardDao.insertBoard(vo);
		return "getBoardList.do";
	}
  // 생략
}
```

---
## Reference
- 스프링 퀵 스타트-채규태 지음
