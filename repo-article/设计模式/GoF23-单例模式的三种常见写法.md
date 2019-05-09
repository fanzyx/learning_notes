

# 简介
> 保证一个类只有一个实例（构造器私有化），并且提供一个访问该实例的全局访问点（静态公有方法返回实例对象）。
> 单例模式只生成一个实例，减少了系统的性能开销，提高效率。

# 三种常见写法

## 饿汉式

> 在类加载的时候，就完成初始化，线程安全，不具备延迟加载特性。

```java
public class SingletonHungry {
    //类加载时就已经初始化，虚拟机只装载一次此对象
    private static SingletonHungry instance = new SingletonHungry();
    //私有化构造器
    private SingletonHungry(){}
    public static SingletonHungry getInstance(){
        return instance;
    }
}
```

## 懒汉式

> 在类加载时不创建实例，采用延迟加载的方式，在运行调用时创建实例，线程不安全，调用效率低。

```java
public class SingletonLazy {
    private static SingletonLazy instance = null;
    //私有构造器
    private SingletonLazy(){}
    //加同步块synchronized，提高线程安全性
    public static synchronized SingletonLazy getInstance(){
        if(null == instance){
            instance = new SingletonLazy();
        }
        return instance;
    }
}
```

## 静态内部类式

> 实现了懒加载，保证了线程安全；兼备了并发高效调用和延迟加载的优势。

```java
public class SingletonClass {
    //静态内部类
    private static class SingletonStatic{
        private static final SingletonClass instance = new SingletonClass();
    }
    //私有构造器
    private SingletonClass(){}
    public static SingletonClass getInstance(){
        return SingletonStatic.instance;
    }
}
```

# 三种写法特点比较

单例模式 | 懒汉模式 | 饿汉模式 | 静态内部类式
---|---|---|---
延迟加载| 具备 | 不具备 | 具备
线程安全| 线程不安全 | 线程安全 |线程安全

如果单例类耗费系统资源较多，建议使用懒汉式和静态内部类式；如果对线程安全性要求高，建议使用饿汉式和静态内部类式。


