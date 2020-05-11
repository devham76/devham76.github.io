---
title: "Linux, 명령어 - find"
date: 2020-05-11 20:00:28 -0400
categories: etc
tags : [Linux]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## find
- find는 리눅스에서 __파일 및 디렉토리를 검색할__ 때 사용하는 명령입니다.
- 이름 그대로 리눅스에서 접근할 수 있는 파일 시스템에서, 파일 및 디렉토리를 "찾는(find)" 것이죠.

```
find [OPTION...] [PATH] [EXPRESSION...]
  OPTION
    -P        : 심볼릭 링크를 따라가지 않고, 심볼릭 링크 자체 정보 사용.
    -L        : 심볼릭 링크에 연결된 파일 정보 사용.
    -H        : 심볼릭 링크를 따라가지 않으나, Command Line Argument를 처리할 땐 예외.
    -D        : 디버그 메시지 출력.
  EXPRESSION
    -name     : 지정된 문자열 패턴에 해당하는 파일 검색.
    -empty    : 빈 디렉토리 또는 크기가 0인 파일 검색.
    -delete   : 검색된 파일 또는 디렉토리 삭제.
    -exec     : 검색된 파일에 대해 지정된 명령 실행.
    -path     : 지정된 문자열 패턴에 해당하는 경로에서 검색.
    -print    : 검색 결과를 출력. 검색 항목은 newline으로 구분. (기본 값)
    -print0   : 검색 결과를 출력. 검색 항목은 null로 구분.
    -size     : 파일 크기를 사용하여 파일 검색.
    -type     : 지정된 파일 타입에 해당하는 파일 검색.
    -mindepth : 검색을 시작할 하위 디렉토리 최소 깊이 지정.
    -maxdepth : 검색할 하위 디렉토리의 최대 깊이 지정.
    -atime    : 파일 접근(access) 시각을 기준으로 파일 검색.
    -ctime    : 파일 내용 및 속성 변경(change) 시각을 기준으로 파일 검색.
    -mtime    : 파일의 데이터 수정(modify) 시각을 기준으로 파일 검색.
```

- ex)
- 도메인이름_오늘날짜.log 인 로그파일에서 도메인 별로 log파일을 찾으려면,

```
find . -name "domain**.log"
```

---
## 참고
- <https://recipes4dev.tistory.com/156?category=768818>
