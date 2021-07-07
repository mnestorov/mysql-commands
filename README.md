# MySQL/MariaDB

MySQL/MariaDB command reference.

## Users

### Show all DB users

```sql
SELECT * FROM mysql.user;
```

### Create new DB user

```sql
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
```

### Change the name of DB user

```sql
RENAME USER 'user'@'localhost' TO 'newuser'@'localhost';
```

### Grant privileges on user

**Option 1**

```sql
GRANT ALL PRIVILEGES ON database_name.* TO 'user'@'localhost';
```

**Option 2**

```sql
GRANT ALL PRIVILEGES ON database_name.* TO 'user'@'localhost' IDENTIFIED BY 'password'
```

**Option 3**

```sql
GRANT ALL PRIVILEGES ON database_name.* TO 'user'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

### Update DB permissions/privilages

```sql
FLUSH PRIVILEGES;
```

### Change a user password from MySQL prompt

```sql
SET PASSWORD FOR 'user'@'localhost' = PASSWORD('password');
```

### Change a users password from unix shell

```bash
[mysql dir]/bin/mysqladmin -u root -h hostname.blah.org -p password 'newpassword'
```

### Delete DB user

```sql
DROP USER 'user'@'localhost';
```

## Database

### Create a database on the sql server

```sql
create database [database_name];
```

### List all databases on the sql server

```sql
show databases;
```

### Switch to a database

```sql
use [database_name];
```

### List all the tables in the DB

```sql
show tables;
```

### Delete DB

```sql
drop database [database_name];
```

### Delete DB table

```sql
drop table [table_name];
```

### Show all data in a DB table

```sql
SELECT * FROM [table_name];
```
