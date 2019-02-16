### 【Spring简介】
1. 设计目标
    - 解决企业应用开发的复杂性，使现有技术更加易用。
2. 核心技术
    - IOC(Inversion of Control)控制反转/DI(Dependency Injection)依赖注入
    - AOP(Aspect Oriented Programming)面向切面编程

3. 存在优点
    - 低侵入式设计
    - 独立于各种应用服务器
    - DI将组件关系透明化，降低了耦合度
    - AOP允许将通用任务进行集中处理
    - 能够良好的与第三方框架整合
![Spring特性](6031360EF97A47D0A590F29A236E2E66)

4. 常用注解
> 在xml中加入<context:component-scan base-package="com.xxxx.service,com.xxxx.dao"/>启动注解扫描；
加入<aop:aspectj-autoproxy />启动AOP注解扫描；
- @Component:标注Bean类
- @Repository:标注数据访问层类
- @Service:标注服务层类
- @Controller:标注控制器类
- @Autowired:自动装配Bean(默认按类型匹配)
- @Resource:自动装配Bean(默认按名称匹配)
- @Aspect:标注增强类
    - @Before:标注前置增强方法
    - @AfterReturning:标注后置增强方法
    - @AfterThrowing:标注异常增强方法
    - @Around:标注环绕增强方法
    - @After:标注最终增强方法
    
5. Bean的作用域：在配置文件中通过元素scope，注解使用@Scope,指定作用域
    - singleton:默认值，以单例模式创建实例
    - prototype:每次获取Bean时，都会创建新实例
    - request:用于Web应用环境，针对每次HTTP请求都会创建一个实例
    - session:用于Web应用环境，同一个会话共享同一个实例


### 【IOC(Inversion of Control)控制反转】
> 解耦合，将组件对象的控制权从代码本身转移到外部容器，使用接口分离关注点，不再关注实现，实现每个组件时，只关注组件内部的业务。

![IOC](00524BF1C8824D2EA77610CEE0EF159E)

1. 设值注入
>  IoC容器通过成员变量的setter方法来注入被依赖对象
2. 构造注入
>  IoC容器通过构造方法来注入被依赖对象，在xml中使用<constructor-arg>元素来表示构造方法的一个参数，使用时不区分顺序，可以用index指定参数位置，type指定参数类型。
3. 使用区别

设值注入 | 构造注入
---|---
通过setter访问器实现 | 通过构造方法实现
灵活性好，但setter方法数量过多 | 灵活性差，仅靠重载限制太多
时效性差 | 时效性好
通过无参构造实例化 | 通过哦匹配的构造方法实例化，但建议保留无参构造

4. 注入不同的数据类型
    - 注入直接量：使用<value>标签实现，要注意特殊字符的处理
    - 引用Bean：使用<ref>标签实现，注意bean属性和local属性的区别
    - 使用内部Bean：
    ```xml
    <property name ="dao">
        <bean class="dao.impl.UserDaoImpl"/>
    </property>
    ```
    - 注入集合:使用<list>、<set>、<map>、<props>标签实现
    - 注入null和空字符串：使用<null/>注入null值；使用<value></value>注入空字符串


### 【使用Spring实现IOC示例】
1. 导入jar包/Maven构建
2. 创建实体类(HelloSpring.java)
```java
package com.fan1111.spring;
public class HelloSpring {
	//定义变量who，其值通过spring框架进行注入，设值注入必须有setter方法
	private String who;
	//获取who的值
	public String getWho() {
		return who;
	}
	//设置who的值
	public void setWho(String who) {
		this.who = who;
	}
	// 定义打印方法，输出一句完整的问候
	public void print(){
		System.out.println("Hello,"+this.getWho()+"!");
	}	
}
```
3. 编写配置文件(ApplicationContext.xml)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<!-- 这个过程相当于new新对象的过程，由bean管理	==	HelloSpring helloSpring = new HelloSpring() -->
	<bean id="helloSpring" class="com.fan1111.spring.HelloSpring">
    	<!-- 指定被赋值的属性名,和set方法是映射的  -->
    	<property name="Who">
    		<!-- 赋给属性的值 -->
    		<value>Spring</value>
    	</property>
	</bean>
</beans>
```
4. 编写测试类(HelloSpringTest.java)
```java
public class HelloSpringTest {
	//读取配置文件
	private ApplicationContext ctx = new ClassPathXmlApplicationContext("ApplicationContext.xml");
	@Test
	public void test() {
	//获得对应Bean对象
	HelloSpring helloSpring = (HelloSpring)ctx.getBean("helloSpring");
	//执行方法
	helloSpring.print();	
	}
}
```
5. 注意
```java
以下三个接口都可以读取配置文件
(最常用)ApplicationContext
FileSystemXMLApplicationContext
BeanFactory

<property>元素中，ref属性和value属性的区别
value:传入的是基础数据类型
ref:传入的是上面定义好的bean对象，通过id值
```
### 【AOP(Aspect Oriented Programming)面向切面编程】
> AOP是一种通过预编译方式和运行期动态代理实现在不修改源代码的情况下给程序动态添加功能的技术

1. 目标
    - 业务代码作为核心关注点，其他代码作为横切关注点 
2. 原理
    - 将复杂的需求分解出不同方面，将公共功能集中解决
    - 采用代理机制组装运行，在不改变原程序的基础上对代码进行增强处理
3. 相关术语
    - 增强处理(Advice)
        - 前置增强(Before):在目标方法前织入增强处理
        - 后置增强(AfterReturning):在目标方法正常执行后织入增强处理
        - 环绕增强(Around):在目标方法前后都织入增强处理
        - 异常抛出增强(AfterThrowing):在目标方法抛出异常后织入增强处理
        - 最终增强(After):不论方法是否抛异常，都在目标方法最后织入增强
    - 切入点(Pointcut)
    - 连接点(Join Pont)
    - 切面(Aspect)
    - 目标对象(Target Object)
    - AOP代理(AOP Proxy)
    - 织入(Weaving)

### 【使用Spring实现AOP的示例】
1. 导入jar包/Maven构建
2. 编写增强类实现日志(UserLogger.java)
```java
package aop;
import org.apache.log4j.Logger;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;

public class UserLogger {
	private Logger logger = Logger.getLogger(UserLogger.class);
	//前置增强，方法名与配置文件中的method属性进行匹配
	public void Mbefore(JoinPoint jp){
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法");
	}
	//后置增强
	public void MafterReturn(JoinPoint jp,Object result){
		logger.info("使用："+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法,返回结果是："+result);
	}
	//异常抛出增强
	public void Mthrow(JoinPoint jp,Exception e){
		logger.error(jp.getTarget()+"类的"+jp.getSignature().getName()+"方法抛出异常"+e);
	}

	//环绕增强
	public Object Maround(ProceedingJoinPoint jp){
		Object result = null;
		//前置设置
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法");
		try {
			result = jp.proceed();
		} catch (Throwable e) {
			logger.error(jp.getTarget()+"类的"+jp.getSignature().getName()+"方法抛出异常"+e);
		}finally{
			logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法执行结束");
		}
		return result;
	}
	//最终增强
	public void Mafter(JoinPoint jp){
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法执行结束");
	}	
}

```

使用注解的增强实现

```java

package aop;
import org.apache.log4j.Logger;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
@Aspect
public class UserLogger {
	private Logger logger = Logger.getLogger(UserLogger.class);
	//定义切入点
    @Pointcut("execution(* service..*.*(..))")
	public void pointCut(){}
	
	//前置增强
	@Before("pointCut()")
	public void Mbefore(JoinPoint jp){
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法");
	}
	//后置增强
	@AfterReturning(pointcut="pointCut()",returning="result")
	public void MafterReturn(JoinPoint jp,Object result){
		logger.info("使用："+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法,返回结果是："+result);
	}
	//异常抛出增强
	@AfterThrowing(pointcut="pointCut()",throwing="e")
	public void Mthrow(JoinPoint jp,Exception e){
		logger.error(jp.getTarget()+"类的"+jp.getSignature().getName()+"方法抛出异常"+e);
	}
	//环绕增强
	@Around("pointCut()")
	public Object Maround(ProceedingJoinPoint jp){
		Object result = null;
		//前置设置
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法");
		try {
			result = jp.proceed();
		} catch (Throwable e) {
			logger.error(jp.getTarget()+"类的"+jp.getSignature().getName()+"方法抛出异常"+e);
		}finally{
			logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法执行结束");
		}
		return result;
	}
	//最终增强
	@After("pointCut()")
	public void Mafter(JoinPoint jp){
		logger.info("使用"+jp.getTarget()+"类的"+jp.getSignature().getName()+"方法执行结束");
	}	
}
```

3. 编写配置文件(ApplicationContext.xml)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop
           http://www.springframework.org/schema/aop/spring-aop.xsd">

	<!-- 声明增强处理bean -->
	<bean id="userLogger" class="aop.UserLogger"></bean>
	<!-- 织入增强 -->
	<aop:config>
		<!-- 设置切入点 -->
		<aop:pointcut expression="execution(* service..*.*(..))" id="pointCut"/>
		<!-- 设置切面 -->
		<aop:aspect ref="userLogger">
			<!-- 前置增强 -->
			<aop:before method="Mbefore" pointcut-ref="pointCut"/>
			<!-- 后置增强 -->
			<aop:after-returning method="MafterReturn" pointcut-ref="pointCut" returning="result"/>
			<!-- 异常抛出增强 -->
			<aop:after-throwing method="Mthrow" pointcut-ref="pointCut" throwing="e"/>
			<!-- 最终增强 -->
			<aop:after method="Mafter" pointcut-ref="pointCut"/>
			<!-- 环绕增强 -->
			<aop:around method="Maround" pointcut-ref="pointCut"/>
		</aop:aspect>
	</aop:config>

</beans>
```

使用注解的配置文件

```xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop
           http://www.springframework.org/schema/aop/spring-aop.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context.xsd">
	
	<!-- 注解扫描,指定基类包，用逗号分隔 -->
	<context:component-scan base-package="dao,service"></context:component-scan>
	<!-- 定义增强类 -->
	<bean class="aop.UserLogger"></bean>
	<!-- 启动AspectJ注解，自动代理 -->
	<aop:aspectj-autoproxy/>
</beans>
```

4. 编写测试类(UserAOPTest.java)
```java
public class UserAOPTest {

	@Test
	public void test() {
		ApplicationContext cxt = new ClassPathXmlApplicationContext("ApplicationContext.xml");
		UserService service = (UserService)cxt.getBean("userService");
		User user = new User();
		user.setUserName("lili");
		user.setUserId(123456);
		try {
			service.addUser(user);
		} catch (Exception e) {
			
		}
	}
}
```

### 【如何定义AOP切入点】
> 切入点，简单的说就是连接点的查询条件，设置一个表达式，符合表达式的方法可以被织入增强处理。例如：<aop:pointcut expression="execution(* service..*.*(..))" id="pointCut"/>

表达式 | 说明
---|---
public * addUser(entity.User) | "*" 表示匹配所有类型的返回值
public void *(entity.User) | "*"表示匹配所有方法名
public void addUser(..) | ".."表示匹配所有参数个数和类型
* com.service.*.*(..) | 匹配com.service包下所有有类的所有方法
* com.service..*.*(..) | 匹配com.service包及其子包下所有类的所有方法











