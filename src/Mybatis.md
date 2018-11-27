### 【MyBatis介绍】
> 前身是iBatis ,是Apache的一个开源项目,主要作用是实体类与SQL语句之间建立映射关系。

- 特点
    - 基于SQL语句，简单易学
    - 能了解底层封装过程
    - SQL语句封装在配置文件中，便于统一管理和维护，降低程序耦合度
    - 方便程序代码调试

### 【持久化及ORM(Object Relational Mapping)】
1. 持久化
> 持久化是程序数据在瞬时状态转化为持久状态的过程。

2. ORM-对象关系映射
> 是一种为了解决面向对象与关系数据库存在的互不匹配现象的技术；编写程序时，以面向对象的方式处理数据；保存数据时，以关系型数据库的方式存储。

3. ORM解决方案
    - 在持久化对象上执行基本的增删改查操作
    - 对持久化对象提供查询语言或API
    - 提高了开发效率

### 【Mybatis核心接口和类】
1. SqlSessionFactoryBuilder
    - 生命周期只存在于方法内
    - 负责构建SqlSessionFactory,提供多个build方法重载
    - 可重用来创建多个SqlSessionFactory实例

2. SqlSessionFactory


3. SqlSession









