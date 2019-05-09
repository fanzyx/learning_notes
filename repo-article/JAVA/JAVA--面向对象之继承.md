
> <p>什么是继承？</p>
> <p style="color:blue">一个对象可以使用另一个对象非私有的属性和方法，Java中所有的类都默认直接或间接的继承了Object类。（子类继承父类）</p>
***

> <p>继承的作用</p>
> <p style="color:blue">1. 描述类之间的关系</p>
> <p style="color:blue">2. 实现代码复用</p>
> <p style="color:blue">3. 实现多态的基础</p>
***
> <p>继承的实现</p>

```java
abstract 关键字
 包含了抽象方法的类一定是抽象类。
 只定义方法，无具体实现代码。例如 public abstract void run();
 抽象方法必须被子类实现。
 抽象类不能实例化。
 抽象类只能用来继承。
 抽象方法的意义：将方法的设计和实现分离。
```
- **声明父类**：父类一般由abstract修饰，无法实例化；
- 子类通过extends关键字继承父类
- **声明子类**：子类中声明独有的属性和方法即可，或者重写父类的abstract方法
***
> <p>JAVA中继承的特点</p>

- **单根性**：JAVA中只能单继承
- **传递性**：子类具有父类及父类所继承的特性
- **注意事项**：
    - 1.私有属性不能继承；
    - 2.构造方法不能继承；
    - 3.不在同包中由默认访问修饰符修饰的属性和方法不能继承；
    - 4.继承关系中的初始化：先调用父类的构造方法，再调用子类的构造方法。 
***

> <p>方法的重载（overload）</p>
> <p style="color:blue">在同一个类中，方法名相同，但参数的类型、个数、顺序不同。</p>

- 返回值不同、参数名称不同均不构成重载。
***

> <p>方法的重写（override）</p>
> <p style="color:blue">子类继承父类时，在子类中重写父类的方法，方法名相同，参数列表相同。</p>
- 子类权限修饰符可以>=父类的权限修饰符。
- 子类的返回值类型<=父类的返回值类型；子类声明异常类型<=父类异常类型。
***

```java
/**
 * 狗狗类，继承了动物类
 * @author 爱转圈
 *
 */
public class Dog extends Animal {
	//重写父类Animal中的eat方法
	@Override
	public void eat(String food) {
		//继承了父类的属性name
		this.setName("狗狗1");
		//可以通过get/set方法来访问父类的属性
		System.out.println(this.getName()+"吃了"+food);
	}
	
	//重载eat方法，参数个数不同了
	public void eat(String food1,String food2) {
		this.setName("狗狗2");
		System.out.println(this.getName()+"吃了"+food1+"后，又吃了"+food2);
	}
}
```