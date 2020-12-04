# Java常用的类

> 已经学习完了面向对象，我们自己学习了类的创建和使用，我们Java的封装好的c的一些东西和java自己定义了很多的类。接下来学习java常用的类：
>
> java的核心的包: 
>
> 	1. lang   java的核心的类   核心包的类不需要导入就直接可以使用
>  	2. util  工具包  这里定义的是java的工具类  Date  Scanner....
>  	3. IO 包  流 javaio流 文件的拷贝 网络底层就是io的数据传输
>  	4. net 网络编程包   
>  	5. nio  新的io包 异步数据传输
>  	6. awt 图形界面 + swing 
>  	7. util.stream  集合流
>  	8. time jdk1.8新的日期api
>
> 

## 1.JavaAPI的使用

> java帮助手册 就是使用javadoc根据java的类和接口自动生成的类和接口的说明书。
>
> 帮助手册 分为三个部分:
>
> 1. 包
> 2. 接口/类
> 3. 接口和类的说明
>
> 每一个程序员手动都应该有很多的手册，随时可以使用。

##  2. Object类

> Object是java类层次结构的根类 ，所有java中的类包括数额组都直接继承该类的方法。
>
> + toString()
> + equasl()
> + hashCode()

##  3. String字符串

> 1. String 是字符串  ""包裹的都是字符串
>
> 2. 字符串是常量  值不可以被改变

### 3.1 创建字符串对象

```java
package com.xdkj.javase.core.classes;

import java.io.UnsupportedEncodingException;

/**
 * String 字符串类
 * 	String() 
 * 	String(byte[])
 * 	String(byte[] ,charset)
 * 	String(String)
 * 	String(byte[] bytes, int offset, int length)  offset 偏移量  length 长度
 * 	String(byte[] bytes, int offset, int length, String charsetName) 
*	String(char[] value, int offset, int count) 
 *
 * */
public class StringDemo01 {

	public static void main(String[] args) throws UnsupportedEncodingException {
		//无参构造器实例化对象  但是字符串没有值
			String str = new String();
			
			System.out.println(str);
			//字符串作为参数
			String str1 = new String("Hello");
			System.out.println(str1);
			
			//字节数组作为参数
			//根据默认的编码 utf-8
			byte [] by = {127,23,45,65,4,97};
			String str2 = new String(by);
			System.out.println(str2);
			//通过指定的编码解析字节数组  创建字符串对象
			//重点知识
			String str3 = new String(by,"gb2312");
			System.out.println(str3);
			//解决乱码
			String str4 = "浣嗘槸瀛楃涓叉病鏈夊€?";
			System.out.println(new String(str4.getBytes("GBK"),"UTF-8"));
			
			//获取字节数组的指定长度 在创建字符串
			String str5 = new String(by,3,1);
			System.out.println(str5);
			//拼接字符 形成新的字符串
			String str6 = new String(new char[] {'a','b','c'});
			System.out.println(str6);
			//获取字符数组的片段 生成新的字符串
			String str7 = new String(new char[] {'a','b','c','d'},0,3);
			System.out.println(str7);
       	 // 简写方式创建字符串对象
        String str8 = "Hello world";
			System.out.println(str8);
	}

}

```

### 3.2 为什么字符串是常量

```java
package com.xdkj.javase.core.classes;

/** 1. 为什么字符串是常量
 *  2. 字符串常见面试题
 * 		String str = new String("Hello World");
 * 		问上边的是几个对象?
 * 				两个对象
 * 3. 	String str = "Hello";
 * 		String str1 = "World";
 * 		String str3 = str + str1;
 * 		String str4 = "HelloWorld";
 * 问?
 * 		str3 == str4 ?  false
 * 		str3.equals(str4)?
 * 
 * */
public class StringDemo02 {
	public static void main(String[] args) {
			//字符串是常量
			//从常量池中获取值
				String  str = "Hello";
					str = "world";
				System.out.println(str);
		
				String str2 = "Hello";
		 		String str1 = "World";
				String str3 = str2 + str1;
		  		String str4 = "HelloWorld";
		  		System.out.println(str3 == str4); //false	
		  		System.out.println(str3.equals(str4));//true
		
	}
}

```

![](_media/字符串是常量.png)

### 3.3 字符串面试题

```java
package com.xdkj.javase.core.classes;

/** 1. 为什么字符串是常量
 *  2. 字符串常见面试题
 * 		String str = new String("Hello World");
 * 		问上边的是几个对象?
 * 				两个对象
 * 3. 	String str = "Hello";
 * 		String str1 = "World";
 * 		String str3 = str + str1;
 * 		String str4 = "HelloWorld";
 * 问?
 * 		str3 == str4 ?  false
 * 		str3.equals(str4)?
 * 
 * */
public class StringDemo02 {
	public static void main(String[] args) {
			//字符串是常量
			//从常量池中获取值
				String  str = "Hello";
					str = "world";
				System.out.println(str);
		
				String str2 = "Hello";
		 		String str1 = "World";
				String str3 = str2 + str1;
		  		String str4 = "HelloWorld";
		  		System.out.println(str3 == str4); //false	
		  		System.out.println(str3.equals(str4));//true
		
	}
}

```

<img src="_media/面试题1.png" style="width:60%">

<img src="_media/面试题2-1607053009086.png" style="width:60%">

### 3.4 String 类常用方法

```java
package com.xdkj.javase.core.classes;

import java.util.Scanner;

/**String 类的常用方法:
 * 	charAt() 返回下标位置的字符值
 * 	codePointAt(0)返回下标位置字符的unicode编码
 * 	compareTo()比较两个字符串的大小 按照字典顺序比较
 * 	compareToIgnoreCase(String str) 忽略大小写比较 
 * 	concat()  拼字符串  + 
 * 	contains(CharSequence s)   是否包含指定的字符序列
 * 	endWith()  以什么字符序列结尾
 * 	startWith()  以什么字符序列开头
 * 	indexOf()  检索字符串中的字符串第一次出现的下标值
 * 	lastIndexOf()检索字符串中的字符串最后一次出现的下标值
 * 	trim()  去除字符串前后空格
 * 	subString(start,end)  截取字符串片段  不包含末尾的字符
 * 	split()   按照正则表达式将字符串切割为字符串数组
 * 	getBytes()  字符串转为  字节数组
 * 	toLowerCase()  转小写
 * 	toUpperCase()转大写
 * 	toCharArray()  转为字符数组
 * 	isEmpty()  是否为空
 * 	replace()  替换
 * 	matches() 正则表达式匹配
 * 	length() 字符串长度
 * 
 * */
public class StringDemo03 {
	public static void main(String[] args) {
		//检索
		System.out.println("HelloWorld".charAt(0));//H
		System.out.println("HelloWorld".codePointAt(0));//72
		System.out.println("Hello".compareTo("Hahaha"));//4
		System.out.println("Hahaha".compareTo("Hello"));//-4
		System.out.println("HELLO".compareTo("HAHAHA"));//4
		
		System.out.println("Hello".concat("World"));//HelloWorld
		System.out.println("HelloWorld".contains("llo"));//true
		
		System.out.println("HelloWorld".contentEquals("Wolrd"));//false
		
		System.out.println("HelloWorld".copyValueOf(new char[] {'l','l'}));
		
		
		System.out.println("Hello".endsWith("hhjh"));//false
		System.out.println("Hello".startsWith("He"));//true
		//返回
		System.out.println("HelloWorld".indexOf('l'));//2
		System.out.println("HelloWorld".lastIndexOf('l'));//8
		
		System.out.println("    Hello  World   ".trim());
		
		System.out.println("HelloWorld".substring(2,6));//llow
		
		System.out.println("HelloWoorld".split("o"));//
		
		for(String str: "HelloWoorld".split("o")) {
			System.out.println(str);
		}
		
		System.out.println("HelloWorld".getBytes());
		
		for(byte by :"HelloWorld".getBytes() ) {
			System.out.println(by);
		}
		System.out.println("------------");
		char [] ch = "HelloWorld".toCharArray();
		System.out.println("HelloWorld".toCharArray());
		
		System.out.println("Hello".toLowerCase());//
		System.out.println("HelloWorld".toUpperCase());
		
		System.out.println("Hello".isEmpty());//fasle
		
		Scanner s = new Scanner(System.in);
		//String sss = s.next();
		//字符串是否为空
			//if(sss != "" && sss != null) {}
			System.out.println();
			
			System.out.println("Hello".length());//
			
			System.out.println("Hello".replace('l', 'w'));
			//正则表达式
			String  regexp  ="[a-zA-Z]"; 
			System.out.println("a".matches(regexp));//true
	}
}

```

### 4. StringBuffer

### 5. StringBuilder

##  6.Math

## 7. Scanner

## 8. Date 和日期的转换

## 9. Calendar新的日期类

## 10.System

## 11. 包装类

## 12. 自动装箱和拆箱

## 13. Arrays

## 14. Random



