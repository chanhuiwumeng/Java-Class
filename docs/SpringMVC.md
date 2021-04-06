# SpringMVC

## 1.SpringMVC简介

> 传统的web开发早期我们是基于servlet和jsp技术 servlet我们只能在doGET  doPost中处理业务，页面跳转重定向，响应数据。
>
> struts2 技术，框架 大量的配置和struts.xml 当spring出现以后，spring是一个容器，ioc di aop的核心思想。所以就基于Spring容器 开发出了SpringMVC.
>
> 他不是一个新的技术，他是一个Spring的web模块、核心的DispactherServlet 基于servlet-api研发的。
>
> Web阶段的开发模式结构:
>
>  m  model 模型  处理数据业务  beans dao service
>
> v  view jsp html thymleaf freemark
>
> c controller servlet作为controller

+ spring-web
+ spring-webmvc

![image-20210402164141485](_media/image-20210402164141485.png)

![](./_media/Snipaste_2021-04-02_16-26-37.png)

**pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.xdkj</groupId>
    <artifactId>spring-mvc-01</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <!--springmvc相关的jar-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.5.RELEASE</version>
    </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
    </dependencies>
</project>
```

**web.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--配置Spring的配置文件-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath*:spring-beans.xml</param-value>
    </context-param>
    <!--配置spring环境加载监听器-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!--配置SpringMVC的核心servlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!--springmvc配置文件-->
            <param-value>classpath*:spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <!--springmvc请求路径  会把请求和静态资源都拦截下来-->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

**spring-beans.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

**spring-mvc.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
       <!--请求转发的路径-->
        <bean id="/first" class="com.xdkj.controller.FirstController"></bean>
        <context:component-scan base-package="com.xdkj.controller"></context:component-scan>
    <!--试图解析器-->
    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

</beans>
```

**FirstController.java**

```java
package com.xdkj.controller;

import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.Arrays;
import java.util.List;

/**
 * ClassName FirstController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-02-16:04
 */
public class FirstController implements Controller {


    @Override
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response)
            throws Exception {
        //模拟数据库获取的数据
        List<String> list = Arrays.asList("Hello","World","spring","Mybatis");
        //模型和视图
        ModelAndView  modelAndView = new ModelAndView();
                modelAndView.setViewName("list");
                modelAndView.addObject("list",list);
        return modelAndView;
    }
}

```

**SecondController.java**

```java
package com.xdkj.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

import java.util.Arrays;
import java.util.List;

/**
 * ClassName SecondController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-02-16:27
 */
@Controller
public class SecondController {


    @RequestMapping("/second")
    public ModelAndView second(){
        List<String> list = Arrays.asList("Hello","World","spring","Mybatis");
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("list");
        modelAndView.addObject("list",list);
        return modelAndView;
    }
}

```

**list.jsp**

```jsp
<%--
  Created by IntelliJ IDEA.
  User: chanh
  Date: 2021/4/2
  Time: 16:08
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>list</title>
</head>
<body>
    ${list}
    <hr>
    <img src="1.jpg" alt="">
</body>
</html>

```

## 2.SpringMVC生命周期

### 2.1 生命周期

![image-20210406160029599](_media/image-20210406160029599.png)

1. 客户端发送请求到DispatcherServlet
2. Dispactherservlet 调用MappedHandler 去查找处理器适配器
3. 处理器适配器去调用处理器处理请求
4. 处理器返回ModelAndView给DispactherServlet
5. DispactherServlet根据ModelAndView去找视图解析器 是否有合适的视图
6. 试图存在就解析视图路径
7. 带着数据去页面渲染。

### 2.2 SpringMVC默认的配置文件

**DispactherServlet.properties**

```properties
# Default implementation classes for DispatcherServlet's strategy interfaces.
# Used as fallback when no matching beans are found in the DispatcherServlet context.
# Not meant to be customized by application developers.

org.springframework.web.servlet.LocaleResolver=org.springframework.web.servlet.i18n.AcceptHeaderLocaleResolver

org.springframework.web.servlet.ThemeResolver=org.springframework.web.servlet.theme.FixedThemeResolver

org.springframework.web.servlet.HandlerMapping=org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping,\
	org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping,\
	org.springframework.web.servlet.function.support.RouterFunctionMapping

org.springframework.web.servlet.HandlerAdapter=org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter,\
	org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter,\
	org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter,\
	org.springframework.web.servlet.function.support.HandlerFunctionAdapter


org.springframework.web.servlet.HandlerExceptionResolver=org.springframework.web.servlet.mvc.method.annotation.ExceptionHandlerExceptionResolver,\
	org.springframework.web.servlet.mvc.annotation.ResponseStatusExceptionResolver,\
	org.springframework.web.servlet.mvc.support.DefaultHandlerExceptionResolver

org.springframework.web.servlet.RequestToViewNameTranslator=org.springframework.web.servlet.view.DefaultRequestToViewNameTranslator

org.springframework.web.servlet.ViewResolver=org.springframework.web.servlet.view.InternalResourceViewResolver

org.springframework.web.servlet.FlashMapManager=org.springframework.web.servlet.support.SessionFlashMapManager
```

## 3. SpringMVC注解开发

![image-20210406175352631](_media/image-20210406175352631.png)

**父项目的pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.xdkj</groupId>
    <artifactId>spring-mvc-demo</artifactId>
    <!--打包方式是pom-->
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>spring-mvc-03</module>
    </modules>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <junit.version>4.12</junit.version>
    </properties>
    <!--规定子模块的jar版本依赖和插件等-->
   <dependencyManagement>
       <dependencies>
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>${junit.version}</version>
               <scope>test</scope>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-core</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-context</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-context-support</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-aop</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-test</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-web</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-webmvc</artifactId>
               <version>5.2.5.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>javax.servlet</groupId>
               <artifactId>javax.servlet-api</artifactId>
               <version>4.0.1</version>
           </dependency>
           <dependency>
               <groupId>jstl</groupId>
               <artifactId>jstl</artifactId>
               <version>1.2</version>
           </dependency>
           <dependency>
               <groupId>org.projectlombok</groupId>
               <artifactId>lombok</artifactId>
               <version>1.18.10</version>
           </dependency>
       </dependencies>
   </dependencyManagement>
</project>
```

**spring-mvc-03.pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>spring-mvc-demo</artifactId>
        <groupId>com.xdkj</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>
    <artifactId>spring-mvc-03</artifactId>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
        </dependency>
        <!--jackson springmvc默认集成的json数据处理的jar-->
    </dependencies>

</project>
```

**spring-mvc.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
        <!--组件扫描-->
    <context:component-scan base-package="com.xdkj"></context:component-scan>
    <!--视图解析器-->
    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
     <!--注解驱动  springmvc中注解驱动是 自动适配 映射处理器 适配器
        注解驱动可以自动帮助我们进行数据的json准换
     -->
    <mvc:annotation-driven></mvc:annotation-driven>
</beans>
```



**web.xml**

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0">

  <display-name>Archetype Created Web Application</display-name>
  <!--服务器容器启动的时候就加载Spring的配置信息-->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath*:spring-core.xml</param-value>
  </context-param>
  <!--上下文加载的监听器-->
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <servlet>
    <servlet-name>springMvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath*:spring-mvc.xml</param-value>
    </init-param>
    <!--服务器启动的时候就加载-->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>springMvc</servlet-name>
    <!--/ 拦截所有的请求  请求和静态资源的请求-->
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```

**FirstController.java**

```java
package com.xdkj.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;

import java.util.Arrays;

/**
 * ClassName FirstController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-06-16:39
 */
@Controller
//@RequestMapping("/first")
public class FirstController {
    /*请求映射 根据页面的请求路径找到方法去处理*/
    @RequestMapping(value = "/hello")
    public ModelAndView hello(){
        ModelAndView modelAndView = new ModelAndView();
            modelAndView.setViewName("list");
            modelAndView.addObject("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        return modelAndView;
    }

    @RequestMapping("/world")
    public ModelAndView world(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("list");
        modelAndView.addObject("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        return modelAndView;
    }
    //path  请求路径 value请求的路径名称  method请求方式  produces响应头格式
    @RequestMapping(value = "/helloWorld",method = RequestMethod.GET,produces = "text/html;charset=utf8")
    public ModelAndView helloWorld(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("list");
        modelAndView.addObject("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        return modelAndView;
    }

    //path  请求路径 value请求的路径名称  method请求方式  produces响应头格式
    @RequestMapping(value = "/haha",method = RequestMethod.GET,produces = "application/json;charset=utf8")
    public ModelAndView haha(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("list");
        modelAndView.addObject("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        return modelAndView;
    }
}

```

**SecondController.java**

```java
package com.xdkj.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.servlet.ModelAndView;

import java.util.Arrays;

/**
 * ClassName SecondController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-06-17:05
 */
@Controller
@RequestMapping("/second")
public class SecondController {

    @RequestMapping(value = "/hello")
    public ModelAndView hello(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("list");
        modelAndView.addObject("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        return modelAndView;
    }


}

```

**ThreeController.java**

```java
package com.xdkj.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

/**
 * ClassName ThreeController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-06-17:14
 */
@Controller
public class ThreeController {
    //使用传统的servletAPI 处理请求
    //传统的servlet-api不会走springmvc配置的字节的视图解析器
    @GetMapping("/list")
    public void handlerRequest(HttpServletRequest request , HttpServletResponse response)
            throws ServletException, IOException {
        //添加数据和页面跳转
        request.setAttribute("list", Arrays.asList("Spring","SpringMVC","Servlet"));
        request.getRequestDispatcher("/WEB-INF/jsp/list.jsp").forward(request,response);
    }

    @GetMapping("/info")
    public void info(HttpServletRequest request , HttpServletResponse response)
            throws ServletException, IOException {
        //添加数据和页面重定向
        request.getSession().setAttribute("list",Arrays.asList("Spring","SpringMVC","Servlet"));
        //WEB_INF下的页面不能直接访问
        //请求重定向
        response.sendRedirect("list");
    }
    //接收参数  处理请求
    @GetMapping("/param")
    public void handlerParam(HttpServletRequest request , HttpServletResponse response)
            throws ServletException, IOException {
        String name = request.getParameter("name");
        String age = request.getParameter("age");
        System.out.println(name +"------"+ age);
        //添加数据和页面重定向
        request.getSession().setAttribute("list",Arrays.asList("Spring","SpringMVC","Servlet"));
        //WEB_INF下的页面不能直接访问
        //请求重定向
        request.getRequestDispatcher("/WEB-INF/jsp/list.jsp").forward(request,response);
    }
}

```

**FourController.java**

```java
package com.xdkj.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

import javax.servlet.http.HttpServletRequest;

/**
 * ClassName FourController
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-04-06-17:28
 */
@Controller
public class FourController {

    @GetMapping("/one")
    public  String  one(){
        //在springmv中我们可以返回一个视图的名字 他会被视图解析器解析 进行页面跳转
        return  "list";
    }

    @GetMapping("/two")
    public  String  two(HttpServletRequest request){
        //在springmv中我们可以返回一个视图的名字 他会被视图解析器解析 进行页面跳转
        request.setAttribute("list","数据展示！！！！！！");
        return  "list";
    }

    @GetMapping("/three")
    public  String  three(Model model){
        //在springmv中我们可以返回一个视图的名字 他会被视图解析器解析 进行页面跳转
        model.addAttribute("list","Model 数据传输！！");
        return  "list";
    }
    //页面传输的所有数据都是字符串
    //参数的自动数据类型转换  基本数据类型
    @GetMapping("/four")
    public  String  four(String name,int age){
        //在springmv中我们可以返回一个视图的名字 他会被视图解析器解析 进行页面跳转
        System.out.println(name+"---------"+age);
        return  "list";
    }
    /*@RequestParam 别名映射  获取到的值赋给后边的变量*/
    @GetMapping("/five")
    public  String  five(@RequestParam("name") String username, @RequestParam("age") int userage){
        //在springmv中我们可以返回一个视图的名字 他会被视图解析器解析 进行页面跳转
        System.out.println(username+"---------"+userage);
        return  "list";
    }
}

```

**index.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
    <h2>Hello World!</h2>
    <a href="hello">FirstController Hello方法处理请求</a>
    <br>
    <a href="world">FirstController World</a>
    <br>
    <a href="helloWorld">FirstController HelloWorld</a>
    <br>
    <a href="haha">FirstController haha</a>
    <br>
    <a href="second/hello">SecondController haha</a>
    <br>---------------servlet-api处理请求-----<br>
    <a href="list">ThreeController list</a>
    <br>
    <a href="info">ThreeController info</a>
    <br>
    <a href="param?name=admin&age=123">ThreeController param</a>
    <br>--------------返回视图名称--------------<br>
    <a href="one">FourController one</a>
    <br>
    <a href="two">FourController two</a>
    <br>
    <a href="three">FourController three</a>
    <br>
    <a href="four?name=admin&age=12">FourController four</a>
    <br>
    <a href="five?name=admin&age=12">FourController five</a>
</body>
</html>

```

**list.jsp**

```jsp
<%--
  Created by IntelliJ IDEA.
  User: chanh
  Date: 2021/4/6
  Time: 16:49
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>list</title>
</head>
<body>
<h3>List Page!!!!!</h3>
    ${list}
</body>
</html>
```





