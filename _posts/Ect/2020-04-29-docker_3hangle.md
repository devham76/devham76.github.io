---
title: "Doker, 한글 버전의 Docker 이미지 생성 및 자바 설치"
date: 2020-04-29 16:00:28 -0400
categories: etc
tags : [doker]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 목표
- 한글 버전을 지원할 수 있도록 docker이미지 생성
- docker 기본 명령어 이해
- 수동으로 자바 설치 및 환경 설정

## 한글 버전 지원 파일 생성
### 1. 명령어 파일 생성 및 입력
![docker 한글파일](https://user-images.githubusercontent.com/55946791/80560383-abd78600-8a1b-11ea-9c7a-3f69244a4355.JPG)

### 2. 명령어 파일 build , 이미지로 생성
- 빌드하기
```
ko_ubuntu:latest라는 이름으로 ./바로 아래에 빌드한다.
$ docker build --tag ko_ubuntu:latest ./
```
(※ 빌드란 ? 소스코드 파일을 실행 가능한 소프트웨어 산출물로 만드는 일련의 과정을 말한다.)

- 빌드가 완료 되어 이미지로 생성되었다.
![docker 한글 이미지](https://user-images.githubusercontent.com/55946791/80560614-8dbe5580-8a1c-11ea-9d23-e32a7efe3c1a.JPG)

### 3. 잘 생성됐는지 확인
- 잘 생성 되었는지 이미지를 컨테이너로 만들고 실행해서 우분투로 접속 후, 설정확인

```
[컨테이너이름] [이미지]
: 이미지로 ko_ubuntu1이름의 컨테이너를 만들고 bash shell로 접속하겠다

docker run -it --name ko_ubuntu1 ko_ubuntu /bin/bash
```
![docker 한글 이미지 완료](https://user-images.githubusercontent.com/55946791/80560882-83e92200-8a1d-11ea-92b3-1635deba72d0.JPG)

### 4. 컨테이너 실행 후 접속
![docker 접속](https://user-images.githubusercontent.com/55946791/80561056-2f927200-8a1e-11ea-83a8-c7e2216411df.JPG)

- 컨테이너를 데몬으로 실행 하지 않았기 때문에 docker ps -a 하면 종료된것으로 나온다.
- docker start [컨테이너 이름]를 이용해서 컨테이너를 재실행한다
- docker exec -it [컨테이너 이름] /bin/bash 로 컨테이너에 접속한다.

### 4. java설치
- 방법1.
```
1.  wget설치
apt-get install wget

2. 오라클에서 jdk 다운 url 가져와서 설치
wget --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn/java/jdk/8u251-b08/3d5a2bb8f8d4428bbe94aed7ec7ae784/jdk-8u251-linux-x64.tar.gz

3. jdk 압축 해제
tar -xvf [jdk파일 이름]
```
- 방법2. 방법1에서 압축 해제가 안되서 이 블로그를 참고했다.
- <https://lsjsj92.tistory.com/394>
- sudo apt-get install openjdk-8-jdk 이후 path설정


---
## 참고
- <http://forum.falinux.com/zbxe/?mid=lecture_tip&l=ru&page=4&m=1&document_srl=808302>
- <https://www.slipp.net/wiki/pages/viewpage.action?pageId=25529274>
