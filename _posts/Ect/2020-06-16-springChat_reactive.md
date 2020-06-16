---
title: "Spring, chatting 프로그램 만들기, Reactive란?"
date: 2020-06-15 20:00:28 -0400
categories: etc
tags : [project, reactive, spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## Reactive
- 막힘없이 흘러다니는 data(event)를 통해 사용자에게 자연스러운 응답을 주고
규모 탄력적으로 리소스를 사용하며 실패에 있어서 유연하게 대처한다
- 모든 지점에서 블럭 되지 않게 하자
- oop와 같은 패러다임
- 모든 것을 비동기적인 data의 stream으로 간주하고, Observer 패턴을 활용하여 비동기 이벤트를 처리한다


### Reactive의 4가지 주요 속성
![recative manifesto](https://user-images.githubusercontent.com/55946791/84739838-4e0cf680-afe7-11ea-92eb-08c22ee55049.jpg)
- __Responsive__ : 사용자에 대한 반응(React)
	- 사용자가 정해진 시간안에 반드시 결과를 받아 볼 수 있게 하는것
- __Scalable(Elastic)__ : 부하(road)에 대한 반응(React)
	- 수평확장을 의미. AWS, Docker를 이용할 수 있다
- __Resillent__ : 실패상황에 대한 반응(React)
- __Event-driven__ : 이벤트에 대한 반응(React)
	- 비동기식 event별로 처리한다


## Reactive Porgramming
- 비동기 데이터 스트림을 사용한 프로그래밍

### Rx : Reactive Extension
- Reactive programming != RX
- RX는 Reactive Programming을 가능하게 해주는 라이브러리
- 옵저버 패턴을 확장
- RxJava : Java에서 Reactive Porgamming을 가능하게 해주는 라이브러리

---
## 참고
- [리액티브란 무엇인가? (What's in a Name : Reactive) Atin](https://hamait.tistory.com/761)
- [왕초보를 위한 <Reactive programming이 뭔지 알기 전에>](https://zeddios.tistory.com/303)
