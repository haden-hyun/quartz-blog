---
title: DB 복사
created: 2024-10-28
modified: 2024-10-28 21:55
cssclasses:
  - max
tags:
  - postgresql/pg_dump
  - postgresql/pg_restore
---
> [!summary] 요약
> - Postgresql이 설치된 폴더 중 `bin` 경로에서 작업
> - `pg_dump`: DB 내 정보를 복사
> - `pg_restore`: 복사된 파일을 복원

---
# 1. 복제(pg_dump)
> [!hint] 기본 틀
> - 스키마 전체: pg_dump -h `[호스트명]` -p `[포트]` -U `[유저명]` -d `[DB명]` -n `[스키마명]`
> - 스키마 내 특정 테이블: pg_dump -h `[호스트명]` -p `[포트]` -U `[유저명]` -d `[DB명]` -t `[스키마명].[테이블명]`
> 	- `-t` : 옵션에 스키마명까지 입력
- `--data_only`: PK 및 Index 와 같은 메타데이터는 제외하고 복사
- `-Fc`: 복사한 결과물을 `.sql`파일이 아닌 `.dump` 파일로 저장하는 경우 사용
	- 복제할 결과물이 많은 경우 쿼리문 열지 못함
- `-n`: 스키마 전체
```linux
-- 특정 테이블만 복사
pg_dump -h postgres -p 5432 -U postgres -d database -t portfolio.tb_daily_balance_main encoding=UTF8 --data-only -Fc > C:/Users/BV-HYUNHAEJUN/Documents/tb_bigvalue_price_info_copy.dump

-- 데이터베이스 전체 복사
pg_dump -h host_server -p 5432 -U postgres -d database -n  encoding=UTF8 -Fc > C:/Users/BV-HYUNHAEJUN/Documents/tb_bigvalue_price_info_copy.dump
```
---
# 2. 복원(pg_restore)
> [!warning] 주의사항
> - 스키마 전체를 복원하는 경우, DB 내에 해당 스키마가 없어야함!!
> - 스키마 전체: pg_restore -h `[호스트명]` -p `[포트]` -U `[유저명]` -d `[DB명]` -n `[스키마명]` `[파일경로]`

```linux
pg_restore -h host_server -U postgres -p 5432 -d database -n etc C:/Users/BV-HYUNHAEJUN/Documents/리뉴얼_운영서버_복제/etc_copy.dump
```

---
>[!example] 참고사이트
>- [Postgresql 백업 및 리스토어](https://sehyeok.tistory.com/189)



