MySQL启动！！！



# 1 数据库的创建和使用

## 1.1 创建数据库

* 基本语法

```mysql
CREATE DATABASE [IF NOT EXISTS] db_name
		[create_specification[,create_specification]...]
		create_specification:
		[DEFAULT]CHARACTER SET charset_name
		[DEFAULT]COLLATE collation_name
```

## 1.2 数据库使用常用语句

* CHARACTER SET:指定数据库采用的字符集，如果不指定字符集，默认utf8

* COLLATE:指定数据库字符集的校对规则，默认是utf8_general_ci

* 显示数据库语句：SHOW DATABASES
* 显示数据库创建语句：SHOW CREAT BATABASE db_name
* 数据库删除语句：DROP DATABASE [IF EXISTS] db_name
* 备份数据库(在DOS下执行)：mysqldump -u 用户名 -p -B数据库一 数据库二  数据库n > 文件名.sql
* 恢复数据库(进入MySQL命令行再执行)：Souse  文件名.sql

* 备份单张表：mysqldump -u 用户名 -p 密码  数据库 表1 表2...>备份的路径

# 2. 表

## 2.1创建

* 基本语法

```MySQL
CREATE TABLE table_name 
(
		field datatype,
		field datatype,
		field datatype,
)character set字符集（不指定则为数据库的字符集；   ）；   collate校对规则（不指定为数据库的校对规则）；  engine引擎；  field指定列名；  datatype指定列类型(字段类型)；     
```

* 创建表时，要根据需要保存的数据创建相应的列，并根据数据的类型定义相应的列类型

## 2.2 删除



## 2.3 修改

* 添加列

  ```mysql
  ALTER TABLE tablename
  ADD   (column datatype  [DEFAULT  expr]
  		[,column datatype]...);
  ```

* 修改列

  ```mysql
  ALTER TABLE tablename
  MODIFY  (column datatype [DEFAULT expr]
  		[,column datatype]...);
  ```

* 删除列

  ```mysql
  ALTER TABLE tablename
  DROP	(column);
  ```

  查看表的结构：desc  表名

  修改表名：Rename   table  表名  to  新表名

  修改字符集： alter  table  表名 character set  字符集

# 3.MySQL的数据类型(列类型)

## 3.1数值类型

在能满足需求的情况下尽量选择小的类型

* 整形：

  * tinyint[一个字节]
  * smallint[两个字节]
  * mediumint[三个字节]
  * int[四个字节]

  ```MySQL
  CREATE TABLE T3(
  		id TINYINT UNSIGNED);
  		INSERT INTO t3 VALUES(127);
  		SELECT * FROOM T3
  ```

  

  * bigint[八个字节]

  ```MySQL
  CREATE TABLE t05(num BIT(8));
  INSERT INTO t05 VALUES(255);
  SELECT * FROM t05;
  ```

  

  

  

* 小数类型

  * float[单精度四个字节]
  * double[双精度八个字节]
  * decimal[M,D]
    * 可以支持更加精确的小数位，M是小数位数的总数，D是小数点后面的位数
    * 如果D是0，则值没有小数点或分数部分。M最大是65，D最大是30.如果D被省略默认是0，如果M被省略默认是10。

## 3.2文本类型

* char   0 - 255
* varchar  0 - 65535
* text  0 - 2^16-1
* longtext 0 ~ 2^32-1

## 3.3二进制类型

* blob  0~2^16-1
* longblob  0~2^32-1

## 3.4日期类型

* date
* time
* datetime
* timestamp[时间戳]

# 4. curd

* INSERT

  ```mysql
  INSERT INTO  table_name[(colum [, colum...])]
  VALUES		(value [, value...]);
  ```

* insert语句使用细节

  * 插入数据应该和字段数据类型相同
  * 数据长度在列的规定范围内
  * 在values中类出的数据位置必须和被加入的列的排列位置相对应
  * 列可以插入空值，前提是字段允许为空值
  * 如果是给表中的所有字段添加数据，可以不写前面的字段名称
  * 不给某个字段值时，如果有默认值就会添加否则报错
  * insert into  表名  字段名  values（），（），（），（）可以添加多条语句

* UPDATE

  ```mysql
  UPFATE tab_naem
  		SET col_name=expr1 [,col_name2=expr2...]
  		[WHERE where_definition]
  ```

* update使用细节

  * 可以使用新值更新原有表中的各列
  * SET子句只是要修改哪些列和要赋予哪些值
  * WHERE句子指定更新那些行，没有就全部更新
  * 如果要修改多个字段，可以通过set字段一= 值1，字段二= 值2....

* DELECT

  ```mysql
  delect from  table_name
  		[WHERE where_definition]
  ```

* delete使用细节

  * 如果不使用where子句就会删除表中所用语句
  * 不能删除某一列的值
  * 仅删除记录不能删除表，如果想删除表需要使用drop语句

## 4.1select语句（单表）

* 基本语法

  ```mysql
  SELECT [DISTINCT] */{column1, column2,column3....}
  		FROM table_name;
  ```

* 注意事项

  * select指定查询哪些列的数据
  * column指定列名
  * *代表查询所有列
  * from指定查询哪张表
  * **DISTINCT可选，指显示结果时是否去掉重复数据**
  
* 使用表达式对查询的列进行运算

  ```mysql
  SELECT */{column/expression,column2/expression,...}
  FROM  table;
  
  //例如
  SELECT `student_name` ,(chinese + english + math) FROM student;
  ```

* 在select语句中使用as语句

  ```mysql
  SELECT column_name  别名  from  表名；
  
  
  //例如
  SELECT `student_name` ,(chinese + english + math) AS total FROM student;
  ```

* order by

  ```mysql
  SELECT column1 , column2, column3...
  			FROM table;
  			order by column asc/desc,....
  ```

* order by 指定排序的列，排序的列既可以是表中的列名，也可以是select语句后指定的列名

  * asc 升序，  desc  降序
  * ORDER BY子句应该位于SELECT语句的结尾


## 4.2查询加强

* 比较日期：SELECT * FROM 表名 WHERE 表中的日期列名  >  比较日期

  ```mysql
  SELECT * FROM emp WHERE hiredate  >  '1992-01-01'
  ```

* 模糊查询

  ```MYSQL
  //%：表示0到多个任意字符
  //_：表示单个任意字符
  //例：如何显示首字符位S的员工姓名和工资
  SELECT ename， sal FROM emp
  		WHERE ename LIKE 'S%'
  ```

* 查询表的结构

  ```mysql
  DESC emp
  ```

* ORDER BY:从低到高的顺序排序；  

  ```mysql
  SELECT * FROM emp
  		ORDER BY sal DESC//后面加ASC表示降序排列
  		
  		
  SELECT * FROM emp
  		ORDER BY sal DESC ， sal DESC;//表示在每组部门号里再按照工资排序
  ```

* 分页查询

  ```mysql
  SELECT * FROM emp
  		ORDER BY empno 
  		LIMIT 每页记录数 * （第几页 — 1） ， 每页记录数
  ```

* **几个子语句的使用顺序**

  ```mysql
  SELECT deptno , AVG(sal) AS avg_sal
  FROM emp1
  GROUP BY deptno
  HAVING avg_sal > 1000
  ORDER BY avg_sal
  LIMIT 0, 2
  ```

  

## 4.3 .函数

### 4.3.1统计函数

* count返回行的总数

  ```MySQL
  select count（*）/count（列名） from tablename
  			[WHERE where_definition]
  			
  			
  //例如
  SELECT COUNT(*) FROM student
  		WHERE (math + english + chinese) > 90
  ```

  

* sum:返回满足where条件行的和

  ```mysql
  select sum(列名){, sum(列名)...}  from  tablename
  			[WHERE where_definition]
  			
  
  
  SELECT SUM(math) FROM student
  ```

* avg:求平均值

  ```mysql
  SELECT AVG(math) FROM student
  ```

* MAX求最高；MIN:求最低

* group by对列进行分组

  ```mysql
  SELECT Column1， column2, column3.. FROM table
  		group by column
  ```

* having :对分组后的结果进行过滤

  ```mysql
  SELECT column1, column2, column3...
  		FROM table
  		group by column having...
  		
  		
  ```

### 4.3.2 字符串函数

* CHARSET(列名)  FROM  表名;返回字符串的字符集

* CONCAT (string)  FROM  表名：连接字串进行拼接

* INSTR  (string， substring)  FROM  DUAL:返回substring在字符串中出现的位置，没有出现返回零，DUAL是亚原表

* UCASE (string) FROM  表名：转成大写

* LCASE (string) FROM 表名：转成小写

* LEFT/RIGHT (string， length) FROM 表名：从字符串左边或者右边取length个字符

* LENGTH (string) FROM 表名：字符串的长度

* REPLACE (str， search_str, replace_str):在字段str中，如果有search_str,就替换为replace_str

* STRCMP (string1, string2):逐字符比较大小

* SUBSTRING(字段，num1 ， num2) FROM emp：从表emp中的字段中的第num1位置开始取出num2个字符

  

### 4.3.3 数学函数

* ABS(num): 绝对值

* BIN(decimal_num):十进制转二进制

* CRILING(num2):向上取整得到逼num2大的最小整数

* CONV(number, from_base, to_base):进制转换

* FLOOR(number):向下取整得到比number小的最大整数

* FORMAT(number, decimal_places):保留小数位数

* HEX(DecimalNumber)：转十六进制

* LEAST(number，number2 [,....]):求最小值

* MOD(numerator, denominator):求余数

* RAND([seed])：返回一个在零到一的随机数，如果不想让随机数变化可以添加一个seed值

* ### 4.3.4 时间日期

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-14 161738.png)

* FROM_UNIXTIME():可以把一个unix_timetamp秒数转成指定格式的日期

SELECT FROM_UNIXTIME(1989324628,'%Y-%m-%d')FROM DUAL

*  unix_timestamp():返回一九七零年至今的秒数

SELECT UNIX_TIMESTAMP()  FROM DUAL

### 4.3.5 加密函数和系统函数 

* USER():可以查看登录到MySQL的有哪些用户，以及登陆的IP

* DATABASE():查询当前使用的数据库名称

* MD5(str)：为字符串算出一个MD5 32位的字符串

  ```MYSQL
  SELECT MD5('XQ') FROM DUAL
  ```

* PASSWARD(str):加密函数

### 4.3.6流程控制函数

* IF(expre1, expre2. expre3):如果expr1为真，就会返回2，否则返回三
* IFNULL(expr1,expr2):如果一不为空，则返回1，否则返回二
* SELECT CASE WHEN expr1 THEN expr2 WHEN expr3 THEN expr4 ELSE expr5 END:1为真返回2，如果3为真返回四否则返回五

## 4.4多表查询

* **说明：**多表查询是指两个或两个以上的表查询
* 多表查询时的过滤条件至少是表数减一

* 自连接： 指在同一张表的连接查询【将同一张表看作是两张表】
  * 需要取别名
  * 列名不明确也要取别名

## 4.5 子查询

* 是指嵌入在其它sql语句中的select语句，也叫嵌套查询

* 单行子查询：是指返回一行数据的子查询语句

* 多行子查询：返回多行数据的子查询，使用关键字in

  ```MySQL
  //查询和10号部门工作相同的员工的名字，岗位，工资，部门号，但是不包含10号部门自己的员工
  SELECT ename, job, sal, deptno
  			FROM emp
  			WHERE job IN (
  				SELECT DISNCT job
  				FROM emp
  				WHERE deptno = 10
  			)AND deptno <> 10
  ```

  

* ALL操作符：

  ```
  //
  SELECT ename, sal, deptno
  		FROM emp
  		WHERE sal > ALL(
  			SELECT sal
  				from EMP
  				WHERE deprno = 30
  		)
  ```

  

* ANY操作符:

  ```
  SELECT ename, sal, deptno
  		FROM emp
  		WHERE sal > ANY(
  			SELECT sal
  				from EMP
  				WHERE deprno = 30
  		)
  ```

  

## 4.6表复制和去重

```mysql
//先创建一个新表
//把原有表的数据复制到新表
INSERT INTO my_table
		(id, name, sal, job, deptno)
		SELECT empno. ename, sal, job, deptno, FROM emp;
		
//自我复制
INSERT INTO my_table
		SELECT * FROM my_table;
		
```



```mysql
//先创建一张临时表，结构和原有表一样
CREATE TABLE my_tmp LIKE my_tab
//通过distinct关键字处理把记录复制到临时表
INSERT INTO my_tem
		SELECT DISTINCT * FROM my_tab
//清楚掉原有表的记录
DELECT FROM my_tab
//把临时表的记录复制到原有表，
INSERT INTO my_tab
		SELECT * FROM my_tmp
//使用drop去掉临时表
DROP TABLE my_tmp
SELECT * FROM my_tab
```

## 4.7表外连接

```mysql
//左连接基本语法
select ...
FROM 表一 LEFT JOIN 表二
ON...
//例如  左外连接
SELECT name, stu.id. grade
		FROM stu LEFT JOIN exam
		ON stu.id = exam.id;
		
//右外连接
SELECT name, stu.id. grade
		FROM stu RIGHT JOIN exam
		ON stu.id = exam.id;
```

# 5.约束

## 5.1主键约束

```mysql
//主键的使用
CREATE TABLE t17 
			(id INT PRIMARY KEY,-- id 是主键
			name VARCHAR(32),
			email VARCHAR(32)
			);
INSERT INTO t17
			VALUES(1, 'jack', 'tom@sfh');
INSERT INTO t17
			VALUES(2, 'tom', 'fdsk');
INSERT INTO t17
			VALUES(1, 'xq', 'xq@fsfs');-- 因为主键值不能重复所以此处报错
//主键不能重复也不能为空
INSERT INTO t17
			VALUES(NULL, 'xq', 'xq@fsfs');-- 报错
//一张表最多有一个主键，但可以是复合主键
CREATE TABLE t18 
			(id INT ,
			name VARCHAR(32),
			email VARCHAR(32),
			PRIMARY KEY(id, name)   -- 复合主键
			);			
```

## 5.2非空约束和唯一约束

**NOT   NULL**

如果在列上定义了not null 那么插入数据时必须为列提供数据

**UNIQUE**

当定义了唯一约束后，改列值不能重复，

如果没有指定非空，那么unique字段可以有多个null

一张表可以有多个unique

## 5.3FOREIGN KEY外键约束

* 用于定义主表和从表之间的关系：外键约束要定义在从表上，主表则必须有主键约束或者是唯一约束，当定义外键约束后，要求外键列数据必须在主表的主键列存在或是为null

```mysql
-- 创建主表
CREATE TABLE my_class(
				id INT PRIMARY KEY,
				name VARCHAR(32) NOT NULL DEFAULT'');
				
--创建从表
CREATE TABLE my_stu(
				id INT PRIMARY KEY,
				enames VARCHAR(32) NOT NULL DEFAULT'',
				class_id INT,
				-- 指定外键关系
				FOREIGN KEY (class_id) REFERENCES my_class(id)
)

SELECT * FROM my_stu
-- 数据测试

INSERT INTO my_class
			VALUES(100, 'JAVA'), (200, 'WEB');
			
INSERT INTO my_stu
			VALUES (1, 'TOM', 100);
INSERT INTO my_stu
			VALUES (2, 'ROM', 300);-- 创建失败，id为三百的班级不存在	
INSERT INTO my_stu
			VALUES (3, 'BOM', 200);
```

* 外键指向的表的字段，要求是primary key或者是unique
* 表的类型必须是inodb才支持外键
* 外键字段的类型要和主键字段的类型一致(长度可以不一致)
* 外键字段的值，必须在主键字段中出现过，或者为NULL[前提是外键字段允许为空]
* 一旦建立主外键关系就不能随意删除

## 5.4CHECK约束

* 用于强制行数据必须满足的条件，5.7版本不支持check只作语法校验，但是不会生效

```mysql
-- 创建表			
CREATE TABLE t23(
			id INT PRIMARY KEY,
			name VARCHAR(32),
			sex VARCHAR(6) CHECK (sex IN('man','woman')),
			sal DOUBLE CHECK (sal > 1000 AND sal < 2000)
);
-- 添加数据
INSERT INTO t23
			VALUES(1, 'jack', 'mid', 1);
SELECT * FROM t23-- 没有错误
```

## 5.5 自增长

```mysql
ALTER TABLE t24 AUTO_INCREMENT = 100 -- 自定义初始增长值 
CREATE TABLE t24(
			id INT PRIMARY KEY AUTO_INCREMENT,
			email VARCHAR(32)NOT NULL DEFAULT '',
			name VARCHAR(32) NOT NULL DEFAULT ''
);
INSERT INTO t24 VALUES(
			NULL, 'FPS', 'TOM'
);-- 执行两次
SELECT * FROM t24
```

**细节**

* 一般来说自增长是可以和primary key配合使用的
* 自增长可以单独使用，但是需要配合unique
* 自增长修饰的字段为整数型的，小数也可以但是很少使用
* 自增长默认从一开始，但是可以用过以下指令修改：alter table 表名 auto_increment = xxx；
* 添加数据时，给自增长字段指定了值，则以指定值为准

# 6.索引

```MySQL
-- 创建一个表
CREATE TABLE t25(
			id INT ,
			name VARCHAR(32)
);
-- 查询表是否有索引
SHOW INDEXES FROM t25;
-- 添加一个唯一索引
CREATE UNIQUE INDEX id_index ON t25 (id);
-- 添加普通索引1
CREATE INDEX id_index ON t25(id);
-- 如何选择
-- 如果某列值不会重复，优先选择unique，否则使用普通索引
-- 添加普通索引2
ALTER TABLE t25 ADD INDEX id_index(id)
-- 添加主键索引
ALTER TABLE t26 ADD PRIMARY KEY (id)
-- 删除索引
DROP INDEX id_index ON t24
-- 删除主键索引
ALTER TABLE t26 DROP PRIMARY KEY
-- 修改索引是先删除再修改
-- 查询索引
SHOW INDEXES FROM t25
SHOW INDEX FROM t25
SHOW KEYS FROM t25

```

适合创建索引的列

* 较频繁的作为查询的字段应该创建索引
* 唯一性太差的字段不适合创建索引
* 更新非常频繁的字段不适合创建索引
* 不会出现在WHERE子句中字段不该创建索引

## 6.1主键索引

主键相当于一个索引

## 6.2唯一索引

UNIQUE 

## 6.3普通索引



## 6.4全文索引





# 7. 事务

```MySQL
-- 创建一张测试表
CREATE TABLE t27(
			id INT, 
			name VARCHAR(32)
);
-- 开始事务
START TRANSACTION 
-- 设置保存点
SAVEPOINT a
-- 执行dml操作
INSERT INTO t27 VALUES (100,'tom');
SELECT * FROM t27;

SAVEPOINT b
-- 执行dml操作
INSERT INTO t27 VALUES (200,'tom');

-- 回退到b
ROLLBACK TO b
-- 回退到a
ROLLBACK TO a
```



* 用于保证数据的一致性，它由一组相关的dml语句组成，该组的dml语句要么全部成功要么全部失败

* 几个重要操作：
  * start  transaction开始一个事务
  * savepoint  保存点名--设置保存点
  * rollback to  保存点名--回退事务
  * rollback  -- 回退全部事务
  * commit  -- 提交事务，所有的操作生效，不能回退

* 细节
  * 如果不开启事务，默认情况dml是自动提交的
  * 如果开始了一个事务且没有创建保存点，执行rollback后回退到事务开始的状态
  * 开始一个事务可以是START TRANSACTION 或者是SET autocommit = off



## 7.1隔离级别

多个连接开启各自事务操作数据库中数据时，数据库系统要负责隔离操作，以保证各个连接在获取数据时的准确性

**脏读：**当一个事务读取另一个事务尚未提交的修改时，产生脏读

**不可重复读：**同一查询在同一事务中多次进行，由于其它提交事务所做的修改，每次返回不同的结果集，此时放生不可重复读

**幻读：**同一查询在同一事务中多次进行，由于其它事务所做的插入操作，每次返回不同的结果集，幻读发生

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-17 200217.png)

对号表示可能出现，差号表示不会出现





---

* 修改隔离级别

  ```MYSQL
  SET SESSION TRANSACTION ISOLATION LEVEL 
  ```

  

* 查看和设置隔离级别

```mysql
-- 创建表
CREATE TABLE `account`(
			id INT, 
			name VARCHAR(32),
			money INT
);
-- 查看当前会话隔离级别
SELECT @@tx——isolation
-- 查看系统当前隔离级别
SELECT @@global.tx_isolation
-- 设置当前会话的隔离级别
SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
-- 设置系统当前隔离级别
SET GLOBAL TRANSACTION ISOLATION LEVEL REPEATABLE READ
```

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-17 203242.png)

## 7.2MySQL表类型和存储引擎

**基本介绍：**

* 表类型由存储引擎决定，
* MySQL数据表支持六种类型：csv，Memory， ARCHIVE,MRG_MYISAM, MYISAM,InnoBDB
* 这六种又分为两类一类是“事务安全型”，其余是“非事务安全性”

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-17 204713.png)

# 8.视图

* 基本概念： 视图是一个虚拟表，其内容由查询定义，同真实表一样，视图包含列，其数据对应真实表

```MySQL
-- 创建视图
CREATE VIEW emp1_view01
			AS
			SELECT empno, ename, job, deptno FROM emp1;
-- 查看创建视图的指令
SHOW CREATE VIEW emp1_view01
-- 删除视图
DROP VIEW emp1_view01
```

* 视图细节

  ```mysql
  -- 视图的细节
  -- 1.创建视图后，到数据库去看，对应视图只有一个视图结构文件
  -- 2.视图的数据变化会影响到基表，基表的数据变化也会影响视图
  -- 修改视图
  UPDATE emp1_view01
  			SET job = 'MANAGER'
  			WHERE empno = 7369
  			-- 结果基表也被修改
  -- 视图中可以再使用视图
  CREATE VIEW emp1_view02
  			AS 
  			SELECT empno, ename FROM emp1_view01;
  			
  SELECT * FROM emp1_view02
  ```

  

# 9. MySQL管理

* 创建用户

create user ‘用户名’ @ ‘允许登陆的值’  identified  by  ‘密码’

```MySQL
-- mysql用户管理
-- 创建新的用户
CREATE USER 'hsp_edu'@'localhost' IDENTIFIED BY '123456'
-- 解读'hsp_edu'@'localhost'表示用户的完整信息，'hsp_edu'是用户名，'localhost'是登录的ip，'123456'是密码，存放到MySQL.user表时密码是加密后的密码
SELECT *
			FROM mysql.user
-- 删除用户
DROP USER 'hsp_edu'@'localhost'
-- 登录用户
-- 修改密码
SET PASSWORD = PASSWORD('abcdefg')
```

* 给用户授权

```MySQL
-- 创建新的用户
CREATE USER 'shunping' @'localhost' IDENTIFIED BY '123456'
-- 创建数据库
CREATE DATABASE testdb 
-- 创建一张表
CREATE TABLE news ( id INT, content VARCHAR ( 32 ) );
-- 添加一条测试数据
INSERT INTO news
VALUES
	( 100, '北京新闻' );
SELECT * FROM news;
-- 给'hsp_edu'@'localhost'分配查看news表和添加news的权限
GRANT SELECT , INSERT ON testdb.news TO 'shunping' @'localhost'
-- 修改顺平的密码
SET PASSWORD FOR 'shunping'@'localhost' = PASSWORD('ABC');
-- 回收shunping 用户的所有权限
REVOKE SELECT , UPDATE , INSERT ON test
-- 权限生效指令
FLUSH  PRIVILEGES;
```

* 细节说明
  * 在创建用户的时候，如果不指定Host，则为%，%表示所有IP都有连接权限
