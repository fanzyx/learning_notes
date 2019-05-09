
## Exception
> <p>什么是异常</p>
> <p style="color:blue">异常机制可以使异常处理代码与正常业务代码分离开来，提高程序的容错性和稳定性。</p>

***

> <p>异常机制常用的关键字</p>

try 、catch  、finally  、throw  、throws

- try:try{}块中放入可能出现异常的代码
- catch:catch(){}块中捕获可能出现的异常
- finally:finally{}块可有可无，无论是否出现异常都会执行块内代码
- throw:用于抛出异常
- throws:用于在方法入口声明可能出现的异常类型

```java
public class LearnException {
	public static void main(String[] args) {
		try {
			//try块内放入可能会出现异常的代码
			learn();
			//出现异常代码之后的代码不会执行
			System.out.println("出现了异常后的代码");
		} catch (Exception e) {
			//catch块会捕获异常并进行处理
			e.printStackTrace();
		} finally {
		    //finally块常用来回收资源
		    //如数据库链接、IO流和网络链接等
			System.out.println("运行到了finally");
		}
	}
	
	//使用throws声明异常，throw抛出异常
	public static void learn() throws Exception {
		//抛出一个异常
		throw new Exception("方法内出现了异常了");
		
	}
	
	/*运行结果：
	 * 
	 * java.lang.Exception: 方法内出现了异常了
	   at 异常.LearnException.learn(LearnException.java:22)
	   at 异常.LearnException.main(LearnException.java:7)
	        运行到了finally*/
}
```

***

> <p>异常类继承关系</p>
![异常关系](https://github.com/wyd288/learning_notes/blob/master/repo-image/JAVA/%E5%BC%82%E5%B8%B8%E5%85%B3%E7%B3%BB.png)
- Error:错误，这种错误无法恢复或不可能捕获，一旦发生，程序将终止运行。
- Exception:异常，可以进行捕获，发生时程序不会终止运行。

***

在捕获异常是，一定要先捕获范围小的异常，再捕获范围大的异常。

> <p>访问异常信息的常用方法</p>

- String getMessage():获取异常的详细描述字符串。
- void printStackTrace():将异常跟踪栈信息输出到标准错误输出。
- StackTraceElement[] getStackTrace():获取异常的跟踪栈信息。

***

> <p>自定义异常</p>

继承Exception类并提供构造方法
```java
public class CreateException extends Exception {
	//无参构造方法
	public CreateException() {
		
	}
	//带参构造方法
	public CreateException(String msg) {
		System.out.println("我是一个自定义异常");
	}
}
```

***



