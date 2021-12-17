# MySQL/MariaDB

MySQL/MariaDB command reference.

**PASSWORD POLICY**

- [Change MySQL Password Policy Level](#change-mysql-password-policy-level)

**USERS**

- [Show All Database Users](#show-all-database-users)
- [Create New Database User](#create-new-database-user)
- [Change The Name Of A Single Database User](#change-the-name-of-a-single-database-user)
- [Grant Privileges On A Single User](#grant-privileges-on-a-single-user)
- [Update Database Permissions Or Privilages](#update-database-permissions-or-privilages)
- [Change A User Password From MySQL Prompt](#change-a-user-password-from-mysql-prompt)
- [Change A Users Password From Unix Shell](#change-a-users-password-from-unix-shell)
- [Delete A Single DB user](#delete-a-single-db-user)

**DATABASES**

- [Create A Database On The SQL Server](#create-a-database-on-the-sql-server)
- [List All Databases On The SQL Server](#list-all-databases-on-the-sql-server)
- [Switch To A Database](#switch-to-a-database)
- [List All The Tables In The Database](#list-all-the-tables-in-the-database)
- [Delete A Single Database](#delete-a-single-database)
- [Delete A Single Database Table](#delete-a-single-database-table)
- [Show All Data In A Database Table](#show-all-data-in-a-database-table)

**BACKUP**

- [How To Backup And Restore MariaDB Databases Using The mysqldump Utility](#how-to-backup-and-restore-mariadb-databases-using-the-mysqldump-utility)
- [Backing Up A Single Database](#backing-up-a-single-database)
- [Backing Up Multiple Databases](#backing-up-multiple-databases)
- [Backing Up All Databases](#backing-up-all-databases)
- [Back Up MariaDB Database With Compression](#back-up-mariadb-database-with-compression)

**RESTORE**

- [Restore A Single Database](#restore-a-single-database)
- [Restore Multiple Databases](#restore-multiple-databases)
- [Restore All Databases](#restore-all-databases)

## PASSWORD POLICY

### Change MySQL Password Policy Level

To change the default password policy level, we can change the settings at runtime using the command line or in the config file `my.cnf/mysqld.cnf` permanently.

Login to MySQL command prompt and execute below query to view current settings of validate_password.

```sql
SHOW VARIABLES LIKE 'validate_password%';
```

The default level is MEDIUM, we can change it to LOW by using the below query. The LOW level required only passwords length to min 8 characters.

```sql
SET GLOBAL validate_password.policy=LOW;
```

## USERS

### Show All Database Users

```sql
SELECT * FROM mysql.user;
```

### Create New Database User

```sql
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
```

### Change The Name Of A Single Database User

```sql
RENAME USER 'user'@'localhost' TO 'newuser'@'localhost';
```

### Grant Privileges On A Single User

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

### Update Database Permissions Or Privilages

```sql
FLUSH PRIVILEGES;
```

### Change A User Password From MySQL Prompt

```sql
SET PASSWORD FOR 'user'@'localhost' = PASSWORD('password');
```

### Change A Users Password From Unix Shell

```bash
[mysql dir]/bin/mysqladmin -u root -h hostname.blah.org -p password 'newpassword'
```

### Delete A Single DB User

```sql
DROP USER 'user'@'localhost';
```

## DATABASES

### Create A Database On The SQL Server

```sql
CREATE DATABASE [database_name];
```

### List All Databases On The SQL Server

```sql
SHOW DATABASES;
```

### Switch To A Database

```sql
USE [database_name];
```

### List All The Tables In The Database

```sql
SHOW TABLES;
```

### Delete A Single Database

```sql
DROP DATABASE [database_name];
```

### Delete A Single Database Table

```sql
DROP TABLE [table_name];
```

### Show All Data In A Database Table

```sql
SELECT * FROM [table_name];
```

## How To Backup And Restore MariaDB Databases Using The *mysqldump* Utility

**mysqldump** - is the utility that we will use to back up our MariaDB database. It’s designed specifically for backup purposes. The cool thing about mysqldump is that you don’t need to stop MariaDB service to make a backup. It can be used to back up a single database, multiple databases, and all databases. By default, it will create a dump file that contains all the statements needed to re-create the database.

### Backing Up A Single Database

```bash
mysqldump -u root -p database_name > database_name.sql
```

### Backing Up Multiple Databases

```bash
mysqldump -u root -p --databases db_name1 db_name2 ...  > multi_database.sql
```

### Backing Up All Databases

```bash
mysqldump -u root -p --all-databases > all-databases.sql
```

### Back Up MariaDB Database With Compression

```bash
mysqldump -u root -p database_name | gzip > database_name.sql.gz
```

### Restore A Single Database

**Option 1 - From unix shell**

```bash
mysql -u root -p database_name < database_name.sql
```

**Option 2 - From within mysql**

```sql
USE [database_name];
SOURCE backup-file.sql;
```

### Restore Multiple Databases

```bash
mysql -u root -p < multi-databases.sql
```

### Restore All Databases

```bash
mysql -u root -p < all-databases.sql
```
