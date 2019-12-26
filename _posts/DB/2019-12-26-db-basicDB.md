---
title: "DATABASE, 데이터베이스(DataBase)"
date: 2019-12-26 15:20:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 데이터베이스란
- database는 통합하여 관리되는 데이터의 집합체
- DBMS(Database Management System) 데이터베이스를 관리하는 미들웨어를 데이터베이스 관리 시스템이라고 한다

## SQL(Structured Query Language)
- sql은 데이터베이스에서 데이터를 정의,조작,제어 하기 위해 사용하는 언어이다
1. DDL(Data Defintion Language)
2. DML(Data Manipulation Language)
3. DCL(Data Control Language)

|--|--|--|
|속성|설명|주요 명령어|
|DDL|DB나 테이블 등을 생성,삭제 하거나 그 구조를 변경하기 위한 명령어 | CREATE,ALTER,DROP
|DML| DB에 저장된 데이터를 처리하거나 조회,검색 | INSERT, UPDATE, DELETE, SELECT등
|DCL| DB에 저장된 <u>데이터를 관리하기 위해 데이터의 보안성 및 무결성 등을 제어하기 위한 명령어</u>| GRANT, REVOKE등

---
## Reference
- <http://tcpschool.com/mysql/DB>
