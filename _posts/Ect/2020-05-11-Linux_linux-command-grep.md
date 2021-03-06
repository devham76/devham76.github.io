---
title: "Linux, 명령어 - grep"
date: 2020-05-11 20:00:28 -0400
categories: etc
tags : [Linux]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## grep
- grep은 입력으로 전달된 __파일의 내용에서 특정 문자열을 찾고자할__ 때 사용하는 명령어입니다.
- 리눅스에서 가장 많이 사용되는 명령어 중 하나이죠.

```
grep [OPTION...] PATTERN [FILE...]
       -E        : PATTERN을 확장 정규 표현식(Extended RegEx)으로 해석.
       -F        : PATTERN을 정규 표현식(RegEx)이 아닌 일반 문자열로 해석.
       -G        : PATTERN을 기본 정규 표현식(Basic RegEx)으로 해석.
       -P        : PATTERN을 Perl 정규 표현식(Perl RegEx)으로 해석.
       -e        : 매칭을 위한 PATTERN 전달.
       -f        : 파일에 기록된 내용을 PATTERN으로 사용.
       -i        : 대/소문자 무시.
       -v        : 매칭되는 PATTERN이 존재하지 않는 라인 선택.
       -w        : 단어(word) 단위로 매칭.
       -x        : 라인(line) 단위로 매칭.
       -z        : 라인을 newline(\n)이 아닌 NULL(\0)로 구분.
       -m        : 최대 검색 결과 갯수 제한.
       -b        : 패턴이 매치된 각 라인(-o 사용 시 문자열)의 바이트 옵셋 출력.
       -n        : 검색 결과 출력 라인 앞에 라인 번호 출력.
       -H        : 검색 결과 출력 라인 앞에 파일 이름 표시.
       -h        : 검색 결과 출력 시, 파일 이름 무시.
       -o        : 매치되는 문자열만 표시.
       -q        : 검색 결과 출력하지 않음.
       -a        : 바이너리 파일을 텍스트 파일처럼 처리.
       -I        : 바이너리 파일은 검사하지 않음.
       -d        : 디렉토리 처리 방식 지정. (read, recurse, skip)
       -D        : 장치 파일 처리 방식 지정. (read, skip)
       -r        : 하위 디렉토리 탐색.
       -R        : 심볼릭 링크를 따라가며 모든 하위 디렉토리 탐색.
       -L        : PATTERN이 존재하지 않는 파일 이름만 표시.
       -l        : 패턴이 존재하는 파일 이름만 표시.
       -c        : 파일 당 패턴이 일치하는 라인의 갯수 출력.
```

### $ grep [OPTION] [PATTERN] [FILE]
ex ) grep -l "eztoc" .

```
[하위 디렉토리에서 "heap" 문자열 탐색. i: 대소문자 구분x]
$ grep -ir "heap"
./contents/java.md:- Heap 메모리 영역에 적재된 객체의 생존 여부를 판단하여 더 이상 사용되지 않는(참조 되지 않는) 객체를 해제하는 방식으로 메모리를 자동 관리한다.
./contents/java.md:**Heap영역은 GC의 주요 대상**

[하위 디렉토리, 대소문자 구분x, 파일 찾기]
$ grep -lir "heap"
contents/java.md
contents/os.md

```
---
## 참고
- <https://recipes4dev.tistory.com/157>
