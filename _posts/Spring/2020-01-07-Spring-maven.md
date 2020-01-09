---
title: "Spring, Maven, Gradle, Logbac"
date: 2020-01-07 13:40:28 -0400
categories: Spring
tags : [Spring]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## Build Tool
- 빠른 기간동안에 <u>계속해서 늘어나는 라이브러리 추가</u>
- 프로젝트를 진행하며 <u>라이브러리 버전 동기화</u>
- 이 두가지를 위해 초기의 JAVA빌드 도구로 Ant라는 도구를 많이 사용했으나 이도구를 보완하기 위해 Maven,Gradle이 등장했다.

## Apache ANT
- xml기반 스크립트 개발
- 형식적인 규직이 없다
- 명확한 빌드 절차 정의가 필요
- 생명주기를 갖지 않기 때문에 target에 대한 의존관계와 일련의 작업을 정의해 주어야 한다

## Maven이란?
- pom.xml을 공유하면 개발환경이 다르더라도 <b>사용할 라이브러리뿐만 아니라 해당 라이브러리가 작동하는데 필요한 다른 라이브러리들까지 관리하여 n/w를 통해서 자동으로 다운 받아준다.</b>
- 필요한 라이브러리를 특정문서(pom.xml)에 정의해 놓으면 자동으로 다운 받아준다.
- 프로젝트 전체적인 라이프 사이클을 관리하는 도구이다

- pom.xml을 이용한 정형화된 빌드 시스템

- build를 쉽게
- ※ jar : 압축파일, 아카이빙이 목적이다(여러가지 파일을 하나로 묶어서 사용하기 편하게 하기 위함)
<br>
[단점]
- xml이 복잡해질 수 있다

## Gradle
- Ant처럼 유연한 범용 빌드 도구
- Maven을 사용할 수 있는 변환 가능 컨벤션 프레임 워크
- 원격 저장소나, pom, ivy 파일 없이 연결되는 의존성 관리 지원
- Ant의 유연한 구조적 장점 + Maven의 편리한 의존성 관리 기능
- Groovy를 이용한 빌드 자동화 시스템

## Maven vs Gradle
- Gradle이 가독성이 좋다
- Gradle이 빌트 테스트 실행 결과가 더 빠르다


---
## logback

```java
package org.slf4j;
public interface Logger {

  // Printing methods:
  public void trace(String message);
  public void debug(String message);
  public void info(String message);
  public void warn(String message);
  public void error(String message);
}
```
![logback](https://user-images.githubusercontent.com/55946791/72055888-ee5f4080-330e-11ea-9149-e9b7e6da6394.JPG)




---
## Reference
- <https://jerryjerryjerry.tistory.com/63>
- <https://jj-one-a-week.blogspot.com/2017/05/ant-maven-gradle.html>
