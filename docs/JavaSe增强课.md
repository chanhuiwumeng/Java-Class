# JavaSe增强课

## 1. JDK1.8接口

> 在前面的学习中我们知道在接口中只能有 常量和抽象方法
>
> 抽象方法必须被接口的实现类重写。
>
> 在JDK1.8中重新定义了接口中的方法:
>
> 1. 抽象方法  抽象方法必须被实现类重写
> 2. 静态方法  static修饰
> 3. 默认方法  default修饰的方法  default修饰的方法 不用在实现类中重写   实现类的对象可以直接调用
> 4. 静态方法  抽象方法  默认的方法可以定义多个。

```java
package com.xdkj.javase.oop09;

public interface Eat {
	void eat();
	
	static void hello() {
		System.out.println("人都是要吃食物的!");
	};
	
	default void say() {
		System.out.println("人都是要说话的");
	}
}

class  Demo1 implements Eat{

	@Override
	public void eat() {
		System.out.println("eat  rice!");
	}
	
}

```

```java
package com.xdkj.javase.oop09;

import java.util.Comparator;

public class EatDemo {

	public static void main(String[] args) {
		Demo1  demo1  = new Demo1();
			demo1.eat();
			demo1.say();
			Eat.hello();
	}

}

```

## 2. 正则表达式

