---
title: "WEB, 웹서버, 아파치 기본"
date: 2019-10-02 22:39:28 -0400
categories: WEB
tags : [WEB, webproject]
---
---
## 인터넷 브라우저와 서버
1. 내 노트북 web browser( client )에서 google.com( domain )을 입력하고 엔터를 친다.
2. ip 주소로 구글 웹서버에 접속(request)하게된다.
3. web server 에서는 저장소에서 client가 요청한 index.html을 찾아 resopnse 해준다

---
![web_basic](https://user-images.githubusercontent.com/55946791/66047071-139b2080-e562-11e9-9363-61880e8947ca.JPG)

## 아파치 서버 설치
1. vmware에 ubuntu server버전 설치
2. sudo apt-get update
3. sudo apt-get apache2 install ;아파치 설치
4. 아파치 시작
- sudo service apache2 start
- sudo service apache2 stop
- sudo serviec apache2 restart
5. ip address로 사설ip 주소 알아내기
6. elinks설치
7. 아파치 웹서버가 잘 실행되고 있는지 웹서버 접속하여 확인
elinks 127.0.0.1 또는 elinks [사설ip] 를 입력하여 확인가능

---
## Reference 
[생활코딩/웹서버,아파치](https://opentutorials.org/course/2598/14446)


---
