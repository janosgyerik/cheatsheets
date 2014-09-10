## Random memo

    sp_help STRING
    sp_helpdb DBNAME
    sp_configure
    sp_who
    sp_spaceused TABLENAME
    
    SELECT name, type FROM dbo.sysobjects WHERE type IN ('U', 'V')
    GO

## Find all tables

    SELECT * FROM sysobjects WHERE type='U' order by name

## Find the columns and schema of a table

    sp_help TABLENAME

    SELECT syscolumns.name, syscolumns.* 
    FROM syscolumns JOIN sysobjects
           ON syscolumns.id=sysobjects.id
    WHERE sysobjects.name='TABLENAME'

## Get the definition of a stored procedure

    sp_helptext name_of_sp

To make the output more readable, replace all occurrences of `/n` with a line break.

## Renaming a table

    sp_rename 'oldname', 'newname'

## Dates

    -- get day part of a date
    SELECT DATEPART(day, getdate())
    -- returns 11
    SELECT DATEPART(day, '20140711')
