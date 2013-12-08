Configuration
-------------
It is a hassle to enter the password on the command line every
time you run the client.  It is better to add it to `~/.my.cnf`
like this:

```
[client]
database=dbname
user=dbuser
password=dbpass
host=dbhost
port=dbport
```

And don't forget to protect the permissions of the file:

```bash
chmod go-rwx ~/.my.cnf
```


Indexes
-------
```sql
-- Create a table with indexes:
CREATE TABLE tname (
    col1 int,
    ...
    INDEX (col1)
) 

-- Show indexes on a table:
SHOW INDEX FROM tname;
```


Managing users
--------------
```sql
-- Create user identified by some password
GRANT ALL PRIVILEGES ON dbname.* TO 'dbuser'@localhost IDENTIFIED BY 'userpass';

-- Create database with some encoding
CREATE DATABASE bugtracker DEFAULT CHARACTER SET utf8;  
```


Get schema and other info
-------------------------
```sql
desc tablename;
 
show variables like "character_set_database";
```


Dump database
-------------
```sql
mysqldump bugtracker --default-character-set=utf8 > bugtracker.dump
mysqldump bugtracker --default-character-set=utf8 -r bugtracker.dump
mysqldump bugtracker --default-character-set=utf8 --skip-extended-insert | grep mantis_bug_text.*some_pattern_in_the_record
```

If your tables have utf-8 encoded data in them, dumping can be
non-intuitive.  You must test restoring from the dump you created
to make sure you will not lose your utf-8 or unicode encoded
data. 


Misc
----
```sql
set names utf8;

source filepath.dump

-- Export data in CSV format
-- note: this requires the *FILE* permission
SELECT id, country FROM countries WHERE eutax = 1
INTO OUTFILE '/tmp/country.txt' FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
```


ALTER TABLE syntax
------------------
```sql
ALTER TABLE tt CHANGE old_col_name new_col_name column_definition;
```


Duplicate a table
-----------------
```sql
CREATE TABLE dupe AS SELECT * FROM other_table;
```

