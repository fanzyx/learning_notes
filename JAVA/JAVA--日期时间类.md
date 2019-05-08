
## Date类
> <p style="color:blue">Date（在java.util包下）对象既包含日期也包含时间。</p>
> <p style="color:blue">Date类的大部分方法已经过时，不再推荐使用。</p>

***

> <p>Date常用方法</p>

```java
public class LearnDate {
	public static void main(String[] args) {
		//------声明------
		//声明一个Date对象，返回当前时间，常用
		Date date1 = new Date();
		/*date1="Mon Dec 31 17:07:46 CST 2018"*/
		
		//返回一个与1970年1月1日00:00:00间隔100000毫秒的Date对象
		Date date2 = new Date(100000L);
		/*date2="Thu Jan 01 08:01:40 CST 1970"*/
		
		
		/*Date常用方法*/
		
		//------比较------
		//比较date1是否在date2之后
		boolean isAfter = date1.after(date2);
		/*isAfter=true*/
		
		//比较date1是否在date2之前
		boolean isBefore = date1.before(date2);
		/*isBefore=false;*/
		
		//------时间获取与设置------
		//获取当前对象与1970年1月1日00:00:00的间隔毫秒数
		Long msecL = date1.getTime();
		//设置当前对象的时间
		date2.setTime(1000000L);
		
		//------格式化时间------
		//设置时间格式为yyyy-MM-dd HH:mm:ss
		SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		String date = dateFormat.format(date1);
		/*date="2018-12-31 17:21:48"*/
		
		/*java官方推荐尽量少使用Date类，
		 * 如果需要对日期时间进行操作，可使用Calendar工具类*/
	}
}

```

## Calendar类
> <p style="color:blue">Calendar是一个抽象类，用来处理日期和时间，它可以作为所有日历类的模板。</p>
> <p style="color:blue">JAVA提供了一个公历子类：GregorianCalendar(格里高利日历)。</p>
自己也可以通过继承Calendar来制作自己的日历

***

> <p>Calendar常用方法</p>

```java
public class LearnCalendar {
	public static void main(String[] args) {
		//------声明Calendar对象，有多个重载方法------
		Calendar calendar = Calendar.getInstance();
		//获取Date对象
		Date date = calendar.getTime();
		
		//------根据Date设置Calendar------
		Calendar calendar2 = Calendar.getInstance();
		calendar2.setTime(date);
		
		
		/*Calendar常用方法*/
		
		//------获取日期时间------
		calendar.get(Calendar.YEAR);//年
		calendar.get(Calendar.MONTH);//月
		calendar.get(Calendar.DATE);//日
		calendar.get(Calendar.HOUR);//时
		calendar.get(Calendar.MINUTE);//分
		calendar.get(Calendar.SECOND);//秒
		
		//------设置日期时间(2018-12-31 17:22:22)------
		calendar.set(2018, 12,31,17,22,22);
		
		//------修改日期时间------
		//将当前年 减去1年
		calendar.add(Calendar.YEAR, -1);
		//将当前月  加上 2个月
		calendar.roll(Calendar.MONTH, 2);
		/*两者区别：roll方法不会向邻域进位或借位
		 * 例如上述roll方法会将月份加上2个月，变成二月，但是年份不变
		 * 若使用add方法，月份也是变成二月，但年份变为2019年 */
	}
}
```
