---
title: "Doker, Dockerfile을 활용해 나만의 이미지 만들기"
date: 2020-04-29 19:00:28 -0400
categories: etc
tags : [doker]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 목표
- 자바, vim, git 설치와 같은 단순 반복적인 작업을 Dockerfile을 활용해 자동화

## 1. Dockerfile 작성
- [Docker hub](https://hub.docker.com/search?q=java8&type=image)에서 필요한 프로그램을 검색해서 계정과 컨테이너를 확인한다.
- FROM 뒤에 이름을 붙여준다. (이 컨테이너로 부터 아래 명령어를 실행하라는 뜻.)

```
FROM openwhisk/java8action

RUN apt-get update  
RUN apt-get install  -y language-pack-ko   

# set locale ko_KR                                                                                                     
RUN locale-gen ko_KR.UTF-8           
ENV LANG ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8  
ENV LC_ALL ko_KR.UTF-8         

RUN apt-get install -y \
  vim \
  git

CMD /bin/bash    
```

## 2. 이미지로 빌드
- ko_java라는 이미지로 빌드 해서 해당 폴더에 만들어라
```
$ docker build -t my_dev
```
![docker image](https://user-images.githubusercontent.com/55946791/80569137-42fc0800-8a33-11ea-99d4-f478ebc9eb75.JPG)


## 3. 이미지를 컨테이너로 실행
```
$ docker run -it --name my_first_dev my_dev /bin/bash
```
