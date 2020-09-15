MAMP 安装后，在.bash_profile添加

```shell
export PATH=$PATH:/Applications/MAMP/Library/bin
```

# 一、MySQL概述

## 1. MySQL的登陆与退出

### 1). 登陆

```shell
mysql -uroot -proot
```

参数选择：

```
-D,  --database=name
--delimiter=name
-h,  --host=name
-p,  --passward
-P,  --port=#
--prompt=name
-u,  --user=name
-V,  --version
```

### 2). 退出

```shell
exit
quit
\q
```

## 2. 修改MySQL提示符

```shell
mysql -uroot -proot --prompt '\h'(提示符)
mysql -uroot -proot --prompt '\u@\h \d->'(提示符)
# 或者
prompt \h(提示符)
```

提示符

```
# 参数
\D    日期
\d		数据库
\h		服务器名称
\u		当前用户
```

```
prompt \u@\h \d
root@localhost (none)
```

## 3. MySQL常用语句与语法规范

```shell
# 显示服务器版本
SELECT VERSION();
# 显示当前日期
SELECT NOW();
# 显示当前用户
SELECT USER();

```

### 1). 规范

- 关键字和函数名称大写
- 数据库名称，表名称，字段名称全部小写
- SQL语句必须以分号结尾

## 4. 数据库操作

### 1). 创建数据库

```
CREATE {DATABASE|SCHEMA} [IF NOT EXISTS] db_name [DEFAULT] CHARACTER SET [=] charset_name
```

```
CREATE DATABASE t1;
SHOW DATABASES;

# 如果不存在t1就创建
CREATE DATABASE IF NOT EXISTS t1;
SHOW WARNINGS;
# 显示创建t1的格式
SHOW CREATE DATABASE t1;

# 创建其他格式的数据库
CREATE DATABASE IF NOT EXISTS t2 CHARACTER SET gbk;
SHOW CREATE DATABASE t2;
```

### 2). 修改数据库

```
ALTER {DATABASE|SCHEMA} [db_name] [DEFAULT] CHARACTER SET [=] charset_name
```

```
ALTER DATABASE t2 CHARACTER SET utf8;
SHOW CREATE DATABASE t2;
```

### 3). 删除数据库

```
DROP {DATABASE|SCHEMA} [IF EXISTS] db_name
```

```
DROP DATABASE t2;
DROP DATABASE IF EXISTS t2;
```

# 二、数据类型与操作数据表

## 1. 数据类型

### 1). 整型

- TINYINT
  - 1字节
  - 有符号：-128-127（-2^7到2^7-1)
  - 无符号：0-255 (0到2^8-1)
- SMALLINT
  - 2字节
  - 有符号（-2^15到2^15-1)
  - 无符号  (0到2^16-1)
- MEDIUMINT
  - 3字节
  - 有符号(-2^23到2^23-1))
  - 无符号(0到2^24-1)
- INT
  - 4字节
  - 有符号(-2^31到2^31-1)
  - 无符号(0到2^32-1)
- BIGINT
  - 8字节
  - 有符号(-2^63到2^63-1)
  - 无符号(0到2^64-1)

### 2). 浮点型

- FLOAT[(M,D)]
  - M数字总位数，D小数点后的位数。
- DOUBLE[(M,D)]

### 3). 日期时间型

- YEAR
- TIME
- DATE
- DATATIME
- TIMESTAMP

### 4). 字符型

- CAHR(M)
- VARCHAR(M)
- TINYTEXT
- TEXT
- DEDIUMTEXT
- LONGTEXT
- ENUM('value1','value2,…') 
  - 最多65535个值
- SET('value1','value2,...')
  - 最多64个成员

## 2. 数据表

数据表示数据库的最重要的组成部分，是其他对象的基础。

### 1). 打开数据库

```
USE 数据库名;
```

```
USE test;
SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| test       |
+------------+
```

### 2). 创建数据表

```
CREATE TABLE [IF NOT EXISTS] table_name(column_name data_type,...);
```

```
CREATE TABLE tb1(
username VARCHAR(20),
age TINYINT UNSIGNED, 
salary FLOAT(8,2) UNSGINED 
);
```

### 3). 查看数据表

```
SHOW TABLES [FROM db_name] [LIKE 'pattern'|WHERE expr]
```

```
SHOW TABLES；
+----------------+
| Tables_in_test |
+----------------+
| tb1            |
+----------------+
SHOW TABLES FROM mysql;
+---------------------------+
| Tables_in_mysql           |
+---------------------------+
| columns_priv              |
| db                        |
| engine_cost               |
| event                     |
| func                      |
| general_log               |
| gtid_executed             |
| help_category             |
| help_keyword              |
| help_relation             |
| help_topic                |
| innodb_index_stats        |
| innodb_table_stats        |
| ndb_binlog_index          |
| plugin                    |
| proc                      |
| procs_priv                |
| proxies_priv              |
| server_cost               |
| servers                   |
| slave_master_info         |
| slave_relay_log_info      |
| slave_worker_info         |
| slow_log                  |
| tables_priv               |
| time_zone                 |
| time_zone_leap_second     |
| time_zone_name            |
| time_zone_transition      |
| time_zone_transition_type |
| user                      |
+---------------------------+
```

#### 查看数据表结构

```
SHOW COLUMNS FROM tbl_name;
```

```
SHOW COLUMS FROM tb1;
+----------+---------------------+------+-----+---------+-------+
| Field    | Type                | Null | Key | Default | Extra |
+----------+---------------------+------+-----+---------+-------+
| username | varchar(20)         | YES  |     | NULL    |       |
| age      | tinyint(3) unsigned | YES  |     | NULL    |       |
| salary   | float(8,2) unsigned | YES  |     | NULL    |       |
+----------+---------------------+------+-----+---------+-------+
```

### 4). 记录的插入与查找

#### 插入

```
INSERT [INTO] tbl_name [(col_name,...)] VALUES(val,...);
```

```
INSERT tb1 VALUES('Tom',25,7863.25);
INSERT tb1 (username,salary) VALUES('John',4000.69);
```

#### 查找

```
SELECT expr,... FROM tbl_name;
```

```
SELECT * FROM tb1;
+----------+------+---------+
| username | age  | salary  |
+----------+------+---------+
| Tom      |   25 | 7863.25 |
| John     | NULL | 4000.69 |
+----------+------+---------+
```

### 5). 空值与非空

```
# 创建
CREATE TABLE t2(
username VARCHAR(20) NOT NULL,
age TINYINT UNSIGNED NULL
);
# 显示
SHOW COLUMNS FROM t2;
+----------+---------------------+------+-----+---------+-------+
| Field    | Type                | Null | Key | Default | Extra |
+----------+---------------------+------+-----+---------+-------+
| username | varchar(20)         | NO   |     | NULL    |       |
| age      | tinyint(3) unsigned | YES  |     | NULL    |       |
+----------+---------------------+------+-----+---------+-------+
# 插入
INSERT t2 VALUES('TOM',NULL);
SELECT * FROM t2;
+----------+------+
| username | age  |
+----------+------+
| TOM      | NULL |
+----------+------+
1 row in set (0.00 sec)
# 插入
INSERT t2 VALUES(NULL,26);
ERROR 1048 (23000): Column 'username' cannot be null
```

### 6). 主键

- 主键约束
- 一张数据表中只能有一个主键
- 主键保证记录的唯一性
- 主键自动NOT NULL

```
root@localhost test->CREATE TABLE tb3
    -> (id SMALLINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    -> username VARCHAR(30) NOT NULL
    -> );
# 显示
SHOW COLUMNS FROM tb3;
+----------+----------------------+------+-----+---------+----------------+
| Field    | Type                 | Null | Key | Default | Extra          |
+----------+----------------------+------+-----+---------+----------------+
| id       | smallint(5) unsigned | NO   | PRI | NULL    | auto_increment |
| username | varchar(30)          | NO   |     | NULL    |                |
+----------+----------------------+------+-----+---------+----------------+
# 插入
INSERT tb3 (username) VALUES('John');
INSERT tb3 (username) VALUES('tom');
INSERT tb3 (username) VALUES('jerry');
# 显示
root@localhost test->SELECT * FROM tb3;
+----+----------+
| id | username |
+----+----------+
|  1 | John     |
|  2 | tom      |
|  3 | jerry    |
+----+----------+
```

有auto_increment的时候，必须用INSERT [INTO] tbl_name (col_name,…) VALUES(val,…); 插入

主键可以不和auto_increment联合使用

```
root@localhost test->CREATE TABLE tb4(
    -> id SMALLINT UNSIGNED PRIMARY KEY,
    -> username VARCHAR(20) NOT NULL
    -> );
# 显示
root@localhost test->SHOW COLUMNS FROM tb4;
+----------+----------------------+------+-----+---------+-------+
| Field    | Type                 | Null | Key | Default | Extra |
+----------+----------------------+------+-----+---------+-------+
| id       | smallint(5) unsigned | NO   | PRI | NULL    |       |
| username | varchar(20)          | NO   |     | NULL    |       |
+----------+----------------------+------+-----+---------+-------+

#插入
INSERT tb4 VALUES(7,'TOM');
INSERT tb4 VALUES(22,'JERRY');
root@localhost test->SELECT * FROM tb4;
+----+----------+
| id | username |
+----+----------+
|  7 | TOM      |
| 22 | JERRY    |
+----+----------+
```

### 7). 唯一约束

- 保证记录唯一性
- 可以为空值
- 每张数据表可以存在多个唯一约束

```
root@localhost test->CREATE TABLE tb5(
    -> id SMALLINT UNSIGNED auto_increment PRIMARY KEY,
    -> username VARCHAR(20) not NULL UNIQUE KEY,
    -> age TINYINT UNSIGNED
    -> );
# 显示
root@localhost test->SHOW COLUMNS FROM tb5;
+----------+----------------------+------+-----+---------+----------------+
| Field    | Type                 | Null | Key | Default | Extra          |
+----------+----------------------+------+-----+---------+----------------+
| id       | smallint(5) unsigned | NO   | PRI | NULL    | auto_increment |
| username | varchar(20)          | NO   | UNI | NULL    |                |
| age      | tinyint(3) unsigned  | YES  |     | NULL    |                |
+----------+----------------------+------+-----+---------+----------------+

# 插入
INSERT tb5 (username,age) VALUES('TOM',22);
```

### 8). 默认约束

当插入记录时，如果没有明确的为字段赋值，则自动赋予默认值。

```
# 创建
root@localhost test->CREATE TABLE tb6(
    -> id SMALLINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    -> username VARCHAR(20) NOT NULL UNIQUE KEY,
    -> sex ENUM('1','2','3') DEFAULT '3'
    -> );
# 显示  
root@localhost test->SHOW COLUMNS FROM tb6;
+----------+----------------------+------+-----+---------+----------------+
| Field    | Type                 | Null | Key | Default | Extra          |
+----------+----------------------+------+-----+---------+----------------+
| id       | smallint(5) unsigned | NO   | PRI | NULL    | auto_increment |
| username | varchar(20)          | NO   | UNI | NULL    |                |
| sex      | enum('1','2','3')    | YES  |     | 3       |                |
+----------+----------------------+------+-----+---------+----------------+

# 插入
INSERT tb6 (username) VALUES('TOM');
root@localhost test->SELECT * FROM tb6;
+----+----------+------+
| id | username | sex  |
+----+----------+------+
|  1 | TOM      | 3    |
+----+----------+------+
```



