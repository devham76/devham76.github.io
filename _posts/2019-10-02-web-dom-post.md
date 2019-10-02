---
title: "WEB, DOM이란?"
date: 2019-10-02 14:30:28 -0400
categories: WEB
tags : [WEB, DOM, front-end]
---
---
- ## Document Object Model
1. 웹페이지를 자바스크립트로 제어하기 위한 객체 모델을 의미한다
2. JavaScript로 문서 객체를 생성하는것.

![800px-DOM-model svg](https://user-images.githubusercontent.com/55946791/66019240-88983700-e51d-11e9-9514-efe437df013c.png)


- ## 문서 객체란?
html문서의 태그(<html><body>..등)들을 JavaScript가 이용할 수 있는 객체(object)로 만든것

- ## JavaScript로 문서객체를 생성한다?
1. 정적으로 문서 객체 생성
- 웹 브라우저가 HTML페이지에 적혀 있는 태그를 읽으면 생성하는 것
- 단순히 적혀져 있는 그대로 문서 객체가 생성되는 것을 표현
2. 동적으로 문서 객체 생성
- HTML 페이지에 없던 문서객체를 JavaScript를 이용해서 생성하는것
- <u>JavaScript로 문서객체를 생성 : HTML페이지에 없던 문서객체를 동적으로 생성하는것</u>

- ## DOM 의 사용
아래의 코드는 JavaScript를 사용해서 동적으로 문서객체를 생성하는 예

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 문서객체 모델(DOM)</title >
<script type= "text/javascript">
    window.onload = function(){
       //1. 문서 객체 생성
       var header = document.createElement('h2'); //h2 태그를 생성해주는 것
       var textNode = document.createTextNode('Hello DOM');

       //2. 노드(요소/텍스트)를 연결.
       header.appendChild(textNode);

       //3. body 문서 객체에 header 문서 객체를 추가.
       document.body.appendChild(header);
    };
</script>
</head>
<body>
   <h1 id ="header_1" name= "" >HEADER-1 </h1 >
   <div >
      <h1 id = "header_2">HEADER-2</h1 >
   </div >
   <hr >
   <h1 id = "clock"></h1>
</body>
</html>
```



---
## Reference 
[쉽게 읽는 프로그래밍](https://m.blog.naver.com/magnking/220972680805)


---
