---
title: "WEB, ReactJS, Data flow with Props"
date: 2019-11-26 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### Props
- 메인(부모) 컴포넌트가 모든 데이터를 가지고 있고 자식 컴포넌트에게 정보를 전달한다.
- 한개의 데이터 소스를 가지고 각 컴포넌트별로 출력만 하면 된다.
- 이를 이용해 강력한 UI를 구축 할 수 있다

#### App.js
```js
import React from 'react';
import Movie from './Movie';
import './App.css';

const moviesTitles = [
  "Harry Poter",
  "Toy Story",
  "Aladin"
]
const movieImages = [
  "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5xq2/image/w2gbbJ7lwG0quKMZtTihufPuvno.jpg",
  "https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/5uYQ/image/R3t_QxnFFfr20i8ekqVdzxUnBYE.jpg",
  "http://img.movist.com/?img=/x00/05/11/49_p1.jpg"
]

function App() {
  return (
    <div className="App">
     <Movie title={moviesTitles[0]} poster={movieImages[0]} />
     <Movie title={moviesTitles[1]} poster={movieImages[1]} />
     <Movie title={moviesTitles[2]} poster={movieImages[2]} />
    </div>
  );
}

export default App;
```

---
#### Movie.js
```js
import React from 'react';
import './Movie.css';


function Movie(props) {
  console.log(props);
  return (
    <div title="hi">
        <MoviePoster poster={props.poster}/>
        <h1>{props.title}</h1>
    </div>
  );
}

function MoviePoster(props) {
    return (
        <img className="posterImg" src={props.poster} />
    );
}   
export default Movie;
```

---
#### 결과
![reactjs props](https://user-images.githubusercontent.com/55946791/69607738-4268db00-1069-11ea-953e-9ee6babdc5e1.JPG)


---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8280>
