---
title: "WEB, ReactJS, Component State"
date: 2019-11-26 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### State
- 리액트 컴포넌트 안에 있는 오브젝트
- <b>state가 바뀔 때 마다, 컴포넌트는 새로운 state와 함께 다시 render한다 </b>
- state를 직접 <b>수정</b>하지 않는다 : <b>setState</b>를 이용한다
-  ex. hello를 출력하고, 2초후에 hello again!으로 수정(setState)되어 출력(render)된다.

```js
class App extends React.Component {

  state = {
    greeting : "Hello"  
  }
  // Render : 1.componentWillMount() 2.render() 3.componentDidMount()
  componentDidMount() {
    setTimeout(() => {
      // state를 직접 수정하지 않는다
      // ex. state.greeting = "hello again!"
      this.setState({
        greeting : "hello again!"
      })
    }, 2000)
  }
  render() {
    return (
      <div className="App">
       {this.state.greeting}
       {movies.map( (movie, index) => {
        return <Movie title={movie.title} poster={movie.poster} key={index} />
      })}
      </div>
      );
    }
}
```

---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8284>
