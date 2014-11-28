### Date related

```sql
-- now, timestamp
SELECT sysdate FROM dual

-- yesterday
SELECT sysdate - 1 FROM dual

-- truncated date (without timestamp)
SELECT TRUNC(SYSDATE) FROM dual

-- extract date part
SELECT sysdate, to_date(sysdate) FROM dual

-- extract year from date
SELECT extract(year from sysdate) FROM dual
```
