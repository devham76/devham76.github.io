---
title: "Linux, 기본 명령어"
date: 2020-05-11 20:00:28 -0400
categories: etc
tags : [Linux]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## pwd (print working directory)

```
$ pwd
/c/Users/ComPuter/Documents/tech-interview-study
```

## cd (change directory)
```
$ cd /home/itholic/mydir
$ pwd
/home/itholic/mydir
```

## ls(list)

```
ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ ls -l
total 12
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/
-rw-r--r-- 1 ComPuter 197121 5424 5월  11 17:20 README.md

ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ ls -al
total 28
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 ./
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:04 ../
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:21 .git/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/

```

## cp(copy)
- 파일 or 디렉토리(-r 옵션) 복사

```
ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study/forder (master)
$ cp text.text text_copy.text

ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study/forder (master)
$ ll
total 2
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:29 text.text
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:30 text_copy.text

------------------
ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ cp -r forder/ forder_copy/

ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ ll
total 12
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:30 forder/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:30 forder_copy/
-rw-r--r-- 1 ComPuter 197121 5424 5월  11 17:20 README.md


```

## mkdir

```
ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ mkdir forder

ComPuter@DESKTOP-U7PIVL5 MINGW64 ~/Documents/tech-interview-study (master)
$ ll
total 12
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:28 forder/
-rw-r--r-- 1 ComPuter 197121 5424 5월  11 17:20 README.md

```

## move
- 파일 or 디렉토리 이동
- 이름 변경시에도 사용한다

```
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:30 forder/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:30 forder_copy/
-rw-r--r-- 1 ComPuter 197121 5424 5월  11 17:20 README.md

$ mv forder_copy/ forder

$ ll
total 12
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:13 contents/
drwxr-xr-x 1 ComPuter 197121    0 5월  11 17:32 forder/
-rw-r--r-- 1 ComPuter 197121 5424 5월  11 17:20 README.md

----
[이름 변경]
$ ls
bye  count.txt  text_copy.text

$ mv bye hi

$ ls
count.txt  hi  text_copy.text


```

## rm (remove)
- 디렉토리는 -r옵션 필요
- 사용자에게 삭제 여부 묻지 않고 삭제시 -f

```
$ ll
total 1
drwxr-xr-x 1 ComPuter 197121 0 5월  11 17:30 forder_copy/
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:30 text_copy.text

$ rm -r forder_copy/

$ ll
total 1
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:30 text_copy.text

```

## touch
- 최근 업데이트 일자를 현재 시간으로 변경

```
$ ll
total 1
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:30 text_copy.text

$ touch text_copy.text

$ ll
total 1
-rw-r--r-- 1 ComPuter 197121 5 5월  11 17:35 text_copy.text

```

## cat (concatenate)
1. 파일 내용을 보여준다

```
$ cat text_copy.text
test 파일 입니다.
리눅스 기본 명령어를 공부하고있습니다.
```

2. 파일을 만들어준다
  - 입력후 ctrl+d누르면 종료

  ```
  $ cat > file2.text
  _____________________________
   cat 을 이용해 덧붙일 파일입니다

  ```

3. 파일을 붙여준다.

```
$ cat text_copy.text file2.text > new_file.txt

$ cat new_file.txt
test 파일 입니다.
리눅스 기본 명령어를 공부하고있습니다.
_____________________________
 cat 을 이용해 덧붙일 파일입니다


```


### head
- 파일의 앞부분을 보여주고 싶은 줄 수 만큼 보여준다

```
$ cat count.txt
1
2
3
4
5
6
7
8
9
10
11
12

$ head -3 count.txt
1
2
3

```

### tail
- 파일의 뒷부분을 보여주고 싶은 줄 수 만큼 보여준다
- 옵션 지정 안하면, 하위 10줄을 보여준다.
- __tail -f__ : 파일 내용을 계속 띄어주고, 파일 변경시 업데이트 된 내용을 보여준다.

```
$ tail -f count.txt
2
3
4
5
6
7
8
9
10
hi every body
bybyye
hello world
(명령어가 종료되지 않고 계속 해당 화면을 출력하며, 파일 내용 변경시 자동으로 갱신해준다)
```

## find
- 특정 파일이나 디렉토리를 검색한다

> find [검색경로] -name [파일명]

- 파일명을 풀 네임으로 하거나 ** 를 이용해서 해당하는것 모두 찾을 수 있다

```
$ find ./ -name "**.md"
./contents/algorithm.md
./contents/db.md
./contents/java.md
./contents/network.md
./contents/os.md
./contents/software-engineering.md
./README.md

$ find ./ -name "**file**"
./file2.text
./new_file.txt

$ ll
total 4
-rw-r--r-- 1 ComPuter 197121  53 5월  11 17:46 count.txt
-rw-r--r-- 1 ComPuter 197121  75 5월  11 17:40 file2.text
-rw-r--r-- 1 ComPuter 197121 154 5월  11 17:41 new_file.txt
-rw-r--r-- 1 ComPuter 197121  79 5월  11 17:36 text_copy.text

```

### find - exec 삭제

```
$ find ./ -name "**file**"
./file2.text
./new_file.txt

$ find ./ -name "**file**" -exec rm {} \;

$ ls
count.txt  text_copy.text

```

### find - exec, sed 파일내용 변경
- hi를 hello로 변경

```
$ cat hi.txt
hi1
hi2
hi3
hi4
hi5
hi6
hi7

$ find ./ -name "hi.txt" -exec sed -i 's/hi/hello/g' {} \;

$ cat hi.txt
hello1
hello2
hello3
hello4
hello5
hello6
hello7

```

### find - type 파일 or 디렉토리 지정 검색

```
$ find ./ -type d
./
./dir1
./dir2
./dir3
./dir4


$ find ./ -type f
./file1
./file2
./file3
./file4$ find ./ -type d
./
./dir1
./dir2
./dir3
./dir4


$ find ./ -type f
./file1
./file2
./file3
./file4
```

- 응용 (이름으로 찾기 + 파일 타입)

```
find ./ -name "**.md" -type f
./contents/algorithm.md
./contents/db.md
./contents/java.md
./contents/network.md
./contents/os.md
./contents/software-engineering.md
./README.md

```

## find  +  | wc -l
- 해당 하는 파일 or 디렉토리 개수

```
$ find ./ -name "**.md**"
./contents/algorithm.md
./contents/db.md
./contents/java.md
./contents/network.md
./contents/os.md
./contents/software-engineering.md
./README.md

$ find ./ -name "**.md" | wc -l
7
```

## grep
- 파일 내부 문자열 검색

```
$ grep [OPTION] [PATTERN] [FILE]
```

- ex)

```
$ grep -r "가상메모리" ./
./contents/os.md:* [가상메모리란?](#가상메모리란?)
./contents/os.md:- 가상메모리- 페이지
./contents/os.md:- 가상메모리를 __같은 크기의 블록으로 나눈것을 페이지__ 라고한다.
./contents/os.md:- 가상메모리를 __서로 크기가 다른 논리적 단위인 세크멘트로 분할해서 메모리를 할당__ 하여 실제 메모리 주소로 변환을 하게 된다.
./contents/os.md:### 가상메모리란?
./contents/os.md:- 가상메모리 어떻게 구현하나요 ? - 페이징, 세크멘테이션
./contents/os.md:- 가상메모리 크기 = 물리메모리 + 스왑영역 (하드디스크에 존재 or 멤리 관리자가 관리하는 영역)
./README.md:* 가상메모리란?

```

```
$ find ./ -type f | xargs grep "가상메모리"
```

---
## 참고
- <https://itholic.github.io/linux-basic-mv/>
- <https://overcode.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%ED%8C%8C%EC%9D%BC-%EC%B0%BE%EA%B8%B0-%ED%8C%8C%EC%9D%BC%EC%86%8D-%EB%AC%B8%EC%9E%90%EC%97%B4-%EC%B0%BE%EA%B8%B0>
