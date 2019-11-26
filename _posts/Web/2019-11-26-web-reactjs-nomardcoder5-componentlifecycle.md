---
title: "WEB, ReactJS, Component Lifecycle"
date: 2019-11-26 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### Lifecycle
- render할때, 즉 컴포넌트를 띄울때 해당 순서대로 작동한다.

#### Render
1. componentWillMount()
2. render()
  - 컴포넌트가 리액트 세계에 존재 하게 됨  
3. componentDidMount()
  - 성공적으로 리액트 세계에 컴포넌트가 자리잡았음을 알게 됨

#### Update
1. componentWillReceiveProps()
  - 컴포넌트가 새로운 props를 받았다
2. shouldComponentUpdate()
  - 이전 props와 새로운 props가 다르다면 업데이트 해줘야 한다

3. componentWillUpdate()
  - 컴포넌트는 업데이트 될것이다
4. render()
5. componentDidUpdate()



---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8283>
