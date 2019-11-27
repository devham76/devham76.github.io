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
- <b>setState</b> : state를 직접 <b>수정</b>하지 않는다. setState를 이용해서 수정한다.
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
- 참고 ) setTimeout(function(){}, 1000) --new version--> setTimeout(()=> , 1000)

---
### ...this.state.movies
- state에 새로운 내용 추가시에 ...this.state.movies를 적절히 활용한다
- ...this.state.movies : 현재 state.movies내용

```js
state = {
  movies: [
    {
      title: "Harry Poter",
      poster: "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5xq2/image/w2gbbJ7lwG0quKMZtTihufPuvno.jpg"
    },
    {
      title: "Toy Story",
      poster: "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5uYQ/image/R3t_QxnFFfr20i8ekqVdzxUnBYE.jpg"
    },
    {
      title: "Aladin",
      poster: "http://img.movist.com/?img=/x00/05/11/49_p1.jpg"
    }
  ]
}

componentDidMount() {
  setTimeout(() => {
    this.setState({
      movies: [  
        // movies state에 이전 리스트
        ...this.state.movies,
        // 아래의 리스트를 추가한다
        {
          title: "Inside Out",
          poster: "http://t1.daumcdn.net/movie/0c0ae692e5a1f4cc79704eb09d21a835b40f567d"
        },

      ]
    })
  }, 1000)
}
```

#### 결과
- 1초 후에 이전의 movies 리스트에 새로운 항목이 추가되어 나타난다.

![reactjs state](https://user-images.githubusercontent.com/55946791/69699962-9b4d7780-112c-11ea-830a-81b3e2f59a0d.JPG)

---
### Loding states
- 필요한 데이터는 항상 즉시 존재하지는 않는다
- 데이터 로드 과정
  - 데이터 없이 컴포넌트가 로딩을한다
  - API를 호출하여 데이터를가져온다.
  - 가져온 데이터를 이용해 컴포넌트 state를 업데이트한다
- 오류 발생
  - state가 비어있는데 (데이터 로드가 아직 안됨) state의 항목을 출력하려고 시도 하면 오류가 발생한다.
- 오류 해결 방법
  - 호출하려는 항목이 state에 없으면, "Loading" 등의 글을 출력하고
  - 호출하려는 항목(데이터)가 로드 되면 그때 출력한다.
  ```js
  {this.state.movies ? this._renderMovies() : "Loading"}
  ```

#### 전체코드
```js
import React, { Component } from 'react';
import Movie from './Movie';
import './App.css';


class App extends React.Component {
  state = {

  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        movies: [
          {
            title: "Harry Poter",
            poster: "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5xq2/image/w2gbbJ7lwG0quKMZtTihufPuvno.jpg"
          },
          {
            title: "Toy Story",
            poster: "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5uYQ/image/R3t_QxnFFfr20i8ekqVdzxUnBYE.jpg"
          },
          {
            title: "Aladin",
            poster: "http://img.movist.com/?img=/x00/05/11/49_p1.jpg"
          },
          {
            title: "Inside Out",
            poster: "http://t1.daumcdn.net/movie/0c0ae692e5a1f4cc79704eb09d21a835b40f567d"
          }
        ]
      })
    }, 3000)
  }

  // 함수로 빼버림
  _renderMovies = () => {
    // movies라는 변수에 데이터 저장
    const movies = this.state.movies.map((movie, index) => {
      return <Movie title={movie.title} poster={movie.poster} key={index} />
    })
    return movies
  }

  // state에 movies가 없기 때문에 state.movies를 출력하라는 코드는 에러가 난다.
  // 해결 방법 -> movies가 없으면 "Loading"출력, 있으면 movies출력
  render() {
    return (
      <div className="App">
        {this.state.movies ? this._renderMovies() : "Loading"}
      </div>
    );
  }
}
export default App;
```

- tip) _renderMovies 함수에서 _를 사용하는 이유
  - 리액트는 자체 기능이 많기 때문에 리액트 자체기능과 나의 기능에 차이를 두려고 '_'를 사용한다


---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8284>
<https://www.inflearn.com/course/reactjs-web/lecture/8285>
<https://www.inflearn.com/course/reactjs-web/lecture/8286>
