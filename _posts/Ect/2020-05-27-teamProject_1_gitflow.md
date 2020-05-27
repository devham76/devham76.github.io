---
title: "만개의 레시피 클론 코딩, git flow"
date: 2020-05-27 20:00:28 -0400
categories: etc
tags : [git]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 문제1. git으로 협업하기
- git으로 협업을 해본 경험이 없어 내가 작성한 코드를 어떻게 로컬 저장소에 올리는지 전체적인 부분에 대해 팀원에게 질문했다.

1. 세팅이 다된 remote develop 브랜치에 create branch here해서 local 브랜치를 만들고
2. 그 환경에서 mustache로 화면을 만들었습니다
3. GitKraken 맨 오른쪽에 stage all changes, commit message, commit 하면 되는건가요?

### 해결1.
git flow 를사용하세요

## 문제2.
git-flow init 후 Fatal: Working tree contains unstaged changes. Aborting 발생

### 해결2.
- git flow는 변경된 파일이 없는 상태에서 초기화 해줘야한다.

1. git stash
	- 변경된 기능은 임시 저장한다.
2. git flow init
	- 초기화
3. git flow feature start chef
	- 특정 기능을 개발하기 위한 branch가 필요하므로 feature를 추가하고 내가 개발할 쉐프 목록을 chef라고 이름을 지어줬다.
4. git stash pop
	- 임시 저장한 내용 불러온다

```
git stash
git flow init
git flow feature start chef
git stash pop
```

## 그렇다면 git flow란 무엇인가?
- __feature - develpo - release - hotfixes - master__ 단계로 branch를 나눠서 코드를 관리하는 전략
- 이를 사용자가 쉽게 접근하고 사용할수 있도록 확장 기능(명령어)를 제공하는 것이 gitflow다.

## 방식
- 기존 git 저장소 내에서 초기화하는 것으로 git-flow의 사용을 시작할 수 있다.
- 명령어를 실행하고 나면 자동으로 master 외에 develop branch가 생성되며,
기본적으로 __develop branch에서 개발하고, master로 release__ 하는 방식이다.
- git flow init
	- 해당 명령어를 실행하면 프로세스 별로 사용할 branch이름을 입력하라는 메시지가 뜬다. (-d 옵션시, 이 과정 생략)

## branch 종류
1. master : __최종 릴리즈에__ 사용되는 안정된 버전
2. develop : 다음 릴리즈를 위해 __개발중인__ 최신 버전
3. feature : __특정 기능 개발을__ 위한 branch
4. release : 릴리즈 __점검을__ 위한 branch
5. hotfix : __긴급 버그__ 픽스를 위한 branch
6. support : __버전 호환성__ 문제를 처리하기 위한 branch

## 결과 화면
- 깃 크라켄 화면
![git flow](https://user-images.githubusercontent.com/55946791/83005103-62df1580-a04b-11ea-8ea4-93f48cb1bc6d.JPG)

- 첫번째 PR
![git flow2](https://user-images.githubusercontent.com/55946791/83005096-61ade880-a04b-11ea-92df-a4ad4b367cfd.JPG)

## 느낀점
그동안 git은 백업용으로 사용했었는다. 처음으로 협업을 위해 사용했는데 쉽지 않았고, 잘 사용하면 굉장히 유용할것같다.
하지만 '잘' 사용하기 위해 계속 공부하고 테스트용 저장소를 이용해서 많이 테스트 해봐야겠다.
그리고 잘한건지 모르겠는데.... 처음으로 PR올리니까 신기하고 재밌다 크크



---
## 참고

[참고1](https://uroa.tistory.com/106)
[git flow 설명화면](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)
