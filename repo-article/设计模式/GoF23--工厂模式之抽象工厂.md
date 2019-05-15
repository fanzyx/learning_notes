
# 特性介绍

- 将对象实例化的过程放在工厂类中，实现创建者和调用者的分离。
- 用来生产不同产品族的全部产品（支持增加产品族，不支持增加新的产品）。
- 抽象工厂模式是工厂方法模式的升级版，在有多个业务分类时，通过抽象工厂模式产生需要的实例对象是比较好的解决方式。
 
# 示例说明

### 场景描述

以汽车生产为例，将汽车组件模拟拆分为发动机、轮胎和座椅三个部分，这三个部分组成一个产品族（即汽车为产品族），发动机、轮胎和座椅可以根据不同维度又可以分成很多种类，比如高级发动机、中级发动机、低级发动机等。

### 调用关系图

![抽象工厂模式调用关系](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E6%8A%BD%E8%B1%A1%E5%B7%A5%E5%8E%82%E6%A8%A1%E5%BC%8F%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码


```java
//发动机接口
public interface Engine {
    void run();
    void start();
}

//高端发动机
public class HighEngine implements Engine {
    @Override
    public void run() {
        System.out.println("转速快");
    }

    @Override
    public void start() {
        System.out.println("启动快");
    }
}

//低端发动机
public class LowEngine implements Engine {
    @Override
    public void run() {
        System.out.println("转速慢");
    }

    @Override
    public void start() {
        System.out.println("启动慢");
    }
}

//座椅接口
public interface Seat {
    void comfort();
}

//高端座椅
public class HighSeat implements Seat{
    @Override
    public void comfort() {
        System.out.println("舒适度好");
    }
}

//低端座椅
public class LowSeat implements Seat {
    @Override
    public void comfort() {
        System.out.println("舒适度差");
    }
}

//轮胎接口
public interface Tyre {
    void wear();
}

//高端轮胎
public class HighTyre implements Tyre {
    @Override
    public void wear() {
        System.out.println("耐磨性好");
    }
}

//低端轮胎
public class LowTyre implements Tyre {
    @Override
    public void wear() {
        System.out.println("耐磨性差");
    }
}

//汽车工厂接口
public interface CarFactory {
    //制造发动机方法
    Engine createEngine();
    //制造座椅方法
    Seat createSeat();
    //制造轮胎方法
    Tyre createTyre();
}

//高端汽车工厂
public class HighCarFactory implements CarFactory {
    @Override
    public Engine createEngine() {
        return new HighEngine();
    }

    @Override
    public Seat createSeat() {
        return new HighSeat();
    }

    @Override
    public Tyre createTyre() {
        return new HighTyre();
    }
}

//低端汽车工厂
public class LowCarFactory implements CarFactory {
    @Override
    public Engine createEngine() {
        return new LowEngine();
    }

    @Override
    public Seat createSeat() {
        return new LowSeat();
    }

    @Override
    public Tyre createTyre() {
        return new LowTyre();
    }
}

//客户端
public class Client {
    public static void main(String[] args){
        //生产高端汽车
        CarFactory hFactory = new HighCarFactory();
        Engine he = hFactory.createEngine();
        Seat hs = hFactory.createSeat();
        Tyre ht = hFactory.createTyre();
        //生产低端汽车
        CarFactory lFactory = new LowCarFactory();
        Engine le = lFactory.createEngine();
        Seat ls = lFactory.createSeat();
        Tyre lt = lFactory.createTyre();

        //也可以根据情况将三个部分高低端混合生产汽车
    }
}

```



