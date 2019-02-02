# MySQL
> MySQL是一种关系数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下产品。

### MySQL存储引擎

- *MyISAM,不支持事务，空间小，以查询为主，要经常使用optimize Table命令来清理磁盘空间，也要经常备份数据
- *InnoDB,适用多删除、更新操作，安全性高，事务处理及并发控制
- Memory,将数据存储在内存中，不支持事务，支持索引，不安全，很少使用
- NDBCluster，主要用于MySQLCluster分布式集群环境时才使用
- CSV，在做报表时比较多
- 其他引擎（需查询）

数据表的存储位置，windows查看my.ini；linux查看 /etc/my.cnf。
### MySQL存储引擎管理命令
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

### MySQL常用函数

##### 聚合函数
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
##### 字符串函数
- CONCAT(str1,str2),字符串链接
- INSERT(str,index,len,newstr),将字符串str中起始位置为index且长度为len的字符串替换为newstr(index起始值1)
- LOWER(str),将字符串转为小写
- UPPER(str),将字符串转为大写
- SUBSTRING(str,index,len),从str中截取起始位置index且长度为len的字符串（index起始值1）

##### 时间日期函数
- CURDATE(),获取当前日期  2018-11-1
- CURTIME(),获取当前时间  20:32:30
- NOW(),获取当前日期和时间  2018-11-1 20:32:50
- WEEK(date),返回日期date为一年中的第几周
- YEAR(date),返回日期date中的年份
- HOUR(date),返回date中的小时值
- MINUTE(date),返回date中的分钟值
- DATEDIFF(date1,date2),返回日期之间相隔的天数date1>date2
- ADDDATE(date,n),返回date加上n天后的日期

##### 数学函数
- CEIL(X),取天花板值   select ceil（2.3） 返回3
- FLOOR(X)，取地板值   select floor（2.3） 返回2
- RAND(),返回0-1之间的随机数


### MySQL中常用命令
##### 连接MySQL
```mysql
mysql -u[username] -p[password]
```
##### 查看所有数据库
```mysql
show databases;
```
##### 转换当前库数据库
```mysql
use database_name;
```
##### 展示当前库所有表
```mysql
show tables;
```
##### 退出数据库
```mysql
exit
```

### MySQL的数据类型

##### 整数类型
- smallint，  2字节
- int，   4字节
- Integer，   同int，默认int（11）
- bigint，    8字节

##### 浮点数
- float， 4字节
- double，    8字节

##### 字符类型
- char， 不可变长度
- varchar，  可变长度

##### 日期类型
- data， yyyy-mm-dd
- datatime， yyyy-MM-dd hh:mm:ss
- time， hh:mm:ss
- timestamp，    更精确的时间
- year， yyyy

##### 其他类型
- blob，   存放二进制文件
- text,    存放大量文本信息    

### MySQL常见SQL优化策略

##### 避免全表扫描
- 对查询进行优化，应尽量避免全表扫描，首先考虑在where和order by 涉及的列上建立索引。

##### 避免判断空值
- 避免在where子句中对字段进行null值判断，否则将导致引擎放弃使用索引而进行全表扫描。可以设置默认值进行优化，使字段有值。

##### 避免不等值判断
- 尽量避免在where子句中使用！=或<>操作符，否则引擎将放弃使用索引而进行全表扫描。

##### 避免使用or逻辑
- 尽量避免在where子句中使用or来连接条件，否则引擎将放弃索引而进行全表扫描。 
- 可以使用union all,select id from table where num=10 union all select id from table where num=20;等价于select id from table where num=10 or num=20；

##### 慎用in 和 not in

##### 注意模糊查询的使用
- like '%aaa%' 可以更改为 like 'aa%' ，前者使用全表扫描。

##### 避免查询条件中字段计算
- 例如：select id from table where num/2=100;
- 可以更改为select id from table where num=100*2；

##### 避免查询条件中对字段进行函数操作。

##### where子句“=”左边不要进行函数、算术运算符或其他表达式运算。

##### 用exists代替in是一个好的选择
- select num from table where num in（select num from table1）;
- 可以替换为select num from table where exists(select 1 from table1 where num=table.num);
- select 1 表示真，select 0 表示假。 
