---
title: "Linux, 명령어 - xagrs"
date: 2020-05-11 20:00:28 -0400
categories: etc
tags : [Linux]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## xargs
- 보통 기본적인 명령어(find, ls, cat) 뒤에 파이프로 추가하여 사용함
- 간단히 설명하면 파이프 이전의 내용을 인자로 받아 명령어를 실행하는 구조

## 예제
- find + xargs rm
: 파일 or 디렉토리 찾아서 삭제

```
$ find ./ -name "*.txt"
./t.txt
./t2.txt


$ find ./ -name "*.txt" | xargs rm

$ ls
test

```

- find + xargs grep [옵션] [찾을 내용] + wc -l
: 찾은 파일 중에서 찾을 내용이 있는 파일들의 개수

```
$ find ./ -type f | xargs grep -i "heap" | wc -l
15
```

- find . -name "woowaatv*.log" | xargs grep -l "eztoc"

---
## 참고
- <http://www.dreamy.pe.kr/zbxe/CodeClip/164220>
