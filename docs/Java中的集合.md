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

### 2.3 Iterator 和 Enumeration的区别

> 功能是重复的。
>
> Iterator 替换了Enumeration：
>
> 1. 添加了remove方法
> 2. 方法名称简写 得到改进

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
>
> linkedlist是双向链表加列表的实现. 因为LinkedList实现了List和Quene接口。

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

![image-20201214153317420](_media/image-20201214153317420.png)

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

## 5. 泛型

1、概述：
		泛型，在C++中被称为模板，就是一种抽象的编程方式。当我们定义类和方法的时候，
		可以用一种通用的方式进行定义，而不必写出具体的类，这些未知的东西会在真正使
        	用的时候在确定。
		对于集合类来说，它们可以存放各种类型的元素。如果在存放之前，就能确定元素的
		类型，那么就可以更加直观，也让代码更加简洁。
	2、好处：
		a、类型安全。 泛型的主要目标是提高 Java 程序的类型安全。通过知道使用
		   泛型定义的变量的类型限制，编译器可以在一个高得多的程度上验证类型
		   假设。没有泛型，这些假设就只存在于程序员的头脑中（或者如果幸运的
                   话，还存在于代码注释中）。
		b、消除强制类型转换。 泛型的一个附带好处是，消除源代码中的许多强制
		   类型转换。这使得代码更加可读，并且减少了出错机会。
		c、潜在的性能收益。 泛型为较大的优化带来可能。在泛型的初始实现中，
		   编译器将强制类型转换（没有泛型的话，程序员会指定这些强制类型转换）
		   插入生成的字节码中。但是更多类型信息可用于编译器这一事实，为未来
                   版本的 JVM 的优化带来可能。由于泛型的实现方式，支持泛型（几乎）
                   不需要 JVM 或类文件更改。所有工作都在编译器中完成，编译器生成类
           	   似于没有泛型（和强制类型转换）时所写的代码，只是更能确保类型安全
		   而已。
	3、泛型在使用中还有一些规则和限制：
    		a、泛型的类型参数只能是类类型（包括自定义类），不能是简单类型。
    		b、同一种泛型可以对应多个版本（因为参数类型是不确定的），不同版本的
		   泛型类实例是不兼容的。
    		c、泛型的类型参数可以有多个。
    		d、泛型的参数类型可以使用extends语句，例如<T extends superclass>。
		  习惯上成为“有界类型”。
    		e、泛型的参数类型还可以是通配符类型。
			例如Class<?> classType = Class.forName(Java.lang.String);

> 为什么要有泛型机制?
>
> 就是在编程中很多时候需要数据类型的转换 ，很麻烦。所以在JDK1.5提出了泛型的机制。
>
> 泛型的分类?
>
> 1. 集合中的泛型  
> 2. 接口的泛型
>
> 泛型的好处:
>
> 1. 解决的java的类类型转换的安全的机制问题
> 2. 程序变的简单起来
> 3. 如果集合规定了泛型 泛型意外的数据就不会加进去 在编译就会出错。
> 4. 提高代码的可读性

```java
package com.xdkj.javase.list;

import java.util.ArrayList;
import java.util.Iterator;

public class ElementDemo {

	public static void main(String[] args) {
		//集合使用的时候 一般集合中存储的是对象  购物车的商品
		// 类的实例化  也就是说集合中存储的对象是用一个类类型的数据
		//如果我们在使用集合的时候里面存储的是相同的类类型的数据 ，我们在遍历的时候还需要强制转换
		//很麻烦
		ArrayList list = new ArrayList();
			list.add(new Student("小明",23));
			list.add(new Student("小红",89));
			list.add(new Student("小花",36));
			list.add(new Student("小李",18));
			list.add(new Student("小王",16));
			list.add(null);
			list.add(new Student("小王",16));
			list.add(null);
		
		System.out.println(list);
		//遍历
		Iterator iterator = list.iterator();
		while(iterator.hasNext()) {
			Student student = (Student)	iterator.next();
			System.out.println(student);
		}
		// 泛型的使用
		//泛型指的是 集合存储数据的类类型  如果是基本数据类型的数据  泛型使用包装类
		//jdk1.5的使用方式
		//ArrayList<Student> list1 = new ArrayList<Student>();
		//jdk1.8的使用方式
		ArrayList<Student> list1 = new ArrayList<>();
			list1.add(new Student("小明",23));
			list1.add(new Student("小红",89));
			list1.add(new Student("小花",36));
			list1.add(new Student("小李",18));
			list1.add(new Student("小王",16));
			list1.add(null);
			list1.add(new Student("小王",16));
			list1.add(null);
		for(Student stu : list1) {
			System.out.println(stu);
		}
        //集合元素是基本数据类型  泛型是基本数据类型的包装类
        ArrayList<Integer> list2 = new ArrayList<>();
			list2.add(23);
			list2.add(88);
			System.out.println(list2);
	}

}

```

### 5.2 泛型在接口中的使用

```java
//泛型
public interface BaseDao<T> {
	void add(T t);
}
```

```java
public interface StudentDao extends BaseDao<Student> {
	
}
```

```java
public interface GoodsDao  extends BaseDao<Goods>{
	
}
```

```java
package com.xdkj.javase.list;

public class BaseDaoDemo {

	public static void main(String[] args) {
		//匿名内部类
		StudentDao stuDao = new StudentDao() {
			@Override
			public void add(Student t) {
				
			}};
			//add 方法在进行重写的时候会自动进行参数类型的填充
			GoodsDao goodsDao = new GoodsDao() {

				@Override
				public void add(Goods t) {
					
				}};
	}

}

```

### 5.3  在方法参数 中使用

```java
//方法的参数类不确定就可以使用泛型的形式
	public static <T> void method(T t ) {
		System.out.println("Hello"+t );
	}
```

### 5.4 方法的参数是接口类型带泛型

> TreeSet(Comparator(? super E) comparator)  参数是接口的实现类类型  实现类又需要泛型。

## 6. Set 集合

> 一个不包含重复元素的 collection。更确切地讲，set 不包含满足 `e1.equals(e2)` 的元素对  `e1` 和 `e2`，并且最多包含一个 null 元素,可以有序也可以无序。

### 6.1 HashSet

> 此类实现 `Set` 接口，由哈希表（实际上是一个 `HashMap` 实例）支持。它不保证 set  的迭代顺序；特别是它不保证该顺序恒久不变。此类允许使用 `null` 元素
>
> + 数据结构是哈希表
> + 是无序的
> + 允许null元素
> + 不是线程同步   效率高

```java
package com.xdkj.javase.set;

import java.util.HashSet;
import java.util.Iterator;
/**HashSet: 
 * 底层是哈希表的结构:
 * 	
 * 
 * 
 * */
public class HashSetDemo {

	public static void main(String[] args) {
		// 所谓的无序是指  添加和获取的顺序不一致
		HashSet<String> set = new HashSet<>();
			set.add("Hello");
			set.add("Java");
			set.add("Java");
			set.add("123");
			set.add("World");
			set.add("World");
			set.add("Python");
			//[Java, Hello, World, Python]
		System.out.println(set);
			//5
		System.out.println(set.size());
			//怎么保证元素的唯一性?
			//底层使用hashMap  
			// HashMap的putVal()方法使用到了三种数据结构数组  链表 红黑树
			//遍历
		Iterator<String> iterator = set.iterator();
			while(iterator.hasNext()) {
				System.out.println(iterator.next());
			}
			
			
	}

}

```

**保证元素的唯一性:**

> 底层使用的是hashMap的put方法 ， add()方法说明，如果set集合中没有包含添加的元素 ， 添加进去返回true,如果 通过hashCode,equals方法比较已经包含了要添加的元素，那么集合不会改变，并且返回false.

```java
  /**
     * Adds the specified element to this set if it is not already present.
     * More formally, adds the specified element <tt>e</tt> to this set if
     * this set contains no element <tt>e2</tt> such that
     * <tt>(e==null&nbsp;?&nbsp;e2==null&nbsp;:&nbsp;e.equals(e2))</tt>.
     * If this set already contains the element, the call leaves the set
     * unchanged and returns <tt>false</tt>.
     *
     * @param e element to be added to this set
     * @return <tt>true</tt> if this set did not already contain the specified
     * element
     */
    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }

```

**加载因子是0.75:**

> 初始的容量是16如果说是超过初始容量以后呢。他会生成新的哈希表，将原来的哈希表覆盖。
>
> 新的 哈希表的大小是多少?

```java
/**
     * Constructs a new set containing the elements in the specified
     * collection.  The <tt>HashMap</tt> is created with default load factor
     * (0.75) and an initial capacity sufficient to contain the elements in
     * the specified collection.
     *
     * @param c the collection whose elements are to be placed into this set
     * @throws NullPointerException if the specified collection is null
     */
    public HashSet(Collection<? extends E> c) {
        map = new HashMap<>(Math.max((int) (c.size()/.75f) + 1, 16));
        addAll(c);
    }
```

### 6.2 TreeSet

> 基于 [`TreeMap`](../../java/util/TreeMap.html) 的 [`NavigableSet`](../../java/util/NavigableSet.html)  实现。使用元素的[自然顺序](../../java/lang/Comparable.html)对元素进行排序，或者根据创建 set 时提供的 [`Comparator`](../../java/util/Comparator.html)  进行排序，具体取决于使用的构造方法
>
> + 不是同步的  效率高
> +  自然排序
> + 比较器排序  Comparable 

**自然排序:**

```java
package com.xdkj.javase.test;

import java.util.TreeSet;

public class TreeSetDemo {

	public static void main(String[] args) {
		//自然排序  
		//String类型 实现了Comparable接口就实现了自然排序
		TreeSet <String> set = new TreeSet<>();
			set.add("Hello");
			set.add("Java");
			set.add("Java");
			set.add("123");
			set.add("World");
			set.add("World");
			set.add("Python");
		System.out.println(set);
		//java.lang.ClassCastException: 
		//com.xdkj.javase.test.Teacher cannot be cast to java.lang.Comparable
		//Teacher没有实现Comparable接口 不能自然排序
        //汉字的顺序根据Unicode 码表排序
		TreeSet <Teacher> tSet = new TreeSet<>();
			tSet.add(new Teacher("张三",33,"西安市"));
			tSet.add(new Teacher("王五",13,"汉中市"));
			tSet.add(new Teacher("翟柳",23,"宝鸡市"));
			tSet.add(new Teacher("张麻子",33,"西安市"));
			tSet.add(new Teacher("张麻子",33,"西安市"));
			System.out.println(tSet);
			//System.out.println("Hello".compareTo(null));
	}

}

```
**自然排序要实现Comparable接口   和重写 CompareTo()方法:**

```java
package com.xdkj.javase.test;

public class Teacher implements Comparable<Teacher> {
	private String teaName;
	private int teaAge;
	private String teaAddress;
	public Teacher() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Teacher(String teaName, int teaAge, String teaAddress) {
		super();
		this.teaName = teaName;
		this.teaAge = teaAge;
		this.teaAddress = teaAddress;
	}
	......get  set ......
        
	@Override
	public String toString() {
		return "Teatcher [teaName=" + teaName + ", teaAge=" + teaAge + ", teaAddress=" + teaAddress + "]";
	}
	/*我们让 自定义类对象进行自然排序。
	 * 怎么排序?
	 * 1. 首先实现Comparable接口  重写CompareTo方法
	 * 2. 我们根据对象的哪一个属性进行比较?
	 * 3. 我们要定义排序主规则: 按年龄 ----> 名字 ----> 地址
	 * 
	 */
	
	@Override
	public int compareTo(Teacher teacher) {
		if(teacher == null) {
			throw new NullPointerException("输入的参数对象不能是null!!!");
		}
		if(this==teacher) {
			return 0;
		}
		
		int  ageResult = this.getTeaAge() - teacher.getTeaAge();
		int nameResult = this.getTeaName().compareTo(teacher.getTeaName()); 
		int addressResult = this.getTeaAddress().compareTo(teacher.getTeaAddress());
		int result  = ageResult == 0 ? (nameResult == 0?addressResult : nameResult):ageResult;
		return result;
	}
	
}

```



### 6.3 LinkedHashSet

## 7. Map

### 7.1 Hashtable

### 7.2 HashMap

#### Hashtable和HashMap的区别

### 7.3 TreeMap

### 7.4 LinkedHashMap

### 7.5 Properties

