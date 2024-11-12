---
title: 데이터 정의 언어(DDL)
created: 2024-07-05
tags:
  - sql/ddl
  - sql/create
  - sql/alter
  - sql/drop
  - sql/postgresql
---
> [!warning] 본 글은 ==PostgreSQL==을 기준으로 작성함

> [!hint] 작성 내용 및 요약
> 1. 테이블 명세 정의: 스키마, 데이터 타입, PK, FK, index 등
> 2. 주요 연산자: `CREATE`, `ALTER`, `DROP`
> 	1. `CREATE`: 새로운 테이블 생성
> 	2. `ALTER`: 테이블 내 열 및 제약조건 생성 및 삭제
> 	3. `DROP`: 테이블 삭제

---
# 1. CREATE
> [!summary] 새로운 릴레이션을 생성
> - 예시) 교수(<u>instructor</u>) 릴레이션 생성
> 	- ID, 이름, 학과명, 연봉 스키마 생성
> 	- PK는 <u>ID</u> 로 지정
> 	- FK는 학과(<u>department</u>) 릴레이션을 참고하여 학과명으로 설정
> 	- 학과명은 null 값이 없도록 설정

```sql
create table 
instructor(ID char(5),
		   name varchar(20) not null,
		   dept_name varchar(20),
		   salary numeric(8,2),
		   primary key (ID),
		   foreign key (dept_name) reference department);
```
---
# 2. ALTER
## 테이블 수정
> ALTER TABLE 테이블명 RENAME TO 변경_테이블명
```sql
alter table instructor
rename to new_instructor
```
## 열 수정
### 열 생성 및 삭제
> 1. 열 생성: ALTER TABLE 테이블명 **ADD** COLUMN 컬럼명 <u>데이터타입</u>
> 2. 열 삭제: ALTER TABLE 테이블명 **DROP** COLUMN 컬럼명 <u>데이터타입</u>

```sql
-- 1. 열 생성
alter table instructor
add column age integer,
add column major varchar(10)
-- 2. 열 삭제
alter table instructor
drop column major
```
### 열 이름 변경
> ALTER TABLE 테이블명 RENAME COLUMN 컬럼명 TO 변경컬럼명
- 한 명령문에 하나의 열 이름만 변경 가능
```sql
alter table instructor 
rename column col_nm1 to new_col_nm1
alter table instructor
rename column col_nm2 to new_col_nm2
```
### 데이터 타입 변경
> ALTER TABLE 테이블명 ALTER COLUMN 컬럼명 TYPE 변경데이터타입
```sql
alter table instructor
alter column salary type varchar(20);
```
## 제약조건(PK 추가 및 삭제)
### 사후 PK 추가 및 삭제
> 1. PK 추가: ALTER TABLE 테이블명 ADD CONSTRAINT pk명 PRIMARY KEY (컬럼명)
> 2. PK 제거: ALTER TABLE 테이블명 DROP CONSTRAINT pk명
```sql
-- 1. PK 생성
alter table instructor
add constraint ID_pk primary key (ID)
-- 2. PK 제거
alter table instructor
drop constraint ID_pk
```
### 사전 설정된 PK 제거
> 1. 설정된 PK 제약 이름 확인
> 2. PK 제거: ALTER TABLE 테이블명 DROP CONSTRAINT 제약PK명

```sql
-- 1. 스키마 내 테이블의 PK 제약 이름 확인: `instructor_pkey`
select conname
from pg_constraint
where conrelid = 'schema.instructor'::regclass
and contype = 'p';
-- 2. PK 조건 제거
alter table instructor
drop constraint instructor_pkey;
```
---
# 3. DROP
> [!warning] 주의할 점
> - `DROP` : 테이블 전체를 삭제. 절대 되돌릴 수 없음
> - `DELETE`: 원하는 데이터만 지울 수 있으며, 삭제 후 되돌릴 수 있음
> - `TRUNCATE`: 인덱스, 데이터가 삭제. 테이블은 삭제되지 않지만, 삭제 후 되돌릴 수 없음
```postgresql 
drop table instructor
```
