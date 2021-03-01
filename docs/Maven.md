# Maven

> Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

## 1. Maven使用简介

+ 解决项目jar包的使用问题
+ 项目分模块开发
+ 项目合并
+ 代码仓库提交
+ 仓库管理

Maven的主要目标是使开发人员能够在最短的时间内理解开发工作的完整状态。为了实现此目标，Maven处理了几个令人关注的领域：

- 简化构建过程
- 提供统一的构建系统
- 提供优质的项目信息
- 鼓励更好的开发实践

### 1.1 下载maven

![image-20210226150910141](_media/image-20210226150910141.png)

**不要使用最新版本**

![image-20210226151758500](_media/image-20210226151758500.png)

### 1.2 配置环境变量

![image-20210226151948422](_media/image-20210226151948422.png)

![image-20210226152134379](_media/image-20210226152134379.png)

![image-20210226152243664](_media/image-20210226152243664.png)

## 2.Maven的初体验

MavenDemo

+ src
  + main
    + java
    + resources

​	|test

​	|pom.xml



![image-20210226153230538](_media/image-20210226153230538.png)

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
	
  <groupId>com.xdkj</groupId>
  <artifactId>Maven-Demo</artifactId>
  <version>1.0</version>
</project>
```

### 3. Maven的生命周期

+ compile 编译
+ test  测试
+ packge  打包
+ deploy 部署
+ run 运行
+ install 所有命令的集合

![image-20210226153935142](_media/image-20210226153935142.png)

## 3. 仓库地址变更

![image-20210226154232894](_media/image-20210226154232894.png)

![image-20210226154422890](_media/image-20210226154422890.png)

## 4.Maven 和IDEA 配置

![image-20210301100231914](_media/image-20210301100231914.png)

![image-20210301100344094](_media/image-20210301100344094.png)

![image-20210301100420713](_media/image-20210301100420713.png)

![image-20210301100513444](_media/image-20210301100513444.png)

![image-20210301100852827](_media/image-20210301100852827.png)

### 3.2 Maven WEB项目

![image-20210301101525170](_media/image-20210301101525170.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.xdkj</groupId>
  <artifactId>maven-demo-03</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>maven-demo-03 Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <finalName>maven-demo-03</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

### 3.3 修改pom.xml默认配置

![image-20210301101908579](_media/image-20210301101908579.png)

### 3.4 新的项目设置maven 

![image-20210301102046314](_media/image-20210301102046314.png)

![image-20210301102132355](_media/image-20210301102132355.png)

## 5.Eclipse Maven配置

![image-20210301111155996](_media/image-20210301111155996.png)

![image-20210301111247499](_media/image-20210301111247499.png)

![image-20210301111323831](_media/image-20210301111323831.png)

![image-20210301111342634](_media/image-20210301111342634.png)

![image-20210301111434906](_media/image-20210301111434906.png)

![image-20210301111724374](_media/image-20210301111724374.png)

![image-20210301111812282](_media/image-20210301111812282.png)

![image-20210301111827975](_media/image-20210301111827975.png)

![image-20210301111851965](_media/image-20210301111851965.png)

![image-20210301112045430](_media/image-20210301112045430.png)

![image-20210301112109465](_media/image-20210301112109465.png)

![image-20210301112204171](_media/image-20210301112204171.png)