### Date related

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
