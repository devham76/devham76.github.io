---
title: "WEB, ReactJS, AJAX on React"
date: 2019-11-27 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### AJAX
- Asynchronous(비동기화) JavaScript and XML
- 뭔가를 불러올때마다 페이지 새로고침을 하지 않아도 된다
- JSON : JavaScript Object Notation / 오브젝트를 자바스크립트로 작성하는 기법

---
### API 사용 순서
- localhost를 부른다
- 리액트를 부른다 (bundle.js)
- API를 호출했다
- 즉, 컴포넌트가 mount되면 url에 가서 fetch(잡아오다)해온다.

![reactjs ajax](https://user-images.githubusercontent.com/55946791/69704194-4e6e9e80-1136-11ea-9e07-277df9aa8ec0.JPG)

#### ReactJS에서 AJAX사용하기
```js
componentDidMount() {
  const url = "https://yts.lt/api/v2/list_movies.json?sort_by=rating";
  // url 을 ajax로 불러온다
  fetch(url)
  .then( potato => potato.json()) // json으로 변경
  .then( json => console.log(json))
  .catch( err => console.log(err))
}
```

### Promise
- 새로운 자바스크립트 컨셉이다
1. <b> asynchronous(비동기화) programming</b>
- <u>fetch()는 동기화 이기 때문에 불편</u>하다.
  - ex) 영화API, 애니메이션API를 호출하려고 한다면, 영화 API가 호출완료 되야 애니메이션 API를 호출할수있다
  - 만약, 영화API의 서버가 느리다면 한참을 기다려야만 애니메이션API를 호출 할 수 있다.
2. <b>시나리오를 잡는 방법을 만들어준다</b>


---
## Reference
- <https://www.inflearn.com/course/reactjs-web/lecture/8288>
- [영화 api](https://yts.ae/api)  
