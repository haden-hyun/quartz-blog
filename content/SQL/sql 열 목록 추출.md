> [!hint] 목적
> 특정 스키마에 있는 특정 테이블의 열 이름 목록을 가져오는 방법


```sql file:열목록
select column_name
from information_schema.columns
where table_schema = '스키마명'
and table_name = '테이블명'
```

#### 테이블 구조 확인
- 데이터베이스 명
- 스키마명
- 테이블명
- 컬럼목록
- 컬럼 위치
- null 여부
- 데이터 타입
- 최대 길이
```sql
SELECT TABLE_CATALOG            as Database  
     , TABLE_SCHEMA             as Schema  
     , TABLE_NAME               as Table  
     , COLUMN_NAME              as Column  
     , ORDINAL_POSITION         as Position  
     , COLUMN_DEFAULT           as Default  
     , IS_NULLABLE              as Nullable  
     , DATA_TYPE                as Data_Type  
     , CHARACTER_MAXIMUM_LENGTH as Max_Length  
     , NUMERIC_PRECISION        as Precision  
     , NUMERIC_SCALE            as Scale  
FROM INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = '지방행정인허가_교육'  
and table_schema = 'mg'  
ORDER BY ORDINAL_POSITION;
```