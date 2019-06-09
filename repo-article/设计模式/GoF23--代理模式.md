
# 特性介绍

- 通过代理，可以详细控制访问某个或某类对象的方法，在调用前和调用后进行处理。
- 抽象角色：定义代理角色和真实角色的公共对外方法
    - 真实角色：实现抽象角色，定义真实角色的业务逻辑供代理角色调用，**关注真正的业务逻辑。**
    - 代理角色：实现抽象角色，通过真实角色的业务逻辑方法来实现抽象方法，并附加自己的操作，**将统一的流程控制放在代理角色中。**
- 代理的分类
    - 静态代理
    - 动态代理
- AOP（面向切面编程）的核心机制之一。

# 场景描述

一个客户想请一个明星唱歌演出，首先会联系明星的经纪人（代理人）进行各项程序的处理，比如签订合同、订票放票、款项处理等等。

# 静态代理

### 调用关系图

![静态代理调用关系图](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E9%9D%99%E6%80%81%E4%BB%A3%E7%90%86%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码

1. 新建一个Star接口，定义各种方法。
```java
/**
 * 明星接口
 * @author wangyds
 * @date  2019/6/9 20:25
 */
public interface Star {
    /**
     * 面谈
     */
    void confer();
    /**
     * 签订合同
     */
    void signContract();

    /**
     * 订票
     */
    void bookTicket();

    /**
     * 唱歌
     */
    void sing();

    /**
     * 收尾款
     */
    void collectMoney();
}
```
2. 新建真实Star，实现接口的各种方法。
```java
/**
 * 真实的明星
 *
 * @author wangyds
 * @date 2019/6/9 20:37
 */
public class RealStar implements Star {
    @Override
    public void confer() {
        System.out.println("real面谈");
    }

    @Override
    public void signContract() {
        System.out.println("real签订合同");
    }

    @Override
    public void bookTicket() {
        System.out.println("real订票");
    }

    @Override
    public void sing() {
        System.out.println("real唱歌");
    }

    @Override
    public void collectMoney() {
        System.out.println("real收钱");
    }
}
```

3. 新建代理Star,可以调用真实Star，唱歌方法为真实Star实现，其他方法由代理人实现。
```java
/**
 * 代理人
 * @author wangyds
 * @date 2019/6/9 20:40
 */
public class ProxyStar implements Star {

    private Star star;

    public ProxyStar(Star star) {
        this.star = star;
    }

    @Override
    public void confer() {
        System.out.println("proxy面谈");
    }

    @Override
    public void signContract() {
        System.out.println("proxy签订合同");
    }

    @Override
    public void bookTicket() {
        System.out.println("proxy订票");
    }

    @Override
    public void sing() {
        star.sing();
    }

    @Override
    public void collectMoney() {
        System.out.println("proxy收钱");
    }
}
```

4. 调用者/客户，真实Star将作为参数传入到代理Star中。
```java
/**
 * 客户端/调用者
 * @author wangyds
 * @date 2019/6/9 20:10
 */
public class Client {

    public static void main(String[] args){
        RealStar real = new RealStar();
        ProxyStar proxyStar = new ProxyStar(real);
        proxyStar.confer();
        proxyStar.signContract();
        proxyStar.bookTicket();
        proxyStar.sing();
        proxyStar.collectMoney();
    }
}
```

5. 输出结果

![静态代理输出](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F/%E9%9D%99%E6%80%81%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E8%BE%93%E5%87%BA%E7%BB%93%E6%9E%9C.png?raw=true)
 
# 动态代理

### 实现方式

通过JDK自带的动态代理来实现。
- java.lang.reflect.Proxy
    - 动态生成代理类和对象
- java.lang.reflect.InvocationHandler
    - 可以通过invoke方法实现对真实角色的代理访问。
    - 每次通过Proxy生成代理类对象时，都要指定对应的处理器对象。


### 调用关系图

![动态代理调用关系图](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E8%B0%83%E7%94%A8%E5%85%B3%E7%B3%BB%E5%9B%BE.png?raw=true)

### 示例代码

1. 新建一个Star接口，定义各种方法。
```java
/**
 * 明星接口
 * @author wangyds
 * @date  2019/6/9 20:25
 */
public interface Star {
    /**
     * 面谈
     */
    void confer();
    /**
     * 签订合同
     */
    void signContract();

    /**
     * 订票
     */
    void bookTicket();

    /**
     * 唱歌
     */
    void sing();

    /**
     * 收尾款
     */
    void collectMoney();
}
```
2. 新建真实Star，实现接口的各种方法。
```java
/**
 * 真实的明星
 *
 * @author wangyds
 * @date 2019/6/9 20:37
 */
public class RealStar implements Star {
    @Override
    public void confer() {
        System.out.println("real面谈");
    }

    @Override
    public void signContract() {
        System.out.println("real签订合同");
    }

    @Override
    public void bookTicket() {
        System.out.println("real订票");
    }

    @Override
    public void sing() {
        System.out.println("real唱歌");
    }

    @Override
    public void collectMoney() {
        System.out.println("real收钱");
    }
}
```

3. 新增Star的处理类StarHandler对真实Star进行处理。
```java
/**
 * Star的处理类
 * @author wangyds
 * @date 2019/6/9 21:32
 */
public class StarHandler implements InvocationHandler {

    private Star realStar;

    public StarHandler(Star realStar) {
        this.realStar = realStar;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args)
            throws Throwable {
        //调用代理类任何方法的时候，都会进入到此方法中。
        //所以可以对方法进行统一处理或者对某个方法进行单独的判断处理。
        Object object = null;
        String sing = "sing";
        System.out.println("真正的方法执行前，面谈、签合同、订票");
        if(sing.equals(method.getName())){
            object =  method.invoke(realStar,args);
        }
        System.out.println("真正的方法执行后，收尾款");
        return object;
    }
}

```

4. 客户端/调用者
```java
/**
 * 客户端/调用者
 * @author wangyds
 * @date 2019/6/9 21:23
 */
public class Client {

    public static void main(String[] args){
        Star realStar = new RealStar();
        StarHandler starHandler = new StarHandler(realStar);
        //通过接口和处理类，生成代理类
        Star proxy = (Star)Proxy.newProxyInstance(ClassLoader.getSystemClassLoader(),new Class[]{Star.class},starHandler);
        proxy.sing();
    }
}
```

5. 输出结果

![动态代理输出](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F/%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E8%BE%93%E5%87%BA%E7%BB%93%E6%9E%9C.png?raw=true)
