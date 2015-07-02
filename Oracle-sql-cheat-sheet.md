### Working with dates

    -- now, timestamp
    SELECT SYSDATE FROM dual
    
    -- yesterday
    SELECT SYSDATE - 1 FROM dual
    
    -- truncated date (without timestamp)
    SELECT TRUNC(SYSDATE) FROM dual
    
    -- extract date part
    SELECT SYSDATE, TO_DATE(SYSDATE) FROM dual
    
    -- extract year from date
    SELECT EXTRACT(YEAR FROM SYSDATE) FROM dual
    
    -- format string to date
    SELECT TO_DATE('2014-12-01', 'YYYY-MM-DD') FROM dual
    
### Working with numbers

    -- rounds to 1.23
    SELECT ROUND(1.234, 2) FROM DUAL

    -- rounds to 1.2
    SELECT ROUND(1.234, 1) FROM DUAL

### Misc

    -- select top 10 rows
    SELECT * FROM dual WHERE ROWNUM < 10
