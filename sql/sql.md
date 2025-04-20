# SQL

## 概述

- 数据库管理系统（DBMS : Database Management System）
- 关系型数据库管理系统（RDBMS : Relational Database Management System）
- 结构化查询语言（SQL : Structured Query Language）
- 数据库工程师（Database Engineer）

## 关系型数据库管理系统

- SQL Server
- DB2
- Oracle
- MySQL
- Access
- 等

## 结构化查询语言

- 是一种数据库查询和程序设计语言，数据库脚本文件（*.sql）
- 用于存取数据以及查询、更新和管理关系数据库系统

## 语言结构

### 数据查询语言（DQL : Data Query Language）

- 查询（SELECT）
- 条件（WHERE）
- 排序（ORDER BY）
- 分组（GROUP BY）
- 组过滤（HAVING）

### 数据操作语言（DML : Data Manipulation Language）

- 插入（INSERT）
- 更新（UPDATE）
- 删除（DELETE）

### 事务处理语言（TPL : Transaction Process Language）

- 事务（BEGIN TRANSACTION）
- 提交（COMMIT）
- 回滚（ROLLBACK）

### 数据控制语言（DCL : Data Control Language）

- 授权（GRANT）
- 回收（REVOKE）

### 数据定义语言（DDL : Data Define Language）

- 创建（CREATE）
- 删除（DROP）

### 指针控制语言（CCL : Cursor Control Language）

- 指针（DECLARE CURSOR）
- 读取（FETCH INTO）
- 更新（UPDATE WHERE CURRENT）

## 数据类型

### 字符型

- 可变（VARCHAR）指定长度，动态分配存储空间
- 定长（CHAR）指定长度，静态分配存储空间，字符后自动补空格

### 文本型

- 无限（TEXT）无指定长度，至少自动分配2K空间，应避免使用该类型，以免浪费存储空间、降低处理性能

### 数值型

- 整数（INT、SMALLINT、TINYINT）自动分配4、2、1个字节空间
- 小数（NUMERIC）可存储正负10的38次方的浮点数

### 布尔型

- 真值（BIT）取值0或1，须在建表时构建BIT型字段，后期无法添加BIT型字段

### 日期型

- 日期（DATETIME）范围 [`1753/01/01`, `9999/12/31`] 精确到毫秒
- 日期（SMALLDATETIME）范围 [`1900/1/1`, `2079/6/6`] 精确到秒

## 数据库对象

- 库（DATABASE）
- 表（TABLE）
- 索引（INDEX）
- 视图（VIEW）
- 存储过程（PROCEDURE）
- 函数（FUNCTION）
- 触发器（TRIGGER）

### DATABASE 库

```sql
CREATE DATABASE 库;
DROP DATABASE 库;
```

### TABLE 表

```sql
CREATE TABLE 表 (列 类型 约束,...);
DROP TABLE 表;
```

```sql
ALTER TABLE 表 ADD 列 类型;
ALTER TABLE 表 DROP COLUMN 列;
```

```sql
-- SQL Server、Access
ALTER TABLE 表 ALTER 列 类型;
-- MySQL、Oracle
ALTER TABLE 表 MODIFY 列 类型;
```

### INDEX 索引

- 提升SELECT性能，但会降低UPDATE、INSERT性能
- 小数据表、需频繁更新插入操作、含大数或NULL、频繁操作列等不宜创建索引

```sql
CREATE [UNIQUE] INDEX 索引 ON 表 (列);
```

```sql
-- SQL Server
DROP INDEX 表.索引;
-- Access
DROP INDEX 索引 ON 表;
-- DB2/Oracle
DROP INDEX 索引;
-- MySQL
ALTER TABLE 表 DROP INDEX 索引;
```

### VIEW 视图

```sql
CREATE [OR REPLACE] VIEW 视图 AS SELECT 列 FROM 表 WHERE 条件;
DROP VIEW 视图;
```

## 查询表数据

### 条件查询

```sql
SELECT 列|* FROM 表 WHERE 条件 AND|OR|NOT 条件;
```

### 查询去重

```sql
SELECT DISTINCT 列|* FROM 表;
```

### 查询别名

```sql
SELECT 列 AS 列别名 FROM 表 AS 表别名;
```

### 查询排序

```sql
SELECT 列|* FROM 表 WHERE 条件 ORDER BY 列 ASC|DESC;
```

### 查询分组

```sql
SELECT 列|* FROM 表 GROUP BY 列;
```

### 分组过滤

```sql
SELECT 列|*,过滤器 FROM 表 GROUP BY 列 HAVING 过滤器条件;
```

### 结果数量

```sql
-- SQL Server、Access
SELECT TOP number|percent 列 FROM 表 WHERE 条件;
-- Oracle
SELECT 列 FROM 表 WHERE 条件 AND ROWNUM <= number;
-- MySQL
SELECT 列 FROM 表 WHERE 条件 LIMIT number;
```

### 多表连接

```sql
-- 交集|左补集|右补集|合集[OUTER]
SELECT 列 FROM 表A INNER|LEFT|RIGHT|FULL [OUTER] JOIN 表B ON 表A.列=表B.列;
-- 自连接
SELECT 列 FROM 表A,表B WHERE 条件;
```

### 结果联合

```sql
-- 使用ALL允许重复值
SELECT A.列 FROM 表A UNION [ALL] SELECT B.列 FROM 表B;
```

### 复制备份

```sql
SELECT 列|* INTO 新表 [IN '它库'] FROM 旧表 WHERE 条件;
```

## 插入表数据

```sql
INSERT INTO 表 VALUES (值,...);
INSERT INTO 表 (列,...) VALUES (值,...);
INSERT INTO 表A SELECT 列|* FROM 表B;
```

## 修改表数据

```sql
UPDATE 表 SET 列=值,... WHERE 条件;
```

## 删除表数据

```sql
DELETE FROM 表 WHERE 条件;
TRUNCATE TABLE 表;
```

## WHERE子句

### 比较

- 等于（=）
- 不等（<>、!=）
- 大于（>）
- 大等于（>=）
- 小于（<）
- 小等于（<=）

### 范围（数字、文本、日期）

- BETWEEN AND
- NOT BETWEEN AND

### 包含

- IN
- NOT IN

### 空

- IS NULL
- IS NOT NULL

### 模式匹配

- LIKE
- NOT LIKE

```sql
-- % 匹配0~n个字符
select * from tbl where col like 'b%s';
-- _ 匹配1个字符（Access中使用?代替_的功能）
select * from tbl where col like '_ang';
-- [] 指定范围内任意一个字符
select * from tbl where col like '[Yy]ang';
-- [^]或[!]不在指定范围内任意一个字符
select * from tbl where col like '[^b]oot' or like '[!b]oot';
```

## 自动增量字段

```sql
-- MYSQL 默认起始值=1，增量=1
CREATE TABLE 表 (列 int NOT NULL AUTO_INCREMENT,...,PRIMARY KEY (ID));
ALTER TABLE 表 AUTO_INCREMENT=起始值;
```

```sql
-- SQL Server
CREATE TABLE 表 (ID int IDENTITY(起始值,增量) PRIMARY KEY,...);
```

```sql
-- Access AUTOINCREMENT(起始值,增量) 默认（1,1）
CREATE TABLE 表 (ID Integer PRIMARY KEY AUTOINCREMENT,...);
```

```sql
-- Oracle 缓存值可提高性能
CREATE SEQUENCE 序列 MINVALUE 1 START WITH 1 INCREMENT BY 1 CACHE 10;
INSERT INTO 表 (自增字段) VALUES (序列.nextval);
```

## 约束

- NOT NULL 约束：保证列中数据不能有 NULL 值
- DEFAULT 约束：提供该列数据未指定时所采用的默认值
- UNIQUE 约束：保证列中的所有数据各不相同
- 主键约束：唯一标识数据表中的行/记录
- 外键约束：唯一标识其他表中的一条行/记录
- CHECK 约束：此约束保证列中的所有值满足某一条件
- 索引：用于在数据库中快速创建或检索数据

```sql
-- 删除约束
ALTER TABLE 表 DROP CONSTRAINT 约束;
```
