---
title: "DATABASE, MYSQL, GROUP BY"
date: 2020-04-17 15:30:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1.

>[고양이와 개는 몇 마리 있을까](https://programmers.co.kr/learn/courses/30/lessons/59040)

```sql
SELECT ANIMAL_TYPE, count(ANIMAL_TYPE) from ANIMAL_INS  group by ANIMAL_TYPE
```

## 2.

>[동명 동물 수 찾기](https://programmers.co.kr/learn/courses/30/lessons/59041)

- __HAVING 은 GROUP BY의 WHERE절과 같다__

```sql
SELECT NAME, COUNT(NAME)
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(*) > 1
```


## 3.

>[입양 시각구하기(1)](https://programmers.co.kr/learn/courses/30/lessons/59412)

- __DATETIME에서 시간만 뽑고싶을 때는 HOUR을 이용한다__

```sql
SELECT HOUR(DATETIME) HOUR, COUNT(*) COUNT
FROM ANIMAL_OUTS GROUP BY HOUR(DATETIME)
HAVING HOUR >= 9 AND HOUR <= 19
ORDER BY HOUR(DATETIME)
```


## 4.

>[입양 시각구하기(2)](https://programmers.co.kr/learn/courses/30/lessons/59413)

- __SET 변수를 이용한다__

```sql
SET @hour= -1;
SELECT
  (@hour := @hour +1) as HOUR,
  (SELECT COUNT(*) FROM ANIMAL_OUTS WHERE HOUR(DATETIME) = @hour) as COUNT
from ANIMAL_OUTS
WHERE @hour < 23
```
