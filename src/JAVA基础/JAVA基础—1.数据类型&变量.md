> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 数据类型&变量

## 一、数据类型
#### 1. **基本类型及其包装类**
> JAVA提供了8种基本数据类型，6种数字类型，1种字符类型，1种布尔类型。
> <br>1字节 = 8位二进制

- **整数**

基本类型|内存占位|包装类型|初始值
---|---|---|---
byte|1个字节|Byte|0
short|2个字节|Short|0
int|4个字节|Integer|0
long|8个字节|Long|0

- **浮点数**

基本类型|内存占位|包装类型|初始值
---|---|---|---
float|4个字节|Float|0.0f
double|8个字节|Double|0.0

- **字符**

基本类型|内存占位|包装类型|初始值
---|---|---|---   
char|2个字节|Character|\u0000

- **布尔**

基本类型|内存占位|包装类型|初始值
---|---|---|---   
boolean|1位，不是1字节|Boolean|false

<br>

#### 2. **引用类型(4字节，地址)**
> 除了基本类型之外的所有类型。引用类型指向一个对象，指向对象的变量是引用变量。

- String
- 数组
- 对象


## 二、变量

#### 1.**静态变量**
> 定义在类里面，方法外面，使用static修饰。
<br>声明后如未手动初始化，系统会默认初始化。

#### 2.**局部变量**
> 定义在方法里面或语句块里面。
<br>声明后，使用前必须要手动初始化。

#### 3.**成员变量**
> 定义在类里面，方法外面。
<br>声明后如未手动初始化，系统会默认初始化。

#### 4.**常量**
> 定义在类里面，方法外面。
常量在程序运行时是不能被修改的。
<br>在 Java 中使用 final 关键字来修饰常量，声明方式和变量类似


## 三、示例
```java
public class Variable {
	//常量，被对象引用，不能改变
	final String CONSTANT_VARIABLE = "constantVariable";
	//静态变量,可以被类和对象引用
	static int a = 1111;
	//成员变量，被对象引用
	String memberVariable = "memberVariable";
	
	public static void main(String[] args) {
		//局部变量，当方法结束时，变量回收。
		byte b1 = 0;
		Byte b2 = 0;
		
		short s1 = 0;
		Short s2 = 0;
		
		int i1 = 0;         
		Integer i2 = 0;
		
		long l1 = 0L;
		Long l2 = 0L;
		
		float f1 = 0.0f;
		Float f2 = 0.0f;
		
		double d1 = 0.0;
		Double d2 = 0.0;
		
		char c1 = 'a';
		Character c2 = 'A';
		
		boolean bl1 = true;
		Boolean bl2 = false;

	}

}
```