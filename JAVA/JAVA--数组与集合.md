
## 数组（Array）
> <p>什么是数组</p>
> <p style="color:blue">数组是相同数据类型（任意类型）的有序集合。</p>
> <p style="color:blue">数组也是对象，数组成员相当于对象的成员变量。</p>

***

> <p>数组下标</p>
> <p style="color:blue">对数组元素进行编号，从0开始，数组中的每个元素都可以通过下标来访问。</p>
> <p style="color:blue">数组长度是确定的，不可变的。如果下标越界则会抛出异常。</p>

***

```java
public class TestArray {
	public static void main(String[] args){
		//数组声明后长度不能改变
		
		//声明数组的方式：
		//1.长度为5的整数型空数组（推荐）
		int[] a1 = new int[5];
		//2.长度为5的整数型空数组
		int a2[] = new int[5];
		//3.长度为5的固定值数组
		int[] a3 = {1,2,5,4,3};
		
		//获取数组的长度
		int len = a1.length;
		
		//将数组a3转换为字符串
		String str = a3.toString();
		
		//为数组a4的第1个元素赋值
		a1[3] = 1;
		
		
		//数组工具类Arrays
		//比较数组a1和a2是否相等（有相同的元素）
		boolean b1 = Arrays.equals(a1, a2);
		
		//将数组a2扩容至长度10，此a2已不再是之前的数组，引用发生了改变
		a2 = Arrays.copyOf(a2, 10);
		
		//对数组a3进行升序排列(从小到大)
		Arrays.sort(a3);
		
		//查询元素val在数组中的下标（要求数组中元素已按照升序排列）。
		int index = Arrays.binarySearch(a1,1);
	}
}
```

## 集合/容器（Collection）
> <p>什么是集合</p>
> <p style="color:blue">集合可以存放不同类型，不限数量的数据对象</p>
> <p style="color:blue">集合存放的是数据对象的引用而不是数据对象的本身</p>

***

> <p>集合/容器的分类</p>
- Collection（接口，存储一组不唯一，无序的对象）
    - List（接口，存储一组不唯一、有序（插入顺序）的对象）
        - ArrayList：实现了长度可变的数组，在内存中分配连续的空间。遍历元素和随机访问元素的效率比较高
        - LinkedList：采用链表存储方式。插入、修改、删除元素时效率比较高
    - Set（接口存储一组唯一，无序的对象）
        - HashSet:通过哈希值确定元素的位置
    - Map（键值对【Key--Value】，Key是以Set方式进行存储的）
        - HashMap:非线程安全，可以接受null值
        - HashTable：线程安全，不可接受null值

***

> <p>如何遍历集合？</p>
> <p style="color:blue">使用iterator（迭代器）或者for循环</p>

***

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Hashtable;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class TestCollection {
	public static void main(String[] args){
		
		//声明一个ArrayList集合
		//查询速度快
		List<String> arrayList = new ArrayList<String>();
		//向集合中添加元素
		arrayList.add("hello");
		//根据index获取集合中的元素
		String str = arrayList.get(0);
		//判断集合中是否包含某元素
		boolean b = arrayList.contains("hello");
		//查找元素在集合中的位置
		int index = arrayList.indexOf("hello");
		//根据index移除集合中的元素
		arrayList.remove(0);
		//移除集合中的指定元素
		arrayList.remove("hello");
		//清空集合，移除集合中的所有元素
		arrayList.clear();
		//集合的大小
		int listSize = arrayList.size();
		
		//遍历集合方式一，获取集合的迭代器（推荐使用）
		Iterator<String> ita = arrayList.iterator();
		while(ita.hasNext()){
			//获取迭代器中的元素
			String s1 = ita.next();
			System.out.println(s1);
		}
		//遍历集合方式二，for循环
		for (String s2 : arrayList) {
			System.out.println(s2);
		}
		
		
		//声明一个LinkedList集合
		//增删改速度快,使用方法同arrayList
		List<String> linkedList = new LinkedList<String>();
		
		/*------------------------------------------*/		
		
		//声明一个HashSet集合
		Set<String> hashSet = new HashSet<String>();
		//添加元素
		hashSet.add("world");
		//判断元素是否存在
		boolean exist = hashSet.contains("world");
		//移除元素
		hashSet.remove("world");
		//集合的大小
		int setSize = hashSet.size();
		//遍历set集合
		Iterator<String> itaSet = hashSet.iterator();
		while(itaSet.hasNext()){
			//获取迭代器中的元素
			String set = itaSet.next();
			System.out.println(set);
		}
		
		/*------------------------------------------*/		
		
		//声明一个HashMap集合(常用)
		Map<String, Object> hashMap = new HashMap<String, Object>();
		//添加元素（键，值）
		hashMap.put("m1", 1);
		//根据键来移除元素（键值对）
		hashMap.remove("m1");
		//判断是否存在指定键m1
		boolean bmk = hashMap.containsKey("m1");
		//判断是否存在指定值1
		boolean bmv = hashMap.containsValue(1);
		//获取集合中所有键
		Set keys = hashMap.keySet();
		//清空集合
		hashMap.clear();
		//集合的大小
		int mapSize = hashMap.size();
		
		
		//声明一个HashTable集合
		//使用方法同HashMap
		Map<String, Object> hashTable = new Hashtable<String, Object>();
	}
}
```


