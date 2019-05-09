
## 多态
> <p>多态的意义</p>
- 父类对象子类创建(父类类型指向子类对象)
- 同一行为，不同对象表现不一样（类似方法重写）

***

> <p>多态的实现方式</p>
- 父类类型作为方法形参，实际传入子类对象；
- 父类类型作为方法返回值，实际返回子类对象；

```java
public class Test{
	public static void main(String[] args){
		//声明了一个Animal类型的dog
		Animal dog = new Dog();
		//声明了一个Animal类型的cat
		Animal cat = new Cat();
		
		//实参传入子类对象
		test1(dog).eat("大骨头");
		test1(cat).eat("咸鱼");
		
		/*输出结果：
		狗狗1吃了大骨头
		猫猫吃了咸鱼*/
	}
	//父类类型作为形参和返回值
	public static Animal test1(Animal animal){
		return animal;
	}	
}
```
***

```java
/**
 * 多态
 * @author 爱转圈
 *
 */
public class Test{
	public static void main(String[] args){
		//声明了一个Animal类型的dog
		Animal dog1 = new Dog();
		//声明了一个Animal类型的cat
		Animal cat = new Cat();
		//多态实现Animal中的eat方法，不同对象实现不同
		dog1.eat("骨头");
		cat.eat("鱼");
		//子类中独有的方法需要将类型强制转换后才能使用
		Dog dog2 = (Dog)dog1;
		dog2.eat("肉","骨头");
		
		/*输出结果：
		狗狗1吃了骨头
		猫猫吃了鱼
		狗狗2吃了肉后，又吃了骨头*/
	}
}

/**
 * 狗狗类，继承了动物类
 * @author 爱转圈
 *
 */
class Dog extends Animal {
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
/**
 * 猫猫类，继承了动物类
 * @author 爱转圈
 *
 */
class Cat extends Animal{
	//重写父类Animal中的eat方法
	@Override
	public void eat(String food) {
		//继承了父类的属性name
		this.setName("猫猫");
		//可以通过get/set方法来访问父类的属性
		System.out.println(this.getName()+"吃了"+food);
	}
}
```
