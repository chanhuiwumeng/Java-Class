# Spring

## 1. Spring简介

>Spring框架是由于[软件开发](https://baike.baidu.com/item/软件开发/3448966)的复杂性而创建的。Spring使用的是基本的JavaBean来完成以前只可能由[EJB](https://baike.baidu.com/item/EJB/144195)完成的事情。然而，Spring的用途不仅仅限于服务器端的开发。从简单性、可测试性和松耦合性角度而言，绝大部分Java应用都可以从Spring中受益。
>
>◆目的：解决企业应用开发的复杂性
>
>◆功能：使用基本的JavaBean代替EJB，并提供了更多的企业应用功能
>
>◆范围：任何Java应用
>
>Spring是一个轻量级控制反转(IoC)和面向切面(AOP)的容器框架。

### 1.1 什么是EJB

> EJB是的Enterprise Java Beans技术的简称, 又被称为企业Java Beans。这种技术最早是由美国计算公司研发出来的。EJB技术的诞生标志着Java Beans的运行正式从客户端领域扩展到服务器领域。在[电子商务](https://baike.baidu.com/item/电子商务/98106)领域运用EJB技术可以简化应用系统的开发, 这是由该技术的结构和特点所决定的。
>
> 我们在WEB阶段我们发现我们所有的Servlet只要被放置在了服务器的容器中我们既可以不用自己去创建Servlet接口的实现类的实例化对象。不需要手动在new对象和引用对象。
>
> EJB太依赖与服务器了。没有服务器就不可能是实现其他的类的自动创建，(IOC  DI).发现除了我们的Servlet接口的实现类。其他的都不能实现EJB规范。

### 1.2 Spring官网

![image-20210322143307232](_media/image-20210322143307232.png)

![image-20210322143621831](_media/image-20210322143621831.png)

![image-20210322144042097](_media/image-20210322144042097.png)

![image-20210322144128763](_media/image-20210322144128763.png)

![image-20210322144227400](_media/image-20210322144227400.png)

### 1.3 Spring模块

![image-20210322145020811](_media/image-20210322145020811.png)

### 1.4 Spring-HelloWorld

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.xdkj</groupId>
    <artifactId>spring-helloworld</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
        <!--spring的核心的jar包导入-->
    <dependencies>
        <!--core 核心-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <!--上下文-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <!--test测试jar包-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <!--aop切面-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <!--ioc di 的jar-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>

    </dependencies>
</project>
```

**Student.java**

```java
public class Student {
    private Integer id;
    private String name;
    private String address;
    -----get  set ------
}
```

**spring-beans.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--spring是一个容器  容器自动帮助我们进行对象的实例化
    score bean的作用域 默认是单例模式
      prototype 获取一次new一个对象-->
    <bean id="student" class="com.xdkj.spring.beans.Student" scope="singleton"></bean>
</beans>
```

**SpringTest.java**

```java
package com.xdkj.spring.test;

import com.xdkj.spring.beans.Student;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * ClassName SpringTest
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-03-22-15:00
 */
public class SpringTest {
    public static void main(String[] args) {
        //Student  stu = new Student();
        //加载spring核心的配置文件  启动Spring容器  类路径  编译后的classes文件夹
        ApplicationContext context  = new ClassPathXmlApplicationContext("classpath:spring-beans.xml");
        //就是ioc
      Student student =   context.getBean("student", Student.class);
        Student student1 =   context.getBean("student", Student.class);
      //com.xdkj.spring.beans.Student@42e26948
        System.out.println(student);
        System.out.println(student1);
    }
}
```

