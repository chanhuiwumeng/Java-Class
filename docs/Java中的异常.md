# Java中的异常

> `Throwable` 类是 Java 语言中所有错误或异常的超类。只有当对象是此类（或其子类之一）的实例时，才能通过 Java  虚拟机或者 Java `throw` 语句抛出。类似地，只有此类或其子类之一才可以是 `catch`  子句中的参数类型。
>
> java中的程序发生错误分为两种: 
>
> 1. Error 错误  错误一般是代码书写问题，虚拟机执行是发生错误。
>
>    a.  一般的我们自己可以检查和处理
>
>    b.  严重的错误一般认为处理不了
>
> 2. Exception   异常

## 1. Exception  异常

> 程序执行发生错误。java很特殊，先编译在运行
>
> 异常也分为两类：
>
> 1. 检查时异常  编译的时候出现的异常 编译不会通过
> 2. 运行时异常 编译会通过  在执行的过程中可能会出现问题。  RuntimeException
> 3. 除了RuntimeExeption剩下的都是检查时异常
> 4. 检查时异常 我们一般需要自己解决保证程序编译通过。
> 5. 运行时异常我们必须要进行异常的处理。
>    + 捕捉异常  try  catch 异常
>    + 抛出异常
> 6. 出现异常程序会终止运行。

### 1.1 **异常处理的方式1  try catch:**

```java
package com.xdkj.javase.core.exception;

public class ExceptionDemo02 {

	public static void main(String[] args) {
		//method1();
		//method2();
		method3();
	}
	public static void method1() {
		//java.lang.ArithmeticException数学运算异常
				try {//可能会抛出异常的代码
					System.out.println(1/0);
					//catch是捕获代码可能会出现的异常对象
				}catch(ArithmeticException e) {
					//java.lang.ArithmeticException: / by zero
					//System.out.println(e);
					System.out.println("被除数不能为0");
					/// by zero  获取异常的信息
					System.out.println(e.getMessage());
					
					//e.printStackTrace();
				}		
	}
	public static void method2() {
		try {
			System.out.println(1/1);
		}catch(ArithmeticException e) {
			System.out.println(e.getMessage());
		}finally {//无论是否有异常 finally中的代码都会执行
				//后边的IO流中我们进行资源的关闭使用
				System.out.println("我们要执行了!!!!");
		}
		
	}
	public static void method3() {
		try {
			System.out.println(1/0);
		}finally {
			System.out.println("程序可能出现错误!!!");
		}
		
	}
}

```

###  1.2 异常的抛出处理

```java
package com.xdkj.javase.core.exception;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class ExceptionDemo03 {

	public static void main(String[] args) {
		//第一种是在catch语句中抛出异常
		// java虚拟机
		/*
		 * try { System.out.println(1/0); }catch(ArithmeticException e) { //抛出异常 throw
		 * e; }
		 */
		//method1();
		
		try {
			method1();
		}catch(RuntimeException e) {
			System.out.println("网络延迟");
		}
		//异常链
		try {
			method2();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (ArithmeticException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	//在方法中抛出异常
	//异常抛出 并不能解决异常存在的问题  
	//抛给虚拟机  虚拟机在抛出异常
	// 最后调用的方法去解决异常
	public static void method1() {
		throw new RuntimeException();
	}
	//异常从方法体抛出
	public static void method2() throws FileNotFoundException,ArithmeticException {
		InputStream  input = new FileInputStream("D:\\java");
		System.out.println(1/0);
	}
	public static void method3() throws FileNotFoundException,
		ArithmeticException,
		ArrayIndexOutOfBoundsException,
		NullPointerException{
		InputStream  input = new FileInputStream("D:\\java");
		System.out.println(1/0);
	}
		//异常从方法体抛出
		//使用大的异常接收小的多个异常  多态
		public static void method4() throws IOException,RuntimeException {
			//里面是小的异常 我们可以使用大的异常进行接收
			InputStream  input = new FileInputStream("D:\\java");
			System.out.println(1/0);
		}
}

```

### 1.3 继承关系中的异常

> 在继承关系中子类重写父类的方法 抛出的异常可以比父类方法抛出的异常小或者相等 ， 但是不能比父类方法的异常更大
>
> 儿子不能比父亲干的事情更坏。

```java
package com.xdkj.javase.core.exception;

public class Father {
	public void hello() throws ArithmeticException{
		
	}
	public static void main(String[] args) {
		Son son = new Son();
		System.out.println(son);
	}
}


```

```java
package com.xdkj.javase.core.exception;

public class Son extends Father {

	/*
	 * @Override public void hello() throws Exception {
	 * System.out.println("Hello Son"); }
	 */
	public static void main(String[] args) {
		Son son = new Son();
		son.hello();
	}
	
}

```

### 1.4 异常链 1.7的处理方式

+ 使用| 处理异常链
+ 使用同一个对象接受所有的异常信息

### 1.5 异常的自动关闭资源的处理方式



### 1.6 自定义异常(***)



