---
title: "WEB, ReactJS, Lists with .maps & set PropTypes"
date: 2019-11-26 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### Array.prototype.map()
- map이라는 기능은 새로운 array를 만든다
- ex. movies 배열을 가지고 맵핑을해서 새로운 배열을 만든다.
- movie는 현재 사이클의 엘리멘트를 의미한다.
```js
{
  movies.map( movie => {
  return <Movie title={movie.title} poster={movie.poster} />
})}
//-- 이 부분은 아래부분과 같다
{[
  <Movie title={movie[0].title poster={movie[0].poster}}>  
  <Movie title={movie[1].title poster={movie[1].poster}}>  
  <Movie title={movie[2].title poster={movie[2].poster}}>  
]}
```

 #####  Each child in a list should have a unique "key" prop.
- 고유한 key이 필요하다
(여기서는 index로 대체)
- 수정한 코드
```js
{movies.map( (movie, index) => {
  return <Movie title={movie.title} poster={movie.poster} key={index} />
})}
```

---
### propTypes
- <b>props의 변수 타입을 설정</b>해준다
- ex) title: PropTypes.string.isRequired
  - title의 타입은 반드시 문자열이여야한다
  - <b>isRequired</b> : title은 항상 있어야 한다. 만약 Movie 함수에서 props.title이 사용되지 않으면 오류 발생
```js
Movie.propTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string
}
function Movie(props) {
  return (
    <div>
        <MoviePoster poster={props.poster}/>
        <h1>{props.title}</h1>
    </div>
  );
}
```



---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8282>
