> ### *爱转圈笔记*
> 勤思、体悟、总结、分享

# 常用类

## String
> <p style="color:blue">String对象是char对象的有序集合，用于表示字符串。</p>
> <p style="color:blue">String对象声明之后就是字符串常量（不可变），每次对其操作实质上都是返回了一个新的String对象。</p>
> <p style="color:orange">声明常量字符串时推荐使用</p>

***

> <p>String类的常用方法</p>

```java
public class LearnString {
	
	public static void main(String[] args){
		//声明String对象的方式
		String str = new String("learnString");
		String str1 = "LEARNString";
		
		/*String类常用方法*/
		
		//获取字符串长度
		int strlength = str.length();
		/*strlength=11*/
		
		//查找字符串中的字符
		//索引从0开始
		char c = str.charAt(1);
		/*c='e'*/
		int index = str.indexOf("e");
		/*index=1*/
		
		//字符串连接
		String strConcat = str.concat(" ,wild");
		/*strConcat=learnString ,wild*/
		
		//判断原字符串是否包含新字符串，包含返回true
		boolean isContains = str.contains("learn");
		/*isContains=true*/
		
		//字符串截取,位置从0开始
		String strSub1 = str.substring(1);
		/*strSub1=earnString*/
		String strSub2 = str.substring(1, 3);
		/*strSub2=ea*/
		
		//字符串比较
		boolean isEquals = str.equals(str1);
		/*isEquals=false*/
		boolean isEqualsIgnoreCase = str.equalsIgnoreCase(str1);
		/*isEqualsIgnoreCase=true,此方法忽略大小写*/
		
		//字符串大小写转换
		String strLower = str.toLowerCase();//全小写
		String strUpper = str.toUpperCase();//全大写
		
		//去除字符串首尾空格
		String strTrim = str.trim();
		
		//字符串替换
		String strReplace = str.replace("learn", "hello");
		/*strReplace=helloString*/
		String strReplaceAll = str.replaceAll("\\w", ",z");
		/*strReplaceAll=zzzzzzzzzzz,第一个参数支持正则表达式*/
		
		//字符串分割
		String[] strSplitArray = strReplaceAll.split(",");
		/*strSplitArray=[z,z,z,z,z,z,z,z,z,z,z]*/	
	}
	
}
```

## StringBuilder/StringBuffer
> <p style="color:blue">声明的StringBuilder/StringBuffer对象是可变的字符串变量。</p>
> <p style="color:orange">StringBuilder是线程不安全的，对字符串频繁操作并且不是多线程访问时推荐使用。</p>
> <p style="color:orange">StringBuffer是线程安全的，对字符串频繁操作并且多线程访问时推荐使用。</p>

***

> <p>StringBuilder/StringBuffer常用方法</p>

```java
public class LearnStringBuilder {
	public static void main(String[] args) {
		//声明一个空的StringBuilder对象
		//在所有对字符串操作结束时，使用toString方法将其转换为String
		StringBuilder strb1 = new StringBuilder();
		StringBuilder strb2 = new StringBuilder("带参");
		
		/*StringBuilder常用方法*/
		
		//字符串连接方法
		strb1.append("abc");
		/*strb1="abc"*/
		
		//字符串插入，索引从0开始
		strb2.insert(1, "一个");
		/*strb2="带一个参"*/
		
		//字符串删除，索引从0开始
		strb2.delete(1, 2);
		/*strb2="带参";*/
		
		//字符串反转
		strb1.reverse();
		/*strb1="cba";*/
		
		//将从索引为start到end的字符串进行替换
		strb2.replace(1,2, "代替的字符串");
		/*strb2="带代替的字符串参";*/
		
		
		/*StringBuffer的用法与上述一致*/
	}
}
```
