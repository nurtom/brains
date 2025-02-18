## Management
### dump database

#mysql 

```bash
mysqldump databasename --not-tablespaces --lock-tables=false > dump.sql
```

## Query snippets
### query items older than x days

#mssql

```sql
WHERE date < DATEADD(day, -30, GETDATE())
```

### create user and table
#mysql 

```mysql
CREATE USER 'mynab'@'localhost' IDENTIFIED BY 'mynab';
CREATE DATABASE mynab;
GRANT ALL PRIVILEGES ON database_name.* TO 'database_user'@'localhost';
```