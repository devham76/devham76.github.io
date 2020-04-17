---
title: "DATABASE, MYSQL, SUM/MAX/MIN"
date: 2020-04-17 15:30:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1.

>[최대값 구하기](https://programmers.co.kr/learn/courses/30/lessons/59415)

```sql
SELECT DATETIME
FROM ANIMAL_INS
ORDER BY DATETIME DESC
LIMIT 1
```

## 2.

>[최솟값 구하기](https://programmers.co.kr/learn/courses/30/lessons/59038)


```sql
SELECT DATETIME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1
```


## 3.

>[동물 수 구하기](https://programmers.co.kr/learn/courses/30/lessons/59406)


```sql
SELECT COUNT(*) COUNT
FROM ANIMAL_INS
```


## 4.

>[중복제거](https://programmers.co.kr/learn/courses/30/lessons/59408)


```sql
SELECT  count(distinct name) from ANIMAL_INS
```
