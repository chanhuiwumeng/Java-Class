# Java中的集合 :imp:

## 1. 集合的简介

> 我们前面学习过数组， 数组是用一个变量来存多个元素的容器，存储基本数据类型的数据。数组的长度是不可变的。
> 在实际的开发中我们需要这样去做: 
>
> ​	我们在购物的时候我们把商品添加到购物车，商品的名称 ，信息，单价，数量。我们在存购物车中获取购买的商品计算总价，
>
> 根据商品的总价计算积分。
>
> 我们对于购物车中的数据怎么去存储和获取呢？
>
> 可以使用数组吗?
>
> 可以，只是在你的商品数量少的情况下我定义长度固定的数组去存储商品是可以的。
>
> 还可以从购物车进行商品的删除。数组怎么删除数据?商品的信息 商品的类  商品的对象。

```java
public class Goods {
	private String goodsName;
	private int goodsCount;
	private double goodsPrice;
    ......get set ...
}
```

```java
package com.xdkj.javase.collection;

public class GoodsDemo {
	public static void main(String[] args) {
		Goods goods1 = new Goods("瓜子",100,9.9);
		Goods goods2 = new Goods("花生",200,9.9);
		Goods goods3 = new Goods("啤酒",20000,12.99);
		Goods goods4 = new Goods("麻辣条",100,3);
		
		//使用容器去存储商品的对象
		Goods [] goods = new Goods[10];
			goods[0] = goods1;
			goods[1] = goods2;
			goods[2] = goods3;
			goods[3] = goods4;
		
		System.out.println(goods);
		for(Goods i : goods) {
			System.out.println(i);
		}
		
	}
}

```

> 使用数组存储商品的对象信息是可以的，但是就是定义数组的长度的时候不能精确的定义到底要多少长度，并且在数组移除商品的时候。我们如果从数组中将元素定义为Null说是将元素移除了，但是数组的内存大小依然是不变的。
>
> 1. 所以我们就想着说有没有更合适的容器去存放 对象的数据信息，
>
> 2. 在存放的时候如果数据增加或者移除 容器的大小是可变的。
> 3. 所以数组就不合适  而是要去使用集合。
> 4. 集合是一个长度动态可变的容器，一般集合中装的都是对象。也可以是基本数据类型。
> 5. 即使是基本数据类型 我们依然要使用基本数据类型的包装类去声明集合的类型。

![image-20201211100133097](_media/image-20201211100133097.png)

## 2. Collection

> *Collection 层次结构* 中的根接口。Collection 表示一组对象，这些对象也称为 collection 的*元素*。一些  collection 允许有重复的元素，而另一些则不允许。一些 collection 是有序的，而另一些则是无序的。JDK 不提供此接口的任何*直接*  实现：它提供更具体的子接口（如 `Set` 和 `List`）实现。此接口通常用来传递  collection，并在需要最大普遍性的地方操作这些 collection。 

### 2.1 Collection中的方法:

+ add
+ addAll
+ clear
+ contains
+ containsAll
+ equals
+ hashCode
+ isEmpty
+ remove
+ removeAll
+ toArry
+ size

```java
package com.xdkj.javase.collection;

import java.util.ArrayList;
import java.util.Collection;

public class CollectionDemmo {

	public static void main(String[] args) {
		
		Goods goods1 = new Goods("瓜子",100,9.9);
		Goods goods2 = new Goods("花生",200,9.9);
		Goods goods3 = new Goods("啤酒",20000,12.99);
		Goods goods4 = new Goods("麻辣条",100,3);
		
		// 使用多态的形式 Collection接口  List子接口的实现类 
		Collection  collection = new ArrayList();
		//集合是个容器 存储元素
		//基本数据类型和对象都可以进行存储
			collection.add("123");
			collection.add(123);
			collection.add('a');
			collection.add(99.99);
			collection.add(goods1);
			
			System.out.println(collection.size());
			System.out.println(collection);
			
			//集合的长度是可以扩增的
			collection.add(goods2);
			collection.add(goods3);
			System.out.println(collection.size());
			System.out.println(collection);
			
			//集合提供remove方法移除元素  集合的长度自动减少
			collection.remove(goods3);
			System.out.println(collection.size());
			System.out.println(collection);		
	}

}

```

```java
public static void method1() {
		Goods goods1 = new Goods("瓜子",100,9.9);
		Goods goods2 = new Goods("花生",200,9.9);
		Goods goods3 = new Goods("啤酒",20000,12.99);
		Goods goods4 = new Goods("麻辣条",100,3.0);
		
		// 使用多态的形式 Collection接口  List子接口的实现类 
		Collection  collection = new ArrayList();
		//集合是个容器 存储元素
		//基本数据类型和对象都可以进行存储
			collection.add("123");
			collection.add(123);
			collection.add('a');
			collection.add(99.99);
			collection.add(goods1);
			
			System.out.println(collection.size());
			System.out.println(collection);
			
			//集合的长度是可以扩增的
			collection.add(goods2);
			collection.add(goods3);
			System.out.println(collection.size());
			System.out.println(collection);
			
			//集合提供remove方法移除元素  集合的长度自动减少
			collection.remove(goods3);
			System.out.println(collection.size());
			System.out.println(collection);
	}
	//集合 的其他的方法
	public static void method2() {
		Collection collection1 = new ArrayList();
			collection1.add("123");
			collection1.add(123);
			collection1.add('a');
			collection1.add(99.99);
		Collection collection2 = new ArrayList();
			Goods goods1 = new Goods("瓜子",100,9.9);
			Goods goods2 = new Goods("花生",200,9.9);
			collection2.add(goods1);
			collection2.add(goods2);
			//集合合并
		collection1.addAll(collection2);
		System.out.println(collection1);
		//是否包含某一个元素
		System.out.println(collection2.contains(goods1));//true
		//判断集合中数据是否相等
		System.out.println(collection1.equals(collection2));//false
		//判断集合是否为空
		System.out.println(collection1.isEmpty());//false
		
		System.out.println(collection1.removeAll(collection2));//true
		System.out.println(collection1);
		
			Object [] obj = 	collection1.toArray();
			System.out.println(obj);
	}
```

### 2.2 Iterator 迭代器

> 提供集合的通用的遍历方式:
>
> 1. hasNext()  判断是否有下一个可迭代的元素
> 2. next()  获取下一个迭代的元素
> 3. remove() 移除下一个迭代的元素

```java
public static void method3() {
		//数组集合
		Collection collection2 = new ArrayList();
			Goods goods1 = new Goods("瓜子",100,9.9);
			Goods goods2 = new Goods("花生",200,9.9);
			collection2.add(goods1);
			collection2.add(goods2);
			System.out.println(collection2);
		//集合的遍历
		//hasNext()  next()
		Iterator  it = collection2.iterator();	
		while(it.hasNext()) {
			//数据的强制转换
			//铺垫泛型
			Goods  good = (Goods)it.next();
			System.out.println(good);
		}
	}
```

**不合法的状态异常:**

```java
public static void method4() {
		//数组集合
		Collection collection2 = new ArrayList();
			Goods goods1 = new Goods("瓜子",100,9.9);
			Goods goods2 = new Goods("花生",200,9.9);
			collection2.add(goods1);
			collection2.add(goods2);
			System.out.println(collection2);
		//集合的遍历
		//hasNext()  next()
		Iterator  it = collection2.iterator();	
		while(it.hasNext()) {
			//数据的强制转换
			//铺垫泛型
			//java.lang.IllegalStateException
			//先移除在获取发生不合法的状态异常
			//it.remove();
			Goods  good = (Goods)it.next();
			//it.remove();
			System.out.println(good);
		}
	}
```

**ConcurrentModificationException并发修改异常**

```java
public static void method5() {
		//数组集合
		Collection collection2 = new ArrayList();
			Goods goods1 = new Goods("瓜子",100,9.9);
			Goods goods2 = new Goods("花生",200,9.9);
			collection2.add(goods1);
			collection2.add(goods2);
			System.out.println(collection2);
		//集合的遍历
		//hasNext()  next()
		Iterator  it = collection2.iterator();	
		while(it.hasNext()) {
			//数据的强制转换
			//铺垫泛型
			//java.lang.IllegalStateException
			//先移除在获取发生不合法的状态异常
			//java.util.ConcurrentModificationException 并发修改异常
			collection2.add(new Goods("香烟",500,15));
			Goods  good = (Goods)it.next();
			System.out.println(good);
		}
	}
```

