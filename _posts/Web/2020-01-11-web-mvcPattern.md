---
title: "WEB, 실전jsp강좌, MVC패턴"
date: 2020-01-11 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, MVC]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## MVC란
- Model,View,Controller의 약자
- 하나의 애플리케이션, 프로젝트를 구성할 때 그 구성요소를 세가지의 역할로 구분한 패턴
- "어떻게 나눌것인가"에 대한 해답 중 하나이다. 특정한 역할들에 대해 역할 분담을 하는 가이드라인을 제시한다
![mvc](https://user-images.githubusercontent.com/55946791/72495363-d38a5000-3869-11ea-968c-9dae69cf013d.JPG)
- Model : DB와의 관계, 클라이언트의 요청에서 필요한 자료를 DB로부터 추출/수정하여 Controller에게전달한다
- View : 사용자에게 보여지는 UI화면, 주로 .jsp파일로 작성하며 Controller에서 어떤 View컴포넌트를 보여줄지 결정한다
- Controller : 클라이언트의 요청을 받고, 적절한 Model에게 지시를 내리고 Model에서 전달받은 데이터를 적절한 View에 전달한다

![mvc_role_diagram](https://user-images.githubusercontent.com/55946791/72199983-f0e4a600-3486-11ea-95f0-3d2878016244.png)

- Model : 백그라운드에서 동작하는 로직을 처리
- View : 사용자가 보게 될 결과 화면을 출력
- Controller : 사용자의 입력처리와 흐름 제어를 담당

### Model
: 애플리케이션의 데이터를 가지고 있고, 데이터 가공을 처리한다
1. 사용자가 편집하기 원하는 모든 데이터를 가지고 있어야 한다
2. 뷰나 컨트롤러에 대한 정보를 알면 안된다.
    - 데이터 변경이 있을때 모델에서 UI를 직접 조정,수정할 수 있도록 뷰를 참조하는 내부 속성값을 가지면 안된다
3. 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야 한다

### View
: 사용자 인터페이스 출력을 담당한다
1. 모델이 가지고 있는 정보를 따로 저장하면 안된다
    - 모델이 가지고 있는 정보를 유지하기 위해 임의의 뷰 내부에 저장하면 안된다
2. 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 한다
    - 뷰는 다른 요소의 동작을 알면x, just화면에 표시역할
3. 변경이 일어나면 변경통지 처리방법 구현해야한다

### Controller
: 데이터(model)와 사용자인터페이스 요소(view)를 있는 다리 역할<br>
: 사용자 입력처리와 흐름제어를 담당

1. 모델이나 뷰에 대해 알고 있어야 한다
    - 모델,뷰는 서로를 모르고 변경을 외부에 알리고 수신하는 방법만 가지고 있다
    - 컨트롤러는 이 둘을 중재하기 때문에 둘에 대해 알아야 한다
2. 모델,뷰의 변경을 모니터링 해야 한다
    - 변경을 받으면 해석해서 각각의 구성 요소에게 통지해야 한다
    - 애플리케이션의 메인 로직은 컨트롤러가 담당


### MVC사용 이유
- 하나의 역할들만 담당하여 처리하게 때문에 맡은바에만 집중하여 처리를 효율적으로 한다
- 유지보수, 확장성, 유연성 증가
- 코드 중복 예방



## MVC Model1 & Model2
- JSP에서는 MVC 모델1(JSP에서 출력/로직을 전처리),2방식(JSP에서 출력만 처리)으로 나눈다

### Model1
![mvc1](https://user-images.githubusercontent.com/55946791/72495522-45fb3000-386a-11ea-82c9-0c949711bc59.JPG)
- MVC에서 View와 Controller가 같이 있는 형태
- 유지보수보다 개발속도가 더 중요할때, 소규모일때


![mvc model1](https://user-images.githubusercontent.com/55946791/72200129-ce538c80-3488-11ea-906d-0bc04e82dd0e.png)
- 사용자 요청을 jsp가 전부 처리한다
- 사용자의 요청을 받은 jsp는 자바빈/서비스 클래스를 사용하여 웹브라우저가 요청한 작업을 처리하고 결과를 출력한다


### Model2
![mvc2](https://user-images.githubusercontent.com/55946791/72495719-dc2f5600-386a-11ea-9f65-1e28cee20496.JPG)
- MVC에서 Model,View,Controller가 모두 모듈화(부품화) 되어 있는 형태

![mvc model2](https://user-images.githubusercontent.com/55946791/72200152-fb07a400-3488-11ea-82df-78a8fea7a608.png)
- 모델1과 달리 사용자 요청을 서블릿이 받는다
- 서블릿은 요청을 View or Model로 전송한다
- View는 ui 출력 담당
- Model은 실질적 기능 담당
- html과 java 소스를 분리 했기 때문에 개발 확장이 쉽고 유지보수에 용이하다



## Reference
- <https://m.blog.naver.com/jhc9639/220967034588>
- <https://coding-factory.tistory.com/69>
- [MVC패턴 게시판,JSP](https://coding-factory.tistory.com/71)
- [실전 jsp강좌](https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1188)
