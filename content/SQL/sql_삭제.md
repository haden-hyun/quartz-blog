---
title: sql_삭제
created: 2024-01-31
modified: 2024-01-31 10:20
cssclasses:
  - max
tags:
  - sql
  - sql/delete
  - dql/truncate
  - sql/drop
---
- `DELETE`: 데이터 지우지만, 테이블 용량 줄지 않아 원하는 데이터만 지울 수 있음
	- 삭제 후 되돌릴 수 있음
- `TRUNCATE`: 인덱스, 데이터 삭제되어 용량 줄어들지만, 테이블은 삭제되지 않음
	- 삭제 후 절대 되돌릴 수 없음
- `DROP`: 테이블 전체를 삭제.
	- 삭제 후 절대 되돌릴 수 없음