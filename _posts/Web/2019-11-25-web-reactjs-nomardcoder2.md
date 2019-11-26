---
title: "WEB, ReactJS, introduction to react"
date: 2019-11-25 15:40:28 -0400
categories: ReactJS노마드코더
tags : [WEB, ReactJS, FrontEnd]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 웹펙
- 웹팩을 이용해서 최근 자바스크립트 (리액트 코드)를 모든 브라우저가 이해할수 있게 변경해줘야한다.
![webpack](https://user-images.githubusercontent.com/55946791/69519011-51358c00-0f9c-11ea-857f-3d7f926701fd.JPG)

### facebook의 create react app
- 복잡한 웹팩을 손쉽게 사용할수있게 한다.
-  <https://liante0904.tistory.com/128> 에서 설치 방법 확인가능

---
### JSX
- <u>리액트로 작성하는 html</u>
- 리액트 컴포넌트를 만들때 사용하는 언어
- ex. class -> className
```js
<header className="App-header">
```
- ex.
```js
import logo from './logo.svg';
<img src={logo} className="App-logo" alt="logo" />
```

---

### render function
- <b>모든 컴포넌트는 render function을 가지고있다.</b>
- render : 이 컴포넌트가 나에게 보여주는 것이 무엇인가.
##### index.js
```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
// 컴포넌트 App를 불러온다
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
// ReactDOM이 render(출력)한다. 무엇을? App을.
// 어디에? id가 root인 곳에.
// root는 index.html에 있다. 그 곳에 출력된다.
serviceWorker.unregister();
```

- public/index.html에 직접 코딩하는 것이 아니라 App.js에 코딩한다
##### App.js
```js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
     hello
    </div>
  );
}

export default App;
```
![reactjs2](https://user-images.githubusercontent.com/55946791/69522161-120b3900-0fa4-11ea-9f2e-70bea2998c5f.JPG)

---
### react vs reactDOM
- react는 UI 라이브러리
- reactDOM은 react를 웹사이트에 출력(render)하는걸 도와주는 모델
(라이브러리를 웹 사이트에 출력해줌)

- 웹사이트 : react를 사용해서 웹사이트에 올리고 싶으면 reactDOM을 사용하면 된다
- 모바일 앱 : react를 사용해서 모바일 앱에 올리고싶다면, reactNative를 사용한다


---
## Reference
<https://www.inflearn.com/course/reactjs-web/lecture/8279>
