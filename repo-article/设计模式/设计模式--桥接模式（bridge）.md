
# 特性介绍

> 当某个事物有多个可变维度的时候可以使用桥接模式。

> 本身只有一个变化的维度，其他变化的维度由外部提供。

# 示例场景

以卖电脑为例。

1. **首先，我们看一下电脑的类型和品牌示意图**

![电脑类型品牌示意图](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/%E7%94%B5%E8%84%91%E5%93%81%E7%89%8C%E5%92%8C%E7%B1%BB%E5%9E%8B.png?raw=true)

2. **不使用桥接模式的情况下，我们对其代码构建是这个样子↓**

![类的层次结构图](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/%E9%94%80%E5%94%AE%E7%94%B5%E8%84%91%E7%B1%BB%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84.png?raw=true)

3. **这时，如果我们想添加新的品牌电脑或者新增新的电脑类型该怎么办？**

- 只能按照新增的品牌和类型再次新建几个类来进行扩展，比较繁琐。
- 使用《桥接模式》可以得到好一些效果。

4. **《桥接模式》怎么处理这种情况呢？**

将多个可变的维度抽离出来，只保留一个变化的维度。

5. **抽离出品牌这个维度：**

  以联想和戴尔两个品牌为例

![电脑品牌维度](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/%E7%94%B5%E8%84%91%E5%93%81%E7%89%8C%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F.png?raw=true)

示例代码
```java
public class Brand {
    public void sale(){
        System.out.print("销售品牌：");
    }
}

class Lenovo extends Brand{
    @Override
    public void sale() {
        super.sale();
        System.out.println("联想");
    }
}
class Dell extends Brand{
    @Override
    public void sale() {
        super.sale();
        System.out.println("戴尔");
    }
}
```

6. **定义电脑类型**

电脑类型：台式机（Desktop）、笔记本（Laptop）和平板(Pad)。类型随着电脑本身变化，不做抽离。

![电脑类型维度](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/%E7%94%B5%E8%84%91%E7%B1%BB%E5%9E%8B%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F.png?raw=true)

示例代码

```java
public class ComputerBridge {
    protected Brand brand;

    public ComputerBridge(Brand brand) {
        this.brand = brand;
    }
    public void sale(){
        //调用品牌，输出品牌
        brand.sale();
    }
}
class DesktopBridge extends ComputerBridge{
    public DesktopBridge(Brand brand) {
        super(brand);
    }
    @Override
    public void sale() {
        super.sale();
        System.out.println("销售台式机");
    }
}
class LaptopBridge extends ComputerBridge{
    public LaptopBridge(Brand brand) {
        super(brand);
    }
    @Override
    public void sale() {
        super.sale();
        System.out.println("销售笔记本");
    }
}
class PadBridge extends ComputerBridge{
    public PadBridge(Brand brand) {
        super(brand);
    }
    @Override
    public void sale() {
        super.sale();
        System.out.println("销售平板");
    }
}
```

7. **最后的使用**

```java
public class Client {
    public static void main(String[] args){
        //可以灵活的将品牌传入到不同的电脑类型中进行输出
        ComputerBridge cb1 = new DesktopBridge(new Lenovo());
        cb1.sale();
        ComputerBridge cb2 = new LaptopBridge(new Dell());
        cb2.sale();
    }
}

输出结果：

> 销售品牌：联想
> 销售台式机

> 销售品牌：戴尔
> 销售笔记本
```

# 模式总结

如果一个事物有都多个变化的维度属性，保留最贴近自身特性的维度，将其他变化的维度抽离出来，在使用的时候进行传入，易于扩展。



