---
title: "Doker, Doker Container 생성"
date: 2020-04-29 16:00:28 -0400
categories: etc
tags : [doker]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


### pull
- 원격 저장소에 이미지가 저장되어있고 git처럼 pull해서 이미지를 가져올수있다
```
docker pull <이미지이름>:<태그>
docker pull ubuntu
```

### images
- 이미지 목록 출력
![docker images](https://user-images.githubusercontent.com/55946791/80558828-9f046380-8a16-11ea-8f16-17fd08783f33.JPG)

### run
- 이미지를 컨테이너로 생성한 뒤 실행
```
docker run --name [이미지 이름] [실행할 파일]
docker run --name javaweb ubuntu
```

- 프로세스 확인 : 현재 프로세스에서 실행되고 있는 모든 이미지 확인
```
docker ps -a
```
![docker ps](https://user-images.githubusercontent.com/55946791/80558672-29989300-8a16-11ea-96fe-74de5764c731.JPG)

### run -dit
- 컨테이너는 데몬으로 띄어줘야 한다
- 그렇지 않으면 생성과 동시에 종료된다.

![docker daemon](https://user-images.githubusercontent.com/55946791/80559024-47b2c300-8a17-11ea-9e79-ef88d9879cce.JPG)

## rm
- 컨테이이너 삭제

![docker rm](https://user-images.githubusercontent.com/55946791/80558940-fb678300-8a16-11ea-9e78-84286a6869e5.JPG)

## start, stop

![docker stop start](https://user-images.githubusercontent.com/55946791/80559091-7a5cbb80-8a17-11ea-8340-f50a8e43c277.JPG)

## exec
- bash shell을 이용해서 컨테이너 실행
```
docker exec -it jwp /bin/bash
```
- jwp라는 컨테이너를 bash shell을 이용해서 실행해준다.
- jwp안에 있는 우분투를 실행하게 된다.

![docker exec](https://user-images.githubusercontent.com/55946791/80559213-cad41900-8a17-11ea-920c-ec0116e98fd0.JPG)


---
## 참고
- <https://www.slipp.net/wiki/pages/viewpage.action?pageId=25529274>
