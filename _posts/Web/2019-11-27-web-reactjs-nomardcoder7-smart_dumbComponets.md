---
title: "WEB, ReactJS, stateless functional (dumb)component"
date: 2019-11-27 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Smart vs Dumb Component
- 모든 컴포넌트에 state가 있는것은 아니다; <b>stateless functional component</b>
- smart : state o, props o
- <b>dumb : state x, props o</b>

### dumb Component
- dumb Component는 <u>클래스형이 아닌 함수형</u>이다
- 어떤 컴포넌트는 componentWillMount, function, update state...등이 필요없는 컴포넌트이다
- render (x), Lifecycle(x)
- 즉, 그냥 return을 하기위해 존재한다
- 그냥 <u>한개의 props</u>만 있으면 된다


#### 변경전
```js
import React, { Component } from 'react';

class MoviePoster extends React.Component {
  static propTypes = {
    poster: PropTypes.string.isRequired
  }
  render() {
    return (
      <img className="posterImg" src={this.props.poster} />
    );
  }
}
```

#### 변경후
```js
import React from 'react';

function MoviePoster({poster}){
  return (
    <img className="posterImg" src={poster} />
  )
}
```



---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8287>
