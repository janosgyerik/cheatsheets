```
sp_help STRING
sp_helpdb DBNAME
sp_configure
sp_who
sp_spaceused TABLENAME

SELECT name, type FROM dbo.sysobjects WHERE type IN ('U', 'V')
GO
```

## Find all tables

    SELECT * FROM sysobjects WHERE type='U' order by name

## Find the columns of a table

```
SELECT syscolumns.name, syscolumns.* 
FROM syscolumns JOIN sysobjects
       ON syscolumns.id=sysobjects.id
WHERE sysobjects.name='the_table'
```

## Get the definition of a stored procedure
```
sp_helptext name_of_sp
```
To make the output more readable, replace all occurrences of `/n` with a line break.

