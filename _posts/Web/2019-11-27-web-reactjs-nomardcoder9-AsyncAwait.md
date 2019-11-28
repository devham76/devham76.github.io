---
title: "WEB, ReactJS, Async&Await"
date: 2019-11-27 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Async, Await
- .then() 을 계속 쓰게 되는 것은 보기 불편하다. 이것을 해결하기 위해 사용한다

#### 변경 전 코드
```js
const url = "https://yts.lt/api/v2/list_movies.json?sort_by=rating";
fetch(url)
.then( potato => potato.json()) // json으로 변경
.then( json => {
  this.setState({
    movies: json.datas.movies
  })
  .then( ()=>
    CALL HELL !
  )
})
.catch( err => console.log(err))
```

#### 변경 후 코드
- 함수안에 집어 넣어서 함수를 호출하도록 했다.

```js
_callApi = () =>{
  const url = "https://yts.lt/api/v2/list_movies.json?sort_by=rating";
  return fetch(url)
  .then( potato => potato.json()) // json으로 변경
  .then( json => json.data.movies)
  .catch( err => console.log(err))
}
```

#### Async & Await
- await 하는 것이란 ?
- const movies = await this._callApi() : _callApi()함수가 끝나는것을 기다리고 결과 값을 movies에 삽입한다.


```js
componentDidMount() {
  this._getMovies();
}

// 비동기화 함수
_getMovies = async() => {
  // call api기능이 끝나는것을 기다리고 끝나면 그 결과값을 movies에 넣는다
  const movies = await this._callApi()

  // 해당부분은 callApi 작업이 완료 되기 전까지는 실행되지 않는다
  this.setState({
     // 모던 자바스크립트의 표현, 이전표현 => movies : movies
    movies
  })
}
```

---

### 전체 코드
```js
import React, { Component } from 'react';
import Movie from './Movie';
import './App.css';


class App extends React.Component {

  state = {}

  componentDidMount() {
    this._getMovies();
  }

  // 비동기화 함수
  _getMovies = async() => {
    // await를 하는 것은 call api기능이 끝나는것을 기다리고
    // 끝나면 그 결과값을 movies에 넣는다
    const movies = await this._callApi()
    // 해당부분은 callApi 작업이 완료 되기 전까지는 실행되지 않는다
    this.setState({
       // 모던 자바스크립트의 표현, 이전표현 => movies : movies
      movies
    })
  }

  //-- url 을 ajax로 불러온다
  _callApi = () =>{
    const url = "https://yts.lt/api/v2/list_movies.json?sort_by=rating";
    return fetch(url)
    .then( potato => potato.json()) // json으로 변경
    .then( json => json.data.movies)
    .catch( err => console.log(err))
  }

  // 리액트는 자체 기능이 많기 때문에
  // 리액트 자체기능과 나의 기능에 차이를 두려고 '_'를 사용한다
  _renderMovies = () => {
    // movies라는 변수에 데이터 저장
    const movies = this.state.movies.map( movie => {
      return <Movie title={movie.title} poster={movie.large_cover_image} key={movie.id} />
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


---
## Reference
- <https://www.inflearn.com/course/reactjs-web/lecture/8290>
