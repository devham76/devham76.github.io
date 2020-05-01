---
title: "Travis CI, AWS S3, CodeDeploy 연동"
date: 2020-05-01 20:00:28 -0400
categories: etc
tags : [CI, AWS]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 목표
- __CI를 이용해서 git에서 push만 해도 테스트와 빌드가 자동으로 되도록 한다.__
- __git push -> Travis CI(배포 파일 생성) -> AWS S3(zip형태로 배포 파일 저장) -> CodeDeploy(AWS S3의 파일을 EC2에 저장)__

> TIP) Travis CI와 AWS S3를 이용하는 이유?
- CodeDeploy가 빌드하고 배포도 할 수 있지만, Travis CI를 이용해서 빌드하고 CodeDeploy를 이용해서 배포하는 이유는
- __빌드 없이 배포만 필요할 경우 대응하기 어렵기 때문이다.__ (확장성이 떨어진다.)
- Travis CI를 이용하면, 빌드된 파일을 CodeDeploy가 사용하게 하기 위해서 AWS S3에 저장해야한다. -> CodeDeploy는 저장 기능이 없기 때문이다.

## CI (Continus Integration)
- 지속적 통합
- 자동으로 __테스트와 빌드__ 가 수행되어 __안정적인 배포 파일을 만드는 과정__

### 젠킨스를 사용하지 않는이유
- 젠킨스는 설치형이기 때문에 이를 위한 EC2 인스턴스가 하나 더 필요하다.
- 이제 시작하는 서비스에서 배포를 위한 EC2인스턴스는 부담스럽기 때문에 오픈소스 웹 서비스인 Travis CI를 사용한다.

## 1. spring boot 프로젝트에서 Travis 실행
- build.gradle과 같은 위치에 travis.yml(야믈)파일을 만든다.
- 해당 파일을 git에 push하면 안정적인 배포 파일이 만들어진다.

```
language: java
jdk:
  - openjdk8

branches:
  only:
    - master

# Travis CI 서버의 Home
cache:
  directories:
    - '$HOME/.m2/repository'
    - '$HOME/.gradle'

script: "./gradlew clean build"

before_install:
  - chmod +x ./gradlew

notifications:
  email:
    recipients:
      - devham76@gmail.com
```

## Travis CI 연동시 구조
![travis ci 연동시 구조](https://user-images.githubusercontent.com/55946791/80796805-21d61b80-8bdb-11ea-96b8-c73554e3c374.jpg)

### AWS S3
- Jar 파일을 전달하기 위해 Travis CI와 연동한다
- CodeDeploy는 저장 기능이 없기 때문에 __Travis CI가 빌드한 결과물__ 을 CodeDeploy가 가져갈 수 있도록 __보관하는 공간__
### AWS CodeDeploy
- AWS S3에서 빌드한 결과물을 가지고 __실제 배포__ 를 실행한다

## 2. Travis CI와 AWS S3의 연동 - AWS KEY 발급
- AWS서비스에 외부 서비스가 접근할수없다.
- 따라서 접근 권한을 가진 Key를 생성해서 __Travis CI가 AWS의 S3와 CodeDeploy에 접근할 수 있도록__ 해야한다.
- IAM를 이용해서 Key를 발급받는다.
- 발급 받은 키를 이용해서 travis.yml파일을 수정한다.

```
...
before_deploy:
  - zip -r springboot2-webservice *
  - mkdir -p deploy
  - mv springboot2-webservice.zip deploy/springboot2-webservice.zip
# CodeDeploy는 Jar파일을 인식하지 못하므로 zip파일로 압축한다.

deploy:
  - provider: s3
    access_key_id: # 발급받은 access key
    secret_access_key: # 발급받은 secret key
    bucket: travis-springboot-build
    region: ap-northeast-2
    skip_cleanup: true
    acl: private
    local_dir: deploy
    wait-until-deployed: true
...

```

- git에 push하고 travis를 확인하면 CI성공화면을 볼 수 있다.
![travis 성공](https://user-images.githubusercontent.com/55946791/80797518-023ff280-8bdd-11ea-9983-0eae8337efdd.JPG)

- __AWS S3를 확인하면 배포할 파일이 zip형태로 저장__ 되어있는것을 확인할 수 있다.
![s3 추가 성공](https://user-images.githubusercontent.com/55946791/80797520-03711f80-8bdd-11ea-90be-7d1b3f72d362.JPG)

## 3. CodeDeploy 설정
### EC2에 IAM 역할 추가하기
- EC2와 CodeDeploy를 연동 하기 위해 IAM역할을 생성한다.

### IAM의 사용자 vs 역할
1. 역할
  - __AWS 서비스에만__ 할당할 수 있는 권한
  - EC2, CodeDeploy, SQS등
2. 사용자
  - __AWS 서비스 외__ 에 사용할 수 있는 권한
  - 로컬 PC, IDC 서버 등

<br>
- EC2역할 생성 후, 인스턴스 설정에서 IAM역할 연결, 인스턴스 재부팅.

### CodeDeploy 에이전트 설치
- EC2에 접속 후 명령어 입력

```
[명령어]
[ec2-user@springboot2-webservice ~]$ aws s3 cp s3://aws-codedeploy-ap-northeast-2/latest/install . --region ap-northeast-2

[결과]
download: s3://aws-codedeploy-ap-northeast-2/latest/install to ./install

[권한 추가]
chmod +x ./install

[설치 진행]
sudo ./install auto

[agent 실행 확인]
sudo service codedeploy-agent status

```

### CodeDeploy를 위한 권한 생성
- CodeDeploy에서 EC2에 접근하려면 권한이 필요하다.
- 따라서 AWS의 서비스이므로 IAM의 역할을 생성한다.

### CodeDeploy란?
- CodeDeploy는 AWS의 배포 삼형제

```
1. Code Commit
- 깃 허브와 같은 코드 저장소의 역할

2. Code Build
- Travis CI와 같은 빌드용 서비스

3. CodeDeploy
- AWS의 배포 서비스
- Code Commit와 Code Build와 달리 대체재가 없다.
```

## 4. Travis CI, S3, CodeDeploy연동
- S3에서 넘겨줄 zip파일을 저장할 디렉토리를 생성한다.
- EC2서버에 접속해서 디렉토리 생성

```
mkdir ~/app/step2 && mkdir ~/app/step2/zip
```

> 목표 : Travis CI의 Build가 끝나면 S3에 zip파일 전송되고, 이 zip파일은
/home/ec2-user/app/step2/zip로 복사되어 압축을 풀 예정이다.

### Travis CI 설정은 .travis.yml로 진행했다.
- __.travis.yml__ (테스트,빌드 후 s3에 파일 전달, codedeploy에 배포요청)
  - 1. 빌드
  - 2. springboot2-webservice로 zip파일 만든 후 deploy/springboot2-webservice.zip로 복사(CodeDeploy가 Jar파일 인식 못하므로 zip으로 만든다.)
  - 3. AWS S3에 파일 전달
  - 4. CodeDeploy에 배포요청

```
...
- provider: codedeploy
   access_key_id:
   secret_access_key:
   bucket: travis-springboot-build
   key : springboot2-webservice.zip
   build_type : zip
   application : springboot2-webservice
   deployment_group: springboot2-webservice-group
   region: ap-northeast-2
   wait-until-deployed: true
...
```

### AWS CodeDeploy 설정은 appspec.yml로 진행한다.
- __appspec.yml__ (CodeDeploy가 배포)
    - soruce: CodeDeploy에서 전달해준 파일중 destination으로 이동시킬 대상지정.
    - / 이므로 전체 파일을 이동시킬것임
    - destination : source에서 지정된 파일을 받을 위치.
    - jar를 실행하는 것 등은 destination에서 옮긴 파일들로 진행한다.
```
version: 0.0  # CodeDeploy버전
os: linux
files:
  - source: /   
    destination : /home/ec2-user/app/step2/zip/
    overwrite: yes
```

### 결과
- 위 두개의 파일을 수정,생성 한 후 git에 push한다.
- AWS의 CodeDeploy에 배포 성공한 내역 확인 가능
![codedeploy 배포성공](https://user-images.githubusercontent.com/55946791/80800759-420ad800-8be5-11ea-9b69-0c0f082a19a8.JPG)

- /home/ec2-user/app/step2/zip에 Travis CI파일 -> AWS S3에 있는 파일들이 해당 폴더 아래에 생성된 것을 확인 할 수 있다
![codedeploy 배포성공 zip 폴더](https://user-images.githubusercontent.com/55946791/80800801-5f3fa680-8be5-11ea-9187-28cc309dfa9d.JPG)

## 최종결론
- .travis.yml
  - 테스트, 빌드 후 필요한 파일을 AWS S3에 복사해서 준다.
  - 필요한 파일 : .jar(자바프로젝트), appspecyml(CodeDeploy가 실행할 파일), .sh(배포할 shell script)
```
before_deploy:
  - mkdir -p before-deploy # zip에 포함시킬 파일들을 담을 디렉토리 생성
  - cp scripts/*.sh before-deploy/
  - cp appspec.yml before-deploy/
  - cp build/libs/*.jar before-deploy/
  - cd before-deploy && zip -r before-deploy * # before-deploy로 이동 후 전체 압축
  - cd ../ && mkdir -p deploy # 상위 디렉토리로 이동 후 deploy 디렉토리생성
  - mv before-deploy/before-deploy.zip deploy/springboot2-webservice.zip # deploy로 zip파일 이동
```

- appspec.yml
  - AWS S3에 있는 파일을 EC2서버의 /home/ec2-user/app/step2/zip/에 복사한다.
  - 모든 파일을 ec2-user권한을 준다.
  - deploy.sh파일을 실행 시켜서 배포한다.

```
version: 0.0
os: linux
files:
  - source: /
    destination : /home/ec2-user/app/step2/zip/
    overwrite: yes

permissions:
  - object: /
    patteren: "**"
    owner: ec2-user
    group: ec2-user

hooks:
  ApplicationStart:
    - location: deploy.sh
      timeout: 60
      runas: ec2-user
```
![배포 완료](https://user-images.githubusercontent.com/55946791/80823313-5ec00380-8c17-11ea-8402-cf7996545297.JPG)
