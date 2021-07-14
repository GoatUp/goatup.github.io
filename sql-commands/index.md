# SQL Commands

There are five types of SQL commands: DDL, DML, DCL, TCL, and DQL.
<!--more-->

## 第1章 SQL 命令类型

![DBMS_SQL_Commands](https://raw.githubusercontent.com/goatup/blog-images/main/sql%20commands/20210714170456.png)

### 1.1 数据定义语言- Data Definition Language - DDL

- DDL 更改表的结构，例如创建表、删除表、更改表等。
- DDL 的所有命令都是自动提交的，这意味着它将永久保存数据库中的所有更改。

**Systax**

```sql
CREATE TABLE table_name (column_name datatype[,....]);
DROP TABLE table_name;	# drop an existing table in a database
ALTER TABLE table_name ADD/MODIFY column_name datatype;
TRUNCATE TABLE table_name;	# delete the data but not the table itself
```

### 1.2 数据操作语言 - Data Manipulation Language - DML

- DML 命令用于修改数据库。它负责数据库中所有形式的更改。
- DML 的命令不是自动提交的，这意味着它不能永久保存数据库中的所有更改。它们可以回滚。

**Systax**

```sql
INSERT INTO table_name [(col1, col2),....] VALUES (value1,value2,....);
UPDATE table_name SET [column_name1= value1,...column_nameN = valueN] [WHERE CONDITION]
DELETE FROM table_name [WHERE condition];  
```

### 1.3 数据控制语言 - Data Control Language -DCL

- DCL 命令用于对任何数据库用户授予和收回权限。

**Systax**

```sql
GRANT privileges ON object TO user;
REVOKE privileges ON object FROM user;
```

```markdown
| Privilege | Description |
| :-------: |-------------|
|  SELECT   |Ability to perform SELECT statements on the table.|
|  INSERT   |Ability to perform INSERT statements on the table.|
|  UPDATE   |Ability to perform UPDATE statements on the table.|
|  DELETE   |Ability to perform DELETE statements on the table.|
|REFERENCES |Ability to create a constraint that refers to the table.|
|   ALTER   |Ability to perform ALTER TABLE statements to change the table definition.|
|    ALL    |ALL does not grant all permissions for the table. Rather, it grants the ANSI-92 permissions which are SELECT, INSERT, UPDATE, DELETE, and REFERENCES.|
```

### 1.4 事务控制语言 - Transaction Control Language - TCL

- TCL 命令只能与 DML 命令一起使用，例如 INSERT、DELETE 和 UPDATE。

**Systax**

```sql
COMMIT;
ROLLBACK;
SAVEPOINT savepoint_name;
```

### 1.5 数据查询语言 - Data Query Language - DQL

- DQL 用于从数据库中获取数据。

**Systax**

```sql
SELECT column_name FROM table_name WHERE condition;
```


