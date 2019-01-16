
# 运算符&控制语句

## 一、运算符

- 赋值运算符
    - 赋值=
- 算术运算符
    - 加+
    - 减-
    - 乘*
    - 除/
    - 取余%
    - ++（自增）
    - --（自减）
- 关系运算符
    - 大于>
    - 小于<
    - 等于==
    - 大于等于>=
    - 小于等于<=
    - 不等于！=
- 逻辑运算符
    - 与&&
    - 或||
    - 非！
- 位运算符
    - &
    - |
    - <<（左移一位，相当于*2）
    - &gt;>（右移一位，相当于/2）
- 扩展运算符
    - +=
    - -=
    - *=
    - /=
    - %=
- 三目运算符
    - （布尔表达式）？为真返回：为假返回

```java
public class Operator {
	//赋值运算符
	public void operator1(){
		int a = 1;//将  a 赋值为1
	}
	//算术运算符
	public void operator2(){
		int a = 1 + 1;//加
		int b = 2 - 1;//减
		int c = 2 * 2;//乘
		int d = 4 / 2;//除
		int e = 12 % 5;//取余（模运算）
		
		a++;//自增，等同于a = a + 1;先使用，再加1
		++a;//自增，等同于a = a + 1;先加1，再使用
		
		b--;//自减，等同于a = a - 1;先使用，再减1
		--b;//自减，等同于a = a - 1;先减1，再使用
		
	}
	//关系运算符
	public void operator3(){
		int a = 1;//比较值a
		int b = 2;//比较值b
		
		boolean c1 = a > b ;//比较 a 是否大于 b，结果赋值给c1
		boolean c2 = a < b ;//比较 a 是否小于 b，结果赋值给c2
		boolean c3 = a == b ;//比较 a 是否等于 b，结果赋值给c3
		boolean c4 = a >= b ;//比较 a 是否大于等于 b，结果赋值给c4
		boolean c5 = a <= b ;//比较 a 是否小于等于 b，结果赋值给c5
		boolean c6 = a != b ;//比较 a 是否不等于 b，结果赋值给c6
	}
	//逻辑运算符
	public void operator4(){
		boolean a = true;//比较值a
		boolean b = false;//比较值b
		
		boolean c1 = a && b;//a和b同时为true，c1为true，否则为false
		boolean c2 = a || b;//a和b有1个为true，c2为true，否则为false
		boolean c3 = !a;//取反，若a为true 则c3为false
	}
	//位运算符
	public void operator5(){
		int a = 100;//运算值a,二进制：     1100100
		int b = 1000;//预算值b，二进制：1111101000
		
		//二进制位运算：0和1相或为1，相与为0，0和0相与相或都为0，1和1相与相或都为1
		int c1 = a & b;//按位与运算，c1二进制：1100000     十进制：96
		int c2 = a | b;//按位或运算，c2二进制：1111101100  十进制：1004
		int c3 = a << 1;//按位向左移1位，相当于乘2，c3十进制：200
		int c4 = a >> 2;//按位向右移1位，相当于除2，c4十进制：25
		//位运算效率较高，但计算较复杂，初学者谨慎使用，二进制运算方法请自行查找
	}
	//扩展运算符
	public void operator6(){
		int a = 22;//运算值a
		a += 2;//等价于a = a + 2;
		a -= 2;//等价于a = a - 2;
		a *= 2;//等价于a = a * 2;
		a /= 2;//等价于a = a / 2;
		a %= 2;//等价于a = a % 2;
	}
	//三目运算符
	public void operator7(){
		int a = 1;//比较值1
		int b = 2;//比较值2
		String str = a > b ? "a" : "b";//若a>b则将“a”赋值str,否则将“b”赋值str 
	}
}
```

## 二、控制语句

#### 1. 顺序结构

程序中代码按顺序执行

#### 2. 选择结构

if(){} <br>
if(){} else{} <br>
if(){} else if(){}	else{} <br>
switch(){}（多值选择时使用，表达式为int或自动转为int的类型以及枚举）

#### 3. 循环结构


while（先判断后执行）<br>
for（先判断后执行）<br>
do	while（先执行后判断）



#### 4. 控制

break：强制终止当前循环。<br>
continue：停止本次循环在continue后面的代码，执行下一次循环。


```java
public class ControlStatement {

	public static void main(String[] args){
		//顺序结构，程序从上到下按顺序执行代码
		caseStructure();
		loopStructure();
	}
	
	//选择结构
	static void caseStructure(){
		int a = 1;//比较值1
		int b = 2;//比较值2
		
		//if判断
		if(a>b){
			//若a>b,则执行此处代码，否则跳过此处向下执行
		}
		
		//多重if判断
		if(a>b){
			//若a>b,则执行此处代码
		}else if(b==a){
			//若b==a，则执行此处代码
		}else{
			//以上条件都不成立时，则执行此处代码
		}
		
		//switch选择结构
		switch(a){//每个case下的break必须加上，否则会按顺序执行，失去选择的意义
		case 1://当a=1时，执行下面b=10
			b = 10;
			break;
		case 2://当a=2时，执行下面b=100
			b = 100;
			break;
		case 3://当a=3时，执行下面b=1000
			b = 1000;
			break;
		default://当a没有匹配case中的值时，执行下面b=4
			b = 4;
			break;
		}
	}
	
	//循环结构
	static void  loopStructure(){
		String str = "abc";
		//for循环
		for(int i=0;i<10;i++){
			str = "123";
			continue;//停止本次循环在continue后面的代码，执行下一次循环。
		}
		
		//while循环，判断是否成立，若成立则执行
		while(true){
			str = "def";
			break;//强制终止当前循环，只能在循环体内和switch语句体内使用break；
		}
		
		//do while 循环，先执行do内的代码，再进行判断
		do{
			str = "def";
		}while("abc".equals(str));
		
	}
}
```



> ### *爱转圈笔记*
> 勤思、体悟、总结、分享