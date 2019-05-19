
# 特性介绍

- 适合构建复杂对象。
- 分离了对象子组件的单独构造和装配，实现了构建和装配的解耦。
- 客户端不必知道产品内部组成的细节，将产品本身与产品的创建过程解耦，使得相同的创建过程可以创建不同的产品对象。
 
# 示例说明

### 场景描述

以电脑的生产装配过程为例，假设一个电脑由显卡、主板和机箱组成，电脑的组件建造和装配由不同的接口控制，具体的实现类负责实际操作。

### 调用关系图

![建造者模式调用关系](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E5%BB%BA%E9%80%A0%E8%80%85%E6%A8%A1%E5%BC%8F%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码

1.新建电脑类和电脑的三个组件类
```java
/**
 * 电脑类
 */
public class Computer {

    private GraphicsCrd graphicsCrd;
    private Mainboard mainboard;
    private Crate crate;
    public GraphicsCrd getGraphicsCrd() {
        return graphicsCrd;
    }

    public void setGraphicsCrd(GraphicsCrd graphicsCrd) {
        this.graphicsCrd = graphicsCrd;
    }

    public Mainboard getMainboard() {
        return mainboard;
    }

    public void setMainboard(Mainboard mainboard) {
        this.mainboard = mainboard;
    }

    public Crate getCrate() {
        return crate;
    }

    public void setCrate(Crate crate) {
        this.crate = crate;
    }
}

/**
 * 显卡类
 */
public class GraphicsCrd{
    private String name;
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public GraphicsCrd(String name) {
        this.name = name;
    }
}

/**
 * 主板类
 */
public class Mainboard{
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Mainboard(String name) {
        this.name = name;
    }
}

/**
 * 机箱类
 */
public class Crate{
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Crate(String name) {
        this.name = name;
    }
}

```

2.新建电脑组件建造接口及其实现类

```java
/**
 * 电脑组件建造接口
 */
public interface ComputerBuilder {
    //建造显卡方法
    GraphicsCrd buildGraphicsCrd();
    //建造主板方法
    Mainboard buildMainboard();
    //建造机箱方法
    Crate buildCrate();
}

/**
 * 电脑组件建造实现类
 */
public class FanyiComputerBuilder implements ComputerBuilder {
    @Override
    public GraphicsCrd buildGraphicsCrd() {
        return new GraphicsCrd("泛亦牌显卡");
    }

    @Override
    public Mainboard buildMainboard() {
        return new Mainboard("泛亦牌主板");
    }

    @Override
    public Crate buildCrate() {
        return new Crate("泛亦牌机箱");
    }
}
```

3.新建电脑装配接口及实现类

```java
/**
 * 电脑装配接口
 */
public interface ComputerDirector {
    //电脑装配方法
    Computer directorComputer();
}

/**
 * 电脑装配实现类
 */
public class FanyiComputerDirector implements ComputerDirector{
    private ComputerBuilder builder;

    public FanyiComputerDirector(ComputerBuilder builder) {
        this.builder = builder;
    }

    @Override
    public Computer directorComputer() {
        Computer computer = new Computer();
        computer.setGraphicsCrd(builder.buildGraphicsCrd());
        computer.setMainboard(builder.buildMainboard());
        computer.setCrate(builder.buildCrate());
        return computer;
    }
}
```

4.新建客户端/调用者

```java
/**
 * 客户端/调用者类
 */
public class Client {
    public static void main(String[] args) {
        ComputerDirector fanyiDirector = new FanyiComputerDirector(new FanyiComputerBuilder());
        Computer comp = fanyiDirector.directorComputer();
        System.out.println("显卡：" + comp.getGraphicsCrd().getName() +
                "  主板：" + comp.getMainboard().getName() +
                "  机箱：" + comp.getCrate().getName());
    }
}
```

