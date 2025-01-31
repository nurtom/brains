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


