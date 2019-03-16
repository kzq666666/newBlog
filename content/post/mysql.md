---
title: "MySQL"
date: 2018-10-30T17:06:30+08:00
showDate: true
draft: false
tags: ["数据库","关系型数据库","MySQL"]
---
mysql数据库是我今年暑假在家学习的，当时学习的时候写了一些笔记，现在把笔记整理到博客上。
### Tips
- sql语句的语法Windows下是不区分大小写的，但在Linux是严格区分的，最好还是用大写吧
- 单双引号表示字符没有区别
- 注释单行一般用 `--`，多行（块）用 `/* */`
- 命名规范遵循基本的命名原则，具体因人而异，个人喜欢小驼峰

### SQL语句分类
* 数据库查询语言DQL（datebase query language）
<br>`SELECT`
* 数据库定义语言DDL（datebase defined language）<br>`CREATE DATABASE`、`CREATE TABLE`、`DROP DATABASE`、`DROP TABLE`
* 数据库操作语言DML（database manage language）<br>`UPDATE`、`INSERT`、`DELETE`

### 数据类型属性
mysql常见的数据类型：varchar(n)、float、int(n)、bigint(n)、date、datetime、text

* 默认值 
<br>`default '默认值'`
* 非空：`NOT NULL `
<br>如果某一个字段别NOT NULL修饰后，添加数据时，此字段必需填写
* 自动增长：`auto_increment`，尽量作用在int类型的字段上
* 主键(唯一的，不能重复，一张表中只能以一个作为主键)：`primary key`
* 唯一健（唯一，可以有很多）：`unique`，被unique修饰的数据不能够重复

一个栗子
```sql
USE kzq;
DROP TABLE students;
CREATE TABLE students(
	id BIGINT(20) AUTO_INCREMENT PRIMARY KEY COMMENT '学生编号',
	stuName VARCHAR(40) COMMENT '学生姓名',
	gender VARCHAR(2) DEFAULT '男' COMMENT '性别',
	className VARCHAR(20) NOT NULL COMMENT '班级',
	phone VARCHAR(20) UNIQUE COMMENT '手机号码'
)
```
### 库与表的创建和删除
```sql
-- 创建库
CREATE DATABASE 库名 CHARACTER SET 编码名
CREATE DATABASE kzq CHARACTER SET utf8

-- 选中某一个数据库
USE 库名
USE kzq

-- 创建表
CREATE TABLE 表名(
	字段1 数据类型 COMMENT .....,
	-- COMMENT为注释（对该字段的具体信息的补充）
	-- 字段1和字段2之间注意不要漏写逗号',' 最后一个字段结尾没有符号
	字段2 数据类型 COMMENT .....,
	.......
)
CREATE TABLE mysqlScore(
	stuName VARCHAR(40) COMMENT "学生姓名",
	stuClass VARCHAR(20) COMMENT "学生班级",
	stuScore FLOAT COMMENT "学生成绩"
);

-- 删除库和表
-- 友情提示：删库需谨慎，正所谓MySQL从删库到跑路
DROP DATABASE 库名
DROP TABLE 表名

-- 查看所有库
SHOW DATABASE

-- 查看创建库的详细信息
SHOW CREATE DATABASE 库名

-- 查看创建表的详细信息
SHOW CREATE TABLE 表名

-- 查看当前用户连接的是哪个数据库
SELECT DATABASE()

-- 查看当前用户连接的库下的所有表
SHOW TABLES

-- 查看某一张表的结构
-- DESC => description
DESC 表名


```
### 表的增（Create）、删（Delete）、改（Update）、查（Retrieve）
#### 增
```sql
USE kzq
-- 方法一
INSERT INTO 表名(字段1,字段2....) VALUES(值1,值2)
INSERT INTO mysqlScore (stuName,stuClass,stuScore) VALUES ('刘仔','xxx',90.5)
-- 在插入时，可以省略掉字段名，但后面的VALUES必须全
INSERT INTO mysqlScore VALUES ('刘仔','xxx',90.5)
-- 同时插入多条数据
INSERT INTO mysqlScore (stuName,stuClass,stuScore) 
VALUES ('刘仔','xxx',90.5),('小刘','xxx',90.6)
-- 方法二
INSERT INTO 表名 SET 字段名1=字段值1
INSERT INTO mysqlScore SET stuName='刘仔'
```

#### 删
```sql
-- 如果"="是放在SET关键字后，则是"赋值运算符"
-- 如果"="是放在WHERE关键字后，则是"关系运算符"
DELETE FROM 表名 WHERE 条件
DELETE FROM mysqlScore WHERE stuName='刘仔'
-- 如果要删除一整张表中的数据，使用truncate，使用truncate删除数据后，如果字段是自增的、则重新排列
TRUNCATE TABLE students;
```

#### 改
```sql
-- 重命名表名
RENAME TABLE 旧表名 TO 新表名
RENAME TABLE aaa TO bbb;

-- 添加字段
ALTER TABLE 表名 ADD 字段名 数据类型
ALTER TABLE person ADD gender VARCHAR(2)

-- 删除字段
ALTER TABLE 表名 DROP 被删除字段名
ALTER TABLE person DROP gender

-- 重命名字段
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新字段名数据类型
ALTER TABLE person CHANGE aaa bbb VARCHAR(40)

-- 修改数据类型（长度）
ALTER TABLE person CHANGE aaa aaa VARCHAR(25)
```

#### 查

```sql
----- 基本查询 ------
-- 逻辑运算符 与and 或or 非not

SELECT 字段1，字段2....FROM 表名 (WHERE 条件)
SELECT stuName,stuClass,stuScore FROM mysqlScore;
SELECT stuName FROM mysqlScore
-- *代表所有字段
SELECT * FROM mysqlScore
-- AS是取别名，WHERE后面是条件
SELECT stuName (AS passName) FROM mysqlScore WHERE stuScore>=60;

-- 降序(DESC)
SELECT * FROM mysqlScore ORDER BY stuScore DESC;
-- 升序(ASC)
SELECT * FROM mysqlScore ORDER BY stuScore ASC;
```


```sql
----- 聚合函数查询 -----
SELECT 函数名（字段） FROM 表名
-- 找出最大值：max(字段)
SELECT MAX(stuScore) AS maxScore FROM mysqlScore;

-- 找出最小值：min(字段)
SELECT MIN(stuScore) AS minScore FROM mysqlScore;

-- 求平均数：avg(字段名)
SELECT AVG(stuScore) AS avgScore FROM mysqlScore;

-- 求和 sum
SELECT SUM(stuScore) AS totalScore FROM mysqlScore;

-- 统计记录 count
SELECT COUNT(*) FROM mysqlScore

-- 常用函数
SELECT NOW()      -- 年月日、时分秒
SELECT CURTIME()  -- 时分秒
SELECT CURDATE()  -- 年月日
SELECT CEIL(2.3)  -- 向上取舍
SELECT FLOOR(2.3) -- 向下取舍
SELECT RAND()     -- 返回0到1的随机数

-- 时间格式函数
SELECT DATE_FORMAT(DATE,'%Y年%m月%d日 %H:%i:%s') AS birthday FROM persons
```
```sql
-------- 查询多条记录和分组查询 --------
-- 多条查询
SELECT * FROM users WHERE id IN (1,3)
SELECT * FROM users WHERE id

-- 查询是否有种类为衣服的类型
SELECT goodCategory FROM goods GROUP BY goodCategory HAVING goodCategory='衣服'

-- 分页查询
-- limit 起始下标,每页显示的数据量
-- goods表中有七条数据记录，每一页显示三条，总共可以分3页
SELECT * FROM goods LIMIT 0,3; -- 第一页
SELECT * FROM goods LIMIT 3,3; -- 第二页
SELECT * FROM goods LIMIT 6,3; -- 第三页
```
```sql
--------- 多表查询 --------
select * from 表1,表2....表n where 条件
/* 多表查询方式：
	内连接
	外连接
		左右连接
		右外连接
*/
-- 内连接
-- on后面接几个表中有关联的条件，没有关联的条件用where
select * from 表1 inner join 表2 on 条件(多个表中有关联的条件) 
where 没关联的条件
-- 查新所有部门中的所有员工
SELECT * FROM dept d INNER JOIN emp e ON d.id = e.deptId
-- 查询在开发部的员工姓名和收入
SELECT d.deptName,e.empName,e.salary
FROM
dept d INNER JOIN emp e
ON d.id = e.deptId WHERE d.dept = '开发部'
-- 左外连接 left join 以左边的表为主，左边的表数据要显示出来
-- 右外连接 right join 以右边的表为主，右边的表数据要显示出来
```
```sql
-------- 模糊查询 --------
LIKE 模糊查询
a%  -- 以a开头，%为占位符
%a 	-- 以a结尾
%a% -- 包含a 
-- 查询中国拍摄的电影的id和title
SELECT id,title FROM movies WHERE country LIKE '%中国%'
```

### 视图
在真实表上面构建的一张虚表 
视图的应用场景：在金融行业，保险行业，财务行业等
```sql
CREATE view 视图名 AS 查询语句;
CREATE VIEW view_all
AS SELECT e.empName,e.salary,d.deptname FROM dept d INNER JOIN emp e ON d.id = e.deptId;

DROP VIEW view_all;
```



### 事务
```sql
-- 开启事务
START TRANSACTION;

-- 回滚事务
ROLLBACK;

-- 提交事务
COMMIT;
```
#### 事务的四大特性
- 原子性(Atomicity)：多组操作为一个整体，不能分割，全部操作成功才算成功，有一步失败就失败了，一环扣一环。
- 一致性(Consistency)：操作前后最终的总量一样，比如说转账，两个人相互转账，这两个人无论向对方怎么转，两个人的总钱数是不变，如果变了，就说明失败了。
- 隔离性(Isolation)：并发(同一时刻多个事务执行)事务之间相互隔离互不干扰。
    - 在mysql中事务有4种隔离级别：
		- `read uncommitted(读取未提交)`
		- `read committed(读取提交)`
		- `repeatable read(可以重复读)`
		- `Serializable`
	- 查看mysql软件的事务隔离级别
	<br>`SELECT @@tx_isolation`
	- 修改mysql软件默认的隔离级别
	<br>`set global transaction isolation level 隔离级别`
	- 不同的隔离级别会引发不同的问题
		- 当mysql事务的隔离级别为read uncommitted时，会引发脏读(一个事务可以读取另一个事务未提交的数据.)，解决脏读问题可以将数据库事务的隔离级别改为:read committed
    	- 当mysql软件的事务隔离级别为:read committed的时候，会引发不可重复读：在同一事物中多次读取的结果不一致如何解决不可重复读：将事物的隔离级别改为repeatable read
    	- 当mysql软件的事务隔离级别为:repeatable read时，会引发虚读(幻读)
		
		
	
* 持久性(Durability)：数据进入到数据库中后，数据会持久存在



### 数据库的备份和还原
- 命令
	- 备份
	<br>mysqldump -u root -p (密码) 需要备份的数据库名>备份后的sql文件名
	mysqldump -u root -p (密码) kzq>c:\kzqBack.sql
	- 还原
	进入mysql环境---->创建一个库---->在库下还原数据
	source 备份数据库文件名
- 软件（图形界面操作sqlyog）
<br>选中需要备份的数据库----->右键------>备份/导出---->转储到sql

### 未整理完的
MySQL存储过程以及一些示例

