
# 特性介绍

> 动态为一个对象增加新功能。

> 是一种用于代替继承的技术，无须通过继承就能扩展对象的新功能，更加灵活。

> 使用装饰器模式的典型例子：++IO流处理++

# 示例场景

以汽车新增功能为例，说明装饰器模式的使用，进而看出装饰器模式与继承的区别。



**下图为模式中接口与各类型之间的关系。**


![类层次结构](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E8%A3%85%E9%A5%B0%E5%99%A8%E6%A8%A1%E5%BC%8F/1.%E8%A3%85%E9%A5%B0%E5%99%A8%E6%A8%A1%E5%BC%8F%E7%B1%BB%E7%BB%93%E6%9E%84%E5%9B%BE.png?raw=true)


**代码实现如下：**

1. 创建抽象组件接口

```java
/**
 * 抽象组件
 * @author andnow
 * @date 2019/8/6
 */
public interface ICar {
    void move();
}
```

2. 创建真实对象

```java
/**
 * 具体构件对象（真实对象）
 * @author andnow
 * @date 2019/8/6
 */
public class Car implements ICar {
    @Override
    public void move() {
        System.out.println("普通行驶");
    }
}
```

3. 创建装饰器对象（持有真实对象）

```java
/**
 * 装饰器对象
 * @author andnow
 * @date 2019/8/6
 */
public class SuperCar implements ICar {
    protected ICar car;

    public SuperCar(ICar car) {
        this.car = car;
    }

    @Override
    public void move() {
        car.move();
    }
}
```

4. 创建具有特定功能的装饰器对象

```java
/**
 * 装饰器对象--飞行汽车
 * @author andnow
 * @date 2019/8/6
 */
public class FlyCar extends SuperCar {

    public FlyCar(ICar car) {
        super(car);
    }

    @Override
    public void move() {
        super.move();
        fly();
    }

    public void fly(){
        System.out.println("飞行");
    }

}

/**
 * 装饰器对象--自动驾驶汽车
 * @author andnow
 * @date 2019/8/6
 */
public class AICar extends SuperCar {

    public AICar(ICar car) {
        super(car);
    }

    @Override
    public void move() {
        super.move();
        autoMove();
    }

    public void autoMove(){
        System.out.println("自动驾驶");
    }

}

```

**调用演示及结果：**

```java
/**
 * 客户端/调用者
 * @author andnow
 * @date 2019/8/6
 */
public class Client {
    public static void main(String[] args) {
        //真实对象--汽车
        Car car = new Car();
        car.move();
        System.out.println("----------------");
        //装饰器对象--飞行汽车
        //装饰汽车
        FlyCar flyCar = new FlyCar(car);
        flyCar.move();
        System.out.println("----------------");
        //装饰器对象--自动驾驶汽车
        //装饰飞行汽车
        AICar aiCar = new AICar(flyCar);
        aiCar.move();
    }
}

//输出结果如下：

普通行驶
----------------
普通行驶
飞行
----------------
普通行驶
飞行
自动驾驶
```

# 模式总结

装饰器模式可以对真实对象实现新功能（产生包装对象），这些包装对象可以任意组合来达到具有特定功能的效果。
