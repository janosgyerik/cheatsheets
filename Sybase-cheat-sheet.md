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

    SELECT sc.* 
    FROM syscolumns sc
    	INNER JOIN sysobjects so ON sc.id = so.id
    WHERE so.name = 'your_table_name'

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
    
## Create table with constraints

    create table #t1 (
        id int,
        curve_date date,
        point_date date,
        maturity int,
        unique clustered (id, curve_date, point_date)
    )
    
    insert into #t1 values (1, '20141014', dateadd(month, 1, '20141014'), 1)
    insert into #t1 values (1, '20141014', dateadd(month, 2, '20141014'), 2)
    insert into #t1 values (1, '20141014', dateadd(month, 3, '20141014'), 3)
    insert into #t1 values (1, '20141013', dateadd(month, 3, '20141013'), 3)
    
    SELECT * FROM #t1
    
    -- will not update anything due to violation of constraint
    update #t1 setcurve_date = dateadd(day, -1, curve_date),
        point_date = dateadd(day, -1, point_date)
        where curve_date = '20141014'

## Creating foreign keys

    CREATE TABLE Employee (
    	EmpId int PRIMARY KEY,
    	Name varchar(20)
    )
    
    CREATE TABLE Dept (
    	DeptId int PRIMARY KEY,
    	DeptName varchar(30),
    	ManagerId int REFERENCES Employee(EmpId)
    )
