# Mybatis

## 1.Mybatis简介

> MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
>
> Mybatis是一款持久层的ORM(Object relation mapping 对象关系映射)框架, 对数据做CRUD操作就是使用java的pojo做CRUD操作。
>
> 对象就是使用java的pojo封装数据库的table ,关系 只要对pojo做CRUD操作就去改变数据库的表，映射  pojo---表 pojo的属性对应表的字段。
>
> ORM: Mybatis 是一款半自动的ORM框架  sql语句自己写
>
> ​	 Hibernate 是一款全自动的ORM框架  不用自己写sql语句

## 1.1 Mybatis下载和使用

![image-20210329154042089](_media/image-20210329154042089.png)

### 1.1.2 Mybatis-helloWold

![image-20210329161645631](_media/image-20210329161645631.png)

**mybatis.cfg.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--数据源环境-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/hehe"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    <!--接口 的 映射文件  -->
    <mappers>
        <!--资源加载-->
        <mapper resource="com/xdkj/dao/StudentDao.xml"/>
    </mappers>
</configuration>
```

**pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.xdkj</groupId>
    <artifactId>mybatis-01</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.49</version>
        </dependency>
        <!--导入mybatis核心jar-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.5</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.10</version>
        </dependency>
        <!--加入日志jar-->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.27</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.27</version>
        </dependency>
    </dependencies>
    <!--配置maven 的资源加载路径-->
        <build>
            <resources>
                <resource>
                    <directory>src/main/java</directory>
                    <includes>
                        <include>**/*.xml</include>
                    </includes>
                </resource>
            </resources>
        </build>
</project>
```

**Student.java**

```java
package com.xdkj.beans;

import lombok.*;

/**
 * ClassName Student
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-03-29-15:45
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
@RequiredArgsConstructor
public class Student {
    private int id;
    @NonNull
    private String name;
    @NonNull
    private String sex;
    @NonNull
    private int age;
    @NonNull
    private String birth;
    @NonNull
    private String department;
    @NonNull
    private String address;
}

```

**StudentDao.java**

```java
package com.xdkj.dao;

import com.xdkj.beans.Student;

import java.util.List;

public interface StudentDao {
    List<Student> queryALl();
    Student  queryById(int id);
    int addStudent(Student student);
    int updateStudent(Student student);
    int deleteStudent(int id);
}

```

**StudentDao.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--命名空间-->
<mapper namespace="studentDao">
<!--查询语句 resultType是查询出一行的结果封装的类型-->
    <select id="selectAll" resultType="com.xdkj.beans.Student">
            select * from student
    </select>
</mapper>
```

**StudentDaoImpl.java**

```java
package com.xdkj.dao.impl;

import com.xdkj.beans.Student;
import com.xdkj.dao.StudentDao;
import com.xdkj.util.MyBatisUtil;
import org.apache.ibatis.session.SqlSession;

import java.util.List;

/**
 * ClassName StudentDaoImpl
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-03-29-15:48
 */
public class StudentDaoImpl  implements StudentDao {
    //获取Mybatis的核心工具类
private SqlSession  session = MyBatisUtil.getSqlSession();
    @Override
    public List<Student> queryALl() {
        //去找哪一个命名空间中的sql语句来执行
        List<Student> list = session.selectList("studentDao.selectAll", Student.class);
        return list;
    }

    @Override
    public Student queryById(int id) {
        return null;
    }

    @Override
    public int addStudent(Student student) {
        return 0;
    }

    @Override
    public int updateStudent(Student student) {
        return 0;
    }

    @Override
    public int deleteStudent(int id) {
        return 0;
    }
}

```

**MybstisUtil.java**

```java
package com.xdkj.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * ClassName MyBatisUtil
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-03-29-15:53
 */
public class MyBatisUtil {
    //SqlSession工厂
    private static SqlSessionFactory  sqlSessionFactory;
    //加载配置文件 获取数据源和映射文件
    //单例的模式
    static{
        //SqlSessionFactoryBuilder 工厂构建器
        //加载配置文件获取输入流
        try {
            InputStream  in = Resources.getResourceAsStream("mybatis.cfg.xml");
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(in);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
    //返回Mybatis的核心工具对象
    public  static  SqlSession  getSqlSession(){
        return  sqlSessionFactory.openSession();
    }
}

```

**SqlSessionTest.java**

```java
package com.xdkj.mybstis.test;

import com.xdkj.beans.Student;
import com.xdkj.dao.StudentDao;
import com.xdkj.dao.impl.StudentDaoImpl;
import org.junit.Test;

import java.util.List;

/**
 * ClassName SqlSessionTest
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-03-29-16:05
 */
public class SqlSessionTest {
    private StudentDao studentDao = new StudentDaoImpl();
    @Test
    public void queryAll(){
        List<Student> students = studentDao.queryALl();
        for (Student student : students) {
            System.out.println(student);

        }
    }
}

```

**log4j.properties**

```properties
# 全局日志配置
log4j.rootLogger=DEBUG, stdout
# MyBatis 日志配置
log4j.logger.org.mybatis.example.BlogMapper=TRACE
# 控制台输出
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n
```



