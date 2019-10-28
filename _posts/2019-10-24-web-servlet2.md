---
title: "WEB, servlet, 초기 파라메터/데이터공유/웹앱감시"
date: 2019-10-24 14:30:28 -0400
categories: 실전jsp강좌
tags : [WEB, SERVLET]
---
### ServletConfig (서블릿 초기화 파라메터)
- 초기화 파라미터 : <u>특정</u> <b>SERVLET이 생성될 때 초기에 필요한 데이터</b>가 있다
  - ex. 특정 경로, 아이디 정보 등
- 모든 servlet에 적용되는게 아니다. '특정'
<br>[방법1] : web.xml에 기술하고 servlet파일에서는 ServletConfig 클래스를 이용해서 사용한다
<br>[방법2] : web.xml이 아닌 servlet파일에 직접 기술 할 수도 있다

![servletconfig](https://user-images.githubusercontent.com/55946791/67461537-8fc3e800-f678-11e9-9a69-8eadf37df62e.JPG)
![초기화](https://user-images.githubusercontent.com/55946791/67462354-58563b00-f67a-11e9-9185-8b8961624a95.JPG)

---
### ServletContext (데이터 공유)
- 여러 Servlet에서 <b>특정 데이터를 공유</b>해야 할 경우
- context parameter를 이용해서 <b>web.xml에 데이터를 기술</b>하고 servlet에서 공유하면서 사용 할 수 있다
![servlet context](https://user-images.githubusercontent.com/55946791/67462807-33ae9300-f67b-11e9-8fd2-ba4cda241191.JPG)

---
### ServletContextListener (웹 어플리케이션 감시)
- 웹 어플리케이션의 <b>생명주기를 감시</b>하는 리스너
- 리스터의 해당 메소드가 웹 어플리케이션의 <b>시작과 종료시 호출</b> 된다
  - ex. contextInitialized(), contextDestoryed()
1. 방법:
 ![servlet context listener](https://user-images.githubusercontent.com/55946791/67463254-0a423700-f67c-11e9-928d-37f2844aa01d.JPG)
 2. 방법 :
![servlet context listener2](https://user-images.githubusercontent.com/55946791/67463784-05ca4e00-f67d-11e9-880d-7f9fb840aeb2.JPG)

3. 결과 :
![servlet context listener result](https://user-images.githubusercontent.com/55946791/67463599-ad934c00-f67c-11e9-8042-6993727c250d.JPG)

---
## Reference

<https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1167>
