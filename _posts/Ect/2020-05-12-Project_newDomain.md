---
title: "프로젝트 관리1 - 도메인 구입하고 AWS에 적용하기"
date: 2020-05-12 20:00:28 -0400
categories: etc
tags : [project]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 개요

<http://ec2-15-165-155-30.ap-northeast-2.compute.amazonaws.com/>
spring과 aws를 공부하기 위해 만든 사이트인데 완성이후에도 요긴하게 잘 사용하고 있다. 그런데 누군가에게 이 사이트를 보여주는데 있어 도메인 주소를 알려주기 어렵고 완성되지 않은 느낌을 주는것같아 도메인을 구입하고, 내친김에 SSL인증서까지 등록해서 보안에 신경쓰기로 했다.

## 1. 도메인 구입
처음엔 무료 도메인을 이용할까하다가 아래의 단점과 외우기 쉽지 않거나 어딘가 신뢰성 없는 도메인의  ( .ba.ro , .kr.pe 등) 느낌을 주기 싫어서 이전 회사에서 사용하던 가비아에서 도메인을 구입하기로 했다.
```
일부 웹사이트에서는 유입자 수를 뺏어 가는 경우도 있고,
일부 광고 코드를 심어서 원치않는 광고를 해야 하는 경우도 있습니다.
```
출처: https://studyforus.tistory.com/132 [Study For Us]

### 가비아 도메인 구입 완료
짜잔 ~!! 개발자햄의 아이디를 넣은 도메인 발급완료 됐다.
나만의 도메인을 꼭 한번 가져보고싶었는데 돈만 낸거지만..ㅎㅎ 기분좋다
![가비아](https://user-images.githubusercontent.com/55946791/81697422-f9360780-949f-11ea-965d-69924a9928d6.JPG)

## 2. AWS Route 53등록
![aws rout 53](https://user-images.githubusercontent.com/55946791/81698018-66499d00-94a0-11ea-8224-6855f5697444.JPG)

![aws rout 53 등록](https://user-images.githubusercontent.com/55946791/81700404-92b2e880-94a3-11ea-97c9-7db62eda2a04.JPG)

1. 레코드 세트 생성 (NS, SOA유형 생성)
2. A유형의 레코드 세트 생성 후 값에 AWS EC2 오픈 IP주소를 입력한다

## 3. 가비아 네임서버 변경
가비아 도메인 관리 -> 전체 도메인 -> 네임설정 선택 후 AWS Route 53에서 발급받은 NS의 값을 입력해준다.

## 결과

![도메인 설정](https://user-images.githubusercontent.com/55946791/81700751-0e149a00-94a4-11ea-9d38-bd0384d3f2a5.JPG)
