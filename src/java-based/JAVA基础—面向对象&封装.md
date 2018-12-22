> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 面向对象——封装

> <p>什么是面向对象（Object Oriented,OO）？</p>
> <p style="color:orange">面向对象是一种将简单的、分散的事物逐渐抽象和归类的<strong style="font-size:18px">思想</strong></p>
***
> <p>什么是类？什么是对象？</p>
> <p style="color:blue">类是对象的抽象（集合），对象是类的实体（个例）</p>
***
在学习面向对象之前，需要先了解一下java中的访问修饰符，它们控制着元素的访问权限。 
<p>√表示在当前范围内可以访问</p>

修饰符\范围 | 同类|同包|子类|所有|备注
---|---|---|---|---|---
private | √||||私有
friendly| √|√|||友好
protected|√|√|√||保护
public|√|√|√|√|公开


## 封装 
> <p>什么是封装？</p>
> <p style="color:blue">高内聚，低耦合；将复杂的内部结构隐藏，只留出部分接口供外部调用。</p>
> <p > 例如动物吃东西，外部只要调用吃方法喂食物就可以了，不用管它怎么吃，怎么消化。 </p>
***
> <p>什么是构造方法？</p>
> <p style="color:blue">构造方法名与类名相同，没有返回值；在声明类时，系统会默认提供一个无参构造方法；若自行声明构造方法，则默认构造方法将被覆盖，所以在声明JavaBean时，手动声明一个无参构造方法，方便以后扩展。</p>
***
> <p>什么是JavaBean？就是自己定义的一种类。</p>
JavaBean | 作用 
---|---
数据Bean | 通过实体类传递数据
业务Bean | 代码复用
***

```java
/**
 * 动物类
 * @author 爱转圈
 *
 */
public class Animal {
	//类默认的构造方法，通过构造方法来实例化对象
	public Animal() {
		//super和this，在此处不做详细解释
		//super指代父类对象
		//this指代当前被实例化的对象
		super();
	}
	//通过private关键字限制外部访问
	private String name;//动物的名字
	private int age;//动物的年龄
	
	//通过public修饰get/set方法用来给外部调用
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		//提供的公共方法中可以对成员变量进行控制
		//而不是让外部直接调用成员变量，防止出现不可预测的问题
		if(age<0){
			this.age = 0;
		}
		this.age = age;
	}
	
	//动物的吃方法
	public void eat(String food){
		//输出当前动物的名字和吃了什么东西
		System.out.println(name+",吃了"+food);
	}
	//动物的睡方法
	public void sleep(){
		//输出当前动物睡着了
		System.out.println(name+",睡着了···");
	}
}
```