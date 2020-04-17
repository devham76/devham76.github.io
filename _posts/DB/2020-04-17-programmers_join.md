---
title: "DATABASE, MYSQL, JOIN"
date: 2020-04-17 15:30:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

![SQL JOIN](https://user-images.githubusercontent.com/55946791/79540127-90d35080-80c2-11ea-8912-c7782c8e08ec.png)

## 1.

>[없어진 기록](https://programmers.co.kr/learn/courses/30/lessons/59042)

## 문제
입양을 __간 기록은 있는데__ , 보호소에 __들어온 기록이 없는__ 동물의 ID와 이름을 ID 순으로 조회하는 SQL문을 작성해주세요.

![INOUT](https://user-images.githubusercontent.com/55946791/79541114-3a671180-80c4-11ea-9c33-4cbb8543fad7.JPG)


```sql
select OUTS.ANIMAL_ID, OUTS.NAME
from  ANIMAL_INS INS
RIGHT join ANIMAL_OUTS OUTS
on INS.ANIMAL_ID =  OUTS.ANIMAL_ID
WHERE INS.ANIMAL_ID IS NULL
```

## 2.

>[있었는데요 없었습니다](https://programmers.co.kr/learn/courses/30/lessons/59043)


```sql
SELECT INS.ANIMAL_ID, INS.NAME
FROM ANIMAL_INS INS, ANIMAL_OUTS OUTS
WHERE INS.ANIMAL_ID = OUTS.ANIMAL_ID
 AND INS.DATETIME > OUTS.DATETIME
ORDER BY INS.DATETIME
```


## 3.

>[오랜 기간 보호한 동물(1)](https://programmers.co.kr/learn/courses/30/lessons/59044)

## 문제
아직 입양을 __못 간 동물 중__ , __가장 오래 보호소에__ 있었던 동물 __3마리의__ 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일 순으로 조회해야 합니다.

## 해결
![INOUT2](https://user-images.githubusercontent.com/55946791/79542104-0391fb00-80c6-11ea-9c99-720e8ca6c716.JPG)

- 아직 입양을 못 간 동물이므로, 입양목록에만 있는 동물을 확인한다.(LEFT JOIN)

```sql
SELECT INS.NAME, INS.DATETIME
  FROM ANIMAL_INS INS
LEFT JOIN  ANIMAL_OUTS OUTS
  ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.ANIMAL_ID IS NULL
  ORDER BY DATETIME
LIMIT 3
```


## 4.

>[보호소에서 중성화한 동물](https://programmers.co.kr/learn/courses/30/lessons/59045)


```sql
SELECT INS.ANIMAL_ID, INS.ANIMAL_TYPE, INS.NAME
FROM ANIMAL_INS INS, ANIMAL_OUTS OUTS
WHERE INS.ANIMAL_ID = OUTS.ANIMAL_ID
 AND INS.SEX_UPON_INTAKE LIKE 'Intact%'
 AND ( OUTS.SEX_UPON_OUTCOME LIKE 'Spayed%' OR  OUTS.SEX_UPON_OUTCOME LIKE 'Neutered%')
ORDER BY INS.ANIMAL_ID ASC
```
