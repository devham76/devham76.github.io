---
title: "DATABASE, table 생성/삭제"
date: 2019-12-04 15:20:28 -0400
categories: DB
tags : [DB]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

### Table 생성
```sql
CREATE TABLE `member` (
	seq int not null auto_increment,
	grade varchar(5) NOT NULL,
	name VARCHAR(20) NOT NULL,
	phone varchar(20),
	primary key (seq)
)ENGINE=myisam DEFAULT CHARSET=utf8
```

### Table 삭제
```sql
DROP table `member`;
```

### Table 수정
- 컬럼 추가 (add)
```sql
ALTER TABLE `attend` ADD COLUMN parking int(1) default 0 after message;
```

- 컬럼 변경 (modify)
```sql
ALTER TABLE table_name MODIFY COLUMN ex_column varchar(16) NULL;
```

- 컬럼 이름까지 변경 (chnge)
```sql
ALTER TABLE table_name CHANGE COLUMN ex_column ex_column2 varchar(16) NULL;
```

- 컬럼 삭제 (drop)
```sql
ALTER TABLE table_name DROP COLUMN ex_column;
```

---

### Insert
```sql
INSERT INTO `memeber` (grade, name) VALUES("13", "이혜미");
```

### Update  
```sql
UPDATE `member` SET phone='0101111111' WHERE name='이혜미';
```

### Delete
```sql
DELETE FROM `member` WHERE seq = 0;
DELETE FROM `member`  # member 테이블 내 모든 데이터 삭제
```


---
## Reference
- <https://vlee.kr/563>
- <https://extbrain.tistory.com/39>
