## Choosing a database
```sql
SHOW DATABASES;
USE databaseName;
```
## Choosing a table
```sql
SHOW TABLES;
SELECT * FROM tableName;
```
## Selecting records from a table
```sql
SELECT * FROM table1;
SELECT column1, column2 FROM table1;
```
## Order by 
this orders all the data based on the given field,
```sql
SELECT column1 FROM table1 ORDER BY column1;
SELECT column1 FROM table1 ORDER BY column1 DESC;
```
the data can also be ordered based on a secondary column if a record contains the same values for the first specified column.
```sql
SELECT * FROM table1 ORDER BY column1, column2;
```
## Where 
```sql
SELECT * FROM table1 WHERE name = 'babayaga';
```
### Like
#### wildcards
they select records based on the given matching patters
- %a --> all things that end with 'a'
- z% --> starts with 'z'
- %a% -> must have an 'a' in the middle
- \_\_a -> exactly a 3 letter word that ends in 'a'
- a\_ -> a two letter word that starts with 'a'

```sql
SELECT * from table1 WHERE name LIKE '%a'
SELECT * from table1 WHERE name LIKE '__a'
```

