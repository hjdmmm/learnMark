# MyBatis框架简介

## 三层架构

区分MVC架构模式

界面层(表现层)：接收用户数据用servlet，显示处理结果用jsp，springmvc框架

业务逻辑层：service类---spring框架

数据访问层(持久层)：dao类---mybatis框架

业务逻辑层和数据访问层在MVC中都属于Model层

## 框架的作用以及常见框架

### 前端框架

1. 前端开发用的框架：(jQuery只是一个类库，还没有庞大到是框架)，Angular.js，React.js，Vue.js
2. 前端UI框架：Extjs，jquery ui，**easy ui**，**bootstrap(最火爆，没有之一)**，layui

### 后端框架

老三样：SSH：struts/struts2，spring，hibernate

新小子：SSM：SpringMVC，Spring，MyBatis

### 表现层框架(Controller)

struts，xwork，struts2，**springMVC**

### 持久层框架(Dao)

Hibernate，ibatis，MyBatis 

### 整合框架

EJB，**spring**

## MyBatis

对JDBC几乎所有的数据库操作进行了封装(加载驱动，创建connection，创建statement，手动设置参数，结果集检索等繁琐操作)，使开发者只需要关注SQL语句本身

1. sql mapper：sql映射，把表中一行数据映射为一个java对象
2. DAOs：数据访问，对数据库

# MyBatis vs 纯JDBC

1. 获取连接，得到statement，rs，关闭资源非常麻烦

   解决：使用SqlSession解决一切

2. 将sql写死在java代码中，修改sql语句，需要重新编译

   解决：将sql语句写在xml配置文件中

3. 向PreparedStatement对占位符的位置设置参数时，非常非所

   解决：MyBatis自动将java对象映射到sql语句，通过statement中的parameterType定义输入参数类型

4. 解析结果集时需要把字段的值设置到相应的实体类属性名中

   解决：MyBatis自动将sql执行结果映射到java对象中，通过statement中的resultType定义输出结果的类型

# 配置文件

mybatis一共有两种配置文件：mybatis-config.xml，Xxx(实体类名)Mapper.xml

## mapper

namespace属性：命名空间，不同的mapper映射文件使用namespace来区分，namespace不允许重复，一般是dao接口的全名

mapper标签是mapper映射文件最顶级的标签，以下mapper映射文件中的标签都是mapper的子标签

## 增删改查标签

标签内写sql语句不用分号

### 标签属性

id属性必写，一般值为接口中的方法名称直接复制粘贴大小写一致不带括号

insert，update，delete一般只写id属性

select标签的parameterType属性为基本数据类型+字符串时可以不写，自动识别；其实不是的时候也可以不写，因为底层是反射机制会自己去对应接口找参数类型

select标签的resultType属性必写，对于resultType，其实不仅可以返回一个该类型，当对象有多个时，还可以返回一个该类型的List，需要我们接收的时候自行判断

能用domain类来封装结果是最好的；但是有的时候用domain封装不了，比如按照姓名分组，查询出来每一个姓名对应的人数，就不能用domain封装结果值，因此要用map封装，map本身也是一个容器，可以放很多个键值对；很多个map又存在List中返回

resultMap属性：用于指定使用的resultMap

### where

动态sql

#### if

where必搭配if使用，会自动屏蔽第一个if条件前的and

### foreach

数组增加查询条件

## resultMap

当数据库字段名称与domain类属性名称不一样时，可以给数据库字段名称起别名；或者使用resultMap标签(与增删改查标签同级，都在mapper管辖下)，

id属性：将来在使用到resultMap标签的时候，用id定位

type属性：domain类名

### id和result

id标签用来配置主键的对应关系

result标签用来配置普通字段对应关系

如tbl_student表有一个主键，两个普通字段；那resultMap字段中就写一个id自字段，两个result子字段

property属性：类属性名

column属性：数据表中字段名

## sql

制作sql片段，简单的字符串拼接

id属性：定位

如select * from tbl_student

在select中用include标签引用



Xxx(实体类名)Mapper(Dao).xml

---

mybatis-config.xml



## configuration

这是主配置文件中最顶级的标签

以下标签都是它的子标签

## plugins

必须放在environments标签前

#### plugin

interceptor属性：全类名

## environments

### environment

#### transactionManager

type属性：JDBC，由JDBC管理事务；MANAGED，由某个服务器管理事务

#### dataSource

type属性：POOLED，使用连接池，mybatis会创建PooledDataSource类；UNPOOLED，不使用连接池，在每次执行sql语句，先创建连接，执行sql，再关闭连接；JNDI，java命名和目录服务，即windows注册表中寻找

##### property

数据库连接信息

## properties

导入配置文件

用于把数据库连接信息存放在一个.properties文件，和MyBatis主配置文件分开，目的是便于修改，保存，处理多个数据库信息

resource属性：文件地址

用${}调用

## settings

设置与数据库交互的环境，例如可以在此处配置二级缓存，配置查询延迟加载策略等，配置的目的是为了更加有效的查询表中的记录

实际项目中基本不用，因为其对查询的优化基本没用

## typeAliases

为类起别名

### typeAliase

type属性：表示为哪个domain起别名

alias属性：别名

### package

批量起别名，MyBatis默认取好的，别名为类名，不区分大小写

name属性：表示哪个包

## mappers

### mapper

resource属性：文件地址

class属性：找到dao层接口的全路径(适用于Dao层写实体类Dao.xml的地方)

### package

批量注册

name属性：dao类路径

# 基本步骤

1. 加入对maven的依赖
2. 创建Dao接口
3. 创建mapper文件
4. 创建mybatis主配置文件
5. 使用SqlSession的实例对象
6. 用sqlSession.getMappper(dao.class)创建出dao接口的实现类和其的一个对象
7. 调用dao实例的方法执行数据库操作

# MyBatis动态代理

MyBatis动态代理是MyBatis根据dao接口，自动创造出一个dao接口的实现类，和该类的实例对象

1. dao接口名和mapper文件名要一致
2. namespace要和dao接口的全名一致
3. 标签的id值要和dao接口的方法名称一致
4. 通过dao中方法的返回值确定调用SqlSession的方法：返回值是List，调用selectList()方法；返回值是int或非List时，调用insert()等方法
5. dao接口不要写重载方法

# 事务机制

MyBatis默认情况下是开启事务机制的，需要我们手动提交事务

openSession(true)可以得到一个开启自动提交机制的SqlSession

# 类

1. Resources：读取主配置文件
2. SqlSessionFactoryBuilder：用于建造SqlSessionFactory
3. SqlSessionFactory：这位更是重量级，一个项目一个就够了，用来获取SqlSession，SqlSessionFactory接口的实现类DefaultSqlSessionFactory
4. SqlSession：SqlSession接口定义了操作数据的方法，SqlSession接口的实现类DefaultSqlSession。使用要求SqlSession不是线程安全的，需要在方法内部使用，在执行sql语句之前，用openSession()获取SqlSession，执行完毕后，用SqlSession.close()，保证它的使用是线程安全的

# 传参

一般只能传入一个参数，因此查询条件多的时候使用domain，领域对象；多表联查的时候使用map集合(然而阿里巴巴开发手册明确禁止使用)

#{}相当于?，用PreparedStatement，底层使用setInt()，setString()等方法，因此字符串自带引号(而不是反引号)，不能用于拼接表名和字段名

${}相当于Statement，有sql注入的风险，但常用来order by的时候输入表名

## 注解方式传入多个参数

使用@Param命名参数

```java
//dao接口中
public User selectUserByUsernameAndPassword(@Param("username") String username, @Param("password") String password);
```

```xml
<!--mapper文件中-->
<select id="selectUserByUsernameAndPassword" resultType="...">
	select count(*) from t_user where username=#{username} and password=#{password}
</select>
```

## 使用对象

完整用法：#{属性名, javaType=java中的属性的数据类型, jdbcType=在数据库中属性的类型}

## 按位置传入多个参数

之前用#{0}方式，从MyBatis3.4开始使用#{arg0}方式

```java
//dao接口中
public User selectUserByUsernameAndPassword(String username, String password);
```

```xml
<!--mapper文件中-->
<select id="selectUserByUsernameAndPassword" resultType="...">
	select count(*) from t_user where username=#{arg0} and password=#{arg1}
</select>
```



## 模糊查询

'%${value}%'，${}是字符串拼接，直接输出字符串，因此默认不带引号

%#{value}%，会变成%'刘'%，不行

直接在value加入%%，这是java中的字符串拼接，可以，但是耦合度高

where name like '%'空格#{value}空格'%'，空格绝对不能省，这是mybatis的字符串拼接

# 输出结果

## resultType

简单类型：七种基本类型及他们的包装类+String

其他类型

建议用全类名，别用别名

如果返回java.util.HashMap，推荐接的时候用Map<Object, Object>来接，返回一个Map，key是列名，value是列值

## resultMap

是mapper的一个子标签和select等增删改查标签的属性，常用于数据表字段名和实体类属性名不一致的情况或多表联查的情况，详见配置文件中的介绍

其实很常用，比如数据库字段名为stu_name，而领域对象中属性名为stuName

resultMap和resultType二选一

# 列名和属性名不一致

1. 使用列名
2. 使用resultMap

# 动态sql

sql的内容是变化的，可以根据条件获取到不同的sql语句，主要变化的是where部分

## OGNL语言

Object-Graph Navigation Language是一种表达式语言(EL)，简单来说就是一种简化了的java属性取值语言，这里不展开说明

## if标签

```xml
<if test="name != null and name != '' ">
    and name = #{name}
</if>
```

## where标签

用来包含多个if标签，当有一个成立时，会自动增加一个where关键字，并去掉if中多余的and，or等

## foreach标签

循环java中的数组和List集合，主要用在sql的in语句中，学生id是

```java
public List<Student> selectFor(List<Integer> idList);

//
    List<Integer> list = new ...;
    list.add(1001);
    list.add(1002);
    list.add(1003);
    dao.selectFor(list);
```

```xml
<!--
想要的效果
select * from student where id in (1001, 1002, 1003)
-->
<select id="selectFor" resultType="List">
	select * from t_student where id in
    
    <!--collection填array或list-->
    <!--item取到的值名称-->
    <!--open插入字符串的起始字符；close插入字符串的结束字符-->
    <!--separator用什么分割值-->
    <foreach collection="list" item="myid" open="(" close=")" separator=",">
    	#{myid}
    </foreach>
</select>
```

# PageHelper

数据分页

使用步骤：

1. maven加依赖
2. mybatis主配置文件中在environments标签前加入plugins标签

