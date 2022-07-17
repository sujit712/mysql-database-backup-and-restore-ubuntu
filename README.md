## EXPORT

- Method 1

```bash
  mysqldump -h host_name -u user_name -p 
  databasename --ignore-table=databasename.table_name_1 --ignore-table=databasename.table_name_1 
  | gzip >  backupfilename.sql.gz
```
  - Method 2

```bash
  mysqldump -h host_name -u user_name -p databasename table_name_1 table_name_2 | gzip > backupfilename.sql.gz
```

- Method 3

```bash
  mysqldump  -h host_name -u user_name -p databasename  | gzip  > backupfilename.sql.gz
```

- Mysql stored procedures are not included in the mysql dump and must be explicitly added.



## IMPORT

- upzip the file using this command.

```bash
  gunzip -d backupfilename.sql.gz
```

- To turn off the foreign key check when importing a database, use the below command.

```bash
  echo 'SET FOREIGN_KEY_CHECKS=0;' | cat - backupfilename.sql > temp && mv temp backupfilename.sql
```

- This will add ``SET FOREIGN_KEY_CHECKS=0; `` on the first line of backupfilename.sql file

```bash
echo "SET FOREIGN_KEY_CHECKS=1;" >> backupfilename.sql
```

- This will add ``SET FOREIGN_KEY_CHECKS=1; `` on the last line of filename.sql file

- Make sure you have correct DEFINER in the file ``DEFINER=`localhost`@`%` ``Else replace or delete all the DEFINERS from the file.

- Finally import the file using below command.

```bash
mysql -f -h hostname -u username -p databasename < backupfilename.sql
```
