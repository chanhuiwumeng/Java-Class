# Java中的集合 :imp:

## 1. 集合的简介 :airplane:

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

## 2. Collection :rainbow_flag:

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

### 2.2 Iterator 迭代器   :point_right:

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

## 3. List

> List: 列表集合
> 	1. list接口  序列集合  列表集合
> 	2. list集合允许元素重复  相同的元素重复 可以有多个null元素 
> 	3. list集合元素可以通过下标进行访问
> 	4. list集合使用特有的迭代器ListIterator在Iterator的基础上 有元素的插入和替换的方法 
> 		指定开始位置的迭代器
> 	list集合特有的方法:
> 		get()  获取list集合中的元素
> 		indexOf()  
> 		lasIndexOf()  
> 		listIterator()  list集合的特有迭代器
> 		subList()  获取集合片段
> 		size()	   获取list集合的元素的个数
> 	a. ArrayList
> 		底层是数组的数据结构  是长度可变的数组
> 		存储元素是要有序的，运行元素重复 和 允许多个null值
> 		是线程不安全的  是不同步的  效率高
> 		读取的效率高 因为是数据我们直接通过下标就可以操作  
> 		删除/添加   的操作效率低了

### 3.1 ArrayList

```java
package com.xdkj.javase.list;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.ListIterator;

public class ListDemo {

	public static void main(String[] args) {
		List list  = new ArrayList();
				list.add("Hello");
				list.add(123);
				list.add('d');
				list.add(new Object());
				list.add(99.99);
				//[Hello, 123, d, java.lang.Object@15db9742, 99.99]
			System.out.println(list);
			//通过下标获取集合中的元素
			System.out.println(list.get(0));
			//获取集合的元素个数
			System.out.println(list.size());
			//元素在集合中第一次出现的下标值
			System.out.println(list.indexOf('d'));
			//最后一次出现的下标值
			System.out.println(list.lastIndexOf(99.99));
			//截取集合片段  不包含结尾下标的集合元素
			System.out.println(list.subList(0, 3));
			System.out.println("------------集合的遍历-----------");
			//遍历
			/*
			 * for(int i=0;i<list.size();i++) { System.out.println(list.get(i)); }
			 */
			
			/*
			 * for(Object i:list) { System.out.println(i); }
			 */
			//通用迭代器
			/*
			 * Iterator it = list.iterator(); while(it.hasNext()) { Object obj = it.next();
			 * System.out.println(obj); }
			 */
			
			//特有的listIterator
			ListIterator iterator = list.listIterator();
			//java.util.NoSuchElementException
			//返回集合中上一个元素
				//System.out.println(iterator.previous());
				iterator.add("88888");
				while(iterator.hasNext()) {
					//iterator.add("88888");
					System.out.println(iterator.next());
					//iterator.set("Java");
				}
				System.out.println(list);
	}

}

```

### 3.2 Vector

> `Vector`  类可以实现可增长的对象数组。与数组一样，它包含可以使用整数索引进行访问的组件。但是，`Vector`  的大小可以根据需要增大或缩小，以适应创建 `Vector` 后进行添加或移除项的操作。
>
> Vector是线程安全的，线程同步的。
>
> Vector读取快 增删慢
>
> 从JDK1.2开始使用ArrayList替换了Vector

```java
package com.xdkj.javase.list;

import java.util.Iterator;
import java.util.Vector;

public class VectorDemo {
	public static void main(String[] args) {
		Vector   vector = new Vector();
			vector.add("123");
			vector.add(123);
			vector.add('d');
		System.out.println(vector);
		for(int i =0;i<vector.size();i++) {
			System.out.println(vector.get(i));
		}
		
		Iterator iterator = vector.iterator();
		while(iterator.hasNext()) {
			System.out.println(iterator.next());
		}
		//使用增强for循环迭代
		//使用listIterator迭代
	}
}

```

### 3.3 LinkedList

> `List` 接口的链接列表实现。实现所有可选的列表操作，并且允许所有元素（包括 `null`）。除了实现  `List` 接口外，`LinkedList` 类还为在列表的开头及结尾 `get`、`remove`  和 `insert` 元素提供了统一的命名方法。这些操作允许将链接列表用作堆栈、[队列](../../java/util/Queue.html)或[双端队列](../../java/util/Deque.html)。
>
> LinkedList是线程不安全的，线程不同步的。
>
> 链表结构:
>
> 读取慢，增删快
>
> 常用的方法:
>
> addFirst()
>
> addLast()
>
> getFirst()
>
> getLast()
>
> element()
>
> pop()
>
> push()
>
> peek()
>
> offer()
>
> offerFirst()
>
> removeFirst()
>
> removeLast();

![image-20201214122133249](_media/image-20201214122133249.png)

```java
package com.xdkj.javase.list;

import java.util.LinkedList;
import java.util.Scanner;

public class LinkedListDemo {

	public static void main(String[] args) {
		//链表的结构
		LinkedList list = new LinkedList();
			list.add("Hello");
			list.add(99);
			list.add('c');
			list.add(99.99);
			list.add(new Object());
		System.out.println(list);
		System.out.println(list.size());
		
		System.out.println(list.pop());
		//获取第一个节点元素
		System.out.println(list.getFirst());
		//获取最后一个节点的值
		System.out.println(list.getLast());
		//第一个节点的值
		System.out.println(list.element());
		System.out.println(list);
		//添加到列表的末尾
		System.out.println(list.offer("00000"));
		System.out.println(list);
		System.out.println("---------------------");
		//获取列表的头
		System.out.println(list.peek());
		
		//压栈  元素插入列表的开头
		list.push(new Scanner(System.in));
		System.out.println(list);
		//弹栈 取出元素  集合中就没有了
		System.out.println(list.pop());
		
		//遍历
		System.out.println("-------------遍历-----------");
		for(Object i : list) {
			System.out.println(i);
		}
		//下标
		for(int i =0;i<list.size();i++) {
			System.out.println(list.get(i));
		}
	}

}

```

**LinkedList  add方法的源码:**

```java
 public boolean add(E e) {
        linkLast(e);
        return true;
    }

```

```java
 private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```

```java
 void linkLast(E e) {
        final Node<E> l = last;
        final Node<E> newNode = new Node<>(l, e, null);
        last = newNode;
        if (l == null)
            first = newNode;
        else
            l.next = newNode;
        size++;
        modCount++;
    }
```

## 4. 数据结构

### 4.1 数组

> 存储相同数据类型的数据。 数组的长度是不可以变化的，在集合的数据结构中，底层是数据数据结构的集合长度四可以变化的。
>
> 数组的数据结构通过数组 的下标进行元素的获取和赋值。

### 4.2 栈

> 栈一般保存的是我们的变量，在方法的栈内存中声明变量和赋值  如果是对象在栈中保存的是对象的声明的变量  引用 的堆内存中的地址值
>
> Stack是Vector的子类 :
>
> + push  压栈
>
> + pop 弹栈

![image-20201214112352123](_media/image-20201214112352123.png)

### 4.3 队列

> 队列和我们站队一样 : 先进先出

![image-20201214112747311](_media/image-20201214112747311.png)

### 4.4 链表

> 链表的特性:
>
> 1. 存储的元素值
> 2. 存储元素值的地址值
> 3. 链表在内存中是无序存储的

+ 单向链表
+ 双向链表(循环链表)

![image-20201214113844383](_media/image-20201214113844383.png)

### 4.5 数

+ 红黑树
  + 二叉树

![image-20201214114132594](_media/image-20201214114132594.png)