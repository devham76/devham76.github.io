---
title: "JAVA, BufferedReader & BufferedWriter"
date: 2020-01-13 20:30:28 -0400
categories: JAVA
tags : [JAVA]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## BufferedReader
- 입력되거나 출력할 데이터를 바로 전달받거나 전달하지 않고 <u>중간에 버퍼링이 된 후에 </u>작업한다
- 버퍼를 거쳐 간접적으로 작업되기 때문에 시스템의 데이터처리 효율성을 높여준다


### BufferedReader vs Scanner
- Scanner
    - space, enter 모두 경계로 인식한다
    - 입력받은 데이터 가공이 편리하다
- BufferedReader
    - enter만 경계로 인식한다
    - String으로 고정되므로 가공이 불편하다
    - 많은 양의 데이터를 입력 받을 때 효율적이다. Buffer 메모리를 사용하기 때문에 작업속도 차이가 많이 난다

### 예제
- BufferedReader

```java
BufferedReader bf = new BufferedReader(new InputStreamReader(System.in)); //선언
String s = bf.readLine(); //String
int i = Integer.parseInt(bf.readLine()); //Int

StringTokenizer st = new StringTokenizer(s); //StringTokenizer인자값에 입력 문자열 넣음
int a = Integer.parseInt(st.nextToken()); //첫번째 호출
int b = Integer.parseInt(st.nextToken()); //두번째 호출

String array[] = s.split(" "); //공백마다 데이터 끊어서 배열에 넣음
```

- BufferedWriter

```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));//선언
String s = "abcdefg";//출력할 문자열
bw.write(s+"\n");//출력
bw.flush();//남아있는 데이터를 모두 출력시킴
bw.close();//스트림을 닫음
```

### 주의할 점
- readLine()시 리턴값은 String으로 고정이다
- 예외처리가 필요하다 readLine시마다 try&catch해주거나 throws IOException을 통해 작업한다


---
## Reference
<https://coding-factory.tistory.com/251>
