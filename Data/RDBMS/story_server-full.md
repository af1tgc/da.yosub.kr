---
title: RDBMS 용량 이슈
description: 
published: true
date: 2023-04-21T02:43:20.436Z
tags: rdbms, mysql
editor: markdown
dateCreated: 2023-04-21T01:05:09.885Z
---

# Server Full

tab을 실행하면?
```
cd data-bash: cannot create temp file for here-document: No space left on device
```
용량 확인
```sql
SELECT 
  TABLE_NAME as tbl,
  ROUND(SUM(data_length+index_length)/(1024*1024), 2) AS mb
FROM information_schema.tables A
GROUP BY tbl
ORDER BY mb DESC; 
```

실제 데이터 용량은 40G.
- The MySQL approximation of PostgreSQL's vacuum is `OPTIMIZE TABLE tablename` ( [offical docs](https://dev.mysql.com/doc/refman/5.7/en/optimize-table.html) ) 
  - REF. [Why is it a vacuum not needed with Mysql compared to the PostgreSQL?](https://stackoverflow.com/questions/25153532/why-is-it-a-vacuum-not-needed-with-mysql-compared-to-the-postgresql)
- `index`, `log file`, `temporary file` 등이 용량을 차지함
  - /var/lib/mysql
  - DB 구조가 불필요하게 복잡해져서인 경우일 수도 있음
- 확인 결과 binlog 가 42G 정도 생성되어 있음.
  - DDL / DML 을 통하여 데이터 변화가 발생할 경우 기록
  - 단, Disk Full 상태에서 sql 쿼리 실행 불가
  
  ```sql
  show binary logs;
  purge master logs to 'binlog.xxx';
  ```

Optimize 실행시
```sql
OPTIMIZE TABLE tablename
```
```
Error Code: 2013. Lost connection to MySQL server during query
```