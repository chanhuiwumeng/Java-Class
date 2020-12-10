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

### 1.4 Finally的面试题

```java
package com.xdkj.javase.core.exception;
/**
 * 程序运行的机制:
 * 1. 从上到下 从左到右
 * 2. 有return  执行完成  方法终止  后边的代码不会执行
 * 3. try  和 finally 中都有return。  那么优先执行 finally中的
 * 		return;
 * 4. try中有return  finally中没有return 执行的是try中的return执行方法结束
 * 
 * */

public class ExceptionDemo4 {

	public static void main(String[] args) {
		System.out.println(method1());//100
	}
	@SuppressWarnings("finally")
	public static int method1() {
		int num = 100;
		try {
			System.out.println(num);
			return num;
		}finally {
			num ++;
		}
	}
	public static int method2() {
		int num = 100;
		try {
			System.out.println(num);
		}finally {
			num ++;
			return num ;
		}
	}
	public static int method3() {
		int num = 100;
		try {
			System.out.println(num);
			return num;
		}finally {
			num ++;
			return num ;
		}
	}
}

```

**描述final  finally finalize的区别:**

1. final修饰类不能被继承 修饰的方法不能被重写 修饰的变量是常量值不能被更改

2. finally是异常机制中的，在finally中的代码无论异常是否会发生都会执行。

3. finally中和try中如果都有return 语句那么优先执行finally中的return语句

4. finalize是Object类中定义的方法，强制GC进行垃圾回收，但是一个程序只能调用一次，即使强制调用,gc也不能

   立刻进行垃圾回收。

5. finalize() 方法是在垃圾收集器删除对象之前对这个对象调用的。 

### 1.5 异常链 1.8的处理方式

+ 使用 | 处理异常链
+ 使用同一个对象接受所有的异常信息

### 1.6 异常的自动关闭资源的处理方式

```java
package com.xdkj.javase.core.exception;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class ExceptionDemo05 {
	public static void main(String[] args) {
		
	}
	
	public static void method() {
		try {
			System.out.println(1/0);
			InputStream  in = new FileInputStream("D://");
		}catch(ArithmeticException | FileNotFoundException e) {
			e.printStackTrace();
		}
	}
	
	public static void method1() {
		InputStream  in = null;
		try {
			System.out.println(1/0);
		in = new FileInputStream("D://");
		}catch(ArithmeticException | FileNotFoundException e) {
			e.printStackTrace();
		}finally {
			try {
				in.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	//jdk1.7
	public static void method2() {
		//jdk1.7新加的  实现了AutoCloseable的类 资源类就可以自动关闭了
		try( InputStream  in  = new FileInputStream("D://");) {
			System.out.println(1/0);
		}catch(ArithmeticException | IOException e) {
			e.printStackTrace();
			} 
	}
}

```

### 1.7 有的异常不能抛只能处理

> 你的程序没有检查时异常 都是运行时异常我们可以将所有的异常全部抛出。最终交给最后的调用者去处理(一定要去处理)
>
> 还可以向外在继续的抛出，抛给JVM.   JVM在将错误的信息输出。
>
> 在实际开发的时候，要么自己手动处理异常，要么在最后一次调用的时候处理方法的异常，始终是要处理的，不要向虚拟机抛出。

```java
package com.xdkj.javase.core.exception;

public class ExceptionDemo06 {
	public static void main(String[] args) throws InterruptedException {
		method();
	}
	
	public static void method()   {
		new Runnable() {
			@Override
			public void run() {
					for(int i =0;i<=100;i++) {
						try {
                            //这里的异常只能处理不能抛出
							Thread.sleep(500);
						} catch (InterruptedException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName()+"---"+ i);
					}
			}
		};
	}
}

```

### 1.8 自定义异常(***)

> 我们在程序的开发中 如果们有自己遇到的问题那么我们可以进行自定义异常，在程序中抛出自定义的异常。

```java
package com.xdkj.javase.core.exception;

public class MyExceptionOne extends Exception {

	public MyExceptionOne() {
		super();
		// TODO Auto-generated constructor stub
	}

	public MyExceptionOne(String message, Throwable cause, boolean enableSuppression, boolean writableStackTrace) {
		super(message, cause, enableSuppression, writableStackTrace);
		// TODO Auto-generated constructor stub
	}

	public MyExceptionOne(String message, Throwable cause) {
		super(message, cause);
		// TODO Auto-generated constructor stub
	}

	public MyExceptionOne(String message) {
		super(message);
		// TODO Auto-generated constructor stub
	}

	public MyExceptionOne(Throwable cause) {
		super(cause);
		// TODO Auto-generated constructor stub
	}
	
}

```

```java
package com.xdkj.javase.core.exception;

import java.util.Scanner;

public class MyExceptionOneDemo {

	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		String name = s.next();
			try {
				method(name);
			} catch (MyExceptionOne e) {
				e.printStackTrace();
			}
	}
	public static void  method(String name) throws MyExceptionOne  {
		
		if(!name.equals("admin")) {
			throw new MyExceptionOne("用户名不正确!");
		}else{
			System.out.println("--------------");
		}
	}
}

```





