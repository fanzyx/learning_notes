# 数据库
> “数据库”是以一定方式储存在一起、能够多个用户共享、具有尽可能小的冗余度、与应用程序彼此独立的数据集合。

### 【基本术语】
- DB：数据库
- DBA：数据库管理员
- DBM：数据库管理系统
- DBS：数据库系统

### 【SQL分类】
1. DDL：数据定义语言
> 用来创建数据库中的各种对象-----表、视图、索引、同义词、聚簇等.----CREATE
2. DCL：数据控制语言
> 用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果，对数据库实行监视等
```
1) GRANT：授权。
2) ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。
回滚---ROLLBACK
回滚命令使数据库状态回到上次最后提交的状态。其格式为：
SQL>ROLLBACK;
3) COMMIT [WORK]：提交。
    在数据库的插入、删除和修改操作时，只有当事务在提交到数据
库时才算完成。在事务提交前，只有操作数据库的这个人才能有权看
到所做的事情，别人只有在最后提交完成后才可以看到。
提交数据有三种类型：显式提交、隐式提交及自动提交。下面分
别说明这三种类型。
(1) 显式提交
用COMMIT命令直接完成的提交为显式提交。其格式为：
SQL>COMMIT；
(2) 隐式提交
用SQL命令间接完成的提交为隐式提交。这些命令是：
ALTER，AUDIT，COMMENT，CONNECT，CREATE，DISCONNECT，DROP，
EXIT，GRANT，NOAUDIT，QUIT，REVOKE，RENAME。
(3) 自动提交
若把AUTOCOMMIT设置为ON，则在插入、修改、删除语句执行后，
系统将自动进行提交，这就是自动提交。其格式为：
SQL>SET AUTOCOMMIT ON；
```
3. DML：数据操纵语言
> 主要有三种形式：插入：INSERT;更新：UPDATE;删除：DELETE
4. DQL：数据查询语言
> 数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE子句组成的查询块：
> SELECT <字段名表>
> FROM <表或视图名>
> WHERE <查询条件>


### 【数据库索引】
1. 索引简介
> 索引是一种有效组合数据的方式，为快速查找到指定记录
2. 索引作用
    - 提高数据库的检索速度
    - 改善数据库性能
3. 索引分类
    - B树索引：InnoDB、MyISAM均支持
    - 哈希索引
4. 常用索引（创建索引时最好给索引加上长度）
    - 普通索引：允许在定义索引的列中插入重复值和空值
    ```sql
    ALTER TABLE table_name ADD INDEX index_name (column_name); 
    ```
    - 唯一索引：索引列数据不重复，允许有空值
    ```sql
    ALTER TABLE table_name ADD UNIQUE (column_name);
    ```
    - 主键索引：主键将自动创建索引，每个值是非空、唯一的
    ```sql
    ALTER TABLE table_name ADD PRIMARY KEY (column_name); 
    ```
    - 复合索引/多列索引：将多个列组合作为索引
    ```sql
    ALTER TABLE table_name ADD INDEX index_name(column1,column2,...);
    ```
    - 全文索引：支持值的全文查找，允许重复值和空值
    ```sql
    ALTER TABLE table_name ADD FULLTEXT (column_name); 
    ```
    - 空间索引：对空间数据类型的列建立的索引

5. 查看和删除索引
    ```sql
    //查看索引
    SHOW INDEX FROM table_name;
    //查看全部索引
    SHOW INDEX FROM table_name\G;
    //删除索引
    DROP INDEX index_name ON table_name;
    ALTER TABLE table_name DROP INDEX index_name;
    Alter TABLE table_name DROP PRIMARY KEY;
    ```
6. 创建索引的指导
    - 频繁搜索的列
    - 经常用作查询选择的列
    - 经常排序、分组的列
    - 经常用作连接的列（主键/外键）
    - 仅包含几个不同值或表内容仅有几行不适合创建索引
7. 注意事项
    - 查询时减少使用*返回全部列，不要返回不需要的列
    - 索引应该尽量小，在字节数小的列上简历索引
    - WHERE子句中有多个表达式时，包含索引列的表达式应置于其他条件之前
    - 避免在ORDER BY 子句中使用表达式

### 【数据库事务】
事务是程序中一系列严密的操作，所有操作执行必须成功完成，否则在每个操作所做的更改将会被撤销
1. 事务的特性，简称ACID属性
    - 原子性（Atomicity）
    > 事务是一个完整的操作，事务的各步操作是不可分的，要么全执行，要么都不执行

    - 一致性（Consistency）
    > 当事务完成时，数据必须处于一致状态
    
    - 隔离性（Isolation）
    > 并发事务之间彼此隔离、独立，它不应以任何方式依赖于或影响其他事务
    
    - 持久性（Durability）
    > 事务完成后，它对数据库的修改被永久保存
    
2. 事务的操作（需要存储引擎支持）
    - 开始事务（BEGIN或START TRANSACTION）
    - 提交事务（COMMIT）
    - 回滚事务（ROLLBACK）
    - 关闭/开启自动提交状态
        - SET autocommit=0|1;(0为关闭，1为开启，mysql默认开启)
> 关闭自动提交后，从下一条语句开始则开启新事务，需使用commit或rollback语句结束该事务（MySQL默认情况下，每条单独的SQL语句视为一个事务）
3. 事务的隔离级别（由低到高）
    - read uncommited：是最低的事务隔离级别，它允许另外一个事务可以看到这个事务未提交的数据。
    - read commited：保证一个事物提交后才能被另外一个事务读取。另外一个事务不能读取该事物未提交的数据。
    - repeatable read：这种事务隔离级别可以防止脏读，不可重复读。但是可能会出现幻象读。它除了保证一个事务不能被另外一个事务读取未提交的数据之外还避免了以下情况产生（不可重复读）。
    - serializable：这是花费最高代价但最可靠的事务隔离级别。事务被处理为顺序执行。除了防止脏读，不可重复读之外，还避免了幻象读。

> **脏读**：指当一个事务正在访问数据，并且对数据进行了修改，而这种数据还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。因为这个数据还没有提交那么另外一个事务读取到的这个数据我们称之为脏数据。依据脏数据所做的操作可能是不正确的。

> **不可重复读**：指在一个事务内，多次读同一数据。在这个事务还没有执行结束，另外一个事务也访问该同一数据，那么在第一个事务中的两次读取数据之间，由于第二个事务的修改第一个事务两次读到的数据可能是不一样的，这样就发生了在一个事物内两次连续读到的数据是不一样的，这种情况被称为是不可重复读。

> **幻象读**：一个事务先后读取一个范围的记录，但两次读取的纪录数不同，我们称之为幻象读（两次执行同一条 select 语句会出现不同的结果，第二次读会增加一数据行，并没有说这两次执行是在同一个事务中）

4. spring事务传播特性
> 事务传播行为就是多个事务方法相互调用时，事务如何在这些方法间传播。(7种)

    - propagation_requierd（默认）：如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这个事务中。
    - propagation_supports：支持当前事务，如果没有当前事务，就以非事务方法执行。
    - propagation_mandatory：使用当前事务，如果没有当前事务，就抛出异常。
    - propagation_required_new：新建事务，如果当前存在事务，把当前事务挂起。
    - propagation_not_supported：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
    - propagation_never：以非事务方式执行操作，如果当前事务存在则抛出异常。
    - propagation_nested：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与propagation_required类似的操作


### 【数据库视图】
1. 视图介绍
> 视图是一张虚拟表，其结构和数据时简历在对表的查询基础上，表示一张表的部分数据或多张表的综合数据；视图中不存放数据；一个原始表可以创建不同的视图。
2. 视图的用途
    - 筛选表中的行
    - 防止未经许可的用户访问敏感数据
    - 降低操作数据库的复杂程度
    - 将多个物理数据库抽象为一个逻辑数据库
3. 视图操作
    - 创建视图
    ```sql
    CREATE VIEW view_name AS SELECT (值列表) FROM table_name;
    ```
    - 删除视图
    ```sql
    DROP VIEW [IF EXISTS] view_name;
    //用if exists 关键字判断视图是否存在
    ```
    - 查看视图
    ```sql
    SELECT (值列表) FROM view_name;
    //查看所有视图
    SHOW TABLE STATUS WHERE COMMENT='view';
    ```
4. 注意事项
    - 视图中可以使用多个表
    - 一个视图可以嵌套另一个视图
    - 对视图数据进行添加、更新和删除操作直接影响所引用表中的数据
    - 当视图数据来自多个表时，不允许添加和删除数据

### 【数据库定义/控制/操作语法】
1. 添加数据库
```sql
CREATE DATABASE testdatabase;
```
2. 删除数据库
```sql
DROP DATABASE testdatabase;
```
3. 添加数据表
```sql
CREATE TABLE test2(uid INT(4) PRIMARY KEY AUTO_INCREMENT,uname VARCHAR(20) NOT NULL);

//修改表名
ALTER TABLE old_table_name RENAME new_table_name;
```
4. 删除数据表
```sql
DROP TABLE test2;
```
5. 添加数据：
``` sql
INSERT INTO table[(列名列表)] VALUES(值列表)；
//自增列不赋值，其他列一一对应；
    - 批量添加
        - 现有表插入新表,如新表已存在不能重复创建：
        CREATE TABLE new_table_name(查询语句)//一个表只能执行一次
        create table phonelist(select stuno,stuphone from student);
        - 插入多条数据：
        INSERT INTO table[(列名列表)] VALUES(值列表1)，(值列表2)，...，（值列表n）;
```
6. 更新数据：
``` sql
UPDATE table_name SET 列1=值，列2=值，...,列n=值 [WHERE 更新条件];
```
7. 删除数据：
```sql
DELETE FROM table_name [WHERE 删除条件];//删除表中数据
    批量删除：TRUNCATE TABLE table_name; 
    TRUNCATE TABLE注意：*如删除所有数据，推荐使用此命令
        1.删除数据无法恢复
        2.自增列重新计数
        3.无法删除有外键关联的主表
```
8. 表字段操作
```sql
//添加字段
ALTER TABLE table_name ADD column1_name column1_type,...;

//删除字段：
ALTER TABLE table_name DROP COLUMN column_name;

//修改字段：
ALTER TABLE table_name ALTER COLUMN column_name column_type；

//修改字段名
ALTER TABLE table_name CHANGE column_name new_name column_type;

//组合主键
ALTER TABLE table_name ADD CONSTRAINT primary_key_name PRIMARY KEY table_name(column1,column2,...);

//添加外键
ALTER TABLE foreign_table_name ADD CONSTRAINT foreign_key_name FOREIGN KEY (column_name) REFERENCES primary_table_name(column_name);

//删除外键
ALTER TABLE foreign_table_name DROP FOREIGN KEY foreign_key_name;
```
### 【数据查询语法】
- 基本语法
``` sql
    SELECT */列名列表 FROM table [WHERE 查询条件]
    select * from user where id=1;
```
- 分组，用在WHERE 之后
``` sql
    GROUP BY (column1[,column2,...])
    //select后的表达式对每一个分组只能返回一个值
    SELECT * FROM user where id>20 GROUP BY gender;
```
- 分组后筛选，用在GROUP BY 之后
``` sql
    HAVING 筛选条件(只能是聚合函数的形式)
    //将使用聚合函数计算并分组后的数据按条件筛选
    SELECT *,COUNT(score) FROM user where id>20 GROUP BY name HAVING COUNT(score)>60;
```

- 排序
``` sql
    ORDER BY (colunm1 [ASC/DESC],column2 [ASC/DESC],...) 
    //ASC默认升序/DESC降序
    SELECT *,COUNT(score) FROM user where id>20 GROUP BY name HAVING COUNT(score)>60 ORDER BY id DESC;
```
- 分页
``` sql
    MySQL分页：
    LIMIT [起始值(下标从0开始)，]页容量;
    
    Oracle分页：
    select column1，column2 from
        （select column1，column2，rn from
            (select column1，column2，rowNum rn from table) 
        where rn<=最大值）
    where rn>最小值
```
- 高级查询
1. 表连接查询（更适合查看多表数据）
``` sql
    1.内连接(等值连接/取交集)
    SELECT u.*,r.roleName FROM smbms_user u 
    INNER JOIN smbms_role r ON u.`userRole`=r.`id`
    INNER JOIN ...  ON  ...
    [WHERE 查询条件];
    2.外连接(以左/右表为主，未匹配的字段为null) 
    SELECT u.*,r.roleName FROM smbms_user u RIGHT [OUTER] JOIN smbms_role r ON u.`userRole`=r.`id`;
    
    //所有的表连接查询都可以用子查询替换，反之不对。
```
2. 模糊查询
``` sql
    //LIKE ：一般与字符串字段配合使用
    通配符：%（匹配N多字符）
            _（匹配一个字符）
            []（该位置取值在给定范围内）
            [^]（取值不在给定范围内）
    SELECT *
    FROM smbms_user
    WHERE userName LIKE '%张%'
    WHERE userName LIKE '张_'
    WHERE phone LIKE '13[5-9]%'
    
    //between:取值是连续的区间
    SELECT *
    FROM smbms_user
    WHERE birthday BETWEEN '1971-1-1' AND '1999-12-12';
    
    //IN / NOT IN：取值为集合，可以跟随返回多条记录的子查询
    SELECT * FROM smbms_user where id IN(1,2,3);
    SELECT * FROM smbms_user where id NOT IN(SELECT id FROM smbms_user WHERE userRole>1);
```
3. 子查询（适合作为增删改查的条件）
``` sql
    可以出现在任何表达式可以出现的位置
    //例如查询年龄小于赵燕的用户
    SELECT userName FROM smbms_user 
        WHERE age<(SELECT age FROM smbms_user 
            WHERE userCode='zhaoyan');
    //子查询和比较运算符联合使用时，必须保证子查询返回的结果不能多于一个
    
    
```



### 【MySQL存储引擎】
1. *MyISAM,不支持事务，空间小，以查询为主，要经常使用optimize Table命令来清理磁盘空间，也要经常备份数据
2. *InnoDB,适用多删除、更新操作，安全性高，事务处理及并发控制
3. Memory,将数据存储在内存中，不支持事务，支持索引，不安全，很少使用
4. NDBCluster，主要用于MySQLCluster分布式集群环境时才使用
5. CSV，在做报表时比较多
6. 其他引擎（需查询）

数据表的存储位置，windows查看my.ini；linux查看 /etc/my.cnf。
### 【MySQL存储引擎管理命令】
```sql
//查看数据库支持的存储引擎
# SHOW engines;

//查看数据库当前使用的存储引擎（默认引擎）
# SHOW variables like '%engine%';

//查看数据库表所使用的存储引擎
# SHOW CREATE TABLE table_name;

//创建表指定存储引擎
# CREATE TABLE table_name(column_name column_type)engine=engine_name;

//修改表的存储引擎
# ALTER TABLE table_name engine=engine_name;

//修改默认的存储引擎
# 在配置文件中修改default-storage-engine=INNODB；

```

### 【MySQL常用函数】
1. 聚合函数
    - AVG(),返回某字段的平均值
    - COUNT(),返回某字段的行数
    - MAX(),返回某字段的最大值
    - MIN(),返回某字段的最小值
    - SUM(),返回某字段的和
```
count(*)包括了所有的列，相当于行数，在统计结果的时候，不会忽略列值为NULL  
count(1)包括了忽略所有列，用1代表代码行，在统计结果的时候，不会忽略列值为NULL  
count(列名)只包括列名那一列，在统计结果的时候，某个字段值为NULL时，不统计。
列名为主键，count(列名)会比count(1)快  
列名不为主键，count(1)会比count(列名)快  
如果表多个列并且没有主键，则 count（1） 的执行效率优于 count（*）  
如果有主键，则 select count（主键）的执行效率是最优的  
如果表只有一个字段，则 select count（*）最优。
```
2. 字符串函数
    - CONCAT(str1,str2),字符串链接
    - INSERT(str,index,len,newstr),将字符串str中起始位置为index且长度为len的字符串替换为newstr(index起始值1)
    - LOWER(str),将字符串转为小写
    - UPPER(str),将字符串转为大写
    - SUBSTRING(str,index,len),从str中截取起始位置index且长度为len的字符串（index起始值1）
3. 时间日期函数
    - CURDATE(),获取当前日期  2018-11-1
    - CURTIME(),获取当前时间  20:32:30
    - NOW(),获取当前日期和时间  2018-11-1 20:32:50
    - WEEK(date),返回日期date为一年中的第几周
    - YEAR(date),返回日期date中的年份
    - HOUR(date),返回date中的小时值
    - MINUTE(date),返回date中的分钟值
    - DATEDIFF(date1,date2),返回日期之间相隔的天数date1>date2
    - ADDDATE(date,n),返回date加上n天后的日期
4. 数学函数
    - CEIL(X),取天花板值   select ceil（2.3） 返回3
    - FLOOR(X)，取地板值   select floor（2.3） 返回2
    - RAND(),返回0-1之间的随机数







### 【MySQL中常用命令】
1. 连接MySQL
```mysql
mysql -u[username] -p[password]
```
2. 查看所有数据库
```mysql
show databases;
```
3. 转换当前库数据库
```mysql
use database_name;
```
4. 展示当前库所有表
```mysql
show tables;
```
5. 退出数据库
```mysql
exit
```

### 【MySQL的数据类型】
1. 整数类型
    - smallint，  2字节
    - int，   4字节
    - Integer，   同int，默认int（11）
    - bigint，    8字节
2.浮点数
    - float， 4字节
    - double，    8字节
3. 字符类型
    - char， 不可变长度
    - varchar，  可变长度
4. 日期类型
    - data， yyyy-mm-dd
    - datatime， yyyy-MM-dd hh:mm:ss
    - time， hh:mm:ss
    - timestamp，    更精确的时间
    - year， yyyy
5.  其他类型
    - blob，   存放二进制文件
    - text,    存放大量文本信息    

### 【MySQL常见SQL优化策略】
1. 避免全表扫描
    - 对查询进行优化，应尽量避免全表扫描，首先考虑在where和order by 涉及的列上建立索引。
2. 避免判断空值
    - 避免在where子句中对字段进行null值判断，否则将导致引擎放弃使用索引而进行全表扫描。可以设置默认值进行优化，使字段有值。
3. 避免不等值判断
    - 尽量避免在where子句中使用！=或<>操作符，否则引擎将放弃使用索引而进行全表扫描。
4. 避免使用or逻辑
    - 尽量避免在where子句中使用or来连接条件，否则引擎将放弃索引而进行全表扫描。 
    - 可以使用union all,select id from table where num=10 union all select id from table where num=20;等价于select id from table where num=10 or num=20；
5. 慎用in 和 not in
6. 注意模糊查询的使用
    - like '%aaa%' 可以更改为 like 'aa%' ，前者使用全表扫描。
7. 避免查询条件中字段计算
    - 例如：select id from table where num/2=100;
    - 可以更改为select id from table where num=100*2；
8. 避免查询条件中对字段进行函数操作。
9. where子句“=”左边不要进行函数、算术运算符或其他表达式运算。
10. 用exists代替in是一个好的选择
    - select num from table where num in（select num from table1）;
    - 可以替换为select num from table where exists(select 1 from table1 where num=table.num);
    - select 1 表示真，select 0 表示假。 




