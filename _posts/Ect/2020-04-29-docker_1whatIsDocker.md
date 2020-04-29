---
title: "Doker, Doker란 무엇인가"
date: 2020-04-29 16:00:28 -0400
categories: etc
tags : [doker]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## Doker란 ?
- __컨테이너 기반의 오픈소스 가상화 플랫폼__

![doker](https://user-images.githubusercontent.com/55946791/80555290-d4a34f80-8a0a-11ea-9a28-536bc6cabd0b.png)
_도커는 컨테이너를 관리하는 플랫폼_

- 다양한 프로그램, 실행환경을 컨테이너로 추상화하고
- 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해준다.

## Doker Image
![docker-image](https://user-images.githubusercontent.com/55946791/80555624-cb66b280-8a0b-11ea-8915-bef99f952b61.png)
- 이미지는 __컨테이너 실행에 필요한 파일과 설정값 등을 포함하고 있는 것__
- 상태값을 가지지 않고 변하지 않는다.(Immutable)
<br>
- 컨테이너는 이미지를 실행한 상태
- 추가되거나 변하는 값은 컨테이너에 저장된다.(이미지는 변하지 않는다.)
<br>
- __이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 더 이상 의존성 파일을 컴파일하고 추가로 설치할 필요가 없다.__
- 새로운 서버가 추가되면 미리 만들어 놓은 이미지를 다운받고 컨테이너를 생성만 하면 된다.

## Doker Layer
![image-layer](https://user-images.githubusercontent.com/55946791/80555896-ade61880-8a0c-11ea-9333-83cf68c82d55.png)
- 도커 이미지를 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 용량이 수백MB에 이른다.
- 처음 이미지를 다운받을 땐 크게 부담 되지 않지만, 이미지에 파일 하나 추가했다고 수백메가를 다시 다운받는 다면 매우 비효율적이다.
<br>
- __layer 레이어__ 라는 개념을 사용해서 해결했다.
- 여러개의 레이어를 하나의 파일 시스템으로 사용할 수 있게 해준다.
- 이미지 뿐만 아니라 컨테이너 생성시에도 레이어 방식을 사용한다.


## 사용
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
- <https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html#%EC%84%9C%EB%B2%84%EB%A5%BC-%EA%B4%80%EB%A6%AC%ED%95%9C%EB%8B%A4%EB%8A%94-%EA%B2%83>
