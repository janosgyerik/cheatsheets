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

    -- yesterday
    SELECT dateadd(day, -1, getdate())
    -- last month
    SELECT dateadd(month, -1, getdate())

## Converting between types, casting

    -- returns 12
    SELECT CONVERT(int, STR_REPLACE('12M', 'M', ''))

## Misc

    -- between and not between
    SELECT * FROM aTable WHERE CODE BETWEEN 877 AND 885
    SELECT * FROM aTable WHERE CODE NOT BETWEEN 877 AND 885
    
