---
title: "WEB, boostcourse, FE, css layout-1"
date: 2019-10-15 17:30:28 -0400
categories: WEB
tags : [WEB, boostcourse, FE]
---

- display (block, inline, inline-block)
- position (static, absolute, relative, fixed)
- float (left, right)
---
#### 1. 블록으로 쌓이는 엘리먼트(display:block)
display속성이 block이거나 inline-block인 경우 그 엘리먼트는 벽돌을 쌓는것처럼 위에서 아래로 채워진다

![div_css](https://user-images.githubusercontent.com/55946791/66806713-2bf83b80-ef63-11e9-8795-38e80bcbaec2.JPG)


#### 2. 옆으로 흐르는 엘리먼트(display:inline)
우측으로, 그리고 아래쪽으로 빈자리를 차지하며 흐른다
※liline속성의 엘리먼트는 높이와 넓이를 지정해도 반영되지 않는다
![inline_css](https://user-images.githubusercontent.com/55946791/66807573-4c74c580-ef64-11e9-9d82-b9f20a9d2072.JPG)


#### 3. 좀 다르게 배치시키기(position 속성)
- position속성을 사용하면 상대적/절대적으로 어떤 위치에 엘리먼트를 배치하는 것이 수월하다
1. <b>position</b> 속성으로 특별한 배치를 할 수 있습니다.
position 속성은 기본 static입니다.
그냥 순서대로 배치됩니다.

2. <b>absolute</b>는 기준점에 따라서 특별한 위치에 위치합니다.
top / left / right / bottom 으로 설정합니다.
기준점을 상위엘리먼트로 단계적으로 찾아가는데 <u>static이 아닌 position이 기준점</u>입니다.

3. <b>relative</b>는 <u>원래 자신이 위치해야 할 곳을 기준</u>으로 이동합니다.
top / left / right / bottom로 설정합니다.

4. <b>fixed</b>는 viewport(전체화면) 좌측, 맨 위를 기준으로 동작합니다.

![position_css](https://user-images.githubusercontent.com/55946791/66808274-da04e500-ef65-11e9-96d1-222c31827971.JPG)


#### 4. 엘리먼트가 배치되는 방식 (float:left)
- float 속성으로 원래 flow에서 벗어날 수 있고 둥둥 떠다닐 수 있다
- 일반적인 배치에 따라서 배치된 상태에서 float는 벗어난 형태로 특별히 배치됩니다.
- 따라서 뒤에 <u>block엘리먼트가 float 된 엘리먼트를 의식하지 못하고 중첩돼서 배치</u>됩니다.
- 이런 특이성 때문에 웹사이트의 전체 레이아웃 배치에서 유용하게 활용됩니다.
[code](https://jsbin.com/sigogapifa/edit?html,css,output)
![float_css](https://user-images.githubusercontent.com/55946791/66809168-ce1a2280-ef67-11e9-9c0e-6a5a11c4ada0.JPG)


---
## Reference

- [Element가 배치되는 방법(CSS layout)] <https://www.edwith.org/boostcourse-web/lecture/16677/>
- [온라인 실습] http://jsbin.com/?html,output
