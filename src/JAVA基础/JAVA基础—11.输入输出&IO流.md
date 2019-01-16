> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 输入输出

## I/O流
> <p>什么是I/O流</p>
> <p style="color:blue">JAVA中的I/O流是实现输入/输出的基础，其可以实现数据的输入/输出操作。</p>

***

> <p>流的分类</p>

1. 输入流和输出流（以内存角度划分）
    - 输入流：只能读取数据，而不能写出数据。
    - 输出流：只能写出数据，而不能读取数据。

2. 字节流和字符流
    - 字节流：操作的数据单元是8位的字节。
    - 字符流：操作的数据单元是16位的字符。

3. 节点流和处理流
    - 节点流：直接与数据源相连，对设备进行读/写数据。
    - 处理流：对一个已经存在的流进行连接或封装，封装后再实现数据读/写，操作简单，执行效率高（常用）。

***

因为计算机所存储的数据都是二进制文件，所以字节流的功能更强大一些。但根据实际情况考虑，在输入/输出是**文本内容**时，优先考虑使用**字符流**。

***

> <p>I/O流常用方法</p>

- InputStream相关方法
    - int read():从输入流中读取单个字节。
    - int read(byte[] b):从输入流中最多读取b.length个字节并存储在数组b中。
    - int read(byte[] b,int off,int len):从输入流中最多读取len个字节并存储在数组b中，存储位置数组的off开始。
- Reader相关方法    
    - int read():从输入流中读取单个字符。
    - int read(char[] c):从输入流中最多读取c.length个字符并存储在数组b中。
    - int read(char[] c,int off,int len):从输入流中最多读取len个字符并存储在数组b中，存储位置从数组的off开始。

- OutputStream相关方法
    - void write(int c):输出指定字节/字符到输出流中。
    - void write(byte[]/char[] buf,int off,int len):输出字节/字符数组中从off位置开始，长度为len的数据。
- Writer相关方法
    - void write(String str):将字符串输出到输出流中。
    - void write(String str,int off,int len):将字符串str从off位置开始输出len长度的字符串到输出流中。


- 使用流时需要注意清空缓冲区和关闭问题，使用以下方法。
    - flush():强制清空缓冲区数据
    - close():关闭流

***


> <p>对象序列化</p>
> <p style="color:blue">对象序列化的目标是将对象保存到磁盘中或在网络中直接传输对象。</p>
> <p style="color:blue">对象序列化是将JAVA对象转换成平台无关的二进制流。</p>

***

> <p>实现序列化</p>
使类实现Serializable接口，不用实现任何方法。

***

```java
public class LearnIO implements Serializable {
	//实现序列化，只需要类实现Serializable接口
	
	//此类中的所有成员变量都必须是可序列化的，否则会抛出异常
	
	//JAVA中的常用类型基本上都实现了Serializable接口
	
	//需要关注的是自定义的类
}
```
