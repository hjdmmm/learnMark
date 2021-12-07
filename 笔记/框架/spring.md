# spring简介

spring，springMVC，springboot，spring cloud称为spring全家桶

spring出现在2002年左右，解决企业开发的问题，减少项目模块之间的关系，类与类之间的管理的难度，帮助开发人员创建对象，管理对象之间的关系。实现模块之间和类之间的解耦合

spring核心技术是ioc，aop

## 非侵入式

Spring框架的API不会在业务逻辑上出现，即业务逻辑是pojo(普通java对象，如不实现框架的接口等，很普通)，由于业务逻辑中没有Spring的API，所以业务逻辑可以从Spring框架快速的移植到其他框架

## 依赖

类A使用了类B的属性和方法，叫做类A依赖类B

## 框架怎么学

1. 框架能干什么。mybatis——访问数据库，对标中数据执行增删改查
2. 框架的语法。框架要完成一个功能，需要一定的步骤支持
3. 框架的内部实现。源码
4. 实现一个框架。

# bean.xml

## beans

### context:component-scan

spring扫描遍历base-package指定的包，把包中和子包中所有的类的注解找出来，按照注解的功能创建对象，或给对象赋值

base-package属性：注解在项目中的包名

### import

用于设置多个配置文件

优势：

1. 每个文件的大小比合成一个文件要小得多，效率高
2. 避免多人竞争带来的冲突

分配方式：

1. 通常一个模块一个配置文件，学生考勤模块一个配置文件，学生成绩一个配置文件
2. 按类的功能分，数据库相关的一个配置文件，事务的功能一个配置文件，servlet一个配置文件

resource属性：其他配置文件的路径，" classpath: "表示类路径(class文件所在的目录)，最好加上；可以使用通配符(*)

### bean

id属性：对象的自定义名称，唯一值，spring通过这个名称找到对象

class属性：类的全名，不能是接口

autowire属性：实现spring为引用数据类型的属性自动赋值，可填byName和byType

#### property

调用对象的setter

name属性：属性名字

value属性：属性值，无论是什么类型，值都必须用引号括起来，这是xml文件的规定

ref属性：bean的id，除string类以外的引用数据类型

ps：Resource类型的属性赋值仍然用value

#### constructor-arg

调用类的有参构造

index属性：第几个参数

name属性：属性名字

value属性：属性值

ref属性：bean的id

### aspectj-autoproxy

自动配置aop

proxy-target-class属性：默认为false，改为true则强制有接口时使用cglib动态代理

# di

实现方式有两种：

1. 在spring配置文件中使用标签和属性完成，称为基于XML的di实现
2. 使用spring中的注解，完成属性赋值，称为基于注解的di实现

语法分类：

1. set注入(设置注入)：spring调用类的set()方法，完成属性的赋值
2. 构造注入：spring调用类的有参构造方法，完成属性赋值
3. 自动注入：spring按照某些规则，给引用类型自动完成赋值

spring中规定java八大基本数据类型+String都是简单类型

放到容器中的对象：dao类，service类，controller类，工具类

spring中的对象默认都是单例的，在容器中叫这个名称的对象只有一个

不放入到spring容器中的对象：实体类对象，servlet，listener，filter

## 控制反转

IoC，Inversion of Control，是一种思想。

把对象的创建赋值管理工作，都交给代码之外的容器实现，也就是说对象的创建是由其他外部资源完成

控制：创建对象，对象的属性赋值，对象之间的关系管理。

反转：把原来的开发人员管理，创建对象的权限，转移给代码之外的容器实现，开发人员主动管理对象

容器：一个服务器软件，一个框架(spring)

ioc的体现：servlet的实例对象由tomcat创建

ioc的技术实现：DI是ioc的技术实现，Dependency Injection，依赖注入，只需要在程序中提供要使用的对象名称就可以，至于对象如何在容器中创建赋值和查找，都由容器内部实现

spring是使用di实现了ioc的功能，spring底层使用反射机制

ioc能够实现解耦合，ioc能够实现业务对象之间解耦合，例如service和dao对象之间解耦合

## 引用类型自动注入

spring框架可以根据某些规则给引用类型赋值，不用手动给引用类型属性赋值了

常用规则：

1. byName(按名称注入)：java类中引用类型的属性名和spring容器中配置文件bean标签的id名称一样，且数据类型是一致的，这样容器中的bean，spring能够赋值给引用类型
2. byType(按类型注入)：java类中引用数据类型和spring容器中(配置文件)bean标签的class属性时同源关系，这样的bean能够赋值给引用类型。同源指相同或父子关系或接口和实现类关系

## XML的di实现

1. maven中加入spring依赖
2. 新建类
3. 创建spring的配置文件，使用bean标签声明对象
4. 使用容器中的对象，通过ApplicationContext接口和它的实现类ClassPathXMLApplicationContext的方法getBean()

spring是在ApplicationContext被创建时，创建所有配置文件中的对象

## 基于注解的di

通过注解完成java对象创建，属性赋值

1. 加入maven的依赖spring-context时会间接加入spring-aop的依赖，使用注解必须使用spring-aop依赖
2. 在类中加入spring的注解(多个不同功能的注解)
3. 在spring的配置文件中，加入一个组件扫描器的标签，说明注解在你的项目中的位置

注解：

1. @Component：位置写在类的上面；value属性的值就是对象的名称；如果只有value一个属性，可以省略value=；或者直接省略不写()，spring提供默认对象名称是类名首字母小写

2. @Repository：用在持久层上，放在dao的实现类上，表示创建dao对象，dao对象是能访问数据库的

3. @Service：用在业务层上，放在service的实现类上，创建service对象，service是做业务处理的，可以有事务等功能

4. @Controller：用在控制器的上面，创建控制器对象，控制器对象能够接受用户提交的参数，显示请求的处理结果

   以上注解都是用来创建对象的，但是后三个注解有额外的功能

   ---

   

5. @Value：位置在属性定义的上面，或setter上面，推荐使用；给简单类型属性赋值，有value属性；如果只有value属性，value=可以省略不写

6. @Autowired：自动添加引用类型属性的对象，只能byType

7. @Resource：这是JDK提供的注解，spring框架提供了对这个注解的功能支持，可以用它来给引用类型属性自动注入值，默认是byName，但byName失败就会用byType

### 指定多个包的三种方式

1. 使用多次组件扫描器，指定不同的包
2. 使用分隔符(;分号或,逗号)
3. 直接指定包为共同父包，可能扫描了不需要的包，降低性能

# 面向切面编程

aop，Aspect Orient Programming，就是动态代理的规范化，把动态代理的实现步骤、方式都定义好了，让开发人员用一种统一的方式使用动态代理

是面向对象编程OOP一种补充

## 术语

Aspect，切面，给你的目标类增加的功能，就是切面，像上面用的日志，事务都是切面。切面的特点，一般都是非业务方法，独立使用的。常见的切面功能有日志，事务，统计信息，参数检查，权限验证

JoinPoint：连接点，连接业务方法和切面的位置

Pointcut：切入点，指多个JoinPoint的集合，表示切面功能执行的位置

目标对象：给哪个类的方法增加功能，这个类就是目标对象

Advice：通知，表示切面功能执行的时间

## 理解面向切面编程

1. 需要在分析项目功能的时候，找出切面
2. 合理的安排切面执行的时间，在目标方法前，还是在目标方法后
3. 合理的安排切面执行的位置，在哪个类，哪个方法增加增强功能

## 什么时候使用aop

1. 想给已写好的类增加功能，但是没有源代码
2. 要给多个类增加相同的功能(事务，日志输出)

## 动态代理

实现方式：

1. jdk动态代理：使用jdk中的Proxy，Method，InvocationHandler创建代理对象，jdk动态代理要求目标类必须实现接口
2. cglib动态代理：第三方的工具库，创建代理对象，原理是继承，通过继承目标类创建子类，子类就是代理对象，要求目标类不能是final的，方法也不能是final的

动态代理作用：

1. 在目标类源代码不改变的情况下，增加功能
2. 减少代码的重复
3. 专注业务逻辑代码
4. 解耦合，让你的业务功能和日志，事务非业务功能分离

## aspectj

1. 新建maven项目
2. 加入依赖：spring依赖，aspectj依赖，junit单元测试
3. 创建目标类：接口和它的实现类，给类中的方法增加功能
4. 创建切面类：普通类。在类的上面加入@Aspect，在类中定义方法，方法就是切面要执行的功能代码，在方法的上面加入aspectj中的通知注解，例如@Before，有需要指定切入点表达式execution()
5. 创建spring的配置文件：声明对象，把对象交给容器统一管理，声明对象可以用注解或者配置文件bean标签

切入点表达式：execution(访问修饰符 返回值类型 包名.类名.方法名(方法参数类型) 抛出异常)

JoinPoint作为切面类方法的参数，可以得到业务方法的信息

### 六种注解

@Before：前置通知，在目标方法之前先执行切面的功能

@AfterReturning：后置通知，在目标方法之后执行的，能够获取到目标方法的返回值

@Around：环绕通知，等同于jdk动态代理，InvocationHandler接口，是功能最强的通知，在目标方法的前和后都能增强功能，控制目标方法是否被执行调用，修改原来的目标方法的执行结果，影响最后的调用结果。参数ProceedingJoinPoint，等同于Method；返回值就是目标方法的返回值。经常用来做事务管理

@AfterThrowing：异常通知，在目标方法抛出异常后执行的通知

@After：最终通知，总是会被执行的代码，相当于finally

@Pointcut：定义和管理切入点的辅助注解

# 继承mybatis框架

把mybatis和spring集成在一起，像一个框架一样使用

ioc能创建对象，可以把mybatis中的对象交给spring统一创建，开发人员从spring中获取对象，开发人员就不用同时面对两个框架了

1. 添加依赖
2. 声明数据源DataSource，作用是连接数据库
3. set注入给DruidDataSource提供连接数据库信息
4. 声明mybatis提供的SQLSessionFactoryBean类，这个类会在内部创建SqlSessionFactory
5. set注入把数据库连接池赋值给dataSource属性
6. set注入把mybatis主配置文件位置赋值给configLocation属性(注意，该属性是Resource类型，但仍然用value赋值)
7. 声明mybatis提供的MapperScannerConfigurer对象，他会扫描某个包，调用getMapper()，自动创建接口到dao对象
8. 声明service对象

# 事务处理

事务是指一组sql语句的集合，集合中有多条sql语句

当操作涉及到多个表，或者多个sql语句，需要保证这些语句都成功才能完成一个功能，就需要使用事务

事务控制应该在service类的业务方法中，因为业务方法会调用多个dao类的方法，执行多个sql语句

jdbc中使用conn.commit()；conn.rollback();

mybatis中使用sqlSession.commit()；sqlSession.rollback()

hibernate中使用session.commit()；session.rollback()

spring提供一种处理事务的统一模型，能使用统一步骤，完成多种不同数据库访问技术的事务处理

声明式事务：把事务相关的资源和内容都提供给spring，spring就能处理事务了，几乎不用代码

spring使用事务管理器对象，事务管理器是一个接口和他的众多实现类

接口PlatformTransactionManager，在spring配置文件中用bean标签声明一下实现类

## 事务设置

1. 隔离级别
2. 超时时间，单位是s，整数值，默认是-1
3. 传播行为，控制业务方法是不是有事务，是哪种事务

## 传播行为

1. PROPAGATION_REQUIRED
2. PROPAGATION_SUPPORTS
3. PROPAGATION_REQUIRES_NEW

## 事务提交和回滚

1. 当业务方法执行成功，没有异常抛出，方法执行完毕后，spring提交事务
2. 当业务方法抛出运行时异常(RuntimeException，和它的子类NullPointException等)，spring执行回滚
3. 当业务方法抛出非运行时异常，主要是受检异常(CheckedException，和它的子类IOException等)和ERROR时，提交事务

## 注解处理事务

@Transactional

可选属性：

1. propagation：传播行为
2. isolation：隔离级别
3. readOnly：只进行select时
4. timeout：超时时间
5. rollbackFor
6. rollbackForClassName
7. noRollbackFor

## 在xml中处理事务

配置方法的事务属性

tx:advice标签
