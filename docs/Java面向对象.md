# Java面向对象

## 1. 面向对象和面向过程的比较

### 1.1  面向过程

做一碗西红柿鸡蛋面: (自己做)

​		买菜----->洗菜---->切菜----->炒菜------>和面---->擀面----->切面------>煮面----->放调料-----吃

上面的这些步骤我们都要自己去参与。

每一个步骤都要去自己实现。

### 1.2 面向对象

​	吃一碗西红柿鸡蛋面:

​	手机---->app--->点外卖---->取餐--->吃

面怎么做的我们不必要知道我们只要结果就可以了。

手机:  

app:

商家:  做面 对于我没呢来说商家将做饭的这些步骤进行自己的封装。我们不要知道做饭的过程和步骤。

商家就是一个对象。对象就是对过程的一个封装。

面向对象就是对面向过程的一个封装。

面向对象是什么?

​	面向对象是一种思想，不是一种技术。

生活中我们面对的一切都是对象。

java底层封装的很多东西就是c语言的东西。

## 2. 什么是类和对象

在代码中我们怎么来体现面向对象呢?

### 2.1 类

	>  交通工具是一个抽象的概念。包含的东西特别多。交通工具他是一个类。
	>
	>  人类: 抽象的概念。
	>
	>  类: 类是具有相同属性和行为的同一种事务的描述，抽象的概念。
	>
	>  人类的描述。
	>
	>  ​	属性: 肤色  体重 身高  语言 
	>
	>  ​	行为: 跑 跳  走  睡...
	>
	>  在代码中怎么去体现呢?
	>
	>  class 文件叫  类  public  class 类名{
	>
	>  }
	>
	>  在java中类文件使我们编程的最小的单位。类文件的名称  类名是对我们代码的一个属性和行为的总称。
	>
	>  怎么使用代码表现人的属性和行为呢?
	>
	>  ​		属性:  我们使用变量来描述类的属性
	>
	>  ​		行为:  使用方法来体现行为
	>
	>  对象: 对象是类的现实存在的事务的体现。
	>
	>  ​	我们通过new 关键字来对类进行实例化；所谓的实例化就是在堆内存中开辟属于类对象的独有的内存空间
	>
	>  ​	类可以实例化多个对象。每一个对象new的空间的地址值是不一样的。
	>
	>  ​	通过.(的的意思)来进行对象的属性的调用  并且可以对属性进行赋值 或者获取属性的值
	>
	>  ​		调用对象的行为  我们在类中定义的方法。

```java
/**
 *  人的类  class Person 就代表人类的描述的类
 * 
 * */
public class Person {
	//类属性
	//名字
	String  name ;
	//年龄
	int age;
	//身高
	double height;
	//体重
	double weight;
	//类的行为
	public void say() {
		System.out.println(" say hello!");
	}
}
```

```java
public class PersonDemo {

	public static void main(String[] args) {
		//对类的实例化
		//对类类型的对象的创建
		Person zhangsan = new Person();
		//com.xdkj.javase.oop.Person@15db9742
		System.out.println(zhangsan);
		//.意思就是的的意思
		//new 在堆内存开辟空间 属性是变量 有数据类型 保存的是默认值
		System.out.println(zhangsan.name);//null
		System.out.println(zhangsan.age);//0
		System.out.println(zhangsan.height);//0.0
		System.out.println(zhangsan.weight);//0.0
		//对象调用方法
		zhangsan.say();
		//类可以实例化多个对象
		Person  lisi = new Person();
		//com.xdkj.javase.oop.Person@6d06d69c
		System.out.println(lisi);
		
		//属性进行赋值
		lisi.name = "李四";
		lisi.age = 28;
		lisi.height = 175.0;
		lisi.weight = 150.0;
		
		System.out.println(lisi.name);
		System.out.println(lisi.age);
		System.out.println(lisi.height);
		System.out.println(lisi.weight);
		//对象.方法名();
		lisi.say();
	}

}
```

## 3. JAVA的面向对象

### 3.1 封装

> 在java中我们的封装:
>
> 1. 项目的封装  对一个项目的业务功能的封装
>
> 2. 包的封装 相同描述或者类型的代码的封装
>
> 3. 类的封装 把一个类的属性和行为进行封装
>
> 4. 类的属性我们要进行私有化  对外提供公开的访问方式  get set方法
>
>    a. 代码功能的完整性
>
>    b. 减少代码的耦合 (高内聚 低耦合)
>
> 5. 对行为功能的封装  方法

```java
public class Person2 {
	//进行属性的私有化
	private String name;
	private int age;
	private double height;
	
	//提供属性的公开的访问方式
	//获取属性的值
	public String getName() {
		return this.name;
	}
	//设置属性的值
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return this.age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	
	public double getHeight() {
		return this.height;
	}
	public void setHeight(double height) {
		this.height = height;
	}
	
	public void say() {
		System.out.println("say Hello  World");
	}
}

```

```java
public class Person2Demo {

	public static void main(String[] args) {
		//类的实例化
		Person2 p = new Person2();
			p.setName("李四");
		System.out.println(p.getName());
			p.say();
		
		Person2 person = new Person2();
			person.setName("王五");
			person.setAge(88);
			person.setHeight(180.0);
		System.out.println(person.getName() + " " +person.getAge()+ "  "+ person.getHeight());	
		
		person.say();
	}
}
```

#### 3.1.1 构造器

> 构造器就是我们常见类的实例化对象时候的模板(模具)。
>
> 在Java中每一个类都有一个默认的无参构造器，隐式的构造器。看不见，但是是默认提供的。
>
> 1. 构造器不是方法   没有返回值类型  和修饰符  
> 2. 构造器的名称必须和类名一致 (都是大驼峰命名法)
> 3. 构造器是可以重载的
> 4. 如果使用了带参数的构造器 无参数的构造器必须手动写出来。不然带参数的构造器会覆盖无参数的构造器
> 5. 虽然无参数的构造器是默认的并且是隐式的 ， 但是我们要去在编程中必须手动写出无参数的构造器
> 6. 在使用带参数的构造器的时候，实际传入的参数的数据类型和构造器中属性顺序值必须一致。

```java
package com.xdkj.javase.oop01;

public class Dog {
	private String dogName;
	private int dogAge;
	private String dogColor;
	
	//默认的无参构造器
	/*
	 * public Dog() {
	 * 
	 * }
	 */
	//从超级类继承的构造器
	public Dog() {
	}
	
	//构造器的重载
	public Dog(String dogName) {
		this.dogName = dogName;
	}
	

	public Dog(String dogName, String dogColor) {
		this.dogName = dogName;
		this.dogColor = dogColor;
	}

	public Dog(String dogName, int dogAge, String dogColor) {
		this.dogName = dogName;
		this.dogAge = dogAge;
		this.dogColor = dogColor;
	}


	public String getDogName() {
		return dogName;
	}
	public void setDogName(String dogName) {
		this.dogName = dogName;
	}
	public int getDogAge() {
		return dogAge;
	}
	public void setDogAge(int dogAge) {
		this.dogAge = dogAge;
	}
	public String getDogColor() {
		return dogColor;
	}
	public void setDogColor(String dogColor) {
		this.dogColor = dogColor;
	}
	
}

```

```java
package com.xdkj.javase.oop01;

public class DogDemo {

	public static void main(String[] args) {
		//我们使用的是无参数的构造器实例化对象
		Dog dog = new Dog();
			System.out.println(dog);
			//null
			System.out.println(dog.getDogName());
			
		Dog dog1 = new Dog("阿黄");
		
		System.out.println(dog1.getDogName());//阿黄
		
		Dog dog2 = new Dog("黄色","汤姆");
		System.out.println(dog2);
		System.out.println(dog2.getDogName() + "  "+ dog2.getDogAge()+ " " + dog2.getDogColor());
	}

}

```

**Eclipse自动生成get set方法和 构造器**

> 快捷键: shift + alt + s

<img src="_media/image-20201126102523586.png" width="300px">

<img src ="./_media/image-20201126102651062.png" width="300px">

#### 3.1.2 this关键字

> this关键字 叫做当前类的实例化对象引用   谁用就代表谁。

```java
		//类类型的变量
		Student stu = new Student();
			System.out.println(stu);
			stu.setStuAge(18);
			stu.setStuName("小明");
		System.out.println(stu.getStuName() + "今年"+ stu.getStuAge()+"岁");
		
		Student stu1 = new Student();
			System.out.println(stu1);
			stu1.setStuAge(16);
			stu1.setStuName("小红");
		System.out.println(stu1.getStuName()
```



![image-20201126094425542](_media/image-20201126094425542.png)

#### 3.1.3 JavaBean

> javaBean我们也叫作一个普通的java对象(Plain Old Java Object)。对对象所在的类有这么几个要求:
>
> 1. 必须有私有 的成员变量(成员属性)
> 2. 必须给私有的成员变量提供公开的访问方式  get  set 方法
> 3. 必须有无参数的构造器。带参数的构造器看实际的需要 ，需要的时候在添加。

#### 3.1.4 static关键字

> static  静态  
>
> 静态的东西属于当前的类(在谁里面声明就属于谁)。
>
> ​	可以修饰 属性: 
>
> ​	可以修饰方法:
>
> static修饰的属性或者方法:
>
> 1. 在类被编译的时候就放置到了内存的静态区中  只有一份
> 2. 静态的内容可以直接使用类名进行访问(要求必须使用类名进行访问  )
> 3. 静态的东西属于类 (类的二进制字节码文件对象)
> 4. 静态的属性 代表对象共有的属性 并且 静态的属性在声明的时候要给初始值
> 5. 静态的属性名要求所有字母大写多个单词使用下划线隔开。 

![image-20201126105250393](_media/image-20201126105250393.png)

```java
package com.xdkj.javase.oop01;

public class Cat {
	
	private String catName;
	private int catAge;
	private String catColor;
	//静态的成员变量代表所有对象共有的属性
	
	static String  ADDRESS_EARTH = "中国";
	
	public Cat() {
		super();
	}
	public Cat(String catName, int catAge, String catColor) {
		super();
		this.catName = catName;
		this.catAge = catAge;
		this.catColor = catColor;
	}
	public String getCatName() {
		return catName;
	}
	public void setCatName(String catName) {
		this.catName = catName;
	}
	public int getCatAge() {
		return catAge;
	}
	public void setCatAge(int catAge) {
		this.catAge = catAge;
	}
	public String getCatColor() {
		return catColor;
	}
	public void setCatColor(String catColor) {
		this.catColor = catColor;
	}
	
	//声明 了一个静态的成员方法
	public static void eatFish() {
		System.out.println("cat eat fish!");
	}
	//普通的成员方法
	public void miao() {
		System.out.println("Miao  miao");
	}
	
}

```

```java
package com.xdkj.javase.oop01;

import java.util.Calendar;

public class CatDemo {
	public static void main(String[] args) {
		Cat  cat = new Cat();
			cat.setCatName("汤姆");
			cat.setCatAge(100);
			cat.setCatColor("蓝色");
			System.out.println(cat);
			System.out.println(cat.getCatName() + " " + cat.getCatAge() + " " + cat.getCatColor());
			//警告  静态的方法应该使用静态的访问方式
			cat.eatFish();
			cat.miao();
			
			Cat  cat1 = new Cat();
			cat1.setCatName("柯基");
			cat1.setCatAge(20);
			cat1.setCatColor("白色");
			System.out.println(cat1);
			System.out.println(cat1.getCatName() + " " + cat1.getCatAge() + " " + cat1.getCatColor());
			//警告  静态的方法应该使用静态的访问方式
			cat1.eatFish();
			cat1.miao();
			//正确访问静态方法的方式
			Cat.eatFish();
			//class com.xdkj.javase.oop01.Cat
			System.out.println(Cat.class);
			//调用类的静态属性
			System.out.println(Cat.ADDRESS_EARTH);
	}
}

```

#### 3.1.5 final关键字

> final 关键字 是最终的意思
>
> 1. final修饰变量 值不可以被改变  就是常量
> 2. final修饰方法  方法不能被重写
> 3. final修饰类 类不可以被继承

#### 3.1.6 匿名对象

> 没有名字的对象就是匿名对象，new Object() 匿名对象只能使用一次在使用完成以后就从内存中释放掉了

```java
public class Teacher {
	private String teaName;
	private int teaAge;
	
	public Teacher() {
		super();
		// TODO Auto-generated constructor stub
	}
	
	public Teacher(String teaName, int teaAge) {
		super();
		this.teaName = teaName;
		this.teaAge = teaAge;
	}
    ...get set...
}
```



```java'
package com.xdkj.javase.opp02;

public class TeacherDemo {

	public static void main(String[] args) {
		
			Teacher  teacher = new Teacher();
				System.out.println(teacher);
				teacher.setTeaName("马丁路德金");
				teacher.setTeaAge(88);
			System.out.println(teacher.getTeaName() +  "  " +  teacher.getTeaAge());
			//匿名对象  就是没有名字的对象  也就是不用变量去接收他
			//com.xdkj.javase.opp02.Teacher@6d06d69c
			System.out.println(new Teacher());
			//是不是匿名对象的使用?
			//匿名对象只在调用的当前行有效  匿名对象是一次性的
			// 就是
			String str = 	new Teacher("张无忌",888).getTeaName();
			
			int    age =    new Teacher("张无忌",888).getTeaAge();
			System.out.println(str);
			System.out.println(age);
			//对象的生命周期
			//匿名对更多是用在方法的参数
			
			method(teacher);
			method(new Teacher());
			method(new Teacher("张三丰",999));
	}
	//类类型的参数
	public static void method(Teacher teacher) {
		System.out.println(teacher.getTeaName());
	}

}

```

#### 3.1.7 变量的作用域

+ 全局变量

+ 局部变量

+ 成员变量和成员方法

+ 静态成员方法和静态成员属性

  ```java
  package com.xdkj.javase.opp02;
  
  import java.util.Calendar;
  
  /**
   * 变量: 
   * 	a. 全局变量
   * 		声明在类的属性的位置  全局变量可以被类中的所有方法使用
   * 		全局变量的生命周期是什么?
   * 			当声明的全局变量的类不在被引用的时候我们就确定类不在被使用了，但是GC也不会立即回收
   * 				
   * 	b. 局部变量
   * 		局部变量的生命周期就是方法执行完成以后从内存中释放。
   * 	c. 局部变量和全局变量同名的时候  使用就近原则
   * 
   *  d.  .java文件中的静态内容在编译时候就放置到静态区内存中  .class文件中的静态的常量在类被调用或者
   *  	导入的时候放置到静态的内存区中
   * */
  public class VariableDemo {
  	//全局变量
  	static int num = 100;
  	public static void main(String[] args) {
  		int num = 200;
  		System.out.println(num);
  		method();
  		VariableDemo vd = new VariableDemo();
  		System.out.println(vd);
  		//空
  		vd = null;
  		//就近原则
  		System.out.println(num);
  		
  		System.out.println(Calendar.DATE);
  		
  	}
  	public static void method() {
  		System.out.println(num);
  	}
  }
  
  ```

#### 3.1.8 代码块

```java
package com.xdkj.javase.opp02;

/**
 * 代码块: {} 包裹起来的就是代码块 
 * 		全局的代码块: 在类的对象被调用的时候被执行 全局的代码块是最先被执行的
 * 		局部代码块: 就是写在方法内部的代码块 
 * 			其实实际的作用就是代码的隔离。
 * 		静态代码块: static 修饰的代码块。
 * 				静态代码块优先执行  在类被编译的时候就执行了
 * 				static修饰的东西只有一份 静态代码块中只能使用static修饰的内容。
 * 				设计模式:
 * 					单例设计模式 
 */
public class BlockDemo {

	private String name;
	
	int age ;

	public BlockDemo() {
		super();
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	// 全局代码块
	{
		System.out.println("Hello World");
		age = 100;
		System.out.println(age);
	}
	static {
		//System.out.println("Hello static block" + age);
	}
	public void hello() {
		int num = 999;
		System.out.println("Hello ---------------" );
		//局部代码块
		{
			int m = 888;
			System.out.println(num);
			System.out.println("Hello ++++++++++++++" + age);
		}
		System.out.println("Hello ==================");
	}

}

```

### 3.2 继承

> 继承：
>
> ​	在我们的生活中，见到的汽车，人，动物....都有继续的特性。
>
> ​	遗传的特性。 子承父业。
>
> ​	如果我们当前 的类定义了属性和行为， 动物Animal定义了动物的属性和行为。
>
> ​		属性:  重量   颜色   
>
> ​		行为:  吃 喝  睡 
>
> ​	那么对于动物的子类:  哺乳动物  脊椎动物 卵生动物 无脊椎动物....他们就默认从动物的类去继承这些特性和行为就可以了。
>
> 在java中我们，如果我们在一个类中定义了属性和行为  那么他的子类就直接继承就可以了，不要在自己去定义了。
>
> ​		extends 关键字就是继承的意思:
>
> 1. 子类继承自父类  那么子类就具有类父类的属性和行为
> 2. 子类继承父类 那么子类也可以对自己的属性和行为进行扩增
> 3. java中只能单继承 一个类只能继承一个类。
> 4. Java我们可以实现多层继承  a> b  b > c
> 5. super关键字 

```java
package com.xdkj.javase.oop3extends;

public class Animals {
	
	private String name;
	private double weight;
	private String color;
	.....get set ...
	public void eat() {
		System.out.println("eat foods!");
	}
	public void sleep() {
		System.out.println("sleep letter!");
	}
}

```

```java
package com.xdkj.javase.oop3extends;

public class Dog extends Animals {
	//我们虽然继承了一个类但是我们可以对当前类的属性进行扩增
	private int footer;

	public int getFooter() {
		return footer;
	}

	public void setFooter(int footer) {
		this.footer = footer;
	}
	
	public void lookDoor() {
		System.out.println("看门");
	}
}

```

```java
package com.xdkj.javase.oop3extends;

public class Fish  extends Animals{
	private String fin;//鳍

	public String getFin() {
		return fin;
	}

	public void setFin(String fin) {
		this.fin = fin;
	}
	
	public void swimming() {
		System.out.println("fish can swimming");
	}
}

```

```java
package com.xdkj.javase.oop3extends;

public class Keji  extends Dog{
	
}

```

```java
package com.xdkj.javase.oop3extends;

public class AnimalsDemo {
	public static void main(String[] args) {
		Animals animals = new Animals();
		System.out.println(animals);
			animals.setName("小狗");
			animals.setWeight(15.00);
			animals.setColor("黄色");
		System.out.println(animals.getName() +" "+ animals.getWeight() + " "+ animals.getColor());	
			animals.eat();
			animals.sleep();
		Dog  dog = new Dog();
		
		System.out.println(dog);
			dog.setName("旺财");
			dog.setWeight(35.00);
			dog.setColor("黑白色");
		System.out.println(dog.getName() + "--"+ dog.getWeight() + "---"+ dog.getColor());
			dog.eat();
			dog.sleep();
			
			dog.setFooter(4);
			dog.lookDoor();
			
			Fish  fish = new Fish();
				fish.setName("金龙鱼");
				fish.setWeight(3.0);
				fish.setColor("红加金色");
				fish.setFin("三个");
				fish.eat();
				fish.sleep();
				fish.swimming();
		System.out.println(fish.getName() + "--"+ fish.getWeight()+"--"+fish.getColor()+"--"+fish.getFin());		
				
	}
}

```

####  3.2.1 **Super关键字:**

> super: 代表父类的引用
>
> super 关键字必须在构造器的第一行
>
> super是隐式的。默认就是在构造的一行样  隐藏的  手动写出会覆盖默认的
>
> super()代表父类的无参数的构造器调用

![image-20201130100554578](_media/image-20201130100554578.png)

```java
package com.xdkj.javase.oop04;

public class Person {
	
	private String name;
	private int age;
	private double height;
	private String address;
	
	
	  public Person() {
		  //Object()
		  super();
	  }
	 
	public Person(String name, int age, double height, String address) {
		super();
		this.name = name;
		this.age = age;
		this.height = height;
		this.address = address;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public double getHeight() {
		return height;
	}
	public void setHeight(double height) {
		this.height = height;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	
	public void eat() {
		System.out.println("eat foods!!!");
	}
	
}

```

```java
package com.xdkj.javase.oop04;

public class PersonDemo {
	public static void main(String[] args) {
		//可以使用父类的无参数的构造器
		System.out.println(new Person());
		//使用父类带参数的构造器
		Person person = new Person("张三",25,150.0,"陕西省西安市");
			System.out.println(person);
			System.out.println(person.getName() + " " + person.getAge() + " " + person.getAddress() );
			person.eat();
			
		//子类的无参数的构造器	
		Man man = new Man();
			man.setName("李四");
			man.setAge(24);
			man.setHeight(120.0);
			man.setAddress("宝鸡市");
		System.out.println(man);
		System.out.println(man.getName() + " "+ man.getAge() + " "+ man.getAddress());
			man.eat();	
			
			Man m = new Man("赵六",88,150.0,"咸阳市");
				System.out.println(m);
				System.out.println(m.getName() + "  " + m.getAge() + " " + m.getHeight() + " "+ m.getAddress());
				
			Man m1 = new Man("小六子",18,120.0,"咸阳市");
				System.out.println(m1);
				System.out.println(m1.getName() + "  " + m1.getAge() + " " + m1.getHeight() + " "+ m1.getAddress());
				
	}
}

```

#### 3.2.3 方法的重写

> 方法的重写: 
>
> 1. 必须要有继承关系
> 2. 子类对父类的方法进行重写  方法的声明一样  但是方法的实现不一样

**方法的重载和方法的重写的区别(overload  @Override):**

1. 方法的重载必须是在同一个类中 方法名称相同 参数列表不同(类型，个数,顺序) 与返回值无关
2. 方法的重写 必须有继承关系  子类对对类的方法进行重写  重写的方法声明一致 方法的实现不同。

#####  3.2.1.1**Super关键字和this的区别**

> 1. this代表当前类的实例化对象  谁用就代表谁
>
> 2. super代表父类的引用  
>
>    a. 在没有继承关系的无参数的构造器的第一行  super()代表  Object超类的无参数的构造器
>
>    b. 在继承关系的无参数或者带参数的构造器的第一行 super()代表父类的无参数的构造器 
>
>    c. super永远都在第一行  一般super是隐式的，可以手动写出。

#### 3.2.3 Object

> 类 `Object` 是类层次结构的根类。每个类都使用 `Object`  作为超类。所有对象（包括数组）都实现这个类的方法。
>
> Object只有一个无参数的构造器 ，默认被所有的类继承。

+ toString()  输出对象本质就是在使用对象调用toString() 

  + getClass().getName() + '@' + Integer.toHexString(hashCode())

  + Object中建议所有子类重写toString()方法是为了方便查看对象的属性值。

```java
@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + ", height=" + height + ", address=" + address + "]";
	}
```

#### 3.2.4 equals和 == 的区别

1. equals 比较的对象必须是同一种类 类型的对象
2. 类的equals方法必须进行重写 比较对象之间的属性值是否相等
3. Object 类中的equals的本质是==比较对象的堆内存的地址值
4. instanceof 关键字    obj  instanceOf  类类型  判断obj是否是 类类型的实例化对象或者类类型的子类的实例化对象
5. 当此方法被重写时，通常有必要重写 hashCode 方法，以维护 hashCode 方法的常规协定，该协定声明相等对象必须具有相等的哈希码
6.  hashCode 方法的常规协定: 如果根据 equals(Object) 方法，两个对象是相等的，那么对这两个对象中的每个对象调用 hashCode 方法都必须生成相同的整数结果。

![image-20201130114413552](_media/image-20201130114413552.png)

![image-20201130114553223](_media/image-20201130114553223.png)

```java
@Override
	public boolean equals(Object  obj) {
		// 传入的是Student  方法原生的参数类型是Object
		// 先去判断类型是否一致 再比较
        if (this == obj)
			return true;
		if (obj == null)
			return false;
		if(! (obj instanceof Student) ) {
			return false;
		}
		//类型相同在比较其他的
		Student  stu =(Student) obj;
		//这里的equals是被String类重写过的equals方法
		return this.getName().equals(stu.getName()) && 
				this.getAge() == stu.getAge() &&
				this.getAddress().equals(stu.getAddress());
	}
	
	
	@Override
	public int hashCode() {
		//String 类中重写了hashCode方法
		//按道理来说这样写是没有问题的
		return this.name.hashCode()*12+188 + this.age + this.address.hashCode()*31+99;
	}
```

**自动生成equals和hashcode方法:**

```java
@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((address == null) ? 0 : address.hashCode());
		result = prime * result + age;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Student other = (Student) obj;
		if (address == null) {
			if (other.address != null)
				return false;
		} else if (!address.equals(other.address))
			return false;
		if (age != other.age)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}
```

### 3.3 访问修饰符

> 在一个源码文件中只能有一个public class 类

```java
public class Student extends Person {
	
}
class Person{
	
}

class Teacher {
	
}
```

![image-20201201105611622](_media/image-20201201105611622.png)

### 3.4 多态

### 3.5 抽象类和抽象方法

### 3.6 接口

## 3.7 内部类

+ 全局内部类
+ 局部内部类
+ 静态内部类
+ 匿名内部类(lambda表达式)



