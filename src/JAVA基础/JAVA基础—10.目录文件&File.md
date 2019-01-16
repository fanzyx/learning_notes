> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 目录文件

## File类
> <p>什么是File类</p>
> <p style="color:blue">File类可以对目录和文件进行创建、删除与重命名。</p>
> <p style="color:blue">File类不能访问文件内容，访问内容需要进行I/O流处理。</p>

***

File类可以根据路径创建File实例，路径可以是绝对路径，也可以是相对路径。<br>默认情况下，相对路径系统会解释为JAVA虚拟机所在的路径。

> <p>File常用方法</p>

- 1.文件名相关方法
    - String getName():返回对象文件名或路径名最后一级。
    - String getPath():返回对象路径名。
    - File getAbsoluteFile():返回对象绝对路径。
    - String getAbsolutePath():返回对象绝对路径名。
    - String getParent():返回对象对应目录的父目录名。
    - boolean renameTo(File newName):重命名文件或目录，成功返回true。

- 2.文件检测相关方法
    - boolean exists():判断文件或目录是否存在。
    - boolean canWrite():判断文件或目录是否可写。
    - boolean canRead():判断文件是否可读。
    - boolean isFile():判断是否是文件。
    - boolean isDirectory():判断是否是目录。

- 3.文件常规信息
    - long lastModified():获取文件最后的修改时间。
    - long length():获取文件内容的长度。

- 4.文件操作相关方法
    - boolean createNewFile():当此对象所对应的文件不存在时，该方法创建一个新文件。
    - boolean delete():删除所对应的文件或路径。
    - void deleteOnExit():注册一个删除钩子，当JVM退出时，删除所对应的文件或目录。

- 5.目录操作方法
    - boolean mkdir():创建一个指定目录（使用该方法时，File必须对应一个路径而不能是一个文件）。
    - String[] list():获取File对象的所有子文件名和路径名。
    - File[] listFiles():获取File对象的所有子文件和路径。
    - static File[] listRoots():获取系统所有根路径。






