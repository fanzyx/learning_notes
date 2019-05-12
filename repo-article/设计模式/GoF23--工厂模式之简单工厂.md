
# 特性介绍

- 将对象实例化的过程放在工厂类中，实现数创建者和调用者的分离。

- 可以用来生产同一等级结构中的任意产品（对于增加新的产品，需要修改已有代码）。

- 简单工厂模式没有遵循开闭原则，但也使用较多。
 
# 演示说明

> 以汽车工厂为例

### 调用关系图

![简单工厂模式调用关系](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E7%AE%80%E5%8D%95%E5%B7%A5%E5%8E%82%E6%A8%A1%E5%BC%8F%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码


```java
/**
 * 汽车类接口
 */
public interface Car {
    /**
     * 汽车运行方法
     */
    void run();
}

/**
 * 奥迪
 */
public class Audi implements Car {
    @Override
    public void run() {
        System.out.println("奥迪车运行奔跑");
    }
}
/**
 * 比亚迪
 */
public class Byd implements Car {
    @Override
    public void run() {
        System.out.println("比亚迪运行奔跑");
    }
}
```


```java
/**
 * 汽车制造工厂（创建者）
 */
public class CarFactory {
    //方式一
    public static Car createCar(String type){
        Car car = null;
        if("Audi".equals(type)){
            car = new Audi();
        }else if("Byd".equals(type)){
            car =  new Byd();
        }
        return car;
    }

    //方式二
    public static Car createAudi(){
        return new Audi();
    }
    public static Car createByd() {
        return new Byd();
    }
}
```


```java
/**
 * 演示客户端（调用者）
 */
public class Client {
    public static void main(String[] args){
        Car audi1 = CarFactory.createCar("Audi");
        Car audi2 = CarFactory.createAudi();
        Car byd1 = CarFactory.createCar("Byd");
        Car byd2 = CarFactory.createByd();
        audi1.run();
        byd1.run();
        audi2.run();
        byd2.run();
    }
}

```


