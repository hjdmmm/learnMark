# JDBC是什么

Java Database Connectivity(Java语言连接数据库)

本质上是SUN公司指定的一套接口，指定Java类与关系型数据库服务器之间沟通规则，在java.sql包下

MySQL数据库厂家编写的JDBC接口的实现类(一大堆class文件)，就叫MySQL驱动

所有的驱动都是以jar包(Java Archive File，与zip文件区别在于多了一个META-INF/MANIFEST.MF文件)的形式存在，去数据库官网下载

# JDBC类与接口介绍

1. java.sql.DriverManager类：负责将Driver(驱动)注册
2. java.sql.Connection接口：负责管理Java工程与数据库服务器之间的连接通道
3. java.sql.PreparedStatement接口：负责管理在连接通道上进行往返交通的交通工具
4. java.sql.ResultSet接口：负责管理数据库服务器返回的临时表

# 注册驱动

1. 去数据库官网下载对应的驱动
2. 在环境变量classpath中载入驱动的jar包

# JDBC编程六步

1. 注册驱动，告诉Java程序连接哪个品牌的数据库
2. 获取连接，表示JVM进程和数据库进程之间的通道打开了，
3. 获取数据库操作对象，专门执行SQL语句
4. 执行SQL语句
5. 处理查询结果集(当第四步是select语句时)
6. 释放资源

注意：

- 如果取了别名，列的名称，不是表中的列的名称，而是查询结果集的列的名称
- getString(第几列)从1数起，事实上JDBC所有下标均以1开始
- SQL语句不用写";"
- 获取的连接和资源(包括conn，stat，rs等)，属于进程间的通信，使用完一定要关闭
- rs.next()会返回true或false，用while循环来获取数据

# SQL注入

在输入密码时加上 or '1' = '1，也显示登录成功

用户输入的数据使得原SQL语句的含义被篡改

解决方法：

使用PreparedStatement(预编译的数据库操作对象)代替Statement

## 对比PreparedStatement和Statement

- Statement存在SQL注入问题，P不会
- Statement是编译一次执行一次，P是编译一次执行N次，因此P的效率更高
- P在编译阶段有类型安全检查

总之，业务方面要求实现SQL注入(SQL语句拼接时)，才使用Statement

# 与事务有关

在步骤2后写conn.setAutoCommit(false);

在try块末尾加conn.commit();

在catch块中加conn.rollback();

# DAO封装

DataBase Access Object：数据库访问对象

作用：数据库访问对象在开发时提供针对某张表的操作细节(增删改查)

优点：在管理系统开发时，用过DAO可以避免反复的SQL命令书写和反复的JDBC开发步骤书写

DAO类：提供数据库访问对象的类

## 开发规则

1. 一个DAO类封装的就是一张表的操作细节
2. 命名规则：表名+Dao EmpDao，DeptDao
3. 所在包名：公司名称.dao hjdmmm.dao

# 实体类

1. 一个实体类用于描述一张表结构
2. 实体类的类名应该与关联的表名保持一致，但是可以忽略大小写：DEPT.frm ---> public class Dept{}
3. 实体类的属性应该与关联的表文件字段保持一致：DEPT INT --> private Integer deptNo
4. 实体类的一个实例对象用于在内存中存储对应的表文件中一个数据行

