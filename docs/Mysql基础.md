# Mysql基础

## 1. 数据库

> 数据库是“按照数据结构来组织、存储和管理数据的仓库”。是一个长期存储在[计算机](https://baike.baidu.com/item/计算机/140338)内的、有组织的、可共享的、统一管理的大量数据的集合
>
> 数据长久存储的集合。
>
> 在数据库的发展历史上，数据库先后经历了层次数据库、网状数据库和关系数据库等各个阶段的发展，数据库技术在各个方面的快速的发展

## 2. 数据库的分类

### 2.1 关系型数据库

+ Oracle  全球最大的商业使用的收费数据库厂商。
+ Mysql  是免费的数据库  已经被oracle收购了
+ mariadb  永久免费的mysql替代品
+ 阿里巴巴mysql 
+ h2 内存数据库  jar
+ sqlServer 微软的数据库 

### 2.2 非关系型数据库(NoSql数据库)

+ redis
+ mogodb
+ HBase

## 3.Mysql的简介

> MySQL是一个**[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)****，**由瑞典MySQL AB 公司开发，属于 [Oracle](https://baike.baidu.com/item/Oracle) 旗下产品。MySQL 是最流行的[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)之一，在 WEB 应用方面，MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (Relational Database Management System，关系数据库管理系统) 应用软件之一。
>
> MySQL是一种关系型数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。
>
> MySQL所使用的 SQL 语言是用于访问[数据库](https://baike.baidu.com/item/数据库/103728)的最常用标准化语言。MySQL 软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，尤其是[开放源码](https://baike.baidu.com/item/开放源码/7176422)这一特点，一般中小型网站的开发都选择 MySQL 作为网站数据库。

### 3.1 Mysql的下载

![image-20210106103646933](_media/image-20210106103646933.png)

![image-20210106103732644](_media/image-20210106103732644.png)

![image-20210106103843341](_media/image-20210106103843341.png)

![image-20210106104047609](_media/image-20210106104047609.png)

### 3.2 Mysql的安装

![image-20210105170800063](_media/image-20210105170800063.png)

![image-20210105170924738](_media/image-20210105170924738.png)

![image-20210105170952515](_media/image-20210105170952515.png)

![image-20210105171021379](_media/image-20210105171021379.png)

![image-20210105171116639](_media/image-20210105171116639.png)

![image-20210105171205293](_media/image-20210105171205293.png)

![image-20210105171306858](_media/image-20210105171306858.png)

![image-20210105171418430](_media/image-20210105171418430.png)

![image-20210105171630134](_media/image-20210105171630134.png)

![image-20210105171704751](_media/image-20210105171704751.png)

![image-20210105171723990](_media/image-20210105171723990.png)

![image-20210105171741297](_media/image-20210105171741297.png)

![image-20210105171836737](_media/image-20210105171836737.png)

![image-20210105172104926](_media/image-20210105172104926.png)

![image-20210105172220697](_media/image-20210105172220697.png)

![image-20210105172425230](_media/image-20210105172425230.png)

![image-20210105172525513](_media/image-20210105172525513.png)

![image-20210105172539130](_media/image-20210105172539130.png)

![image-20210105172637482](_media/image-20210105172637482.png)

### 3.3 Mysql的卸载

传统的控制面板卸载可以卸载软件不会清除注册表，不会卸载MYSQL57服务

使用一些专用的卸载工具去卸载可以清除注册表再次安装的时候就没有问题。

## 4. Mysql的使用

### 4.1 连接到Mysql数据库

+ mysql -uroot -hlocalhost -p  在输入数据库的密码
+ exit退出mysql命令客户端

![image-20210106110044044](_media/image-20210106110044044.png)

```sql
 mysql -uroot -p
Enter password: ****
```

### 4.2  查看Mysql 默认的数据库

> show databases;

```sql
mysql> show databases;     
+--------------------+     
| Database           |     
+--------------------+     
| information_schema |     
| atcrowdfunding     |     
| atcrowdfunding01   |     
| cloud              |     
| clouddb01          |     
| clouddb02          |     
| clouddb03          |     
| liuyishou          |     
| manager            |     
| mybookshop         |     
| mysql              |     
| performance_schema |     
| project            |     
| sys                |     
| xdcrm              |     
| xdkjexam           |     
+--------------------+     
16 rows in set (0.01 sec)  
```

![image-20210106111208622](_media/image-20210106111208622.png)

> 可以袭击配置Data和编码等

### 4.3 选择使用数据库和查看数据库中的表

```sql
mysql> use mysql;
Database changed
mysql> show tables;
+---------------------------+
| Tables_in_mysql           |
+---------------------------+
| columns_priv              |
| db                        |
| engine_cost               |
| event                     |
| func                      |
| general_log               |
| gtid_executed             |
| help_category             |
| help_keyword              |
| help_relation             |
| help_topic                |
| innodb_index_stats        |
| innodb_table_stats        |
| ndb_binlog_index          |
| plugin                    |
| proc                      |
| procs_priv                |
| proxies_priv              |
| server_cost               |
| servers                   |
| slave_master_info         |
| slave_relay_log_info      |
| slave_worker_info         |
| slow_log                  |
| tables_priv               |
| time_zone                 |
| time_zone_leap_second     |
| time_zone_name            |
| time_zone_transition      |
| time_zone_transition_type |
| user                      |
+---------------------------+
31 rows in set (0.00 sec)
```

### 4.4 数据库的创建

```sql
mysql> create database haha;
Query OK, 1 row affected (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| atcrowdfunding     |
| atcrowdfunding01   |
| cloud              |
| clouddb01          |
| clouddb02          |
| clouddb03          |
| haha               |
| liuyishou          |
| manager            |
| mybookshop         |
| mysql              |
| performance_schema |
| project            |
| sys                |
| xdcrm              |
| xdkjexam           |
+--------------------+
17 rows in set (0.00 sec)
```

### 4.5 表的创建和表的查看

```sql
mysql> create table student(
    -> name varchar(20),
    -> age int(11)
    -> );
Query OK, 0 rows affected (0.02 sec) 
                          
mysql> show tables;       
+----------------+        
| Tables_in_haha |        
+----------------+        
| student        |        
+----------------+        
1 row in set (0.00 sec)   
```

### 4.6 查看表的物理结构

```sql
mysql> desc student;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

### 4.7 查看表的创建时的语句

```sql
mysql> show create table student;
+---------+-------------------------------------------------------------------------------------------------------------------------------+
| Table   | Create Table                                                                                                                  |
+---------+-------------------------------------------------------------------------------------------------------------------------------+
| student | CREATE TABLE `student` (
  `name` varchar(20) DEFAULT NULL,
  `age` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
+---------+-------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

### 4.8 查看表的数据

```sql
mysql> select * from student;
Empty set (0.00 sec)
```

### 4.9 表中插入数据

```sql
mysql> insert into student values("admin",18),("joke",88);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from student;
+-------+------+
| name  | age  |
+-------+------+
| admin |   18 |
| joke  |   88 |
+-------+------+
2 rows in set (0.00 sec)
```

### 4.10 Mysql注意的地方:

1. Mysql的sql语句末尾加分号;
2. 一般情况下Mysql中的所有单词小写
3. 有的时候我们在添加的时候 表名，字段名 数据库名 使用驼峰命名法
4. 表名字段名多个单词组成使用_隔开
5. 因为Mysql学习中命令很多建议写个记事本
6. 语句先在记事本中写完，检查没问题再在mysql命令端复制粘贴运行。

