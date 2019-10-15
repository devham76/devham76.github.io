---
title: "WEB, boostcourse, FE, css layout-2"
date: 2019-10-15 17:30:28 -0400
categories: WEB
tags : [WEB, boostcourse, FE]
---

#### 배경색이 사라지게 된 이유?
<b>[원인]</b> float를 사용했기 때문에 떠있게 되고, .wrap는 .left와 .right를 자기 자식으로 생각하지 않게 되었다
<b>[해결]</b> overflow 속성을 주면 float를 자기 자식으로 인식하게 되어있다

#### footer가 올라오는 이유?
<b>[원인]</b> .left와 .right가 float를 사용했기 때문에 떠있게 되고, 빈 부분에 footer가 채우러 올라가게 되었다
<b>[해결]</b> clear:left 또는 right/both를 사용해서 left를 인식해서 올라가지 않도록 한다

![결과화면](https://user-images.githubusercontent.com/55946791/66814078-f65a4f00-ef70-11e9-900e-1131f42425c5.JPG)

```html
<header>부스트코스는 정말 유익합니다.</header>
<div id="wrap">
   <nav class="left">
      <ul>
         <li>menu</li>
         <li>home</li>
         <li>name</li>
      </ul>
   </nav>
   <div class="right">
      <h2>
         <span>반가워요!</span>
         <div class="emoticon">:-)</div>
      </h2>
   <ul>
      <li>crong</li>
      <li>jk</li>
      <li>honux</li>
      <li>pobi</li>
   </ul>
   </div>
   <div class="realright">
      oh~ right
   </div>
</div>
<footer>코드스쿼드(주)</footer>
```
```css
li {
   list-style:none;
}

header {
   background-color : #eee;
}

#wrap {
   overflow:auto;
   margin:20px 0px;
}

.left, .right, .realright {
   float:left;
   height: 200px;
}

.left {
   width:17%;
   margin-right:3%;
   background-color : #47c;
}

.right {
   width : 60%;
   text-align:center;
   background-color : #47c;
}

.realright {
   width: 17%;
   margin-left:3%;
   background-color : #67c;
}

.right > h2 {
   position:relative;
}

.right .emoticon {
   position:absolute;
   top:0px;
   right:5%;
   color:#fff;
}

footer {
   background-color : #eee;
   clear:left;
}
```
---
## Reference

- [6) float 기반 샘플 화면 레이아웃 구성] <https://www.edwith.org/boostcourse-web/lecture/16678/>
- [온라인 실습] http://jsbin.com
