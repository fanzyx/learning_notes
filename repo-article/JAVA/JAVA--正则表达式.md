
## 正则表达式
> <p>什么是正则表达式</p>
> <p style="color:blue">正则表达式时一个强大的字符串处理工具，可以对字符串进行查找、分割、替换、提取等操作。</p>

***

> <p>正则表达式的字符</p>

1. 支持的合法字符

字符| 说明
---|---
x | 字符x(x可以表示任何合法字符)
\t | 制表符（'\u0009'）
\n | 换行符（'\u000A'）
\r | 回车符（'\u000D'）
\f | 换页符（'\u000C'）
\a | 报警(bell)符（'\u0007'）
\e | Escape符（'\u001B'）

2. 特殊字符

字符| 说明
---|---
$ | 匹配一行的结尾。
^ | 匹配一行的开头。
() | 标记子表达式的开始和结束位置。
[] | 用于确定中括号表达式的开始和结束位置。
{} | 用于标记前面子表达式的出现频度。
* | 指定前面子表达式可以出现零次或多次。
+ | 指定前面子表达式可以出现一次或多次。
? | 指定前面子表达式可以出现零次或一次。
. | 匹配除换行符\n之外的任何单字符。
\ | 转义符。
丨| 指定两项之间匹配其中任意一项（或的意思）。

3. 预定义字符

字符| 说明
---|---
\d | 匹配0-9所有数字。
\D | 匹配非数字。
\s | 匹配所有空白字符，包括空格、制表符、回车符、换页符、换行符等。
\S | 匹配所有非空白字符。
\w | 匹配所有的单词字符，包括0-9,26个字母和下划线(_)。
\W | 匹配所有非单词字符。

***

> <p>JAVA中对正则表达式的支持</p>

- String类中的方法
    - boolean matches(String regex):判断字符串是否匹配指定正则表达式。
    - String replaceAll(String regex,String replacement):将所有符合regex条件的字符串全部替换成replacement。
    - String replaceFirst(String regex,String replacement):将第一个符合regex条件的字符串替换成replacement。
    - String[] split(String regex):以regex为分隔符，分隔字符串。

- Pattern类：正则表达式编译后在内存中的形式。
- Matcher类：用于匹配正则表达式，多个matcher对象可以共享一个pattern，其方法不在此处详细说明。

> <p>JAVA中对正则表达式的使用</p>

```java
public class LearnRegular {
	public static void main(String[] args) {
		//模拟一个字符串
		String str = "我的电话是13147996460";
		//创建正则表达式规则，匹配以13或15开头的号码
		Matcher m = Pattern.compile("((13)|(15))\\d{9}").matcher(str);
		//将所有符合条件的字符串输出
		while(m.find()){
			//m.group()方法是获取上一个匹配到的子串
			System.out.println(m.group());
		}	
	}
	/*输出：
	13147996460*/
}

```
