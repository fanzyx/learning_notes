# MyBatis
> 前身是iBatis ,是Apache的一个开源项目,主要作用是实体类与SQL语句之间建立映射关系。


### 特点
- 基于SQL语句，简单易学。
- 能了解底层封装过程。
- SQL语句封装在配置文件中，便于统一管理和维护，降低程序耦合度。
- 方便程序代码调试。


### 持久化及ORM(Object Relational Mapping)

##### 1.持久化
> 持久化是程序数据在瞬时状态转化为持久状态的过程。

##### 2.ORM-对象关系映射
> 是一种为了解决面向对象与关系数据库存在的互不匹配现象的技术；编写程序时，以面向对象的方式处理数据；保存数据时，以关系型数据库的方式存储。

##### 3.ORM解决方案
- 在持久化对象上执行基本的增删改查操作。
- 对持久化对象提供查询语言或API。
- 提高了开发效率。


### 核心接口和类

##### 1.SqlSessionFactoryBuilder
- 生命周期只存在于方法内。
- 负责构建SqlSessionFactory,提供多个build方法重载。
- 可重用来创建多个SqlSessionFactory实例。

```java
InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
	//以字节流形式创建会话工厂
SqlSessionFactory FACTORY = new SqlSessionFactoryBuilder().build(is);

配置信息以三种形式提供给build方法
InputStream(字节流)、Reader(字符流)、Configuration(类)
```

##### 2.SqlSessionFactory
- 生命周期与应用的生命周期相同。
- 负责创建SqlSession实例。
- 在其运行期内只有一个实例（单例）。

```java
SqlSession session = FACTORY.openSession(boolean autoCommit)
//autoCommit是控制事务控制的参数
true：关闭事务控制（默认）
false：开启事务控制
```

##### 3.SqlSession
- 生命周期为一次会话，会话结束后必须关闭。
- 线程级别，不能够共享。
- 包含了SQL执行的所有方法。

```java
//按语句查询
session.selectList("查询语句");
//按接口查询，
session.getMapper(接口名.class).方法名();
//最后关闭session,一般放在try{}catch{}语句中的finally{}语句块
session.close();
```

### 核心配置文件

##### 1.配置文件结构

```xml
configuration----配置
    properties----引入相关的属性配置文件
    settings----修改MyBatis在运行时的行为方式
    tyypeAliases----为Java类型命名一个别名/简称
    typeHandlers----类型处理器
    objectFactory----对象工厂
    plugins----插件
    environments----环境配置
        environment----环境变量
            transactionManager----事务管理器
            dataSource----数据源
    mappers----映射器
```

##### 2.配置文件示例

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<!-- 引入外部数据库配置文件 -->
	<properties resource="database.properties"></properties>
	<!-- 配置运行相关信息 -->
	<settings>	
		<setting name="logImpl" value="LOG4J" />
	</settings>
	<!-- 配置别名,扫描整个包下的类 -->
	<typeAliases>
		<!-- <typeAlias alias="user" type="com.fan1111.pojo.User"/> -->
		<package name="com.fan1111.pojo"/>
	</typeAliases>
	<!-- 配置运行环境 -->
	<environments default="development">
		<environment id="development">
			<transactionManager type="JDBC"></transactionManager>
			<dataSource type="POOLED">
                                <!-- 读取外部数据库配置信息 -->
				<property name="driver" value="${DRIVER}"/>
				<property name="url" value="${URL}"/>
				<property name="username" value="${USER}"/>
				<property name="password" value="${PWD}"/>
			</dataSource>
		</environment>
	</environments>	
	<!-- 映射器 -->
	<mappers>
		<mapper resource="com/fan1111/dao/user/UserMapper.xml"/>
		<mapper resource="com/fan1111/dao/provider/ProviderMapper.xml"/>
	</mappers>
</configuration>
```

##### 3.常用全局配置属性（settings元素）
![settings常用全局配置](https://github.com/wyd288/learning_notes/blob/master/repo-image/MyBatis/settings%E5%B8%B8%E7%94%A8%E5%85%A8%E5%B1%80%E9%85%8D%E7%BD%AE.png?raw=true)



##### 4.配置文件中配置数据源的两种方式

```xml
直接配置方式：
    <properties>
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://127.0.0.1:3306/fanyi"/>
        <property name="user" value="root"/>
        <property name="password" value="1234"/>
    </properties>
引入配置方式：
    <properties resource="database.properties"></properties>
如果两种方式同时使用，在环境变量中引入数据源时，引入方式会优先于直接方式。
```

### mapper映射

##### 1.映射userMapper示例
按照映射关系，数据库字段名与JavaBean的属性名要保持一致。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 命名空间要与接口对应 -->
<mapper namespace="com.fan1111.dao.user.UserMapper">
<!-- id要与对应接口中的方法名一致 -->
	<select id="userList" resultType="user">
		SELECT * FROM table_user
	</select>
	<resultMap type="User" id="userRole">
		<result property="id" column="id"/>
		<result property="userRoleName" column="RoleName"/>	
	</resultMap>
    <!-- 参数传递使用#{参数名/Map的key/注解名} -->
	<select id="userRole" resultMap="userRole" parameterType="Map">
		select u.*,r.RoleName from table_user u,table_role r 
		WHERE u.userRole = r.id and u.userRole = #{userRole} and u.userName LIKE CONCAT('%',#{userName},'%')
	</select>
	<!-- 添加用户的SQL映射 -->
	<insert id="addUser" parameterType="User">
		INSERT INTO table_user(userCode,userName,userPassword,gender,birthday,phone,address,userRole,createdBy,creationDate) 
		VALUES(#{userCode},#{userName},#{userPassword},#{gender},#{birthday},#{phone},#{address},#{userRole},#{createdBy},#{creationDate})
	</insert>	
	<update id="updUser" parameterType="User">
		UPDATE table_user SET 
			userCode=#{userCode},
			userName=#{userName},
			userPassword=#{userPassword},
			gender=#{gender},
			birthday=#{birthday},
			phone=#{phone},
			address=#{address},
			userRole=#{userRole},
			modifyBy=#{modifyBy},
			modifyDate=#{modifyDate}
		WHERE id=#{id}
	</update>
<delete id="delUser">
		delete from table_user where id = #{id}
	</delete>		
</mapper>
```

##### 2.resultMap属性和子元素

属性
- id----resultMap的唯一标识
- type----java实体类

子元素
- id----一般对应数据库中该行的主键id，设置此项可提高mybatis性能
- result----映射到JavaBean的某个“简单类型”属性，如Integer、String
- association----映射到JavaBean的某个“复杂类型”属性，如JavaBean类
- collection----映射到JavaBean的某个“复杂类型”属性，如集合

##### 3.association复杂类型——关联

```xml
 <resultMap type="Role" id="roleResult">
	<id property="id" column="r_id"/>
	<result property="roleCode" column="roleCode"/>
	<result property="roleName" column="roleName"/>
</resultMap>
	
<resultMap type="User" id="userRoleResult">
    <id property="id" column="id"/>
    <result property="userCode" column="userCode"/>
    <result property="userName" column="userName"/>
    <result property="userRole" column="userRole"/>
    <association property="role" javaType="Role" resultMap="roleResult"/>		
</resultMap>
```

##### 4.collection复杂类型——集合

```xml
<resultMap type="User" id="userAddress">
	<id property="id" column="id"/>
	<result property="userCode" column="userCode"/>
	<result property="userName" column="userName"/>
	<collection property="addressList" ofType="Address">
		<id property="id" column="a_id"/>
		<result property="contact" column="contact"/>
		<result property="addressDesc" column="addressDesc"/>
		<result property="postCode" column="postCode"/>
		<result property="tel" column="tel"/>
	</collection>
</resultMap>
```

### 动态SQL

##### 1.if
> 实现简单的条件判断。

```xml
<select id="userList" resultType="user">
	SELECT * FROM table_user WHRER 1=1
	<if test="id != null">AND id=#{id}</if>
</select>
```

##### 2.where
> 智能处理and/or，简化where条件判断。

```xml
<select id="userList" resultType="user">
	SELECT * FROM table_user 
	<where>
		<if test="id != null">
			AND id=#{id}
		</if>
	</where>	
</select>
```

##### 3.trim
> 更灵活的去除多余的关键字，可代替where。

属性 | 说明
---|---
prefix | 前缀
prefixOverrides | 可覆盖的前缀
suffix |后缀
suffixOverrides |可覆盖的后缀

```xml
<update id="modify" parameterType="User">
    update table_user
    <trim prefix="set" suffixOverrides="," suffix="where id=#{id}">
        <if test="userCode != null">userCode = #{userCode},</if>
        <if test="userName != null">userName = #{userName},</if>
    </trim>
</update>
```

##### 4.choose(when/otherwise)
> 相当于switch语句，当when有条件满足时，跳出choose，一般情况下很少使用。

```xml
<choose>
	<when test="条件1">语句1</when>
	<when test="条件2">语句2</when>
	<when test="条件3">语句3</when>
	<otherwise>语句4</otherwise>
</choose>
```

##### 5.foreach
> 迭代一个集合，通常用于in条件

属性 | 说明
---|---
item | 被迭代项目
collection | 集合：list、array、map-key
index | 下标，可选
open | 开始符号，可选
separator | 分隔符，可选
close | 关闭符号，可选

```xml
<resultMap type="User" id="userMapByRole">
	<id property="id" column="id"/>
	<result property="userCode" column="userCode"/>
	<result property="userName" column="userName"/>
</resultMap>
<select id="getUserByRoleId" resultMap="userMapByRole">
	SELECT * FROM table_user where userRole in
	<foreach collection="array" item="roleIds" open="(" separator="," close=")">
	#{roleIds}
	</foreach>
</select>
```


