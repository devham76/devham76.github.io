---
title: "Spring, MVC FrameWork 개발"
date: 2020-01-31 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## Controller 분리

### 기존
- DispatcherServlet클래스로 Controller를 모두 구현했다
- 클라이언트의 모든 요청을 하나의 서블릿이 처리한다
- 개발과 유지보수가 어렵다

### 해결
- Sping MVC와 동일한 구조의 프레임워크를 직접 구현하여 적용해본다
- 중요 => <u>DispatcherServlet클래스는 새로운 기능이 추가되도 변경되지 않는다</u>
### 구조
![mvc framework](https://user-images.githubusercontent.com/55946791/73514063-8f837780-4433-11ea-81bd-28541028673a.jpg)
1. DispatcherServlet : <u>Client로부터 요청을 받는다</u>
2. HandlerMappling : 요청path와 일치하는 <u>Controller객체를 반환</u>한다
3. Controller : 반환된 객체에서 실질적인 사용자 <u>요청 메소드를 실행</u>한다
4. String : Controller 실행결과로 받은 <u>이동파일 이름</u>
5. ViewResolver : <u>이동파일 경로 + 파일 이름을 반환</u>한다
6. View : 이동할 파일로 <u>이동</u>한다<br>

## 코드
![mvc framework2](https://user-images.githubusercontent.com/55946791/73514670-e5f1b580-4435-11ea-9899-604977b2b64c.JPG)
### DispatcherServlet
```java
public class DispatcherServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
    private HandlerMapping handlerMapping;
    private ViewResolver viewResolver;


    // 스블릿 실행시 초기에 무조건 실행됨
	public void init() throws ServletException{
		// 어떤 컨트롤러를 가져올지 정함
		handlerMapping = new HandlerMapping();
		// 컨트롤러 실행 후 경로 지정
		viewResolver = new ViewResolver();
		viewResolver.setPrefix("./");
		viewResolver.setSuffix(".jsp");
	}
  ...

  private void process(HttpServletRequest request, HttpServletResponse response) throws IOException{

    // 1. 클라이언트의 요청 path 정보를 추출한다.
    String uri = request.getRequestURI();
    String path = uri.substring(uri.lastIndexOf("/"));

    // 2. HandlerMappling을 통해 path에 해당하는 Controller반환
    Controller ctrl = handlerMapping.getController(path);

    // 3. 검색된 Controller실행 후에 결과 파일 반환
    String viewName = ctrl.handleRequest(request, response);

    // 4. ViewResolver를 통해 viewName에 해당하는 화면을 검색한다.
    String view = null;
    if(!viewName.contai ns(".do")) {
      view = viewResolver.getView(viewName);
    } else {
      view = viewName;
    }

    // 5. 해당화면으로 이동
    response.sendRedirect(viewName);
  }
}
```

### HandlerMapping
```java
public class HandlerMapping {

	private Map<String, Controller> mappings;

	public HandlerMapping() {
		mappings = new HashMap<String,Controller>();
		mappings.put("login.do", new LoginController());
		mappings.put("logout.do", new LogoutController());
		mappings.put("insertBoard.do", new InsertBoardController());
		mappings.put("updateBoard.do", new UpdateBoardController());
		mappings.put("deleteBoard.do", new DeleteBoardController());
		mappings.put("getBoard.do", new GetBoardController());
		mappings.put("getBoardList.do", new GetBoardListController());
	}

	public Controller getController(String path) {
		return mappings.get(path);
	}
}
```

### LoginController
```java
public class LoginController implements Controller{

	@Override
	public String handleRequest(HttpServletRequest request, HttpServletResponse response) {
		System.out.println("login처리");
		// 1. 사용자 입력 정보 추출
		String id = request.getParameter("id");
		String password = request.getParameter("password");

		// 2. DB연동 처리
		UserVO vo = new UserVO();
		vo.setId(id);
		vo.setPassword(password);

		UserDAO userdao = new UserDAO();
		UserVO user = userdao.getUser(vo);

		// 3. 화면네비게이션
		if(user != null){
			return "getBoardList.do";
		}else {
			return "login";
		}
	}
}
```

### ViewResolver
```java
public class ViewResolver {
	public String prefix;
	public String suffix;

	public void setPrefix(String prefix) {
		this.prefix = prefix;
	}
	public void setSuffix(String suffix) {
		this.suffix = suffix;
	}
	public String getView(String viewName) {
		return prefix + viewName + suffix;
	}
}
```

---
## Reference
- 스프링 퀵 스타트-채규태 지음
