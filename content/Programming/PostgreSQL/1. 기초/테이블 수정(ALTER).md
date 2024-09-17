---
title: 테이블 수정(ALTER)
created: 2024-09-17
modified: 2024-09-17 15:00
cssclasses:
  - max
tags:
  - postgresql/ddl/alter
  - postgresql/테이블수정
  - postgresql/열수정
---
> [!summary] 요약
> - 1차적으로 테이블 그 자체 또는 테이블 내 열 값을 수정할 경우 `ALTER` 명령어를 사용함
> - 그 후 조건에 맞게 2차 명령어 입력
> 	- `rename`: 테이블 및 열 이름 변경
> 	- `add` : 새로운 열 및 제약조건 추가
> 	- `drop` : 기존 열 및 사전 제약조건 제거

- sql 코드블럭 실험
- sql, postgresql, mysql
```sql
-- 일반 SQL
select * from table_name
```

```postgresql
-- PostgreSQL
select * from table_name
```

```mysql
-- Mysql
select * from table_name
```

# 1. 테이블 수정
> 기존에 생성한 테이블의 이름을 변경
```postgresql
alter table 테이블명
rename to NEW_TABLE
```

# 2. 열 수정
## 1) 새로운 열 생성 및 삭제
## 2) 열 이름 변경
## 3) 열 데이터 타입 변경
## 3. 제약조건(PK, index 등) 수정
## 1) 사후 PK 추가 및 삭제
## 2) 사전 PK 제거

---
>[!example] 참고사이트


