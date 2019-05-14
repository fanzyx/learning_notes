
# 特性介绍

- 将对象实例化的过程放在工厂类中，实现创建者和调用者的分离。
- 符合开闭原则，扩展新的类只需要创建新的工厂并实现工厂接口，不需要修改已有的代码。
- 缺点是产生的文件量较多，在大型项目中可以考虑使用。
 
# 示例说明

### 场景描述

模拟奥迪车和比亚迪车的生产销售过程。

### 调用关系图

![工厂方法模式调用关系](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95%E6%A8%A1%E5%BC%8F%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码

（为了方便展示，未使用标准注释）

```java

//汽车接口，定义汽车的功能
public interface Car {
    /**
     * 汽车运行方法
     */
    void run();
}

//奥迪车
public class Audi implements Car {
    @Override
    public void run() {
        System.out.println("奥迪车运行奔跑");
    }
}

//比亚迪车
public class Byd implements Car {
    @Override
    public void run() {
        System.out.println("比亚迪运行奔跑");
    }
}

//汽车工厂接口
public interface CarFactory {
    Car createCar();
}

//奥迪车工厂，只生产奥迪车
public class AudiFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new Audi();
    }
}

//比亚迪车工厂，只生产比亚迪车
public class BydFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new Byd();
    }
}

//调用者（模拟客户）
public class Client {
    public static void main(String[] args){
        Car audi = new AudiFactory().createCar();
        Car byd = new BydFactory().createCar();
        audi.run();
        byd.run();
    }
}

```



