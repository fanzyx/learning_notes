> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 抽象类&接口

## 抽象类
> <p>什么是抽象类</p>
> <p style="color:blue">抽象类使用abstract修饰，不能被实例化，只能用来继承；其内方法可以既声明又实现，也可以只声明不实现。</p>

***

> <p>抽象类的意义</p>
> <p style="color:blue">将方法的设计和实现分离。</p>

***

> <p>什么是抽象方法</p>
> <p style="color:blue">抽象方法使用abstract修饰，只声明不实现。抽象方法必须被继承的子类实现。例如 public abstract void run();</p>

```java
/**
 * 抽象类
 * @author 爱转圈
 */
public abstract class Test1 {
	//声明抽象方法
	public abstract void eat();
	//声明非抽象方法
	public void sleep(){
		System.out.println("sleep");
	}
}

/**
 * 继承抽象类
 * @author 爱转圈
 */
public class Children extends Test1 {
	//实现了抽象类中的eat方法
	@Override
	public void eat() {
		System.out.println("eat");
	}
}

```


## 接口
> <p>接口——JAVA实现多继承的方式</p>
> <p style="color:blue">接口是一组规范，定义了规则，表示一种能力，子类实现时相当于获取这种能力</p>
- 声明接口（Interface）
- 子类实现接口(implements)

***

> <p>接口的特性</p>
> <p style="color:blue">只有常量和抽象方法</p>
> <p style="color:blue">不能被实例化</p>
> <p style="color:blue">实现了接口的类，必须实现该接口的所有方法</p>
> <p style="color:blue">只有常量和抽象方法</p>

```java
/**
 * 测试接口
 * @author 爱转圈
 */
public interface Test2 {
	//声明公开抽象方法
	//默认使用public abstract修饰
	void run();
}


/**
 * 继承抽象类和实现接口的类
 * @author 爱转圈
 */
public class Children extends Test1 implements Test2{
	//实现了抽象类中的eat方法
	@Override
	public void eat() {
		System.out.println("eat");
	}
	
	//实现了接口中的run方法
	@Override
	public void run() {
		System.out.println("run");
	}
}
```
