### Date related

```sql
-- now, timestamp
SELECT sysdate FROM dual

-- extract date part
SELECT sysdate, to_date(sysdate) FROM dual
```
