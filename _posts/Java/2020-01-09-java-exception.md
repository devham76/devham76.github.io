---
title: "JAVA, 예외처리"
date: 2020-01-09 14:40:28 -0400
categories: JAVA
tags : [JAVA, java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 오류란?
- 컴파일 오류 : 프로그램 코드 작성 중 발생하는 <u>문법적 오류</u>
- 실행 오류 : 실행 중인 프로그램이 의도하지 않은 동작을 하거나<u>(bug)</u> 프로그램이 중지되는 오류<u>(runtime error)</u>
- 자바는 예외 처리를 통해 프로그램의 <u>비정상 종료를 막고 log를 남길</u> 수 있다


## 오류와 예외 클래스
- 시스템 오류 (error) : 가상 머신에서 발생, 프로그래머가 처리x, 동적메모릴 다사용, stack over flow등..
- <u>예외 (Exception) : 프로그램에서 제외 할 수 있는 오류</u>
  - 읽으려는 파일이 없다, n/w이나 소켓연결 오류 등
  - 자바 프로그램에서는 예외에 대한 처리를 수행함

## 예외 클래스
![exception](https://user-images.githubusercontent.com/55946791/72050784-4ee98000-3305-11ea-9cf8-ee01c246b5c8.JPG)

- RuntimeExeption : 0으로 나눴다 등
- IOException : 파일/소켓이 없다 등

## 예외 처리
- try-catch / try-catch-finally
  - try : 예외 발생 가능 코드 부분
  - catch : try에서 예외발생시 수행되는 부분
  - finally : 예외 발생 여부에 상관 없이 항상 수행되는 부분, 리소스를 정리하는 코드를 주로 씀




---
## Reference
- fastcampus
